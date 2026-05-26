# Blind SQL Injection with Time Delays

## Objetivo

Explorar Blind SQL Injection utilizando atraso na resposta da aplicação.

---

## Payload utilizado

```sql
'||pg_sleep(10)--
```

## Como funciona

```sql
pg_sleep(10)
```

faz o banco esperar 10 segundos antes de responder.

Resultado:

- Demora → payload executado
- Resposta normal → payload não executado

---

## Aprendizado

Mesmo sem retornar mensagens ou erros, uma aplicação ainda pode vazar informações através do tempo de resposta.
