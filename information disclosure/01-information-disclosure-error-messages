# Information Disclosure — Error Messages

## Contexto

A aplicação de e-commerce expõe mensagens de erro internas diretamente ao usuário. O parâmetro `productId` na URL do produto aceita qualquer valor, mas o back-end espera um número inteiro — e quando recebe algo diferente, devolve o stack trace completo sem nenhum tratamento.

---

## Análise inicial

Endpoint vulnerável:

```
GET /product?productId=2
```

O parâmetro `productId` é um inteiro. Ao substituir o valor por uma string qualquer (`a`, por exemplo), a aplicação quebra internamente e não captura o erro antes de exibi-lo.

```
GET /product?productId=a
```

---

## Exploração

A resposta foi um `Internal Server Error` com o stack trace completo:

```
java.lang.NumberFormatException: For input string: "a"
    at java.base/java.lang.NumberFormatException.forInputString(NumberFormatException.java:67)
    at java.base/java.lang.Integer.parseInt(Integer.java:661)
    ...
    Apache Struts 2 2.3.31
```

Nenhuma ferramenta necessária — um parâmetro inválido na URL foi suficiente.

O stack trace revelou:
- Linguagem: **Java**
- Framework: **Apache Struts 2, versão 2.3.31**
- Estrutura interna de classes e métodos do servidor

---

## Impacto

A versão exposta (Apache Struts 2.3.31) possui vulnerabilidades públicas conhecidas e catalogadas no CVE. Um atacante que obtém essa informação sabe exatamente qual exploit procurar — o reconhecimento que normalmente levaria horas foi eliminado por um único request com parâmetro inválido.

---

## Mitigação

Capturar exceções no back-end e retornar mensagens genéricas ao usuário (`Algo deu errado`, sem detalhes técnicos). Logs de erro devem existir, mas apenas internamente — nunca expostos na resposta HTTP.

---

## Técnicas de information disclosure além de error messages

Durante o estudo desse módulo, mapeei outros vetores comuns usados na vida real:

**Google Dorks** — busca por informações sensíveis indexadas pelo Google sem querer. Exemplos: `filetype:txt inurl:robots.txt`, `intext:senha site:trello.com`. Base de dorks disponível em exploit-db.com/google-hacking-database.

**WHOIS** — consulta de registro de domínio expõe nome do responsável, email, endereço e provedor de hospedagem. Ferramentas: who.is, registro.br.

**GitHub/GitLab** — repositórios públicos com chaves de API, credenciais hardcoded ou histórico de commits com dados sensíveis removidos depois mas ainda acessíveis.

**Respostas de APIs** — endpoints que retornam mais campos do que o front-end exibe. Inspecionar o JSON bruto da resposta frequentemente expõe IDs internos, emails e flags de permissão.

**Wayback Machine / Waymore** — versões antigas de páginas e arquivos que foram removidos do site mas permanecem arquivados. Útil para encontrar endpoints descontinuados e parâmetros antigos.

**Paths comuns** — testar manualmente `/robots.txt`, `/admin`, `/.git`, `/backup`. Se o diretório `.git` estiver acessível publicamente, é possível reconstruir o código-fonte completo via terminal com ferramentas como `git-dumper`.
