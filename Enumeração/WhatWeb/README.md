## 1. O que é o WhatWeb (conceito real)

WhatWeb é uma ferramenta de **fingerprinting de aplicações web**.

Ele identifica:

- tecnologias (PHP, ASP.NET, Java, Node)
- frameworks (Django, Laravel, Express)
- CMS (WordPress, Joomla, Drupal)
- servidores (Apache, Nginx, IIS)
- versões quando possível
- plugins, temas, banners
- linguagens, bibliotecas JS, CDN
- até padrões de cookies

No pentest real, ele serve para **descobrir rapidamente**:

- qual aplicação estou atacando?
- ela é vulnerável?
- que scripts NSE, que payloads, que exploits podem funcionar?
- é um WordPress? Um Tomcat?
- tem WAF?
- tem framework fraco?
- tem versão exposta?

Mentalidade:

> “WhatWeb não explora nada.
>  Ele diz COMO eu devo explorar.”

------

# 2. Como o WhatWeb funciona por baixo dos panos (simplificado)

WhatWeb usa **assinaturas** (fingerprints).
 Ele analisa:

### 2.1. Cabeçalhos HTTP

Ex.:

- `Server: Apache/2.4.29`
- `X-Powered-By: PHP/5.6`
- `Set-Cookie: JSESSIONID=...`
- `X-AspNet-Version: 4.0.30319`

### 2.2. HTML da página

- `<meta generator="WordPress 5.5.2">`
- `<script src="/wp-includes/...">`
- `<title>Joomla! Site</title>`

### 2.3. Padrões de resposta

- códigos de status
- formatos de URL
- padrões JS/CSS

### 2.4. Regras de plugin

Cada tecnologia tem um fingerprint próprio.

Exemplo:

- WordPress → `/wp-login.php`, `/wp-content/`
- phpMyAdmin → `/themes/pmahomme/`
- Laravel → cookie `XSRF-TOKEN`, roteamento `/?`
- Spring Boot → banner `Whitelabel Error Page`

------

# 3. Comandos principais + quando usar

## ✔ 3.1. Scan simples

```

whatweb http://alvo.com
```

Útil quando?

- Só quer saber rapidamente “o que é isso”.

## ✔ 3.2. Scan verbose (detalhado)

```

whatweb -v http://alvo.com
```

Mostra:

- cada plugin acionado
- conteúdo detectado
- justificativas

Útil para aprendizado e análise profunda.

## ✔ 3.3. Scan agressivo

```

whatweb -a 3 http://alvo.com
```

Níveis:

- `-a 1`: passivo
- `-a 3`: ativo (detecta mais)
- `-a 4`: MUITO agressivo (evite em pentest externo)

Quanto maior, mais requisições e mais ruído.

## ✔ 3.4. Scan em múltiplos sites

```

whatweb -i sites.txt
```

Onde `sites.txt` contém:

```

http://alvo1.com
http://alvo2.com
http://alvo3.com
```

## ✔ 3.5. Salvando em JSON (pra automatizar)

```

whatweb -a 3 --log-json resultado.json http://alvo.com
```

Útil para:

- automação
- parsing
- análise histórica

------

# 4. O que é relevante para um pentester (o OURO do WhatWeb)

Vou te mostrar AGORA como um pentester analisa **cada categoria** de informação encontrada.

## ✔ 4.1. Tipo de servidor (Apache, Nginx, IIS)

Por quê isso importa?

- versões antigas de Apache → exploits famosos
- IIS → vulnerabilidades específicas (WebDAV, NTLM leaks)
- Nginx → má configuração de path traversal

Ex:
 `Server: Apache/2.4.29 (Ubuntu)`
 Eu penso:

- versão antiga?
- mod_php?
- diretórios padrão expostos?
- vulnerability mapping: CVE for Apache 2.4.29

------

## ✔ 4.2. Linguagem e plataforma

Quando você vê:

- `X-Powered-By: PHP/5.6` → PHP 5.6 está morto e cheio de RCE
- `X-Powered-By: ASP.NET`
- `Set-Cookie: JSESSIONID` → Java / Tomcat / Spring
- `X-Powered-By: Express` → Node.js

O que isso muda?

- muda os payloads
- muda os tipos de injeção
- muda vetores de RCE

------

## ✔ 4.3. CMS detectado (WordPress, Drupal, Joomla)

Se aparece:

**WordPress 5.0**

Eu penso:

- `/wp-admin/` acessível?
- `/xmlrpc.php` → brute force e amplificação
- plugins vulneráveis?
- temas vulneráveis?
- enumerar usuários via `/wp-json/wp/v2/users`

Dependendo da versão, já sei quais CVEs se aplicam.

------

## ✔ 4.4. Frameworks detectados

Exemplos:

- Laravel
- Django
- Flask
- Spring Boot
- Ruby on Rails

Isso é enorme porque:

- cada framework tem **ataques específicos**
- cada framework tem **rotas previsíveis**
- cada framework tem **leaks comuns**

Exemplo:

**Laravel** → muitos leaks de debug, SSRF, RCE, exposição de `.env`

**Spring Boot** → `/actuator` exposto = privesc total

**Rails** → vulnerável a parâmetro mágico (`Rails < 5.2`)

------

## ✔ 4.5. WAF detectado

Se o WhatWeb detectar:

- Cloudflare
- Sucuri
- ModSecurity

Você muda a ENTIRE estratégia:

- payloads ofuscados
- scans mais lentos
- bypass via spoofing, burp match-and-replace
- enumerar IP real (resolução via DNS histórico)

------

## ✔ 4.6. Cookies importantes

Exemplos:

`PHPSESSID`
 → PHP clássico → tente LFI, sessão fraca, path predictable

`JSESSIONID`
 → app Java → Session fixation, Spring attacks

`XSRF-TOKEN`
 → Laravel ou outra framework com CSRF embutido

Cookies também revelam:

- tipo de sessão
- se tem `HttpOnly`
- se tem `Secure`
- se estão mal configurados

------

# 5. Quando WhatWeb apita “coisas estranhas”

### Caso 1: tecnologias contraditórias

Exemplo:

- Apache + ASP.NET
   Isso sugere proxy reverso, load balancer, ou misconfig.

### Caso 2: banner muito detalhado

Exemplo:

```
Server: Apache/2.4.29 (Ubuntu) OpenSSL 1.1.0g mod_fastcgi/2.4.7
```

Isso dá munição para:

- busca de CVEs compatíveis
- análise de módulos carregados
- fingerprinting da distro

### Caso 3: página retornando erros detalhados

Exemplo:

```
WhatWeb: "Laravel Debug Mode" detected
```

Isso geralmente significa:

- RCE
- env leak
- stack trace para mapear rotas
- expondo credenciais