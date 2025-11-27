# Logs e journalctl

Antigamente nos sistemas Linux, tinhamos todos os logs agrpados dentro da pasta /var/log/, porém, atualmente, seguimos com um  novo padrão que utiliza uma ferramenta que armazena os logs em formato binário, não só em texto.



Você pode visualizar **TODOS** os logs do sistema usando o comando `journalctl`.



`journalctl -xe` mostra os últimos logs e vai para o fim da página, útil para saber o que recentemente aconteceu no sistema.



Podemos também, filtrar por serviço usando

- `journalctl -u apache2`

- `journalctl -u ssh`



Assim como, filtrar por processo com: 

`journalctl _PID=1234`



Podemos ver por unidade systemd

- `journalctl -u mysql`

- `journalctl -u mysql`



Para ver os logs desde o boot, usamos

`journalctl -b`



Da pra usar o grep junto para filtrar, como: 

`journalctl | grep "Failed password"
journalctl -u ssh | grep "authentication"`



---

## Perspectiva de atacante

Por que ler logs na perspectiva de atacante é relevante?

Vários motivos:



Sysadmins podem cometer o erro de imprimir credenciais sensíveis em arquivos de logs, como:

`echo "Password=Admin123!" >> /var/log/install.log`



Ou alguns scripts geram logs de:

`echo "Connecting with user root and pass 123456"`



Com isso, uma arquivo meramente informativo nos dá acesso a determinada área / serviço de bandeja.



Outra coisa é que, quando algum serviço falha, pode dar informação de valor para nós, como um diretório ou arquivo que deveria ser secreto.

Por exemplo: 

`journalctl -u mysql | grep "error"`

Gerou:

`Failed to start MySQL: Can't read /etc/mysql/backup.key`

Entendeu que o arquivo backup.key pode ter credênciais, chaves ou alguma forma de acesso?



### Outras vulnerabilidades de logs

Podem nos informar caminhos interessantes, como:

- scripts secretos

- usuários internos

- caminhos sensíveis

- diretórios incomuns

- binários chamados por root

- erros que mostram stack traces



Vamos pensar nesse exemplo: 

`journalctl -u backup`



retornou:

`Running /opt/admin/backup.sh as root`



Com esse log, podemos saber que:

- existe `/opt/admin/backup.sh` - pode ter o bit SUID ativado

- é executado como root

- podemos verificar permissões, world-writable no arquivo ou diretório /opt/admin.

---




