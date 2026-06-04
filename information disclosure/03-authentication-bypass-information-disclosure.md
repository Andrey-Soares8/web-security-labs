# Information Disclosure — Authentication Bypass via TRACE Method

## Contexto

O painel administrativo da aplicação restringe acesso com base no IP do cliente. O problema: essa lógica depende de um header HTTP customizado que qualquer cliente pode forjar — e o método TRACE revelou exatamente qual header usar.

---

## Análise inicial

Testando paths comuns na URL:

```
/robots.txt  → nada útil
/backup      → não encontrado
/admin       → encontrado, mas bloqueado:
               "Admin interface only available to local users"
```

A aplicação confirmou que `/admin` existe, mas filtra por localidade. A questão passou a ser: como ela determina se o usuário é "local"?

---

## Exploração — Fase 1: Descoberta via TRACE

O método HTTP `TRACE` é usado para diagnóstico — ele ecoa de volta a requisição completa como o servidor a recebeu, incluindo headers adicionados por proxies e middlewares internos.

No Burp Repeater, troquei o método de `GET` para `TRACE`:

```
TRACE /admin HTTP/2
Host: 0a6100230405e18a83d8054200490043.web-security-academy.net
```

A resposta revelou a requisição completa como vista pelo servidor, incluindo um header que não estava na requisição original:

```
X-Custom-IP-Authorization: 187.34.207.53
```

Esse header estava sendo injetado automaticamente pela infraestrutura da aplicação com o IP real do cliente. A lógica de autorização do painel admin era baseada nele — algo equivalente a:

```php
if ($_SERVER['HTTP_X_CUSTOM_IP_AUTHORIZATION'] == '127.0.0.1') {
    // permitir acesso admin
}
```

---

## Exploração — Fase 2: Bypass via Match & Replace

Com o mecanismo exposto, a solução foi forjar o header em todas as requisições automaticamente. No Burp Proxy, adicionei uma regra em **Match and Replace**:

```
Type:    Request header
Match:   (vazio)
Replace: X-Custom-IP-Authorization: 127.0.0.1
```

Isso injetou o header com IP de loopback em cada request. O painel `/admin` foi liberado imediatamente — a aplicação passou a me tratar como usuário local.

Com acesso ao painel, o usuário `carlos` foi deletado.

---

## Impacto

Dois problemas encadeados tornaram isso possível. O método TRACE estava habilitado em produção, vazando a lógica interna de autorização. E a própria lógica dependia de um header que qualquer cliente pode forjar livremente — controle de acesso baseado em header sem validação server-side não oferece nenhuma proteção real.

---

## Mitigação

Desabilitar o método TRACE em produção — ele não tem uso legítimo em aplicações web. Nunca basear lógica de autorização em headers que o cliente pode manipular. Controle de acesso a painéis administrativos deve acontecer no servidor com autenticação real, não por verificação de IP via header.
