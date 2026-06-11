# Web Security Labs

![PortSwigger](https://img.shields.io/badge/PortSwigger-Web%20Security%20Academy-orange)
![Burp Suite](https://img.shields.io/badge/Burp%20Suite-Testing%20Tool-red)
![Status](https://img.shields.io/badge/Status-In%20Progress-blue)

Repositório com write-ups técnicos de laboratórios da **PortSwigger Web Security Academy**, focado em segurança de aplicações web, análise de vulnerabilidades e metodologia prática de exploração em ambiente controlado.

O objetivo deste projeto é documentar meu aprendizado hands-on em **Application Security**, registrando o raciocínio técnico, etapas de análise, payloads utilizados, impacto da vulnerabilidade e possíveis mitigações.

---

## 🎯 Objetivo

Construir experiência prática em segurança web através de:

* Análise de vulnerabilidades reais em laboratórios controlados
* Uso de ferramentas como Burp Suite, navegador e scripts auxiliares
* Documentação técnica clara e objetiva
* Entendimento do impacto de cada falha
* Criação de um portfólio público de aprendizado em cybersecurity

Todos os labs documentados foram resolvidos em ambiente educacional da PortSwigger Web Security Academy.

---

## 📊 Progresso Atual

| Categoria              | Write-ups Publicados | Status          |
| ---------------------- | -------------------: | --------------- |
| Information Disclosure |                    4 | ✅ Documentado   |
| SQL Injection          |                    9 | ✅ Documentado   |
| XSS                    |                    3 | ✅ Documentado   |
| Broken Authentication  |                    2 | 🔄 Em andamento |
| Access Control         |                    0 | ⏳ Planejado     |
| SSRF                   |                    0 | ⏳ Planejado     |
| XXE                    |                    0 | ⏳ Planejado     |
| File Upload            |                    0 | ⏳ Planejado     |

**Total:** 18 write-ups publicados.

---

## 🧠 Skills Demonstradas

* Análise de requisições HTTP/HTTPS
* Exploração de SQL Injection
* Blind SQL Injection com respostas condicionais e time-based
* Cross-Site Scripting refletido, armazenado e DOM-based
* Authentication bypass
* Information disclosure
* Enumeração e análise de endpoints
* Uso do Burp Suite Repeater, Intruder e Proxy
* Documentação técnica de vulnerabilidades
* Organização de evidências e payloads

---

## 🛠️ Tecnologias e Ferramentas

* Burp Suite
* Navegador com DevTools
* HTTP/HTTPS
* SQL
* JavaScript
* Python para scripts auxiliares, quando necessário
* PortSwigger Web Security Academy

---

## 📁 Estrutura do Repositório

```txt
web-security-labs/
├── sql-injection/
│   └── Write-ups de SQL Injection
├── xss/
│   └── Write-ups de Cross-Site Scripting
├── information-disclosure/
│   └── Write-ups de Information Disclosure
├── broken-authentication/
│   └── Write-ups de falhas de autenticação
└── README.md
```

---

## 📝 Estrutura dos Write-ups

Cada write-up segue uma estrutura simples e objetiva:

```md
# Nome do Lab

## Módulo
Categoria da vulnerabilidade.

## Dificuldade
Nível do laboratório.

## Objetivo
O que era necessário fazer para resolver o lab.

## Vulnerabilidade
Tipo da falha, causa técnica e impacto.

## Metodologia
Etapas de análise, enumeração e exploração.

## Payloads Utilizados
Payloads ou requisições relevantes usados no laboratório.

## Resultado
Como a vulnerabilidade foi confirmada e o lab resolvido.

## Mitigação
Como a falha poderia ser corrigida em um ambiente real.
```

---

## 📌 Categorias

### SQL Injection

Write-ups focados em exploração de falhas de SQL Injection, incluindo técnicas union-based, error-based, blind conditional response e blind time-based.

### Cross-Site Scripting

Write-ups sobre XSS refletido, armazenado e DOM-based, com análise de sinks, sources, contexto de execução e impacto no navegador.

### Information Disclosure

Write-ups sobre exposição indevida de informações sensíveis, arquivos ocultos, endpoints administrativos e comportamento inseguro da aplicação.

### Broken Authentication

Write-ups sobre falhas em autenticação, bypass de controles, enumeração de usuários e problemas em fluxos de login.

---

## 🚀 Próximos Objetivos

* Completar os módulos principais da PortSwigger Web Security Academy
* Aprofundar em Access Control, SSRF, XXE e File Upload
* Melhorar a padronização dos write-ups
* Adicionar mais evidências visuais quando fizer sentido
* Criar scripts auxiliares para automatizar partes repetitivas dos labs
* Evoluir a documentação com foco em impacto e mitigação

---

## ⚠️ Uso Ético

Este repositório tem finalidade exclusivamente educacional.

Os laboratórios documentados pertencem à PortSwigger Web Security Academy e foram resolvidos em ambiente controlado. As técnicas descritas aqui devem ser usadas apenas em sistemas próprios, ambientes de laboratório ou aplicações onde exista autorização explícita.

---

## 📫 Contato

**GitHub:** [@Andrey-Soares8](https://github.com/Andrey-Soares8)

**LinkedIn:** [andreysoares8](https://www.linkedin.com/in/andreysoares8/)

---

Feito para documentar evolução prática em segurança de aplicações web.
