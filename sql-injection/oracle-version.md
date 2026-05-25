# SQL Injection - Querying Database Type and Version (Oracle)

## Objetivo

Explorar uma vulnerabilidade SQL Injection utilizando `UNION` para identificar o tipo e a versão do banco de dados Oracle.

---

## Análise Inicial

Após confirmar que a aplicação era vulnerável a SQL Injection, o próximo objetivo foi entender a estrutura da query original.

Para utilizar `UNION`, a consulta injetada precisa possuir a mesma quantidade de colunas da query original.

Foi realizado o seguinte teste:

```sql
' UNION SELECT 'abc','def' FROM dual--
```

---

## Screenshot

![Column Test](./screenshots/1.png)

---

## Como o Payload Funciona

### Fecha a string original

O:

```sql
'
```

fecha a string existente da query.

---

### Usa UNION para combinar consultas

```sql
UNION
```

junta o resultado da consulta injetada com a consulta original da aplicação.

---

### Testa quantidade de colunas

```sql
SELECT 'abc','def'
```

Os valores `abc` e `def` não possuem significado especial.

Eles foram utilizados apenas como valores de teste para descobrir:

- Quantas colunas existem
- Se as colunas aceitam texto
- Se o UNION funciona corretamente

---

### Uso do FROM dual

```sql
FROM dual
```

No Oracle, consultas simples precisam referenciar uma tabela.

`dual` é uma tabela especial utilizada para retornar valores sem depender de tabelas reais.

---

## Resultado do teste

Como `abc` e `def` apareceram na aplicação, foi possível concluir:

- A query possui 2 colunas
- Ambas aceitam valores de texto
- O `UNION` estava funcionando

---

## Extraindo informações reais

Depois de identificar a estrutura da query, os valores de teste foram substituídos por dados reais do banco:

```sql
' UNION SELECT BANNER,NULL FROM v$version--
```

---

## Screenshot

![Oracle Version](./screenshots/oracle2.png)
---

## Como o segundo payload funciona

```sql
SELECT BANNER,NULL
FROM v$version
```

### BANNER

`BANNER` é uma coluna que contém informações sobre a versão do banco Oracle.

---

### NULL

Foi utilizado `NULL` apenas para manter a quantidade correta de colunas.

A consulta precisava continuar retornando duas colunas.

---

### v$version

`v$version` é uma tabela interna do Oracle que armazena:

- Versão do banco
- Release
- Arquitetura
- Componentes instalados

---

## Resultado

Foi possível identificar:

- Oracle Database 11g
- Versão específica do banco
- Informações adicionais do ambiente

---

## Impacto

Uma vulnerabilidade desse tipo pode permitir:

- Enumeração do banco de dados
- Descoberta de tecnologias utilizadas
- Coleta de informações sensíveis
- Facilitar ataques posteriores

---

## Mitigação

- Prepared Statements
- Parameterized Queries
- Validação de entrada
- ORM seguro
- Menor privilégio no banco de dados

---

## Aprendizados

Esse laboratório mostrou que SQL Injection não é apenas inserir payloads aleatórios.

Antes de extrair dados reais, foi necessário:

- Entender a estrutura da query original
- Descobrir a quantidade de colunas
- Identificar quais delas aceitavam texto
- Trocar valores de teste por informações reais do banco

Isso reforçou a importância de entender a lógica por trás da vulnerabilidade em vez de apenas decorar payloads.
