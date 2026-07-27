# Tutorial: como limpar `lid_jids` na tabela `contacts` do MEGA usando PostgreSQL

Este tutorial explica como esvaziar ou remover a propriedade `lid_jids` armazenada dentro da coluna `additional_attributes` da tabela `contacts`.

A coluna `additional_attributes` normalmente é do tipo `jsonb` e pode conter dados como:

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

O objetivo recomendado é transformar `lid_jids` em um array vazio:

```json
"lid_jids": []
```

Dessa forma, a estrutura do JSON é preservada e os demais atributos do contato não são alterados.

---

## 1. Acessar o PostgreSQL

Se o PostgreSQL estiver instalado diretamente no servidor:

```bash
psql -U postgres -d nome_do_banco
```

Exemplo:

```bash
psql -U postgres -d mega_production
```

Se o PostgreSQL estiver sendo executado dentro de um container Docker:

```bash
docker exec -it NOME_DO_CONTAINER_POSTGRES psql -U postgres -d nome_do_banco
```

Exemplo:

```bash
docker exec -it mega-postgres psql -U postgres -d mega_production
```

Para localizar o container:

```bash
docker ps
```

---

## 2. Confirmar o tipo da coluna

Execute:

```sql
SELECT
  column_name,
  data_type,
  udt_name
FROM information_schema.columns
WHERE table_name = 'contacts'
  AND column_name = 'additional_attributes';
```

O resultado esperado deve indicar que a coluna é do tipo `jsonb`.

Exemplo:

```text
column_name           | data_type    | udt_name
----------------------+--------------+---------
additional_attributes | USER-DEFINED | jsonb
```

Dependendo da ferramenta utilizada, o tipo também pode aparecer diretamente como `jsonb`.

---

## 3. Visualizar os contatos que possuem `lid_jids`

Antes de realizar a atualização, confira os registros que serão afetados:

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

O operador:

```sql
?
```

verifica se uma chave existe dentro de um objeto `jsonb`.

---

## 4. Contar quantos contatos serão alterados

```sql
SELECT COUNT(*) AS contatos_com_lid_jids
FROM contacts
WHERE additional_attributes ? 'lid_jids';
```

Para contar somente os registros em que `lid_jids` realmente contém dados:

```sql
SELECT COUNT(*) AS contatos_com_lid_jids_preenchidos
FROM contacts
WHERE additional_attributes ? 'lid_jids'
  AND jsonb_typeof(additional_attributes->'lid_jids') = 'array'
  AND jsonb_array_length(additional_attributes->'lid_jids') > 0;
```

Essa segunda consulta não conta contatos cujo valor já seja:

```json
"lid_jids": []
```

---

## 5. Criar uma cópia de segurança

Antes de realizar uma atualização em massa, crie um backup dos registros afetados.

### Opção A: criar uma tabela de backup completa

```sql
CREATE TABLE contacts_lid_jids_backup_20260723 AS
SELECT *
FROM contacts
WHERE additional_attributes ? 'lid_jids';
```

Confirme o backup:

```sql
SELECT COUNT(*)
FROM contacts_lid_jids_backup_20260723;
```

> Altere `20260723` para a data em que a operação for realizada.

### Opção B: salvar somente as colunas necessárias

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

Essa opção utiliza menos espaço no banco de dados.

---

## 6. Esvaziar `lid_jids` em todos os contatos

A consulta recomendada é:

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

Isso transforma:

```json
"lid_jids": [
  "271842120057064@lid",
  "271842120057064:41@lid"
]
```

em:

```json
"lid_jids": []
```

Os demais campos de `additional_attributes` permanecem sem alterações.

---

## 7. Executar de forma segura usando uma transação

É recomendável executar a alteração dentro de uma transação:

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

