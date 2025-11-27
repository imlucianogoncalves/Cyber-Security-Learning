# Roadmap Completo: Pentest → Red Team

Este roadmap fornece um caminho estruturado para desenvolver habilidades de pentesting até alcançar o nível de Red Team, com checkpoints, mini-laboratórios e recursos para cada fase.

---

## Fase 1 — Linux Profissional para Pentester

**Duração:** 2 a 3 semanas  
**Objetivo:** Operar com total autonomia em qualquer shell Linux comprometido

### O que você precisa aprender

- Permissões (chmod, chown, chgrp)
- SUID / SGID / Sticky Bit
- Processos: ps, top, pgrep, pkill
- systemctl e gerenciamento de serviços
- Logs e journalctl
- Redes: ip, ss, netstat, tcpdump
- Bash (loops, condicionais, pipes, redirecionamento)
- Variáveis de ambiente
- Reverse e bind shells

### Por que isso importa no pentest?

Aproximadamente 90% das explorações levam você a um shell de baixo privilégio. Sem domínio de Linux, você não consegue interpretar o que está vendo. No Red Team, isso é ainda mais crítico: é necessário manter OPSEC, pivotar, explorar serviços, escalar privilégios e não deixar rastros.

### Recursos de estudo (gratuitos)

- **OverTheWire Bandit** (obrigatório)
- "The Linux Command Line" – edição gratuita
- Linux Journey
- Man pages (man chmod, man tcpdump, etc.)

### Checklist da fase

- [ ] Entendo permissões numéricas e simbólicas
- [ ] Sei identificar SUID/SGID
- [ ] Sei ler logs com journalctl
- [ ] Sei manipular processos
- [ ] Sei configurar/entender systemctl
- [ ] Sei usar tcpdump para capturar tráfego
- [ ] Sei escrever um script bash simples
- [ ] Sei abrir reverse shells em várias linguagens

### Mini-desafio

**Desafio:** Crie um script bash que monitora processos suspeitos e grava logs a cada 10 segundos. Depois, crie um cronjob para executá-lo automaticamente.

### Critério de conclusão

Você pode avançar quando conseguir pegar um shell "www-data" e mapear completamente o sistema: usuários, permissões, serviços, processos, rede e pontos potenciais de privesc — sem tutoriais.

---

## Fase 2 — Enumeração e Reconhecimento Profissional

**Duração:** 2 semanas  
**Objetivo:** Descobrir tudo sem explodir nada

### O que aprender

#### Reconhecimento Passivo

- whois
- crt.sh
- DNSDumpster
- Shodan / Censys
- subfinder

#### Reconhecimento Ativo

- nmap avançado
- rustscan
- Análise de banners
- Fingerprinting manual
- ffuf / gobuster
- enum4linux
- smbclient

### Por que isso importa?

Exploração é 20%. **Enumeração é 80%**. No Red Team, isso define:

- Vetor de entrada
- Superfície de ataque
- Ativos expostos
- Portas internas úteis
- Caminhos para pivotar

### Recursos de estudo

- Nmap Book (gratuito)
- Guia oficial FFUF
- HackTricks (melhor fonte viva de enumeração)
- Labs HTB "Starting Point"

### Checklist

- [ ] Rodar nmap em modos diferentes (rápido, completo, stealth)
- [ ] Enumerar SMB manual e com ferramentas
- [ ] Identificar tech stack web
- [ ] Fazer fuzzing de diretórios com wordlists corretas
- [ ] Interpretar banners manualmente
- [ ] Identificar CVE potencial apenas pelo banner

### Mini-desafio

**Desafio:** Pegue 3 máquinas fáceis do VulnHub e faça apenas ENUMERAÇÃO, sem explorar. Escreva um relatório com:

- Portas abertas
- Serviços
- Possíveis vulnerabilidades
- Hipóteses de exploração

### Critério de conclusão

Você pode avançar quando olha um banner de serviço e consegue dizer quais são os ataques possíveis, mesmo sem tentar.

---

## Fase 3 — Web Hacking Profundo (OWASP + Técnicas Práticas)

**Duração:** 6 a 8 semanas  
**Objetivo:** Dominar Web a ponto de identificar qualquer vulnerabilidade comum de forma manual

### O que aprender

#### Vulnerabilidades Principais

- SQL Injection (todos os tipos)
- XSS (todos os tipos)
- SSRF
- SSTI
- LFI / RFI / Path Traversal
- Upload bypass
- IDOR / Broken Access Control
- Open Redirect
- Command Injection
- Deserialization
- Auth bypass
- JWT attacks

#### Ferramentas

- Burp Suite (avançado)
- Intruder / Repeater / Collaborator
- wfuzz
- ffuf

### Por que isso importa?

Hoje 70% das entradas de Red Team são via:

- Web apps internos
- APIs
- Aplicações mal configuradas
- Painéis de administração
- IDORs e falhas de autorização

É onde você desenvolve seu pensamento ofensivo lógico.

### Recursos de estudo

- **PortSwigger Web Security Academy** (100% obrigatório)
- OWASP Web Testing Guide
- Juice Shop
- Root-Me web

### Checklist

- [ ] Identificar SQLi manualmente
- [ ] Executar XSS avançado (DOM, stored, filter bypass)
- [ ] Encontrar IDOR sem ferramenta
- [ ] Identificar e explorar SSRF
- [ ] Explorar upload bypass com polyglots
- [ ] Usar Burp Suite com total fluidez
- [ ] Fazer fuzzing inteligente de parâmetros
- [ ] Manipular cookies, sessões e JWT

### Mini-desafio

**Desafio Web Completo:** No Juice Shop, encontre:

1. 1 SQLi
2. 1 XSS
3. 1 falha de upload
4. 1 IDOR
5. 1 SSRF

