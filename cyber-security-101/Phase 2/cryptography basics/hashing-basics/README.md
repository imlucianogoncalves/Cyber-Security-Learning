# Hashing - Básico

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

## Objetivos De Aprendizagem

Após a conclusão desta sala, você aprenderá sobre:

- Funções Hash e colisões
- O papel do hashing em sistemas de autenticação
- Reconhecendo valores de hash armazenados
- Valores de hash Cracking
- O uso de hashing para proteção de integridade

---

## Funções Hash

As funções Hash são diferentes da criptografia. Não há chave, e é para ser impossível (ou computacionalmente impraticável) ir da saída de volta para a entrada. 

---

Ele gera um "resumo" do conteúdo, que onde, qualquer único bit alterado pode causar uma mudança significativa no hash.

Alguns codificadores (são usados com o comando + arquivo ou texto):

`md5sum, sha1sum, sha256sum, e sha512sum`

---

Parece que servidores e sistemas não armazenam a senha bruta em seu HD, mas sim o hash da senha, por que, se por exemplo, eu tentar fazer login, ele não vai consultar a minha senha em sí, mas o hash dela, verificando se coincidem.

---

Importante:

Ao armazenar senhas em sistemas, devemos ter algumas atitudes, que a principal é:

Não guardar a senha no sistema, nem que seja criptografada.

O que deevmos fazer é gerar um hash daquela senha específica e aí sim armazenar esse hash no banco de dados, pois ao usuario tentar fazer login ou coisa do tipo, comparamos o hash gerado pela senha inputada com o hash do banco de dados - assim, nunca vazando a real senha.

Outra coisa que podemos fazer para deixar AINDA MAIS SEGURO, é adicionar **salt** a senha, pois algumas pessoas podem tentar quebrar com uma tabela rainbow, o salt nada mais é que adicionar alguma lógica além do hash em sí, então vamos supor que o salt é

123123 

e o hash é

2a8a572dfbb7f4364f4410a3135936b7 

O dado guardado no banco de dados seria:

1231232a8a572dfbb7f4364f4410a3135936b7

ou 

2a8a572dfbb7f4364f4410a3135936b7123123

--- 

## Reconhecendo hashes de senha

Na pasta /etc/shadow - as senhas normalmente tem esse formato:

`$prefix$options$salt$hash`

$y$ — yescrypt: esquema de hash escalável, escolha padrão e recomendada em novos sistemas

$gy$ — gost-yescrypt: usa a função hash GOST R 34.11-2012 e o método hash yescrypt

$7$ — scrypt: função de derivação de chave baseada em senha

$2b$, $2y$, $2a$, $2x$ — bcrypt: hash baseado na cifra de bloco Blowfish, originalmente desenvolvido para OpenBSD, suportado também em FreeBSD, NetBSD, Solaris 10+, e várias distribuições Linux

$6$ — sha512crypt: hash baseado em SHA-2 com saída de 512 bits, desenvolvido para GNU libc e comumente usado em sistemas Linux

$md5$ — SunMD5: hash baseado no algoritmo MD5, originalmente desenvolvido para Solaris

$1$ — md5crypt: hash baseado no algoritmo MD5, originalmente desenvolvido para FreeBSD

`strategos:$y$j9T$76UzfgEM5PnymhQ7TlJey1$/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4:19965:0:99999:7:::`

No exemplo acima, temos quatro partes separadas por $:

- y indica o algoritmo hash utilizado, yescrypt
- j9T é um parâmetro passado para o algoritmo
- 76UzfgEM5PnymhQ7TlJey1 o sal é usado
- /OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4 é o valor do hash


---

# Quebrando senhas 

## Hashcat

Sintaxe básica:

`hashcat -m <hash_type> -a <attack_mode> hashfile wordlist`

$HEX[206b6d3831303838] -> $HEX[042a0337c2a156616d6f732103]