SELECT COUNT(*) AS contatos_com_array_vazio
FROM contacts
WHERE additional_attributes->'lid_jids' = '[]'::jsonb;
```

Se o resultado estiver correto:

```sql
COMMIT;
```

Se você identificar algum problema antes do `COMMIT`:

```sql
ROLLBACK;
```

> Depois de executar `COMMIT`, não será mais possível usar `ROLLBACK` para desfazer essa transação.

---

## 8. Atualizar somente uma conta

Por exemplo, para limpar `lid_jids` somente na conta `account_id = 2`:

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

Antes de executar a atualização, você pode verificar os registros:

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

## 9. Atualizar somente um contato

Por exemplo, para o contato com `id = 14580`:

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

Validação:

```sql
SELECT
  id,
  name,
  additional_attributes->'lid_jids' AS lid_jids
FROM contacts
WHERE id = 14580;
```

---

## 10. Atualizar vários contatos específicos

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

## 11. Remover completamente a chave `lid_jids`

Caso você prefira remover a propriedade, em vez de mantê-la vazia:

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

Depois:

```json
{
  "city": "",
  "description": ""
}
```

Para o MEGA, normalmente é mais conservador manter:

```json
"lid_jids": []
```

em vez de remover a chave, principalmente se o código espera que essa propriedade exista.

---

## 12. Verificar o resultado

### Confirmar que não existem arrays com dados

```sql
SELECT COUNT(*) AS lid_jids_pendentes
FROM contacts
WHERE additional_attributes ? 'lid_jids'
  AND jsonb_typeof(additional_attributes->'lid_jids') = 'array'
  AND jsonb_array_length(additional_attributes->'lid_jids') > 0;
```

O resultado esperado é:

```text
0
```

### Conferir contatos atualizados

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

## 13. Restaurar usando a cópia de segurança

Se você criou esta tabela:

```sql
contacts_lid_jids_backup_20260723
```

pode restaurar o conteúdo original de `additional_attributes` da seguinte forma:

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

Para restaurar somente `lid_jids`, sem substituir todo o JSON:

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

A segunda opção é mais segura caso outros atributos tenham sido alterados depois da criação do backup.

---

## 14. Sequência final recomendada

Esta é a sequência completa recomendada:

```sql
-- 1. Contar os registros afetados
SELECT COUNT(*)
FROM contacts
WHERE additional_attributes ? 'lid_jids'
  AND jsonb_typeof(additional_attributes->'lid_jids') = 'array'
  AND jsonb_array_length(additional_attributes->'lid_jids') > 0;

-- 2. Criar o backup
CREATE TABLE contacts_lid_jids_backup_20260723 AS
SELECT
  id,
  account_id,
  additional_attributes,
  updated_at
FROM contacts
WHERE additional_attributes ? 'lid_jids';

-- 3. Iniciar a transação
BEGIN;

-- 4. Esvaziar os arrays
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

-- 5. Verificar se ainda existem arrays preenchidos
SELECT COUNT(*) AS lid_jids_pendentes
FROM contacts
WHERE additional_attributes ? 'lid_jids'
  AND jsonb_typeof(additional_attributes->'lid_jids') = 'array'
  AND jsonb_array_length(additional_attributes->'lid_jids') > 0;

-- 6. Confirmar a alteração
COMMIT;
```

---

## Considerações importantes

- O comando não altera `phone_number`.
- O comando não altera `identifier`.
- O comando não altera o nome do contato.
- O comando não altera fotos, país, empresa ou perfis sociais.
- Somente o conteúdo de `additional_attributes.lid_jids` é substituído.
- Faça um backup antes de aplicar alterações em massa.
- Se o MEGA continuar adicionando valores em `lid_jids`, será necessário revisar o código ou a integração responsável por gravar esses identificadores.
- Em bancos de dados grandes, execute a operação em um período de baixa utilização.
- Caso existam réplicas, workers ou processos de sincronização ativos, verifique se eles não voltam a preencher o campo imediatamente.

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

Depois:

```json
{
  "city": "",
  "country": "",
  "lid_jids": [],
  "description": "",
  "company_name": ""
}
```
