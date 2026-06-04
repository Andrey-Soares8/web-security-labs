# Information Disclosure — Version Control History

## Contexto

O diretório `.git` da aplicação estava exposto publicamente. Com acesso ao histórico de commits, foi possível recuperar uma senha de administrador que havia sido removida do código — mas que ainda estava visível no diff do commit.

---

## Análise inicial

Testando paths comuns na URL:

```
/robots.txt  → nada útil
/backup      → não encontrado
/admin       → bloqueado
/.git        → acessível
```

O diretório `.git` aberto em produção significa que todo o histórico de versionamento do projeto está disponível para download.

---

## Exploração — Fase 1: Download do repositório

Com o `.git` acessível, baixei o conteúdo completo recursivamente via terminal:

```bash
wget -r https://0a1a006104f5c78b81e511c7006b006d.web-security-academy.net/.git
```

Isso baixou todos os objetos do repositório localmente — commits, blobs, trees.

---

## Exploração — Fase 2: Análise do histórico

Dentro do diretório baixado, inspecionei o log de commits:

```bash
git log
```

Um commit chamou atenção imediato:

```
"Remove admin password from config"
```

Mensagens como essa são um sinal claro de que uma credencial foi hardcoded e depois removida — mas no Git, "remover" não apaga o histórico. O dado ainda existe no diff.

Inspecionei as alterações desse commit:

```bash
git show <hash do commit>
```

O diff do arquivo `admin.conf` mostrou a linha removida:

```diff
- ADMIN_PASSWORD=env_password_value
+ ADMIN_PASSWORD=$ENV_VAR
```

A senha original estava visível em texto puro na linha marcada com `-`.

---

## Exploração — Fase 3: Acesso e impacto

Com a senha recuperada, fiz login como `administrator` diretamente na aplicação. O painel admin foi acessado e o usuário `carlos` deletado.

---

## Impacto

Expor o `.git` em produção equivale a entregar o código-fonte completo da aplicação — incluindo todo o histórico de alterações. Credenciais removidas em commits anteriores continuam acessíveis para sempre no histórico. Em ambientes reais, esse vetor já foi responsável por vazamentos de chaves de API, tokens de acesso e senhas de banco de dados.

---

## Mitigação

Nunca subir credenciais para repositórios, mesmo que a intenção seja remover depois — o histórico do Git é permanente. Bloquear acesso público ao diretório `.git` via configuração do servidor web. Usar variáveis de ambiente desde o início para qualquer dado sensível. Ferramentas como `truffleHog` e `git-secrets` automatizam a detecção de credenciais no histórico.
