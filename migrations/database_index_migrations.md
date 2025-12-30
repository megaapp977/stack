# Guía de Migraciones de Índices en Producción

## Problema

Al crear índices en tablas grandes (>10M registros) en producción, pueden ocurrir lock timeouts que impiden completar la migración.

## Tablas grandes en este proyecto

- `messages` - >50M registros
- `conversations` - >10M registros  
- `contacts` - >5M registros
- `notifications` - >20M registros

## Buenas prácticas

### 1. Siempre usar índices concurrentes

```ruby
class AddMyIndex < ActiveRecord::Migration[7.1]
  disable_ddl_transaction!  # ← REQUERIDO para concurrentes
  
  def change
    add_index :table, :column, 
      algorithm: :concurrently,  # ← No bloquea escrituras
      if_not_exists: true        # ← Idempotente
  end
end
```

### 2. Dividir migraciones grandes

❌ **Malo**: 20 índices en una migración
```ruby
def change
  add_index :table1, :col1, algorithm: :concurrently
  add_index :table2, :col2, algorithm: :concurrently
  # ... 18 más
end
```

✅ **Bueno**: Una migración por tabla grande
```ruby
# 20241230_add_messages_indexes.rb
def change
  add_index :messages, :source_id, algorithm: :concurrently
end

# 20241230_add_conversations_indexes.rb  
def change
  add_index :conversations, [:account_id, :status], algorithm: :concurrently
end
```

### 3. Configurar timeouts en migraciones

```ruby
class AddIndexToLargeTable < ActiveRecord::Migration[7.1]
  disable_ddl_transaction!
  
  def up
    # Solo en producción
    if Rails.env.production?
      execute('SET statement_timeout = "30min"')
      execute('SET lock_timeout = "5min"')
    end
    
    add_index :large_table, :column, algorithm: :concurrently
  end
end
```

### 4. Usar índices parciales cuando sea posible

```ruby
# ❌ Malo: indexar toda la tabla
add_index :conversations, :status

# ✅ Bueno: solo registros activos (10% del total)
add_index :conversations, :status,
  where: 'status IN (0, 1) AND deleted_at IS NULL',
  name: 'idx_conversations_active'
```

### 5. Monitorear índices en creación

```bash
# Ver progreso en tiempo real
bundle exec rails db:indexes:monitor

# Consulta SQL directa
SELECT 
  phase, 
  round(100.0 * blocks_done / nullif(blocks_total, 0), 1) as percent,
  age(now(), query_start) as duration
FROM pg_stat_progress_create_index p
JOIN pg_stat_activity a ON p.pid = a.pid;
```

## Workflow recomendado

### Para desarrollo/staging
```bash
bundle exec rails db:migrate
```

### Para producción - índices en tablas grandes

1. **Revisar migración antes de desplegar**
   ```bash
   # Ver migraciones pendientes
   bundle exec rails db:migrate:status
   
   # Verificar índices faltantes
   bundle exec rails db:indexes:check_missing
   ```

2. **Opción A: Ejecutar durante ventana de mantenimiento**
   ```bash
   # Detener workers
   docker-compose stop worker
   
   # Ejecutar migración
   bundle exec rails db:migrate
   
   # Reiniciar workers
   docker-compose start worker
   ```

3. **Opción B: Ejecutar en horario de baja actividad (madrugada)**
   ```bash
   # Usar rake task seguro
   bundle exec rails db:indexes:create_pending
   
   # O manualmente:
   bundle exec rails runner "
     execute('SET statement_timeout = \"30min\"')
     execute('SET lock_timeout = \"5min\"')
     add_index :table, :column, algorithm: :concurrently
   "
   ```

4. **Opción C: Saltar temporalmente**
   ```bash
   # Marcar como ejecutada
   bundle exec rails runner "
     ActiveRecord::Base.connection.execute(
       \\\"INSERT INTO schema_migrations (version) 
        VALUES ('YYYYMMDDHHMMSS') ON CONFLICT DO NOTHING\\\"
     )
   "
   
   # Crear índice después manualmente
   bundle exec rails db:indexes:create_pending
   ```

