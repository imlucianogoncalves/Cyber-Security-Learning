# Linux Fundamentals

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

## SSH (Secure SHell)

É um protocolo entre dispositivos de forma criptografada. Enviadmos os dados no formato humano e durante o processo de transporte, tais dados são criptografados.

- Permite executar comandos remotamente em outro dispositivo
- Todos os dados são criptografados quando são enviados pela internet.

### Flags e/ou Switches

A maioria dos comandos permite que passemos argumentos junto aos comandos própriamente ditos, como **ls -la**: nesse caso, o **ls** é o comando e o **-la** é o flags ou switch.

### Permissões

Temos 3 tipos de permissões

- Read
- Write
- Execute

---

**SU** alternar entre usuarios - precisamos saber o usuario e a senha.lssu 

---

**/etc/** é um diretório usado para armazenar arquivos de sistema que são usados pelo sistema operacional.

**/etc/passwd e /etc/shadow** são arquivos especiais que o sistema usa para armazenar as senhas de cada usuario em formtação criptografada em **sha512**.

---

**/var/** é a abreviação de variáveis - armazena dados que são acessados ou gravados com frequência. **/var/ /log/** estão aqui - guarda tbm outros dados que não estão atrelados a um usuario específico em sí.

---

**/root** é a home do usuario root - não tem nada além de seus arquivos e dados  de "usuario".

---

**/tmp** guarda dados de arquivos temporarios - para coisas que vão ser reutilizadas 2 ou mais vezes - quando o pc reinicia, apaga tudo.

---

**nano** para criar e/ou editar arquivos de texto.

---

**wget + url** é usado par abaixar arquivos.

---

## SCP

> **MUITO IMPORTANTE**

**SCP** é usado para transferir arquivos da máquina local pra máquina remota e vise versa.

A sintaxe do comando é: 

**scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt**

Variável 	Valor
O endereço IP do sistema remoto  	192.168.1.30
Usuário no sistema remoto 	ubuntu
Nome do arquivo no sistema local 	importante.txt
Nome que desejamos armazenar o arquivo como no sistema remoto 	Transferido.txt 

O contrário é: **scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt**

---

Para abrir um HTTP.Server em python:

**python3 -m http.server**

MUUUUITO IMPORTANTE - vamos supor que consegui acesso a um terminal remoto e preciso transferir um arquivo pra ele, eu posso simplesmente subir um HTTP.Server e servir o arquivo de malware e/ou payload para executar no servidor.

---

**cron a partir do crontabs** para executar tarefas programadas.

**crontab -e** para editar os contrabs e/ou adicionar.