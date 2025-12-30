# Guia de Migrações de Índices em Produção

## Problema

Ao criar índices em tabelas grandes (>10M registros) em produção, podem ocorrer timeouts de lock que impedem a conclusão da migração.

## Tabelas grandes neste projeto

- `messages` - >50M registros
- `conversations` - >10M registros  
- `contacts` - >5M registros
- `notifications` - >20M registros

## Melhores práticas

### 1. Sempre use índices concorrentes

```ruby
class AddMyIndex < ActiveRecord::Migration[7.1]
  disable_ddl_transaction!  # ← OBRIGATÓRIO para concorrentes
  
  def change
    add_index :table, :column, 
      algorithm: :concurrently,  # ← Não bloqueia escritas
      if_not_exists: true        # ← Idempotente
  end
end
```

### 2. Dividir migrações grandes

❌ **Ruim**: 20 índices em uma migração
```ruby
def change
  add_index :table1, :col1, algorithm: :concurrently
  add_index :table2, :col2, algorithm: :concurrently
  # ... 18 mais
end
```

✅ **Bom**: Uma migração por tabela grande
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

### 3. Configurar timeouts em migrações

```ruby
class AddIndexToLargeTable < ActiveRecord::Migration[7.1]
  disable_ddl_transaction!
  
  def up
    # Apenas em produção
    if Rails.env.production?
      execute('SET statement_timeout = "30min"')
      execute('SET lock_timeout = "5min"')
    end
    
    add_index :large_table, :column, algorithm: :concurrently
  end
end
```

### 4. Usar índices parciais quando possível

```ruby
# ❌ Ruim: indexar toda a tabela
add_index :conversations, :status

# ✅ Bom: apenas registros ativos (10% do total)
add_index :conversations, :status,
  where: 'status IN (0, 1) AND deleted_at IS NULL',
  name: 'idx_conversations_active'
```

### 5. Monitorar criação de índices

```bash
# Ver progresso em tempo real
bundle exec rails db:indexes:monitor

# Consulta SQL direta
SELECT 
  phase, 
  round(100.0 * blocks_done / nullif(blocks_total, 0), 1) as percent,
  age(now(), query_start) as duration
FROM pg_stat_progress_create_index p
JOIN pg_stat_activity a ON p.pid = a.pid;
```

## Fluxo de trabalho recomendado

### Para desenvolvimento/staging
```bash
bundle exec rails db:migrate
```

### Para produção - índices em tabelas grandes

1. **Revisar migração antes de implantar**
   ```bash
   # Ver migrações pendentes
   bundle exec rails db:migrate:status
   
   # Verificar índices faltantes
   bundle exec rails db:indexes:check_missing
   ```

2. **Opção A: Executar durante janela de manutenção**
   ```bash
   # Parar workers
   docker-compose stop worker
   
   # Executar migração
   bundle exec rails db:migrate
   
   # Reiniciar workers
   docker-compose start worker
   ```

3. **Opção B: Executar durante horário de baixa atividade (madrugada)**
   ```bash
   # Usar rake task segura
   bundle exec rails db:indexes:create_pending
   
   # Ou manualmente:
   bundle exec rails runner "
     execute('SET statement_timeout = \"30min\"')
     execute('SET lock_timeout = \"5min\"')
     add_index :table, :column, algorithm: :concurrently
   "
   ```

4. **Opção C: Pular temporariamente**
   ```bash
   # Marcar como executada
   bundle exec rails runner "
     ActiveRecord::Base.connection.execute(
       \\\"INSERT INTO schema_migrations (version) 
        VALUES ('YYYYMMDDHHMMSS') ON CONFLICT DO NOTHING\\\"
     )
   "
   
   # Criar índice depois manualmente
   bundle exec rails db:indexes:create_pending
   ```

## Solução de problemas

### Erro: `PG::LockNotAvailable: lock timeout`
**Causa**: Não foi possível obter lock no tempo limite
**Solução**: Executar em horário de menor atividade

### Erro: `PG::QueryCanceled: statement timeout`  
**Causa**: Índice demorou muito para ser criado
**Solução**: Aumentar `statement_timeout` ou usar índice parcial

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

### Cancelar criação de índice
```sql
-- Ver PIDs de índices em criação
SELECT pid FROM pg_stat_progress_create_index;

-- Cancelar (se for seguro)
SELECT pg_cancel_backend(pid);
```

## Checklist antes do deploy

- [ ] A migração cria índices em tabelas grandes?
- [ ] Usa `disable_ddl_transaction!`?
- [ ] Usa `algorithm: :concurrently`?
- [ ] Usa `if_not_exists: true`?
- [ ] Configura timeouts para produção?
- [ ] Está dividida em migrações pequenas?
- [ ] Coordenou horário de baixa atividade se necessário?

## Ferramentas úteis

```bash
# Verificar índices faltantes
bundle exec rails db:indexes:check_missing

# Criar índices pendentes (madrugada)
bundle exec rails db:indexes:create_pending

# Criação automática (para cron)
bundle exec rails db:indexes:auto_create

# Monitorar progresso
bundle exec rails db:indexes:monitor

# Ver status da migração
bundle exec rails db:migrate:status
```

## Configuração de Cron (automação)

Chatwoot usa **sidekiq-cron** para tarefas agendadas. A criação automática de índices já está configurada em `config/schedule.yml`.

### Configuração automática

O job `Internal::CreatePendingIndexesJob` executa diariamente às 2:30 AM UTC:

```yaml
# config/schedule.yml
create_pending_indexes_job:
  cron: '30 2 * * *'
  class: 'Internal::CreatePendingIndexesJob'
  queue: low
  active_job: true
```

### Variáveis de ambiente (opcional)

```bash
# config/application.yml ou .env
INDEX_SAFE_HOURS=2-5                      # Horário seguro (2:00-5:00 AM)
INDEX_MAX_DURATION_MINUTES=120            # Máximo 2 horas por execução
INDEX_MAX_ACTIVE_CONNECTIONS=50           # Cancelar se houver muita carga
```

### Comportamento automático

O job automaticamente:
- ✅ Só executa em produção/staging
- ✅ Verifica que está no horário seguro (2-5 AM por padrão)
- ✅ Cancela se houver muita carga no sistema
- ✅ Limita duração máxima (2 horas por padrão)
- ✅ Para se sair do horário seguro
- ✅ Registra tudo nos logs do Sidekiq

### Monitorar execuções

```bash
# Ver logs do Sidekiq
tail -f log/sidekiq.log | grep CreatePendingIndexesJob

# Ver no Sidekiq Web UI
# http://your-app.com/sidekiq/cron

# Executar manualmente do console Rails
Internal::CreatePendingIndexesJob.perform_now

# Ou do rake
bundle exec rails db:indexes:auto_create
```

## Referências

- [PostgreSQL: Building Indexes Concurrently](https://www.postgresql.org/docs/current/sql-createindex.html#SQL-CREATEINDEX-CONCURRENTLY)
- [Rails: Safe Migrations](https://github.com/ankane/strong_migrations)
