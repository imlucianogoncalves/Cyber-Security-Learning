# Network Core Protocols

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe


## DNS

DNS opera na camada de aplicação - camada 7 do modelo OSI.

DNS usa o tráfego UDP:53 e TCP:53 como fallback padrão.

Tipos de DNS

- A: mapeia um host para um ou mais endereços IPv4.

- AAAA: semelhante ao registro A, mas para IPv6.

- CNAME - mapeia um nome de domínio para outro domínio

- MX - Mail Exchange: especifica o servidor de e-mail responsável pelo tratamento dos emails do dominio.

NSLOOKUP - mostra o endereço IP de um domínio

WHOIS - consulta os registros daquele domínio, quem é o proprietário, e-mail, quando expira, etc.

## HTTP(S)

HTTP (S) se baseia em TCP.

Alguns comandos ou métodos que seu navegador emite para o web server são:

- GET - recuperar dados de um servidor, como um html ou imagem.

- POST - nos permite enviar novos dados ao servidor, como enviar um form ou fazer upload de um arquivo.

- PUT - usado para criar um novo recurso no servidor e para atualizar e sobrescrever infos existentes

- DELETE - ele exclui um arquivo ou recurso.

HTTP e HTTPS usam normalmente portas 80 e 443 respectivamente, menos comumente 8080 e 8443

# FTP

É usado para transfeir arquivos.

Comandos definidos pelo protocolo FTP:

- USER - para inserir o nome de usuario
- PASS - para inserir a senha
- RETR - para baixar um arquivo do servidor ftp para o cliente
- STOR - usado para carregar um arquivo do cliente para o servidor.

Atua na porta 21 como padrão.

## SMTP 

Envio de e-mails  - Simple Mail Transfer Protocol (SMTP) - como um cliente e-mail e um servidor de e-mail se comunicam.

Comandos do SMTP quando ele transfere um e-mail

- HELO ou EHLO inicia um SMTP sessão
- MAIL FROM especifica o endereço de E-mail do remetente
- RCPT TO especifica o endereço de E-mail do destinatário
- DATA indica que o cliente começará a enviar o conteúdo da mensagem de E-mail
- . é enviado em uma linha por si só para indicar o final da mensagem de E-mail 

## POP3 - recebendo o e-mail

O POP3 é usado para que o cliente se comunique com o servidor de e-mail e recupera mensagens de e-mail

SMTP é como entregar seu envelope ou pacote aos correios e o POP# é verificar a caixa de correio para novas cartas ou pacotes.

Comandos comuns do POP3:


- USER <username> identifica o usuário
- PASS <password> fornece a senha do Usuário
- STAT solicita o número de mensagens e o tamanho total
- LIST lista todas as mensagens e seus tamanhos
- RETR <message_number> recupera a mensagem especificada
- DELE <message_number> marca uma mensagem para exclusão
- QUIT termina o POP3 sessão aplicando alterações, como exclusões

## IMAP

Internet Message Access Protocol (IMAP) sincroniza as mensagens, as recebe como um interceptador, você as ve e elas não são apagadas.

Ao contrário do POP3 - que apaga os outros e-mails e só o armazena em si proprio.


- LOGIN <username> <password> autentica o usuário
- SELECT <mailbox> seleciona a pasta mailbox para trabalhar
- FETCH <mail_number> <data_item_name> Exemplo fetch 3 body[] para buscar a mensagem número 3, cabeçalho e corpo.
- MOVE <sequence_set> <mailbox> move as mensagens especificadas para outra caixa de correio
- COPY <sequence_set> <data_item_name> copia as mensagens especificadas para outra caixa de correio
- LOGOUT faz logout

| Protocolo | Transporte | Porta |
|------------|-------------|-------|
| TELNET | TCP | 23 |
| DNS | UDP ou TCP | 53 |
| HTTP | TCP | 80 |
| HTTPS | TCP | 443 |
| FTP | TCP | 21 |
| SMTP | TCP | 25 |
| POP3 | TCP | 110 |
| IMAP | TCP | 143 |
