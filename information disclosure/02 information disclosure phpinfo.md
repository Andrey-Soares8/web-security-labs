# Information Disclosure — PHP Info File

## Contexto

A aplicação expõe um arquivo `phpinfo.php` dentro do diretório `/cgi-bin/`, acessível publicamente. Esse tipo de arquivo é gerado automaticamente pelo PHP para fins de diagnóstico e nunca deveria existir em ambiente de produção — ele imprime a configuração completa do servidor.

---

## Análise inicial

Tentativas iniciais com paths comuns na URL não retornaram nada:

```
/robots.txt  → nada relevante
/admin       → não encontrado
/backup      → não encontrado
```

A abordagem mudou para inspeção passiva via Burp Suite. Na aba **Target > Site map**, a estrutura de diretórios da aplicação ficou visível após a navegação normal pelo site:

```
/
├── cgi-bin/
│   └── phpinfo.php   ← arquivo suspeito
├── image/
├── product/
└── resources/
```

O nome `cgi-bin` chamou atenção — é um diretório tradicional de servidores web usado para scripts executáveis no servidor. Encontrar um `phpinfo.php` dentro dele é um sinal claro de arquivo de diagnóstico esquecido.

---

## Exploração

Com o arquivo identificado no site map, enviei a requisição para o **Repeater** e executei:

```
GET /cgi-bin/phpinfo.php HTTP/2
Host: 0ace002e0494f2c2bd0bf76b00be00fb.web-security-academy.net
```

A resposta retornou a página completa do `phpinfo()`:

- **PHP Version:** 7.4.3-4ubuntu2.29
- **System:** Linux 79a0aedeff91 4.14.355-281.714
- **Server API:** CGI/FastCGI
- **Build Date:** Mar 25 2025
- **Configuration paths:** `/etc/php/7.4/cgi/php.ini`, `/etc/php/7.4/cgi/conf.d/`
- **Loaded extensions:** json, sockets, calendar, ftp, e vários outros

---

## Impacto

A versão exata do PHP exposta permite busca direta por CVEs correspondentes. As configurações de extensões e paths do servidor facilitam ataques direcionados — um atacante sabe exatamente o que está instalado e onde. Em versões antigas do PHP, o próprio `phpinfo.php` servido via CGI é vetor de RCE através de manipulação de argumentos na query string (CVE-2012-1823).

---

## Mitigação

Remover qualquer arquivo `phpinfo.php` de ambientes de produção. Se necessário para diagnóstico, restringir acesso por IP via configuração do servidor web. Auditar regularmente o servidor em busca de arquivos de debug esquecidos.
