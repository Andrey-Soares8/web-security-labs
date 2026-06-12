# Web Security Labs

![PortSwigger](https://img.shields.io/badge/PortSwigger-Web%20Security%20Academy-orange)
![Burp Suite](https://img.shields.io/badge/Burp%20Suite-Community%20Edition-blue)
![Status](https://img.shields.io/badge/Status-Em%20andamento-yellow)

Repositório com write-ups técnicos de laboratórios da PortSwigger Web Security Academy, focado em segurança de aplicações web, análise de vulnerabilidades e metodologia prática de exploração em ambiente controlado.

O objetivo deste projeto é documentar meu aprendizado hands-on em Application Security, registrando raciocínio técnico, etapas de análise, payloads utilizados, evidências, impacto da vulnerabilidade e possíveis mitigações.

---

## Objetivo

Construir experiência prática em segurança web através de:

- Análise de vulnerabilidades reais em laboratórios controlados
- Uso de ferramentas como Burp Suite, navegador e DevTools
- Leitura e manipulação de requisições HTTP/HTTPS
- Documentação técnica clara e objetiva
- Entendimento do impacto real de cada falha
- Criação de um portfólio público de aprendizado em cybersecurity

Todos os labs documentados foram resolvidos em ambiente educacional da PortSwigger Web Security Academy.

---

## Progresso Atual

| Categoria | Write-ups publicados | Status |
|---|---:|---|
| SQL Injection | 9 | ✅ Documentado |
| Information Disclosure | 4 | ✅ Documentado |
| XSS | 3 | ✅ Documentado |
| Broken Authentication | 2 | ✅ Documentado |
| Access Control | 3 | ✅ Documentado |
| SSRF | 0 | ⏳ Planejado |
| XXE | 0 | ⏳ Planejado |
| File Upload | 0 | ⏳ Planejado |

**Total: 21 write-ups publicados.**

---

## Labs Recentes Documentados

### Access Control

- User ID controlled by request parameter
- Insecure direct object references
- User role controlled by request parameter

O módulo de Access Control está sendo documentado com foco em autorização quebrada, IDOR, controle de função por parâmetros manipuláveis e falhas de validação no servidor.

---

## Skills Demonstradas

- Análise de requisições HTTP/HTTPS
- Uso do Burp Suite Proxy, Repeater e Intruder
- Exploração de SQL Injection
- Blind SQL Injection com respostas condicionais e time-based
- Cross-Site Scripting refletido, armazenado e DOM-based
- Análise de sources e sinks em JavaScript
- Authentication bypass
- Information disclosure
- Enumeração e análise de endpoints
- Insecure Direct Object References (IDOR)
- Bypass de autorização por parâmetros e cookies manipuláveis
- Análise de controle de acesso server-side vs client-side
- Organização de evidências técnicas com imagens
- Documentação de impacto e mitigação

---

## Tecnologias e Ferramentas

- Burp Suite
- Navegador com DevTools
- HTTP/HTTPS
- SQL
- JavaScript
- Python para scripts auxiliares, quando necessário
- PortSwigger Web Security Academy

---

## Estrutura do Repositório

```txt
web-security-labs/
├── sql-injection/
│   └── Write-ups de SQL Injection
├── xss/
│   └── Write-ups de Cross-Site Scripting
├── information disclosure/
│   └── Write-ups de Information Disclosure
├── Broken Authentication/
│   └── Write-ups de falhas de autenticação
├── access-control/
│   └── Write-ups de falhas de controle de acesso
└── README.md
```

---

## Estrutura dos Write-ups

Cada write-up segue uma estrutura objetiva, focada em raciocínio técnico e evidências:

```txt
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

Sempre que fizer sentido, os write-ups incluem imagens do Burp Suite, da aplicação vulnerável e da confirmação final do lab resolvido.

---

## Categorias

### SQL Injection

Write-ups focados em exploração de falhas de SQL Injection, incluindo técnicas union-based, error-based, blind conditional response e blind time-based.

### Cross-Site Scripting

Write-ups sobre XSS refletido, armazenado e DOM-based, com análise de sinks, sources, contexto de execução e impacto no navegador.

### Information Disclosure

Write-ups sobre exposição indevida de informações sensíveis, arquivos ocultos, endpoints administrativos e comportamento inseguro da aplicação.

### Broken Authentication

Write-ups sobre falhas em autenticação, bypass de controles, enumeração de usuários e problemas em fluxos de login.

### Access Control

Write-ups sobre falhas de autorização, IDOR, acesso indevido a áreas administrativas e controle de privilégios baseado em dados manipuláveis pelo usuário.

---

## Próximos Objetivos

- Continuar o módulo de Access Control
- Aprofundar em SSRF, XXE e File Upload
- Melhorar a padronização dos write-ups
- Adicionar evidências visuais relevantes em cada lab
- Documentar tentativas descartadas quando elas fizerem parte do raciocínio
- Criar scripts auxiliares para automatizar partes repetitivas dos labs
- Evoluir a documentação com foco em impacto, mitigação e clareza técnica

---

## Uso Ético

Este repositório tem finalidade exclusivamente educacional.

Os laboratórios documentados pertencem à PortSwigger Web Security Academy e foram resolvidos em ambiente controlado. As técnicas descritas aqui devem ser usadas apenas em sistemas próprios, ambientes de laboratório ou aplicações onde exista autorização explícita.

---

## Contato

GitHub: [@Andrey-Soares8](https://github.com/Andrey-Soares8)

LinkedIn: [andreysoares8](https://www.linkedin.com/in/andreysoares8)

---

Feito para documentar evolução prática em segurança de aplicações web.
