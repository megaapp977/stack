# Tutorial: limpiar `lid_jids` en la tabla `contacts` de MEGA usando PostgreSQL

Este tutorial explica cómo vaciar o eliminar la propiedad `lid_jids` almacenada dentro de la columna `additional_attributes` de la tabla `contacts`.

La columna `additional_attributes` normalmente es de tipo `jsonb` y puede contener datos como:

```json
{
  "city": "",
  "country": "",
  "lid_jids": [
    "271842120057064@lid",
    "271842120057064:41@lid",
    "15225709457570@lid"
  ],
  "description": "",
  "company_name": ""
}
```

El objetivo recomendado es convertir `lid_jids` en un array vacío:

```json
"lid_jids": []
```

De esta manera, se conserva la estructura del JSON y no se modifican los demás atributos del contacto.

---

## 1. Acceder a PostgreSQL

Si PostgreSQL está instalado directamente:

```bash
psql -U postgres -d nombre_de_la_base
```

Ejemplo:

```bash
psql -U postgres -d mega_production
```

Si PostgreSQL está ejecutándose dentro de Docker:

```bash
docker exec -it NOMBRE_CONTENEDOR_POSTGRES psql -U postgres -d nombre_de_la_base
```

Ejemplo:

```bash
docker exec -it mega-postgres psql -U postgres -d mega_production
```

Para localizar el contenedor:

```bash
docker ps
```

---

## 2. Confirmar el tipo de la columna

Ejecuta:

```sql
SELECT
  column_name,
  data_type,
  udt_name
FROM information_schema.columns
WHERE table_name = 'contacts'
  AND column_name = 'additional_attributes';
```

El resultado esperado debe indicar que la columna es `jsonb`.

Ejemplo:

```text
column_name           | data_type    | udt_name
----------------------+--------------+---------
additional_attributes | USER-DEFINED | jsonb
```

También puede aparecer directamente como `jsonb`, dependiendo de la herramienta utilizada.

---

## 3. Ver contactos que contienen `lid_jids`

Antes de actualizar, revisa los registros afectados:

```sql
SELECT
  id,
  name,
  account_id,
  phone_number,
  identifier,
  additional_attributes->'lid_jids' AS lid_jids
FROM contacts
WHERE additional_attributes ? 'lid_jids'
ORDER BY id
LIMIT 100;
```

El operador:

```sql
?
```

comprueba si existe una clave dentro de un objeto `jsonb`.

---

## 4. Contar cuántos contactos serán modificados

```sql
SELECT COUNT(*) AS contactos_con_lid_jids
FROM contacts
WHERE additional_attributes ? 'lid_jids';
```

Para contar únicamente registros donde `lid_jids` tiene datos:

```sql
SELECT COUNT(*) AS contactos_con_lid_jids_con_datos
FROM contacts
WHERE additional_attributes ? 'lid_jids'
  AND jsonb_typeof(additional_attributes->'lid_jids') = 'array'
  AND jsonb_array_length(additional_attributes->'lid_jids') > 0;
```

Esta segunda consulta evita contar contactos cuyo valor ya sea:

```json
"lid_jids": []
```

---

## 5. Crear una copia de seguridad

Antes de realizar una actualización masiva, crea una copia de los registros afectados.

### Opción A: crear una tabla de respaldo

```sql
CREATE TABLE contacts_lid_jids_backup_20260723 AS
SELECT *
FROM contacts
WHERE additional_attributes ? 'lid_jids';
```

Confirma el respaldo:

```sql
SELECT COUNT(*)
FROM contacts_lid_jids_backup_20260723;
```

> Cambia `20260723` por la fecha en la que realices la operación.

### Opción B: respaldar solamente las columnas necesarias

```sql
CREATE TABLE contacts_lid_jids_backup_20260723 AS
SELECT
  id,
  account_id,
  additional_attributes,
  updated_at
FROM contacts
WHERE additional_attributes ? 'lid_jids';
```

Esta opción ocupa menos espacio.

---

## 6. Vaciar `lid_jids` en todos los contactos

La consulta recomendada es:

