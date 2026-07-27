# Tutorial: cleaning `lid_jids` in MEGA's `contacts` table with PostgreSQL

This tutorial explains how to empty or remove the `lid_jids` property stored in the `additional_attributes` column of the `contacts` table.

The `additional_attributes` column is normally a `jsonb` value and may contain data such as:

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

The recommended goal is to turn `lid_jids` into an empty array:

```json
"lid_jids": []
```

This preserves the JSON structure without changing the contact's other attributes.

---

## 1. Access PostgreSQL

If PostgreSQL is installed directly on the server:

```bash
psql -U postgres -d database_name
```

Example:

```bash
psql -U postgres -d mega_production
```

If PostgreSQL is running in a Docker container:

```bash
docker exec -it POSTGRES_CONTAINER_NAME psql -U postgres -d database_name
```

Example:

```bash
docker exec -it mega-postgres psql -U postgres -d mega_production
```

To find the container:

```bash
docker ps
```

---

## 2. Confirm the column type

Run:

```sql
SELECT
  column_name,
  data_type,
  udt_name
FROM information_schema.columns
WHERE table_name = 'contacts'
  AND column_name = 'additional_attributes';
```

The expected result should indicate that the column is a `jsonb` value.

Example:

```text
column_name           | data_type    | udt_name
----------------------+--------------+---------
additional_attributes | USER-DEFINED | jsonb
```

Depending on the tool you use, the type may also appear directly as `jsonb`.

---

## 3. View contacts that contain `lid_jids`

Before updating anything, review the records that will be affected:

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

The operator:

```sql
?
```

checks whether a key exists in a `jsonb` object.

---

## 4. Count how many contacts will be changed

```sql
SELECT COUNT(*) AS contacts_with_lid_jids
FROM contacts
WHERE additional_attributes ? 'lid_jids';
```

To count only records where `lid_jids` contains data:

```sql
SELECT COUNT(*) AS contacts_with_populated_lid_jids
FROM contacts
WHERE additional_attributes ? 'lid_jids'
  AND jsonb_typeof(additional_attributes->'lid_jids') = 'array'
  AND jsonb_array_length(additional_attributes->'lid_jids') > 0;
```

This second query does not count contacts whose value is already:

```json
"lid_jids": []
```

---

## 5. Create a backup

Before running a bulk update, create a backup of the affected records.

### Option A: create a full backup table

```sql
CREATE TABLE contacts_lid_jids_backup_20260723 AS
SELECT *
FROM contacts
WHERE additional_attributes ? 'lid_jids';
```

Confirm the backup:

```sql
SELECT COUNT(*)
FROM contacts_lid_jids_backup_20260723;
```

> Replace `20260723` with the date on which you perform the operation.

### Option B: back up only the required columns

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

This option uses less database space.

---

## 6. Empty `lid_jids` for every contact

The recommended query is:

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

This changes:

```json
"lid_jids": [
  "271842120057064@lid",
  "271842120057064:41@lid"
]
```

into:

```json
"lid_jids": []
```

The other fields in `additional_attributes` remain unchanged.

---

## 7. Run the update safely in a transaction

It is preferable to perform the change inside a transaction:

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

SELECT COUNT(*) AS contacts_that_now_have_an_empty_array
FROM contacts
WHERE additional_attributes->'lid_jids' = '[]'::jsonb;
```

If the result is correct:

```sql
COMMIT;
```

If you find a problem before `COMMIT`:

```sql
ROLLBACK;
```

> After you run `COMMIT`, you can no longer use `ROLLBACK` to undo that transaction.

---

## 8. Update only one account

For example, to clean `lid_jids` only for `account_id = 2`:

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

Before running the update, you can check the records:

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

## 9. Update only one contact

For example, for the contact with `id = 14580`:

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

Validation:

```sql
SELECT
  id,
  name,
  additional_attributes->'lid_jids' AS lid_jids
FROM contacts
WHERE id = 14580;
```

---

## 10. Update several specific contacts

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

## 11. Completely remove the `lid_jids` key

If you prefer to remove the property instead of keeping it empty:

```sql
UPDATE contacts
SET additional_attributes = additional_attributes - 'lid_jids'
WHERE additional_attributes ? 'lid_jids';
```

Before:

```json
{
  "city": "",
  "lid_jids": [
    "271842120057064@lid"
  ],
  "description": ""
}
```

After:

```json
{
  "city": "",
  "description": ""
}
```

For MEGA, it is usually more conservative to keep:

```json
"lid_jids": []
```

rather than removing the key, especially if the code expects that property to exist.

---

## 12. Verify the result

### Check that no populated arrays remain

```sql
SELECT COUNT(*) AS pending_lid_jids
FROM contacts
WHERE additional_attributes ? 'lid_jids'
  AND jsonb_typeof(additional_attributes->'lid_jids') = 'array'
  AND jsonb_array_length(additional_attributes->'lid_jids') > 0;
```

The expected result is:

```text
0
```

### Review the updated contacts

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

## 13. Restore from the backup

If you created this table:

```sql
contacts_lid_jids_backup_20260723
```

you can restore the original `additional_attributes` value as follows:

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

To restore only `lid_jids` without replacing the entire JSON object:

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

The second option is safer if other attributes were changed after creating the backup.

---

## 14. Recommended final sequence

This is the complete recommended sequence:

```sql
-- 1. Count the affected records
SELECT COUNT(*)
FROM contacts
WHERE additional_attributes ? 'lid_jids'
  AND jsonb_typeof(additional_attributes->'lid_jids') = 'array'
  AND jsonb_array_length(additional_attributes->'lid_jids') > 0;

-- 2. Create the backup
CREATE TABLE contacts_lid_jids_backup_20260723 AS
SELECT
  id,
  account_id,
  additional_attributes,
  updated_at
FROM contacts
WHERE additional_attributes ? 'lid_jids';

-- 3. Start the transaction
BEGIN;

-- 4. Empty the arrays
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

-- 5. Check that no populated arrays remain
SELECT COUNT(*) AS pending_lid_jids
FROM contacts
WHERE additional_attributes ? 'lid_jids'
  AND jsonb_typeof(additional_attributes->'lid_jids') = 'array'
  AND jsonb_array_length(additional_attributes->'lid_jids') > 0;

-- 6. Confirm the change
COMMIT;
```

---

## Important considerations

- The command does not change `phone_number`.
- The command does not change `identifier`.
- The command does not change the contact's name.
- The command does not change photos, country, company, or social profiles.
- It replaces only the contents of `additional_attributes.lid_jids`.
- Create a backup before applying bulk changes.
- If MEGA continues to add values to `lid_jids`, review the code or integration that stores those identifiers again.
- For a large database, perform the operation during a low-traffic period.
- If replicas, workers, or synchronization processes are active, confirm that they do not immediately populate the field again.

---

## Expected result

Before:

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

After:

```json
{
  "city": "",
  "country": "",
  "lid_jids": [],
  "description": "",
  "company_name": ""
}
```