Documente tudo como se fosse para um cliente.

### Critério de conclusão

Você pode avançar quando lê uma aplicação web por 10 minutos e identifica pontos de entrada, parâmetros interessantes e caminhos de exploração com naturalidade.

---

## Fase 4 — Exploração de Serviços + Privilege Escalation Linux & Windows

**Duração:** 8 semanas  
**Objetivo:** Comprometer hosts e virar root/SYSTEM sempre que possível

### O que aprender

#### Exploração por Serviço

- FTP
- SSH
- SMB
- Redis
- Docker
- Jenkins
- Rsync
- MySQL/MongoDB/PostgreSQL

#### Privilege Escalation Linux

- SUID / SGID
- sudo -l abuses
- PATH hijacking
- Capabilities
- Cronjobs
- Kernel exploits
- Docker escapes
- Wildcard injection

#### Privilege Escalation Windows

- Unquoted service paths
- Permissões fracas
- seImpersonatePrivilege
- PrintSpoofer / RoguePotato
- Token abuse
- Registry escalation
- PowerShell Constrained Mode bypass
- SAM/LSA dumping

### Por que isso importa?

Ganhar acesso é apenas metade da batalha. O Red Team precisa:

- Escalar
- Persistir
- Viver na rede
- Mover lateralmente

É aqui que os pentesters de verdade começam a se diferenciar.

### Recursos de estudo

- HackTricks (privesc bible)
- GTFOBins
- PayloadAllTheThings
- TryHackMe "Linux PrivEsc"
- TryHackMe "Windows PrivEsc"

### Checklist

- [ ] Identificar SUID vulnerável
- [ ] Abusar de sudo com scripts inseguros
- [ ] Explorar serviços mal configurados
- [ ] Escalar privilege via capabilities
- [ ] Abusar de seImpersonatePrivilege
- [ ] Executar PrintSpoofer ou equivalente
- [ ] Identificar Windows misconfigs manualmente
- [ ] Usar linpeas / winpeas com entendimento

### Mini-desafio

**Desafio:** Pegue 5 máquinas do VulnHub/HTB Easy e:

1. Comprometa
2. Escale
3. Documente
4. Refaça depois sem ferramentas automáticas

### Critério de conclusão

Dado um shell limitado, você encontra pelo menos 3 rotas diferentes para virar root.

---

## Fase 5 — Active Directory, Movimento Lateral & Pivoting

**Duração:** 8 a 12 semanas  
**Objetivo:** Operar exatamente como um invasor interno

### O que aprender

#### Active Directory

- LDAP structure
- Kerberos (TGT, TGS, SPNs)
- Kerberoasting
- AS-REP roasting
- BloodHound (análise real)
- Delegações
- Pass-the-Hash
- Pass-the-Ticket
- Overpass-the-Hash
- Golden / Silver Tickets
- DC Sync / DC Shadow
- GPO abuse
- Forest → Child trust exploitation

#### Movimento Lateral

- PsExec
- WinRM
- WMI Exec
- SMB pivot
- Token impersonation

#### Pivoting

- proxychains
- sshuttle
- chisel
- socat

### Por que isso importa?

Red Team = AD mastery. A maior parte das empresas opera em AD. Você precisa navegar, quebrar, escalar e sobreviver dentro dele.

### Recursos de estudo

- HackTricks AD
- Attacktive Directory (gratuito)
- BloodHound docs
- MITRE ATT&CK
- IppSec (HTB AD machines)

### Checklist

- [ ] Extrair SPNs
- [ ] Realizar kerberoasting
- [ ] AS-REP roasting
- [ ] Criar tickets forjados
- [ ] Identificar caminhos em BloodHound
- [ ] Mover lateralmente de 3 formas
- [ ] Pivotar entre redes segmentadas
- [ ] Manter persistência discreta no AD

### Mini-desafio

**Desafio:** Monte seu próprio AD com 2 hosts + 1 DC e comprometa-o.

Objetivo:

1. Initial access
2. Movimento lateral
3. Elevar até Domain Admin

### Critério de conclusão

Dado um AD desconhecido, você consegue mapear, pivotar e encontrar caminho até DA sem tutoriais.

---

## Fase 6 — Red Team de Verdade (OPSEC, Evasão, C2)

**Duração:** Contínua  
**Objetivo:** Operar com sigilo, persistência e stealth

### O que aprender

#### OPSEC Ofensivo

- Logs
- Artefatos
- Evasão
- Engano
- Anti-forense

#### Evasão de AV/EDR

- Syscalls diretas
- Injection
- Desobfuscation & reobfuscation
- Bypass de AMSI
- Bypass de ETW
- Uso de LOLBins

#### C2 Frameworks

- Sliver
- Havoc
- Mythic
- Covenant

#### Infraestrutura

- Redirectors
- Domain fronting
- TLS montagem

### Checklist

- [ ] Criar infra red team
- [ ] Configurar C2
- [ ] Criar payload minimamente evasivo
- [ ] Usar técnicas de injeção
- [ ] Fazer OPSEC de logs
- [ ] Operar sem acionar EDR básico

### Mini-desafio

**Desafio:** Monte infraestrutura mínima com Sliver + redirector Nginx. Gere um implant e execute em máquina isolada.

---

## Notas Finais

Este roadmap é um guia progressivo. Cada fase constrói sobre a anterior, e é fundamental não pular etapas. A prática constante, documentação de processos e revisão de conceitos são essenciais para a evolução de pentester para Red Team operator.

**Lembre-se:** A diferença entre um pentester e um Red Team operator não está apenas nas técnicas, mas na mentalidade operacional, no pensamento adversário e na capacidade de manter persistência e sigilo em ambientes hostis.