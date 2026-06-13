# Web Security Labs

![PortSwigger](https://img.shields.io/badge/PortSwigger-Web%20Security%20Academy-orange)
![Burp Suite](https://img.shields.io/badge/Burp%20Suite-Proxy%20%7C%20Repeater%20%7C%20Intruder-blue)
![Status](https://img.shields.io/badge/status-28%20write--ups%20documentados-brightgreen)
![Security](https://img.shields.io/badge/foco-Application%20Security-red)

Repositório com write-ups técnicos de laboratórios da PortSwigger Web Security Academy, focado em segurança de aplicações web, análise de vulnerabilidades e metodologia prática de exploração em ambiente controlado.

O objetivo deste projeto é documentar meu aprendizado hands-on em Application Security, registrando raciocínio técnico, etapas de análise, payloads utilizados, evidências, impacto da vulnerabilidade e possíveis mitigações.

Todos os labs documentados foram resolvidos em ambiente educacional e autorizado.

---

## Objetivo

Construir experiência prática em segurança web através de:

- Análise de vulnerabilidades reais em laboratórios controlados
- Uso de Burp Suite, navegador e DevTools
- Leitura, interceptação e manipulação de requisições HTTP/HTTPS
- Exploração manual antes de automação
- Documentação técnica clara e objetiva
- Registro de evidências com prints e payloads
- Entendimento do impacto real de cada vulnerabilidade
- Criação de um portfólio público voltado para Application Security

---

## Progresso Atual

| Categoria | Write-ups publicados | Status |
|---|---:|---|
| SQL Injection | 9 | ✅ Documentado |
| Information Disclosure | 4 | ✅ Documentado |
| Cross-Site Scripting (XSS) | 3 | ✅ Documentado |
| Broken Authentication | 3 | ✅ Documentado |
| Access Control | 3 | ✅ Documentado |
| Server-Side Request Forgery (SSRF) | 2 | ✅ Documentado |
| XML External Entity (XXE) | 2 | ✅ Documentado |
| File Upload Vulnerabilities | 2 | ✅ Documentado |

**Total: 28 write-ups publicados.**

---

## Módulos Documentados

### SQL Injection

Write-ups focados em exploração de falhas de SQL Injection, incluindo recuperação de dados ocultos, login bypass, enumeração de estrutura de banco, UNION attacks, extração de múltiplos valores, blind SQL Injection por resposta condicional e time-based.

**Principais técnicas demonstradas:**

- Manipulação de parâmetros vulneráveis
- Bypass de autenticação via SQL Injection
- Uso de `UNION SELECT`
- Enumeração de tabelas e colunas
- Extração de dados sensíveis
- Blind SQL Injection com resposta condicional
- Blind SQL Injection com atraso de tempo
- Identificação de versão de banco de dados Oracle, MySQL e Microsoft

---

### Information Disclosure

Write-ups sobre exposição indevida de informações sensíveis, análise de mensagens de erro, arquivos ocultos, endpoints administrativos, metadados, comportamento inseguro da aplicação e vazamento por versionamento.

**Principais técnicas demonstradas:**

- Análise de mensagens de erro
- Enumeração de arquivos e endpoints
- Identificação de `phpinfo()` exposto
- Bypass de autenticação via informação vazada
- Exploração de diretórios `.git` expostos
- Reconstrução de informações sensíveis a partir de arquivos públicos

---

### Cross-Site Scripting (XSS)

Write-ups sobre XSS refletido, armazenado e DOM-based, com foco em contexto de execução, análise de sources e sinks, payloads mínimos e impacto no navegador.

**Principais técnicas demonstradas:**

- XSS refletido em parâmetro de busca
- Stored XSS em comentário/chat
- DOM XSS via `location.search`
- Análise de `innerHTML` como sink inseguro
- Diferença entre execução no servidor e execução no navegador
- Validação de payloads no contexto correto

---

### Broken Authentication

Write-ups sobre falhas em autenticação, enumeração de usuários, bypass de 2FA, brute force protegido de forma fraca e análise de diferenças nas respostas da aplicação.

**Principais técnicas demonstradas:**

- Username enumeration
- Password brute force em laboratório
- Análise de mensagens de erro
- Bypass simples de 2FA
- Uso de Burp Intruder
- Controle de velocidade com Resource Pool
- Ataques sincronizados com Pitchfork

---

### Access Control

Write-ups sobre falhas de autorização, IDOR, acesso indevido a áreas administrativas e controle de privilégios baseado em dados manipuláveis pelo usuário.

**Labs documentados:**

- User ID controlled by request parameter
- Insecure direct object references
- User role controlled by request parameter

**Principais técnicas demonstradas:**

- IDOR via parâmetro previsível
- Enumeração de objetos por ID
- Acesso indevido a recursos de outros usuários
- Manipulação de cookie `Admin=false` para `Admin=true`
- Diferença entre controle client-side e server-side
- Validação de autorização por recurso, não apenas por sessão

---

### Server-Side Request Forgery (SSRF)

Write-ups sobre abuso de funcionalidades server-side para forçar o back-end a realizar requisições internas.

**Labs documentados:**

- Basic SSRF against the local server
- Basic SSRF against another back-end system

**Principais técnicas demonstradas:**

- Manipulação de parâmetro `stockApi`
- Acesso ao painel interno via `localhost`
- Entendimento de loopback no contexto do servidor
- Enumeração de rede interna `192.168.0.X`
- Identificação de back-end interno na porta `8080`
- Execução de ação administrativa via SSRF

---

### XML External Entity (XXE)

Write-ups sobre exploração de XML parsers mal configurados, entidades externas e leitura de recursos internos.

**Labs documentados:**

- Exploiting XXE using external entities to retrieve files
- Exploiting XXE to perform SSRF attacks

**Principais técnicas demonstradas:**

- Identificação de entrada XML
- Criação de `DOCTYPE`
- Uso de entidade externa com `SYSTEM`
- Leitura de arquivo local com `file://`
- Chamada de entidade via `&entity;`
- Uso de XXE para SSRF
- Diferença entre XML, entidade interna e entidade externa

---

### File Upload Vulnerabilities

Write-ups sobre upload inseguro de arquivos, execução de PHP no servidor, web shell básica e bypass de validações fracas.

**Labs documentados:**

- Remote code execution via web shell upload
- Web shell upload via Content-Type restriction bypass

**Principais técnicas demonstradas:**

- Upload de arquivo `.php`
- Confirmação de execução com `getcwd()`
- Enumeração de filesystem com `scandir()`
- Identificação de diretórios relevantes como `/home`
- Leitura de arquivo com `file_get_contents()`
- Bypass de validação fraca alterando `Content-Type`
- Diferença entre extensão real do arquivo e tipo declarado pelo cliente

---

## Skills Demonstradas

- Análise de requisições HTTP/HTTPS
- Interceptação de tráfego com Burp Suite Proxy
- Testes manuais com Burp Repeater
- Enumeração e fuzzing com Burp Intruder
- Manipulação de cookies, parâmetros e headers
- Exploração de SQL Injection
- Blind SQL Injection condicional e time-based
- Exploração de XSS refletido, armazenado e DOM-based
- Análise de JavaScript, sources e sinks
- Exploração de Information Disclosure
- IDOR e falhas de Access Control
- SSRF contra serviços locais e redes internas
- XXE para leitura de arquivos e SSRF
- Upload inseguro de arquivos e execução de web shell
- Enumeração de filesystem em ambiente Linux
- Organização de evidências técnicas com imagens
- Escrita de impacto, causa raiz e mitigação

---

## Tecnologias e Ferramentas

- Burp Suite
- Navegador com DevTools
- HTTP/HTTPS
- HTML
- JavaScript
- SQL
- XML
- PHP básico para labs de File Upload
- Linux filesystem básico
- PortSwigger Web Security Academy

---

## Estrutura do Repositório

```text
web-security-labs/
├── sql-injection/
│   ├── screenshots/
│   └── Write-ups de SQL Injection
├── xss/
│   ├── images/
│   └── Write-ups de Cross-Site Scripting
├── information disclosure/
│   └── Write-ups de Information Disclosure
├── Broken Authentication/
│   ├── images/
│   └── Write-ups de falhas de autenticação
├── access-control/
│   ├── images/
│   └── Write-ups de falhas de controle de acesso
├── SSRF/
│   ├── images/
│   └── Write-ups de SSRF
├── XXE/
│   ├── images/
│   └── Write-ups de XXE
├── file-upload/
│   ├── images/
│   └── Write-ups de File Upload
└── README.md
```

---

## Estrutura dos Write-ups

Cada write-up segue uma estrutura objetiva, focada em raciocínio técnico e evidências:

```text
# Nome do Lab

## Contexto
Descrição breve do lab e do objetivo.

## Análise Inicial
Primeiros testes, hipóteses e vetores avaliados.

## Exploração
Passo a passo da exploração que levou à solução.

## Por que funcionou
Explicação técnica da causa da vulnerabilidade.

## Impacto
Consequência da falha em um ambiente real.

## Mitigação
Como a falha poderia ser corrigida.

## Aprendizados
Pontos práticos absorvidos durante o lab.
```

Sempre que faz sentido, os write-ups incluem imagens do Burp Suite, da aplicação vulnerável e da confirmação final do lab resolvido.

---

## Diferencial do Repositório

Este repositório não documenta apenas o payload final. A ideia é registrar o raciocínio completo:

- O que foi testado primeiro
- O que não funcionou
- Por que determinado vetor foi descartado
- Qual detalhe levou à solução
- Qual era a causa real da vulnerabilidade
- Qual seria o impacto em uma aplicação real
- Como corrigir a falha corretamente

Esse formato deixa o portfólio mais próximo de uma análise técnica real de segurança, e não apenas de uma lista de respostas dos labs.

---

## Próximos Objetivos

- Padronizar nomes de arquivos em todos os módulos
- Revisar títulos e sumários dos write-ups antigos
- Melhorar a organização das imagens por lab
- Adicionar índice interno por categoria
- Revisar português técnico e clareza dos textos
- Adicionar severidade, impacto e mitigação de forma mais consistente
- Evoluir o repositório como portfólio para Application Security / SOC / Pentest Jr

---

## Uso Ético

Este repositório tem finalidade exclusivamente educacional.

Os laboratórios documentados pertencem à PortSwigger Web Security Academy e foram resolvidos em ambiente controlado. As técnicas descritas aqui devem ser usadas apenas em sistemas próprios, ambientes de laboratório ou aplicações onde exista autorização explícita.

---

## Contato

GitHub: [@Andrey-Soares8](https://github.com/Andrey-Soares8)

LinkedIn: [andreysoares8](https://www.linkedin.com/in/andreysoares8/)

---

Feito para documentar evolução prática em segurança de aplicações web.
