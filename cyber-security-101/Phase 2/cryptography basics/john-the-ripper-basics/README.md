# John the Ripper - Básico

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

John the Ripper é uma ferramenta de quebra de hash bem conhecida, amada e versátil - combina velocidade de crackeamento com variedades de tipos de hash compatíveis.

Objetivos De Aprendizagem

Após a conclusão desta sala, você aprende sobre o uso de John para:

- Quebrando hashes de autenticação do Windows
- Crack /etc/shadow hashes
- Cracking de arquivos Zip protegidos por senha
- Cracking de arquivos RAR protegidos por senha
- Craqueamento SSH chaves 

---

Jumbo John é a versão extendida mais popular de John the Ripper.

---


Sintaxe básica do John é

`john [opções] [caminho]`

---

## Craqueamento automático

`john --wordlist=[path to wordlist] [path to file]`

---

Da pra usar sites externos pra identificar o tip odo hash ou uma ferramenta em pythn, o `hash-id.py`;

---

Depois de descobrirmos o tipo do hash, podemos passar tal informação para o john, com:

`john --format=[format] --wordlist=[path to wordlist] [path to file]`

onde --format é o tipo de hash.

Exemplo de uso:

`john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt`

Quando usamos um tipo de hash padrão, como o md5 puro, precisamos passar essa informação também, então usamos, por exemplo `raw-md5` assim dizemos que aquele hash md5 não tem nenhum ajuste extra.

`john --list=formats | grep -iF "md5"`

Para procurar os formatos aceitos.

---

## Crackeando autenticação de hashes do Windows

NTHash / NTLM

São hashes usados no sistema operacional Windows para guardar as senhas de usuarios e serviços.

Bem importante num ataque, podemos usar para pegar dados de uma máquina Windows ou banco de dados Active Directory.

No Windows, podemos usar:

- Mimikatz 

e no Active Directory:

NTDS.dit

---

Para essa tarefa do THM - tive de usar o `--format=NT`

---

## Quebrando Hashes de /etc/shadow 

O John é bem específico sobre os formatos em que precisa de dados pra trabalhar com ele, então, pra quebrar o /etc/shadow, precisamos trabalhar junto com o /etc/passwd, assim o john entende os dados que está sendo dado.

Pra fazer isso, podemos rtabalhar com uma ferramenta que faz o unshadow, a sintaxe é a seguinte:

`unshadow [path to passwd] [path to shadow]`

- [path to passwd]: O arquivo que contém a cópia do /etc/passwd arquivo que você tirou da máquina de destino
- [path to shadow]: O arquivo que contém a cópia do /etc/shadow arquivo que você tirou da máquina de destino 

em `[path to **]` podemos usar tanto o arquivo tanto a linha específica que queremos, por exemplo: 


/etc/passwd
`root:x:0:0::/root:/bin/bash`

/etc/shadow
`root:$6$2nwjN454g.dv4HN/$m9Z/r2xVfweYVkrr.v5Ft8Ws3/YYksfNwq96UL1FX0OJjY1L6l.DS3KEVsZ9rOVLB/ldTeEL/OIhJZ4GMFMGA0:18576::::::`

Depois disso, ele gera um arquivo ao qual passamos para o john crackear - as vezes precismaos definir o formato novamente, que é sha512crypt, as vezes não.


root:x:0:0::/root:/bin/bash root:$6$Ha.d5nGupBm29pYr$yugXSk24ZljLTAZZagtGwpSQhb3F2DOJtnHrvk7HI2ma4GsuioHp8sm3LJiRJpKfIf7lZQ29qgtH17Q/JDpYM/:18576::::::

---

## Single Crack

Single Crack (modo --single) do John: usa o nome de usuário (e campos GECOS) como base e aplica mangling rules (pequenas mutações: maiúsculas, números, símbolos) para gerar senhas prováveis.

Uso rápido:

`john --single --format=raw-sha256 hashes.txt`

— no arquivo os hashes devem vir com username:hash (ex.: joker:1efee0...).

---

## Quebrando senhas de ZIPs protegidos

Resumo prático, técnico e rápido

Converter o ZIP para hash legível pelo John:
zip2john [opções] arquivo.zip > zip_hash.txt

Exemplo (arquivo local):
zip2john ~/John-the-Ripper-The-Basics/Task09/secure.zip > /tmp/zip_hash.txt

Quebra com John (wordlist comum):
john --wordlist=/usr/share/wordlists/rockyou.txt /tmp/zip_hash.txt

Observações rápidas:

zip2john extrai o hash e meta que o John consegue processar; raramente precisa passar opções.

Redirecionamento > grava a saída num arquivo que você alimenta no john.

Se quiser ver o progresso/resultado: john --show /tmp/zip_hash.txt.

---

## SSH

Resumo prático, técnico e rápido — Craqueamento de passphrases de chaves SSH

Objetivo: recuperar a passphrase de uma chave privada id_rsa para permitir uso da chave em autenticação SSH.

Ferramenta de conversão: ssh2john (ou ssh2john.py) converte id_rsa para um hash que o John pode processar.
Exemplo: