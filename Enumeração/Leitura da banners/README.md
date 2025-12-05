# 1. O que é banner?

Em redes, **banner** é qualquer informação que um serviço devolve quando você se conecta a ele.

Exemplos de banners:

- versão do serviço
- versão do sistema operacional
- data de compilação
- módulos habilitados
- software específico (ex: OpenSSH, Apache, Exim)

Isso aparece quando você usa:

```

nmap -sV IP
```

Ou até ao conectar manualmente com:

```

nc IP PORT
```

------

# 2. Por que banners são importantes?

Porque **versão = oportunidade de ataque**.

Pentester experiente olha um banner e pensa:

- “Esse serviço tem CVE?”
- “Essa versão é antiga?”
- “Tem exploit?”
- “Esse componente é vulnerável por padrão?”
- “Isso é um DC? Um servidor web? Um appliance?”

Muitas vezes você **identifica a falha ANTES de rodar qualquer exploit**.

------

# 3. Como banners aparecem no Nmap

Exemplo real de banner via Nmap:

```

80/tcp open  http    Apache httpd 2.4.29 (Ubuntu)
```

Esse é o banner.

Ele contém:

1. Serviço → `http`
2. Software → `Apache`
3. Versão → `2.4.29`
4. Sistema → `(Ubuntu)` → indica hospedagem

------

# 4. Como interpretar banners (nível iniciante → intermediário)

Agora vamos ver OS PRINCIPAIS SERVIÇOS e o que você deve procurar.

------

# ✔ 4.1. SSH (extremamente comum)

Exemplo:

```

22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8
```

O que isso te diz?

- OpenSSH 7.2 é **antigo**
- Sistemas antigos geralmente têm mais misconfigurations
- Indica que provavelmente é Ubuntu 16.04 (EOL → vulnerável)
- Pode ter:
  - credenciais fracas
  - chaves fracas
  - usuário padrão
  - OpenSSH auth bypass em versões específicas

Sinal de alerta:

- versões **≤ 6.6** → MUITO antigas
- banners com “protocol 1” → horrível

------

# ✔ 4.2. HTTP (Apache / Nginx / IIS)

Exemplo:

```

80/tcp open  http Apache 2.4.29 (Ubuntu)
```

Interpretação:

- Apache 2.4.29 é vulnerável a:
  - mod_proxy RCE
  - mod_ssl problemas em versões específicas
  - options misconfigurations
- O fato de rodar “(Ubuntu)” indica sistema Linux comum → privesc provável

Outro exemplo:

```

80/tcp open http Microsoft IIS 7.5
```

Sinal de perigo total:

- IIS 7.5 = Windows Server 2008
- Windows 2008 = sistema **EOL**, cheio de CVEs graves
- Frequentemente expõe:
  - WebDAV
  - asp.aspx antigos
  - execução remota

Banner velho = superfície enorme.

------

# ✔ 4.3. SMB (Windows)

Exemplo:

```

445/tcp open microsoft-ds Windows 6.1 (Samba 4.3.11-Ubuntu)
```

Ou:

```

445/tcp open microsoft-ds Windows 7 Professional 7601 Service Pack 1
```

Interpretação:

- Windows 7 SP1 = **eterno alvo**
- Possível:
  - EternalBlue (MS17-010)
  - Absolutamente cheio de vulnerabilidades
- Indica domínio ou file server

Qualquer banner Windows antigo → exploração provável.

------

# ✔ 4.4. FTP (vsftpd, FileZilla, ProFTPD)

Exemplo:

```

21/tcp open ftp vsftpd 2.3.4
```

Se vir **vsftpd 2.3.4** → *ataque imediato*.

É uma versão infame:
 → backdoor: login com `:)` dá shell root.

Outro exemplo:

```

21/tcp open ftp ProFTPD 1.3.5
```

ProFTPD tem:

- mod_copy exploit
- diversos RCE em versões específicas

------

# ✔ 4.5. SMTP (Postfix, Exim)

Exemplo:

```

25/tcp open smtp Exim 4.89
```

Exim 4.x quase sempre significa:

- postura fraca
- histórico enorme de RCE
- CVE-2019-10149 (RCE remoto total)

Banner identificou vulnerabilidade imediatamente.

------

# ✔ 4.6. MySQL

Exemplo:

```

3306/tcp open mysql 5.5.50-0ubuntu0.14.04.1
```

Interpretação:

- MySQL 5.5 → EXTREMAMENTE velho
- Pode ter:
  - auth bypass
  - credenciais fracas
  - root sem senha (incrivelmente comum)
  - tabelas sensíveis acessíveis (mysql.user)

Banner velho → exploração trivial.

------

# ✔ 4.7. RDP

```

3389/tcp open ms-wbt-server Microsoft Terminal Services
```

Se aparecer:

```

RDP Security Mode: legacy
```

Isso significa:

- criptografia fraca
- MITM possível
- brute force possível (sem NLA)

Se ver "Windows 7" → CVE-2019-0708 (BlueKeep).

------

# ✔ 4.8. Jenkins

```

8080/tcp http Jetty 9.4.z
X-Jenkins: 2.138
```

Qualquer Jenkins exposto → você provavelmente consegue:

- read only access
- script console exploitation
- enumerar usuários
- pegar API tokens

Jenkins exposto em produção é red flag.

------

# 5. Onde procurar CVEs rapidamente?

Assim que você vê:

```

Apache 2.4.29
OpenSSH 7.2
Exim 4.89
ProFTPD 1.3.5
vsftpd 2.3.4
```

Você deve procurar:

- **searchsploit nome versão**
- **CVE nome versão**
- **Exploit-DB**
- **HackTricks**
- **Nuclei templates (avançado)**

Mas no nível iniciante:

```

searchsploit apache 2.4
searchsploit proftpd 1.3
searchsploit exim 4
```

------

# 6. Como pentester iniciante deve pensar ao ver um banner

Assim que você lê o banner, faça estas perguntas:

### ✔ “A versão é velha?”

Versão velha quase sempre = surface de ataque.

### ✔ “O serviço é sensível?”

SMB/FTP/SSH → risco enorme.

### ✔ “O serviço roda como root?”

Apache/Exim frequentemente sim.

### ✔ “Dá para fazer brute force?”

Se for FTP, SSH, RDP → possivelmente.

### ✔ “É serviço que costuma ser mal configurado?”

Jenkins, Tomcat, Redis, MongoDB → sim.

------

# 7. Exemplo de análise completa de banner (iniciante → profissional)

Scan:

```

22/tcp open  ssh OpenSSH 7.2p2 Ubuntu 4ubuntu2.8
80/tcp open  http Apache 2.4.29 (Ubuntu)
139/tcp open netbios-ssn Samba smbd 3.X (workgroup: WORKGROUP)
445/tcp open microsoft-ds Samba smbd 3.X (workgroup: WORKGROUP)
```

Seu raciocínio:

### 22/SSH

- Ubuntu 16.04 (EOL)
- Provavelmente sem patches
- Senhas fracas possíveis

### 80/Apache

- 2.4.29 → vulnerável a vários módulos
- rodando em Ubuntu, provavelmente com PHP

### 139/445 → Samba

- Versões antigas combo
- Samba 3.x → muitas CVEs
- Possível credencial guest
- Compartilhamentos expostos

Pronto. Só lendo banners você já sabe:

- reconhecer versão antiga
- reconhecer sistema EOL
- reconhecer risco
- direcionar FASE DA ENUMERAÇÃO

Isso é mentalidade profissional.