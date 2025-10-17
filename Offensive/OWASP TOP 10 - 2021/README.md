# OWASP TOP 10 - 2021 - Essentials

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

---

O OWASP TOP 10 é um guia das Top 10 vulnerabilidades mais comuns daquele periodo.

Nessa lição, vamos aprender:

- Broken Access Control
- Cryptographic Failures
- Injection
- Insecure Design
- Security Misconfiguration
- Vulnerable and Outdated Components
- Identification and Authentication Failures
- Software and Data Integrity Failures
- Security Logging & Monitoring Failures
- Server-Side Request Forgery (SSRF)


# 1. Broken Access Control

È quando alguém consegue acesso a uma área que não poderia conseguir normalmente, como um painel administrativo, um recurso que deveria ser privado.

## IDOR ( Insecure Direct Object Reference)

O IDOR é sobre a vulnerabilidade que permite acesso a recursos que normalmente não seriam visíveis.

Vamos supor que loguei em minha conta no web bank e a url está assim:

`https://bank.thm/account?id=111111`

Se por acaso eu alterasse o ID,

`https://bank.thm/account?id=222222`

Eu cairia na conta de outra pessoa, sem logar.

---

# Cryptographic Failures

Uma falha criptográfica é uma vulnerabilidade causada pelo uso incorreto ou ausência de criptografia para proteger dados confidenciais. Em aplicações web, isso pode expor informações durante a transmissão (dados em trânsito) ou no armazenamento (dados em repouso).

Essas falhas permitem ataques como Man-in-the-Middle e podem resultar na divulgação de informações pessoais ou credenciais de acesso.

---

Aqui foi me dado um exercicio, onde eu:

1. Verifiquei o código fonte da página /login, onde achei uma nota falando sobre a pasta /assets

2. Ao acessar a pasta /assets, encontrei um arquivo webapp.db, que é um arquivo de banco de dados SQLite.

3. Baixei o arquivo e naveguei pelo banco de dados, encontrei uma tabela users com hashes dos usuarios.

4. Joguei o hash de senha do admin no Crackstation e obtive a senha.

5. Ao logar com a senha de admin, obtive a flag.

---

# Injection

Falhas de injeção ocorrem quando uma aplicação interpreta entradas do usuário como comandos ou parâmetros, permitindo que invasores executem ações não autorizadas. Os tipos mais comuns são:

- Injeção SQL: o invasor insere comandos SQL maliciosos para acessar, alterar ou excluir dados no banco de dados.

- Injeção de comando: o invasor consegue executar comandos do sistema no servidor da aplicação.

A prevenção envolve validar e controlar as entradas do usuário, usando listas de permissões ou remoção de caracteres perigosos, além de bibliotecas específicas que ajudam a filtrar e proteger as entradas automaticamente.

---

Nessa tarefa, o host usa uma função que faz uma consulta direto em um aplicativo no /bin do sistema.

Nos aproveitamos disso executando certos comandos e obtendo informações-chave sobre o sistema.

---

# Insecure Design

Design inseguro acontece quando a falha está na forma como o sistema foi planejado, e não em um erro de código. Isso ocorre quando a segurança não é bem pensada desde o início do projeto.

Um exemplo é o caso do Instagram, onde o sistema de redefinição de senha por SMS tinha um limite de tentativas por IP. Um invasor podia usar vários IPs diferentes e testar todos os códigos possíveis — um erro de projeto, não de programação.

Essas falhas são difíceis de corrigir, pois exigem rever o design do sistema.
Para evitar, é essencial planejar a segurança desde o início, com modelagem de ameaças e boas práticas de desenvolvimento seguro.

Aqui, foi relativamente fácil - na redefinição de senha, a autenticação de dois fatores é responder algumas perguntas - entre elas, encontrei uma que poderia ser mais fácil, que pergunta a cor favorita do usuario - com um processo de força bruta manual, fiz diversas tentativas e consegui autitencar o reset de senha.

# Security Misconfiguration

Configuração de segurança incorreta ocorre quando um sistema poderia ser seguro, mas foi mal configurado — não é necessariamente um bug no software, é problema de administração.

Pontos principais:

Permissões incorretas (ex.: buckets S3 abertos).

Recursos desnecessários ativados (serviços, páginas, contas).

Contas padrão com senhas não alteradas.

Mensagens de erro muito detalhadas que vazam informação.

Falta de cabeçalhos HTTP de segurança.

Risco: essas falhas tornam possível acessar dados sensíveis, explorar XXE, executar comandos via páginas administrativas ou abusar de interfaces de depuração.

Exemplo: consoles de depuração expostos (como o console do Werkzeug) permitem execução arbitrária de código se deixados em produção.

Mitigação rápida: revisar configurações, remover recursos desnecessários, trocar senhas padrão, limitar exposição de debug e aplicar cabeçalhos/permissões corretas.

---

A tarefa desse foi legal, nós abusamos de um subdiretório de depuração padrão para o Python ao qual não foi desativado pelo desenvolvedor, ganhando assim, acesso de execução de comandos python, onde pudemos realizar um payload que executa comandos normais no sistema.

# Vulnerable and Outdated Components

Usar componentes (CMS, bibliotecas, frameworks, plugins) desatualizados é perigoso porque versões antigas frequentemente têm falhas públicas e exploits prontos. Um exemplo: um WordPress desatualizado pode conter RCE conhecido e já explorável — basta um atacante identificar a versão e usar um exploit existente.

Risco principal: alto impacto com pouco esforço do atacante.

Nesse desafio, analisei o CMS usado na URL, busquei por ele no Exploit DB - encontrei um exploit de RCE para aquela versão, executei e pronto.

