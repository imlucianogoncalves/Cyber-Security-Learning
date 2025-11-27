# Critografia de Chave Pública - Básico

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

Ao se comunicar com seu parceiro de negócios por meio de uma plataforma de mensagens on-line, você precisa ter certeza do seguinte:

- **Autenticação:** Você quer ter certeza de se comunicar com a pessoa certa, não com outra pessoa fingindo.
- **Autenticidade:** Você pode verificar se a informação vem da fonte reivindicada.
- **Integridade:** Você deve garantir que ninguém altere os dados que você troca.
- **Confidencialidade:** Você deseja impedir que uma parte não autorizada escute suas conversas.

A criptografia pode fornecer soluções para satisfazer os requisitos acima, entre muitos outros. A criptografia de chave privada, ou seja, a criptografia simétrica, protege principalmente a confidencialidade. No entanto, a criptografia de chave pública, ou seja, a criptografia assimétrica, desempenha um papel significativo na autenticação, autenticidade e integridade. 

--

Nesta sala, abordaremos vários criptossistemas assimétricos e aplicativos que os utilizam, como:

- RSA
- Diffie-Hellman
- SSH
- Certificados SSL / TLS
- PGP e GPG


---

Por que usar a assimétria?

Ela pode ser mais lenta e mais complicada de se configurar, porém, ela garante a integridade e confidencialidade das informações. Por isso é uma boa opção.

---

# SSH

Normalmente são usadas senhas para logar, mas com certeza em algum dia vou me deparar com login via chaves - essa usa chaves pública e privadas para provar que o cliente é um usuário válido e autorizado no servidor.

Essas chaves por padrão são chaves **RSA** você pode escolher o algoritmo gerar e também uma senha ara criptografar a chave SSH

`ssh-keygen` - programa para gerar chaves, ele suporta vários algoritmos.

O seguinte é apenas para sua informação. Nesta fase, recomendamos que você reconheça apenas seus nomes.

- DSA (algoritmo de assinatura Digital) é um algoritmo de criptografia de chave pública projetado especificamente para assinaturas digitais.

- ECDSA (Elliptic Curve Digital Signature Algorithm) é uma variante do DSA que usa criptografia de curva elíptica para fornecer tamanhos de chave menores para segurança equivalente.

- ECDSA-SK (ECDSA com chave de segurança) é uma extensão do ECDSA. Ele incorpora chaves de segurança baseadas em hardware para proteção aprimorada de chave privada.

- Ed25519 é um sistema de assinatura de chave pública usando EdDSA (Edwards-curve Digital Signature Algorithm) com Curve25519.

- Ed25519-SK (Ed25519 com chave de segurança) é uma variante do Ed25519. Semelhante ao ECDSA-SK, ele usa uma chave de segurança baseada em hardware para melhorar a proteção da chave privada.

como são as chaves pública e privadas

Estão no formato **ed25519**

Chave pública:


```
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAACmFlczI1Ni1jdHIAAAAGYmNyeXB0AAAAGAAAABAmn14FDP
QUln6899Lzc8zRAAAAGAAAAAEAAAAzAAAAC3NzaC1lZDI1NTE5AAAAIMDYLw4yQfGd23pV
ABlWlMvs/bm45/egGtmM0XcEkQSsAAAAoFB5OsI4sI8O0XU+T/h0xTxsqqH2E/+T1Nks06
CglhbPyd6zoNuCE9SGLaWq2VPo87mfbR1Ouzg39vHAlfYgqWrwHfvZqmmqmCxZmKYGAiNj
YMMEo3Tk0yaSDEHcsVnsUxrXyfDv3arsl+p7F/TK3X0ocSJ/SwmkrUULY3zWkq/NL6cRQj
lao5BXJWGOg0FzlB3rCpxfg/nIjm1XHkku9Pc=
-----END OPENSSH PRIVATE KEY-----
```

Chave privada: 

```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMDYLw4yQfGd23pVABlWlMvs/bm45/egGtmM0XcEkQSs kur0g4n3@proton.me

```

---

Tomar cuidado com as chaves privadas como se fosse uma senha e criptografa-la quando possível.

---

** MUITO IMPORTANTE **

Normalmente, dentro de ~/.ssh / authorized_keys, temos uma lista de todas as chaves públicas guardas.

O THM me deu a dica de que em CTFs, isso pode ser muito bom para encontrar maneiras de escalar privilégios e encontrar bakcdoors.

---

# Assinaturas e Certificados Digitais

Exemplos de assinaturas digitais:

Imagine que Bob quer mandar um documento para Alice e provar que foi ele quem escreveu.

Etapas:

Bob cria o documento.

O computador dele faz um resumo (hash) desse arquivo — tipo uma “impressão digital” do documento.

Bob criptografa esse hash com a chave privada dele → isso é a assinatura digital.

Ele envia:

o documento normal

a assinatura digital

Quando Alice recebe, ela:

Gera o hash do documento que recebeu;

Usa a chave pública de Bob pra descriptografar a assinatura;

Se os dois hashes forem iguais, isso prova:

Que o documento não foi alterado (integridade ✅);

Que Bob assinou (autenticidade ✅).

---

Certificados é bem intuitivo, a empresa paga um serviço anual que gera tal ceritificado, que é lido pelo navegador e aceito.

---

# PGP - Pretty Good Privacy

Software que implementa criptografia para criptoografar arquivos, realizar assinatura digital e muito mais.

GnuPG ou GPG é a implementaçao open-source do OpenPGP

---

- Em CTFs você pode precisar usar GPG/PGP para descriptografar arquivos.

- Chaves privadas do GPG podem ser protegidas por frases-senha (igual a chaves SSH).

- Se a chave tiver senha, você pode tentar quebrá-la com gpg2john + John the Ripper.

- Nesta tarefa específica, a chave não está protegida por frase-senha.

- A página de man do GPG está disponível online para referência.