```sql
UPDATE contacts
SET additional_attributes = jsonb_set(
  additional_attributes,
  '{lid_jids}',
  '[]'::jsonb,
  true
)
WHERE additional_attributes ? 'lid_jids';
```

Esto transforma:

```json
"lid_jids": [
  "271842120057064@lid",
  "271842120057064:41@lid"
]
```

en:

```json
"lid_jids": []
```

Los demás campos de `additional_attributes` se mantienen sin cambios.

---

## 7. Forma segura usando una transacción

Es preferible ejecutar el cambio dentro de una transacción:

```sql
BEGIN;

UPDATE contacts
SET additional_attributes = jsonb_set(
  additional_attributes,
  '{lid_jids}',
  '[]'::jsonb,
  true
)
WHERE additional_attributes ? 'lid_jids'
  AND jsonb_typeof(additional_attributes->'lid_jids') = 'array'
  AND jsonb_array_length(additional_attributes->'lid_jids') > 0;

SELECT COUNT(*) AS contactos_que_ahora_tienen_array_vacio
FROM contacts
WHERE additional_attributes->'lid_jids' = '[]'::jsonb;
```

Si el resultado es correcto:

```sql
COMMIT;
```

Si detectas un problema antes del `COMMIT`:

```sql
ROLLBACK;
```

> Después de ejecutar `COMMIT`, ya no será posible usar `ROLLBACK` para deshacer esa transacción.

---

## 8. Actualizar solamente una cuenta

Por ejemplo, para limpiar `lid_jids` únicamente en `account_id = 2`:

```sql
BEGIN;

UPDATE contacts
SET additional_attributes = jsonb_set(
  additional_attributes,
  '{lid_jids}',
  '[]'::jsonb,
  true
)
WHERE account_id = 2
  AND additional_attributes ? 'lid_jids'
  AND jsonb_typeof(additional_attributes->'lid_jids') = 'array'
  AND jsonb_array_length(additional_attributes->'lid_jids') > 0;

COMMIT;
```

Antes de ejecutar la actualización, puedes verificar:

```sql
SELECT
  id,
  name,
  phone_number,
  identifier,
  additional_attributes->'lid_jids' AS lid_jids
FROM contacts
WHERE account_id = 2
  AND additional_attributes ? 'lid_jids';
```

---

## 9. Actualizar solamente un contacto

Por ejemplo, para el contacto con `id = 14580`:

```sql
UPDATE contacts
SET additional_attributes = jsonb_set(
  additional_attributes,
  '{lid_jids}',
  '[]'::jsonb,
  true
)
WHERE id = 14580
  AND additional_attributes ? 'lid_jids';
```

Validación:

```sql
SELECT
  id,
  name,
  additional_attributes->'lid_jids' AS lid_jids
FROM contacts
WHERE id = 14580;
```

---

## 10. Actualizar varios contactos específicos

```sql
UPDATE contacts
SET additional_attributes = jsonb_set(
  additional_attributes,
  '{lid_jids}',
  '[]'::jsonb,
  true
)
WHERE id IN (
  26740,
  14580,
  21106
)
AND additional_attributes ? 'lid_jids';
```

---

## 11. Eliminar completamente la clave `lid_jids`

Si prefieres remover la propiedad en lugar de conservarla vacía:

```sql
UPDATE contacts
SET additional_attributes = additional_attributes - 'lid_jids'
WHERE additional_attributes ? 'lid_jids';
```

Antes:

```json
{
  "city": "",
  "lid_jids": [
    "271842120057064@lid"
  ],
  "description": ""
}
```

Después:

```json
{
  "city": "",
  "description": ""
}
```

Para MEGA, normalmente es más conservador dejar:

```json
"lid_jids": []
```

en lugar de eliminar la clave, especialmente si el código espera que esa propiedad exista.

---

## 12. Verificar el resultado

### Comprobar que no quedan arrays con datos

```sql
SELECT COUNT(*) AS lid_jids_pendientes
FROM contacts
WHERE additional_attributes ? 'lid_jids'
  AND jsonb_typeof(additional_attributes->'lid_jids') = 'array'
  AND jsonb_array_length(additional_attributes->'lid_jids') > 0;
```

El resultado esperado es:

```text
0
```

### Revisar contactos actualizados

```sql
SELECT
  id,
  name,
  account_id,
  phone_number,
  identifier,
  additional_attributes->'lid_jids' AS lid_jids
FROM contacts
WHERE additional_attributes->'lid_jids' = '[]'::jsonb
ORDER BY id DESC
LIMIT 100;
```

---

## 13. Restaurar desde la copia de seguridad

Si creaste esta tabla:

```sql
contacts_lid_jids_backup_20260723
```

puedes restaurar el contenido original de `additional_attributes` así:

```sql
BEGIN;

UPDATE contacts AS c
SET
  additional_attributes = b.additional_attributes,
  updated_at = b.updated_at
FROM contacts_lid_jids_backup_20260723 AS b
WHERE c.id = b.id;

COMMIT;
```

Para restaurar únicamente `lid_jids`, sin reemplazar todo el JSON:

```sql
BEGIN;

UPDATE contacts AS c
SET additional_attributes = jsonb_set(
  c.additional_attributes,
  '{lid_jids}',
  b.additional_attributes->'lid_jids',
  true
)
FROM contacts_lid_jids_backup_20260723 AS b
WHERE c.id = b.id
  AND b.additional_attributes ? 'lid_jids';

COMMIT;
```

La segunda opción es más segura si otros atributos fueron modificados después de crear el respaldo.

---

## 14. Consulta final recomendada

Esta es la secuencia completa recomendada:

```sql
-- 1. Contar registros afectados
SELECT COUNT(*)
FROM contacts
WHERE additional_attributes ? 'lid_jids'
  AND jsonb_typeof(additional_attributes->'lid_jids') = 'array'
  AND jsonb_array_length(additional_attributes->'lid_jids') > 0;

-- 2. Crear respaldo
CREATE TABLE contacts_lid_jids_backup_20260723 AS
SELECT
  id,
  account_id,
  additional_attributes,
  updated_at
FROM contacts
WHERE additional_attributes ? 'lid_jids';

-- 3. Iniciar transacción
BEGIN;

-- 4. Vaciar los arrays
UPDATE contacts
SET additional_attributes = jsonb_set(
  additional_attributes,
  '{lid_jids}',
  '[]'::jsonb,
  true
)
WHERE additional_attributes ? 'lid_jids'
  AND jsonb_typeof(additional_attributes->'lid_jids') = 'array'
  AND jsonb_array_length(additional_attributes->'lid_jids') > 0;

-- 5. Verificar que no quedan arrays con datos
SELECT COUNT(*) AS lid_jids_pendientes
FROM contacts
WHERE additional_attributes ? 'lid_jids'
  AND jsonb_typeof(additional_attributes->'lid_jids') = 'array'
  AND jsonb_array_length(additional_attributes->'lid_jids') > 0;

-- 6. Confirmar
COMMIT;
```

---

## Consideraciones importantes

- El comando no modifica `phone_number`.
- El comando no modifica `identifier`.
- El comando no modifica el nombre del contacto.
- El comando no modifica fotografías, país, empresa ni perfiles sociales.
- Solamente reemplaza el contenido de `additional_attributes.lid_jids`.
- Realiza un respaldo antes de aplicar cambios masivos.
- Si MEGA continúa agregando valores a `lid_jids`, será necesario revisar el código o integración que vuelve a guardar esos identificadores.
- En una base de datos grande, ejecuta la operación durante un periodo de baja actividad.
- Si existen réplicas, workers o procesos de sincronización activos, comprueba que no vuelvan a poblar el campo inmediatamente.

---

## Resultado esperado

Antes:

```json
{
  "city": "",
  "country": "",
  "lid_jids": [
    "271842120057064@lid",
    "271842120057064:41@lid",
    "15225709457570@lid"
  ],
  "description": "",
  "company_name": ""
}
```

Después:

```json
{
  "city": "",
  "country": "",
  "lid_jids": [],
  "description": "",
  "company_name": ""
}
```
