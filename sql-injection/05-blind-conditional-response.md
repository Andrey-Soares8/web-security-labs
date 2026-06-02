# Blind SQL Injection — Conditional Errors (Oracle)

## Contexto

Diferente dos labs anteriores, aqui a aplicação não retorna dados nem mensagens visíveis. A única coisa que vaza informação é o **comportamento da resposta**: erro HTTP 500 quando a condição é verdadeira, resposta normal quando é falsa.

O vetor estava no cookie `TrackingId`.

---

## Confirmando a injeção

Dois payloads para verificar se o banco respondia a condições:

```sql
TrackingId=xyz'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'
```
→ Retornou erro 500 (divisão por zero executada, condição verdadeira)

```sql
TrackingId=xyz'||(SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'
```
→ Resposta normal (condição falsa, erro não disparou)

Comportamento confirmado: dá pra usar erro/sem erro como canal de informação.

---

## Extraindo a senha

Com o canal confirmado, o próximo passo foi testar a senha do `administrator` caractere por caractere com `SUBSTR`.

Payload base:

```sql
TrackingId=xyz'||(SELECT CASE WHEN (SUBSTR(password,1,1)='a') THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
```

O número do meio em `SUBSTR(password,1,1)` indica a posição do caractere. Fui trocando manualmente: posição 1, depois 2, depois 3, e assim por diante.

Para cada posição, rodei o **Burp Intruder** no modo **Sniper** com o payload variando de `a-z` e `0-9`. Quando a resposta voltava com erro 500, o caractere estava correto.

Resultado: senha completa extraída caractere a caractere.

---

## Impacto

Blind SQLi com conditional errors é mais trabalhoso, mas igualmente destrutivo. Sem nenhuma mensagem visível na tela, foi possível extrair credenciais completas do banco de dados.

---

## Mitigação

Prepared statements eliminam a injeção. Além disso, mensagens de erro genéricas para o usuário evitam que o comportamento interno da aplicação vire canal de exfiltração.
