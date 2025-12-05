# Roadmap Completo de Pentest & Red Team

---

## PARTE 1 — RESULTADO RÁPIDO (0 → JUNIOR OPERACIONAL)

**Objetivo:**  
Fazer você hackear máquinas, entender vulnerabilidades, escalar privilégios básicos e terminar apto para fazer labs (HTB Easy, TryHackMe) sozinho.

**Tempo:** 1 a 3 meses (com 3–4 horas/dia)

---

### 1. Fundamentos (O mínimo necessário pra operar)

**O que aprender:**

- Linux básico (cd, ls, cp, grep, find, chmod, chown, ps…)
- Redes essenciais (TCP/IP, DNS, HTTP)
- Entendimento do Shell
- Nmap básico
- Browsers + DevTools

**Checklist:**

- [x] Sei navegar no sistema com facilidade
- [x] Sei manipular arquivos e permissões
- [x] Sei entender um nmap -sV
- [x] Sei analisar resposta HTTP

**Mini-desafio:**  
Comprometer Metasploitable2 explorando 2 serviços básicos.

---

### 2. Enumeração Básica (o que um iniciante PRECISA dominar)

**O que aprender:**

- Nmap (varredura total, portas, scripts)
- WhatWeb
- gobuster / ffuf básico
- enum4linux básico
- Leitura de banners

**Checklist:**

- [x] Rodar nmap corretamente
- [ ] Identificar serviços vulneráveis pelo banner
- [x] Fazer fuzzing simples

**Mini-desafio:**  
Em 3 máquinas fáceis do VulnHub: apenas listar superfície de ataque (portas, serviços, tech stack).

---

### 3. Web Hacking Básico

**Aprender:**

- OWASP Top 10 superficial
- SQLi básica
- XSS básico
- LFI simples
- Upload malicioso básico

**Checklist:**

- [ ] Identificar parâmetros vulneráveis
- [ ] Fazer SQLi com ajuda de sqlmap
- [ ] Explorar XSS simples
- [ ] Subir webshell via upload

**Mini-desafio:**  
Completar 5 labs básicos do PortSwigger.

---

### 4. Shell e Privilege Escalation Básica

**Aprender:**

- SUID discovery
- sudo -l abusos
- PATH Hijacking simples
- Cronjobs básicos expostos
- LinPEAS (interpretar saída)

**Checklist:**

- [ ] Encontrar SUIDs
- [ ] Abusar de sudo mal configurado
- [ ] Entender saída do linpeas

**Mini-desafio:**  
Virar root em 3 máquinas fáceis do VulnHub.

---

### 5. Ciclo de Pentest Básico

**Aprender:**

- Recon
- Enumeração
- Exploração
- Escalação
- Relatório simples

**Checklist:**

- [ ] Capto evidências
- [ ] Explico descoberta
- [ ] Explico impacto

**Mini-desafio:**  
Fazer um relatório real sobre a máquina "Basic Pentesting" do TryHackMe.

---

### RESULTADO DO NÍVEL 1

- ✔ Você hackeia máquinas "Easy"
- ✔ Você entende vulnerabilidades comuns
- ✔ Você sabe ganhar e manter um shell básico
- ✔ Você pensa como pentester iniciante

---

## PARTE 2 — MELHORANDO (JUNIOR → PLENO)

**Objetivo:**  
Fazer você se tornar um pentester independente, capaz de comprometer ambientes e explicar tudo tecnicamente com clareza.

**Tempo:** 3 a 8 meses

---

### 1. Linux PROFISSIONAL

**Aprender:**

- Permissões avançadas
- SUID / SGID / Sticky bit
- Processos (ps/top/pgrep/pkill)
- systemctl (serviços, unidades, timers)
- journalctl (logs, filtros)
- tcpdump
- bash avançado

**Checklist:**

- [ ] Interpretar processos suspeitos
- [ ] Ler logs com precisão
- [ ] Manipular serviços
- [ ] Criar scripts operacionais

**Mini-desafio:**  
Encontrar e explorar um serviço root vulnerável via análise de processos.

---

### 2. Enumeração Profissional

**Aprender:**

- nmap avançado (stealth, evasão, scripts NSE)
- ffuf avançado (param fuzzing)
- SMB/RPC enum profissional
- SNMP
- Redis
- Rsync
- Fingerprinting manual

**Checklist:**

- [ ] Identificar CVEs só lendo banner
- [ ] Fuzzing inteligente
- [ ] Enumerar SMB sem ferramentas automáticas

**Mini-desafio:**  
Pegar as portas de uma máquina e listar 5 hipóteses de exploração para cada serviço.

---

### 3. Web Hacking Profundo

**Aprender:**

- SQLi manual (error-based, blind, boolean, time)
- XSS avançado (DOM, stored, polyglots)
- SSTI
- SSRF com bypass
- LFI → RCE
- Upload bypass avançado
- JWT attacks
- Race conditions
- Cache poisoning
- Request smuggling básico

**Checklist:**

- [ ] Identificar 10 classes de bugs manualmente
- [ ] Usar Burp Intruder com raciocínio
- [ ] Explorar SSRF e pivotar internamente

**Mini-desafio:**  
Encontrar 5 vulnerabilidades diferentes no Juice Shop.

---

### 4. Exploração de Serviços (Intermediário)

**Aprender:**

- FTP/SSH/SMTP/Redis/SMB
- Jenkins, Docker, Rsync
- CVE research
- Exploração sem metasploit

**Checklist:**

- [ ] Comprometer serviço sem tool automática
- [ ] Fazer chains de exploração

**Mini-desafio:**  
Comprometer máquina sem usar metasploit.

---

### 5. Privilege Escalation Profunda

**Aprender:**

**Linux:**

- Wildcards
- Capabilities
- NFS misconfigs
- Docker escapes
- Kernel exploits com segurança

**Windows:**

- Windows PrivEsc
- Unquoted paths
- Weak permissions
- SeImpersonate
- Tokens
- PowerShell privesc

**Checklist:**

- [ ] Encontrar 3 caminhos diferentes para root
- [ ] Entender completamente linpeas/winpeas

**Mini-desafio:**  
Virar root em 10 máquinas fáceis/médias.

---

### 6. Active Directory Básico → Intermediário

**Aprender:**

- Kerberos básico
- SPNs
- Kerberoasting
- AS-REP
- BloodHound

**Checklist:**

- [ ] Enumerar domínio
- [ ] Encontrar caminhos de ataque
- [ ] Explorar roasted users

**Mini-desafio:**  
Comprometer o laboratório "Attacktive Directory".

---

### RESULTADO DO NÍVEL 2

- ✔ Você hackeia máquinas "Medium"
- ✔ Você conduz pentests inteiros sozinho
- ✔ Você escala privilégios com lógica
- ✔ Você entende AD básico
- ✔ Você já é o que chamamos de Pentester Pleno

---

## PARTE 3 — ESPECIALISTA (PLENO → SÊNIOR → RED TEAM)

**Objetivo:**  
Criar um profissional com nível das empresas top (SpecterOps, NCC, TrustedSec). Esse nível inclui tudo: web avançado, rede, AD, evasão, C2, OPSEC, cloud, etc.

**Tempo:** 1 a 3 anos

---

### 1. HTTP & Web Avançado (nível pesquisador)

**Aprender:**

- Request smuggling avançado
- H2C smuggling
- Cache poisoning real
- WebSockets hacking
- OAuth & OIDC
- HTTP/2, HTTP/3
- CDN misconfigs
- WAF bypass moderno (Unicode, caching, malformed requests)

**Mini-desafio:**  
Quebre um aplicativo com técnicas de request smuggling.

---

### 2. Network Deep-Dive

**Aprender:**

- VLAN hopping
- Router exploitation
- IPv6 ataques (mitm6)
- NAC bypass
- Wi-Fi enterprise exploitation
- VPN internals
- Firewall bypasses

**Mini-desafio:**  
Montar laboratório com 3 redes segmentadas e pivotar entre elas.

---

### 3. Active Directory Avançado

**Aprender:**

- Silver/Golden tickets
- DCSync
- DCShadow
- Amsi bypass
- NTLM relaying profissional
- Child/Forest trust exploitation
- Evasão em AD
- Post-exploitation stealth

**Mini-desafio:**  
Comprometer um domínio → pivotar → comprometer outro domínio (forest).

---

### 4. Red Team (C2, OPSEC, Evasão, Implantação)

**Aprender:**

- Sliver / Havoc / Mythic
- Payload stages e carregadores
- Injectors (syscall, thread hijack, process hollowing)
- ETW bypass
- AMSI bypass
- EDR evasion
- Infra C2 real (redirectors, domain fronting, TLS)

**Mini-desafio:**  
Montar Sliver + redirector + payload evasivo. Operar por 24h sem acionar deteção.

---

### 5. Cloud Security (AWS)

**Aprender:**

- IAM avançado
- Assume-role attacks
- SSRF → metadata → takeover
- S3 exploitation
- Lambda execution abuse
- Cloud persistence

**Mini-desafio:**  
Comprometer ambiente simulado AWSGoat.

---

### 6. Mobile Security

**Aprender:**

- Android reversing
- iOS internals
- API abuse
- MITM de mobile traffic

**Mini-desafio:**  
Encontrar 3 bugs reais num APK local.

---

### 7. DevOps / CI/CD Security

**Aprender:**

- GitLab RCE
- Jenkins privilege abuse
- Supply chain attacks
- Docker → K8S pivots

**Mini-desafio:**  
Explorar pipeline vulnerável e obter secrets.

---

### 8. Reverse Engineering & Exploit Dev

**Aprender:**

- Buffer overflow avançado
- ROP
- ASLR bypass
- Heap exploitation
- Ghidra / IDA

**Mini-desafio:**  
Desenvolver exploit para binário vulnerável.

---

### 9. Physical & Social Engineering

**Aprender:**

- RFID cloning
- Lockpicking
- Tailgating profissional
- BadUSB
- Payload drops

**Mini-desafio:**  
Criar hardware implant funcional (ambiente controlado).

---

### ✅ RESULTADO DO NÍVEL 3

- ✔ Você é capaz de operar como Red Team real
- ✔ Você domina AD, evasão, payloads, pivoting, cloud, web avançado
- ✔ Você tem nível para trabalhar em qualquer empresa top

---

**🎓 Boa sorte na sua jornada!**