
# Reflected XSS — HTML Context sem Encoding

## Contexto

A barra de busca da aplicação reflete o termo pesquisado diretamente na página sem nenhum tratamento. O browser interpreta o conteúdo refletido como HTML, o que permite injetar tags executáveis junto com o input.

---

## Análise inicial

Endpoint vulnerável:

```
GET /?search=teste
```

A resposta renderizava o termo na página:

```html
<h1>0 resultados para: teste</h1>
```

O valor do input ia direto pro HTML sem encoding — qualquer caractere especial chegava intacto ao browser.

---

## Exploração

Payload inserido na barra de busca:

```html
<script>alert(1)</script>
```

A resposta virou:

```html
<h1>0 resultados para: <script>alert(1)</script></h1>
```

O browser interpretou como HTML válido, executou o script e disparou o `alert(1)`.

Nenhuma ferramenta necessária — payload direto no campo de busca.

---

## Impacto

Em ambiente real, `alert(1)` seria substituído por código que rouba cookies de sessão, redireciona o usuário para páginas falsas ou realiza ações em nome da vítima. O vetor funciona distribuindo um link com o payload na URL — qualquer pessoa que clicar executa o script no próprio browser.

---

## Mitigação

Escapar caracteres HTML especiais antes de renderizar qualquer dado controlado pelo usuário. Os caracteres `<` e `>` viram `&lt;` e `&gt;` — o browser exibe como texto e nunca interpreta como tag. A regra é simples: dado do usuário nunca entra cru no HTML.
