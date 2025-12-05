# 1. O que é *fuzzing* de diretórios?

Quando você acessa um site (ex.: `http://site.com`), você só vê o que o desenvolvedor quis mostrar.

Mas **quase sempre existem diretórios e arquivos ocultos**, como:

- `/admin`
- `/backup`
- `/test`
- `/old`
- `config.php.bak`
- `/private/`

Como atacante, você quer descobrir essas partes escondidas.

**Gobuster** e **FFUF** fazem isso: eles testam muitas palavras da wordlist tentando encontrar caminhos válidos no servidor.

------

# 2. Gobuster — o básico

Gobuster é simples, rápido e ótimo para iniciantes.

## 2.1. Quando usar Gobuster?

Use Gobuster quando você quer:

- Encontrar **diretórios**
- Encontrar **arquivos**
- Enumerar **subdomínios**

Ele é focado nisso — direto ao ponto.

------

## 2.2. Comando mais básico

### Descobrir diretórios:

```

gobuster dir -u http://site.com -w /usr/share/wordlists/dirb/common.txt
```

Explicação:

- `dir` = modo de descobrir diretórios
- `-u` = URL alvo
- `-w` = wordlist

------

## 2.3. Procurar arquivos com extensões

```

gobuster dir -u http://site.com -w common.txt -x php,txt,bak
```

Isso faz tentar:

- `/admin.php`
- `/admin.txt`
- `/admin.bak`

e assim por diante.

------

## 2.4. Subdomínios (DNS)

```

gobuster dns -d site.com -w subdomains.txt
```

Vai testar:

- `admin.site.com`
- `api.site.com`
- `dev.site.com`

------

## 2.5. Como interpretar o básico

Exemplos típicos:

```

/admin      (Status: 301)
/backup     (Status: 403)
/test       (Status: 200)
/nothing    (Status: 404)
```

Significado breve:

- **200** → Existe e é acessível
- **301/302** → Redireciona, mas **existe**
- **403** → Existe, mas proibido (muitas vezes dá para bypassar)
- **404** → Não existe (ignore)

------

# 3. FFUF — o básico

FFUF é mais moderno, mas pode ser tão simples quanto Gobuster no início.

Ele usa **FUZZ** como marcador na URL.

------

## 3.1. Quando usar FFUF?

Use FFUF quando você quiser:

- Fazer o mesmo que o Gobuster, **mas de forma mais flexível**
- Testar parâmetros GET e POST (ex.: descobrir nome de parâmetro)
- Filtrar resultados por código HTTP/tamanho (sem complicar)

Mas aqui vamos ficar só no **essencial**:

- fuzzing de diretórios
- fuzzing simples de parâmetros

------

# 3.2. FFUF para diretórios (igual ao Gobuster)

```

ffuf -u http://site.com/FUZZ -w /usr/share/wordlists/dirb/common.txt
```

`FUZZ` será substituído pelas palavras da wordlist.

------

## 3.3. Filtrar códigos HTTP

Se você só quer ver 200 e 301:

```

ffuf -u http://site.com/FUZZ -w common.txt -mc 200,301
```

`-mc` = match codes

------

## 3.4. Fuzzing de parâmetros (o mais básico possível)

Isso é algo que Gobuster NÃO faz.

Exemplo: tentar descobrir qual parâmetro existe:

```

ffuf -u "http://site.com/page.php?FUZZ=1" \
     -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt \
     -mc 200
```

Ele tenta:

- `?id=1`
- `?user=1`
- `?q=1`
- `?search=1`
- etc.

Isso te ajuda a descobrir:

- parâmetros ocultos
- endpoints secretos
- funcionalidades internas

------

# 4. Como interpretar o FFUF (básico)

Resultado típico:

```

admin       [Status: 200, Size: 1512]
backup      [Status: 403, Size: 800]
test        [Status: 301, Size: 0]
```

Mesma lógica do Gobuster:

- **200** → existe
- **403** → proibido, mas existe
- **301/302** → redirecionamentos interessantes
- **404** → ignora

------

# 5. Wordlists recomendadas (iniciante)

### Diretórios:

- `/usr/share/wordlists/dirb/common.txt`
- `/usr/share/wordlists/dirb/big.txt`
- `/usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt`

### Parâmetros:

- `/usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt`

### Subdomínios:

- `/usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt`

------

# 6. O essencial para iniciantes (resumo rápido)

### Gobuster:

- Ideal para diretórios e subdomínios
- Sintaxe simples
- Menos flexível que FFUF

Use assim:

```

gobuster dir -u http://alvo -w common.txt
```

------

### FFUF:

- Faz tudo que Gobuster faz
- Pode fuzzar parâmetros
- Permite filtrar por código/tamanho

Use assim:

```

ffuf -u http://alvo/FUZZ -w wordlist.txt
```

Ou para parâmetros:

```

ffuf -u "http://alvo/page?FUZZ=1" -w params.txt 
```