## Troubleshooting

### Error: `PG::LockNotAvailable: lock timeout`
**Causa**: No se pudo obtener lock en tiempo límite
**Solución**: Ejecutar en horario de menor actividad

### Error: `PG::QueryCanceled: statement timeout`  
**Causa**: Índice tardó demasiado en crearse
**Solución**: Aumentar `statement_timeout` o usar índice parcial

### Ver queries bloqueadas
```sql
SELECT 
  pid,
  usename,
  pg_blocking_pids(pid) as blocked_by,
  query as blocked_query
FROM pg_stat_activity
WHERE cardinality(pg_blocking_pids(pid)) > 0;
```

### Cancelar índice en creación
```sql
-- Ver PIDs de índices en creación
SELECT pid FROM pg_stat_progress_create_index;

-- Cancelar (si es seguro)
SELECT pg_cancel_backend(pid);
```

## Checklist antes de deploy

- [ ] ¿La migración crea índices en tablas grandes?
- [ ] ¿Usa `disable_ddl_transaction!`?
- [ ] ¿Usa `algorithm: :concurrently`?
- [ ] ¿Usa `if_not_exists: true`?
- [ ] ¿Configura timeouts para producción?
- [ ] ¿Está dividida en migraciones pequeñas?
- [ ] ¿Se coordinó horario de baja actividad si es necesario?

## Herramientas útiles

```bash
# Verificar índices faltantes
bundle exec rails db:indexes:check_missing

# Crear índices pendientes (madrugada)
bundle exec rails db:indexes:create_pending

# Creación automática (para cron)
bundle exec rails db:indexes:auto_create

# Monitorear progreso
bundle exec rails db:indexes:monitor

# Ver estado de migración
bundle exec rails db:migrate:status
```

## Configuración de Cron (automatización)

Chatwoot usa **sidekiq-cron** para tareas programadas. La creación automática de índices ya está configurada en `config/schedule.yml`.

### Configuración automática

El job `Internal::CreatePendingIndexesJob` se ejecuta diariamente a las 2:30 AM UTC:

```yaml
# config/schedule.yml
create_pending_indexes_job:
  cron: '30 2 * * *'
  class: 'Internal::CreatePendingIndexesJob'
  queue: low
  active_job: true
```

### Variables de entorno (opcional)

```bash
# config/application.yml o .env
INDEX_SAFE_HOURS=2-5                      # Horario seguro (2:00-5:00 AM)
INDEX_MAX_DURATION_MINUTES=120            # Máximo 2 horas por ejecución
INDEX_MAX_ACTIVE_CONNECTIONS=50           # Cancelar si hay mucha carga
```

### Comportamiento automático

El job automáticamente:
- ✅ Solo ejecuta en producción/staging
- ✅ Verifica que esté en horario seguro (2-5 AM por defecto)
- ✅ Cancela si hay mucha carga en el sistema
- ✅ Limita duración máxima (2 horas por defecto)
- ✅ Se detiene si sale del horario seguro
- ✅ Registra todo en logs de Sidekiq

### Monitorear ejecuciones

```bash
# Ver logs de Sidekiq
tail -f log/sidekiq.log | grep CreatePendingIndexesJob

# Ver en Sidekiq Web UI
# http://your-app.com/sidekiq/cron

# Ejecutar manualmente desde consola Rails
Internal::CreatePendingIndexesJob.perform_now

# O desde rake
bundle exec rails db:indexes:auto_create
```

## Referencias

- [PostgreSQL: Building Indexes Concurrently](https://www.postgresql.org/docs/current/sql-createindex.html#SQL-CREATEINDEX-CONCURRENTLY)
- [Rails: Safe Migrations](https://github.com/ankane/strong_migrations)
