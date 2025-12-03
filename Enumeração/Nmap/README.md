# NMAP

Essa é uma das plataformas-base em pentest, com ele, conseguimos diversas informações sobre o alvo, como:

- quais hosts estão vivos

- quais portas estão abertas

- quais serviços rodando

- quais versões

- às vezes até **vulnerabilidades conhecidas** (via scripts)

------

Alguns conceitos básicos que precisamos saber:

As portas TCP/UDP vão de 0 a 65535, por padrão o nmap não escaneia todas essas portas, somente as 1000 mais conhecidas.

As portas mais conhecidas são:

- 22 SSH

- 80 HTTP

- 443 HTTPS

- 445 SMB

- 3306 MySQL

Se elas estão abertas, significa que estão "aceitando conexão". Aí que entramos.

Essas portas, podem ter 4 possíveis status de saída.

Sendo eles:

- **open** – tem serviço respondendo

- **closed** – ninguém ouvindo, mas host respondeu com RST → host existe

- **filtered** – firewall no meio, não dá para saber se tem algo lá

- **open|filtered** – Nmap não conseguiu diferenciar (muito comum em UDP)

------

## Tipos de varreduras

No NMAP temos três principais tipos de varreduras, cada uma com seu devido objetivo e situação de uso: 

1. **TCP Connect Scan – `-sT`**

2. **TCP SYN Scan – `-sS`**

3. **UDP Scan – `-sU`**

### TCP Connect Scan (`-sT`)

- É o scan **mais simples** do ponto de vista técnico.
- Usa a chamada de sistema `connect()` do SO.
- Faz o **three-way handshake completo** (SYN → SYN/ACK → ACK).

Características:

- Fácil de detectar (logado em serviços, firewalls, etc.)
- Mais lento que `-sS` em scans grandes
- Funciona mesmo sem privilégios root (útil às vezes em ambiente restrito)

Uso típico:

```

nmap -sT -p 1-1000 192.168.1.10
```

### TCP SYN Scan (`-sS`) – o clássico scan “furtivo”

- Envia apenas o **SYN**.
- Se recebe **SYN/ACK**, marca como **open** e responde **RST** em vez de completar a conexão.
- Se recebe **RST**, marca como **closed**.
- É o famoso “half-open scan”.

Vantagens:

- Mais rápido que `-sT`
- Menos ruído (não completa handshake) → menos logado em alguns serviços mais antigos
- Padrão quando você roda Nmap como root

Uso típico:

```

nmap -sS -p- 192.168.1.10
```

### UDP Scan (`-sU`)

- Muito mais chato.
- UDP não tem handshake, então o Nmap faz:
  - envia pacote UDP
  - se vem **ICMP port unreachable** → `closed`
  - se não vem nada → `open|filtered`
- Lento por natureza (timeout maior)
- Alta taxa de falso-positivo `open|filtered`

Uso típico:

```

nmap -sU -p 53,123,161 192.168.1.10
```

Como pentester, UDP scan é importante para:

- DNS (53)
- NTP (123)
- SNMP (161)
- Servidores de jogos, VPNs, etc.

---

## Exemplo de uso típico num caso real

1. Descobrir hosts:

```

nmap -sn 192.168.1.0/24
```

1. Descobrir portas rapidamente nas máquinas vivas:

```

nmap -sS --top-ports 100 192.168.1.10-50
```

1. Varredura completa em host interessante:

```

nmap -sS -p- 192.168.1.10
```

1. Identificar versão de serviços:

```

nmap -sS -sV -p 22,80,443,3306 192.168.1.10
```

1. Rodar scripts específicos (vamos chegar lá).

### Timing (`-T0` a `-T5`)

- `-T0` / `-T1`: super lento, stealth, raramente necessário
- `-T3`: padrão (bom equilíbrio)
- `-T4`: mais rápido, aceitável em LAN/muitos alvos internos
- `-T5`: agressivo, pode explodir serviços / gerar muito ruído

Regra prática:

- interno em lab/teste → `-T4` ok
- externo / ambiente sensível → ficar em `-T3` ou ajustar manualmente