# SQL Injection - Login Bypass

## Objetivo

Explorar uma vulnerabilidade de SQL Injection para realizar bypass de autenticação sem conhecer a senha do usuário.

---

## Análise Inicial

O formulário possuía dois campos:

* Username
* Password

Ao inserir caracteres especiais e testar entradas diferentes, foi possível perceber que a aplicação provavelmente construía a autenticação diretamente em uma query SQL.

Exemplo provável:

```sql
SELECT * FROM users
WHERE username='administrator'
AND password='senha'
```

O problema é que a entrada do usuário estava sendo concatenada diretamente na consulta.

---

## Exploração

Payload utilizado:

```sql
administrator' OR 1=1--
```

---

## Como o Payload Funciona

### 1. Fecha a string original

O caractere:

```sql
'
```

fecha a string do username.

---

### 2. Adiciona uma condição verdadeira

```sql
OR 1=1
```

retorna sempre verdadeiro.

---

### 3. Comenta o restante da query

```sql
--
```

faz o SQL ignorar o restante da instrução.

Query final:

```sql
SELECT * FROM users
WHERE username='administrator'
OR 1=1--'
AND password='qualquercoisa'
```

Como `1=1` sempre é verdadeiro, a verificação da senha deixa de ter efeito.

---

## Testes Realizados

### Não funcionou:

```sql
--'
```

Motivo:

Nenhum usuário válido foi especificado antes do comentário.

---

### Não funcionou:

```sql
OR '1'='1'
```

na senha.

Motivo:

A forma como `AND` e `OR` são processados pode alterar a lógica da consulta, fazendo com que a injeção não produza o resultado esperado.

Isso mostrou que SQL Injection não é apenas decorar payloads; é entender como a query está sendo construída pela aplicação.

---

## Resultado

Foi possível acessar a conta administrator sem conhecer a senha.

---

## Impacto

Esse tipo de vulnerabilidade pode permitir:

* Bypass de autenticação
* Acesso indevido a contas
* Escalada de privilégios
* Comprometimento da aplicação

---

## Mitigação

* Prepared Statements
* Parameterized Queries
* Validação de entrada
* ORM seguro
* Menor privilégio no banco de dados

---

## Aprendizados

Esse laboratório reforçou que SQL Injection consiste em manipular a lógica da consulta SQL, e não apenas inserir payloads aleatórios até algo funcionar.
