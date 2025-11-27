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
