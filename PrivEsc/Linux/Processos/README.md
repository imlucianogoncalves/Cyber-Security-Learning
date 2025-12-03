# Processos no Linux (ps, top, pgrep, pkill)

Objetivos da aula:

No final você deve ser capaz de:

- ler a árvore de processos como um atacante

- identificar processos úteis para privesc

- identificar serviços vulneráveis

- reconhecer backdoors e serviços incomuns

- usar `ps`, `pgrep`, `top`, `pkill` com profundidade

- investigar o dono de cada processo

- mapear superfície de ataque pós-shell

---

Processos são **tudo o que está rodando no sistema**.

Para um pentester, processos revelam:

- credenciais expostas

- comandos rodando como root

- caminhos sensíveis (scripts, binários, configs)

- serviços vulneráveis

- backdoors

- cronjobs executando coisas suspeitas

- programas usando portas internas

- serviços rodando sob usuários fracos

- VMs, containers, dev tools

---

Para vermos os processos rodando no sistema, podemos usar `ps`. Porém o ideal mesmo, é usarmos `ps aux`, já que:

- a = mostra processo de todos os usuarios

- u = mostra o dono do processo

- x = mostra processos sem terminal associado 

A saída é algo como:

![](/home/lugon/.config/marktext/images/2025-11-28-06-23-32-image.png)

Aqui, nós, como pentesters procuramos:

- processos que rodam como root

- processos que chamam scripts externps

- processos python, node, java (apps vulneráveis)

- binários em diretórios incomuns (opt/, home/, tmp/)

- processos rodando em screen/tmux

- processos com argumentos suspeitos

---

Já com `ps -ef`, temos uma opção parecida com `ps aux` mas conseguimos ver o pid pai e pid filho (PPID).

Isso é bom, por que vemos:

- processos root filhos de processos não-root → suspeito

- serviços com PPID incomum → possível misconfig

- árvore estranha → backdoor ou script vulnerável

---

Para achar um processo específico, podemos usar o `pgrep + [busca]`, alguns exemplos:

- `pgrep ssh`

- `pgrep apache`

- `pgrep cron`

Você pode deixar mais detalhado usando `pgrep -af [busca]`, com isso mostramos os argumentos e comando executado.

---

Para matar um processo, ou, termina-lo, usamos o comando `pkill + [serviço]`.

Mas atenção, pois, matar um processo em ambiente real é fazer muito ruído, sysadmins/EDR veem isso como comportamento malicioso.

Tomar cuidado e não usar para qualquer coisa.

---

Para ver os processos do sistema em tempo real, usamos o comando `top`, onde podemos ver:

- processos em execução

- consumo de C PU e RAM

- quem é o dono do processo

- comandos usados

- spikes anormais

Como pentester, você observa:

- spikes de CPU em serviços fracos

- processos rodando como root

- serviços muito antigos

- processos rodando em diretórios errados

- processos que chamam scripts externos

Exemplo de coisa suspeita:

`root    1324  30.0  /tmp/update`

Um processo root em `/tmp` → perigo total.

---

## Exploração em processos

### Pegando credênciais vazadas

 Alguns processos passam as credenciais nos argumentos

`ps aux | grep mysql`

Imprime:

`/usr/bin/mysqld --user=root --password=SuperSecret123!`

### Descobrindo scripts root

`ps aux | grep root`

Você encontra:

`root /usr/local/bin/backup.sh
root /opt/scripts/update.py
root /usr/bin/php /var/www/admin/cron.php`

Esses arquivos são objetivos imediatos de privesc.

### Descobrindo serviços rodando versões vulneráveis

`ps aux | grep apache
ps aux | grep nginx
ps aux | grep python`

Se encontrar:

`python3 app.py (rodando flask 0.10)`

Flask 0.10 tem RCE em debug mode.

### Encontrando binários maliciosos

Qualquer processo em:

- /tmp

- /dev/shm

- /var/tmp

- home de usuários

- /opt improvável

É um bom candidato para análise.

## Atividade:

**Qual a diferença entre ps aux e ps -ef?**

`ps aux` mostra todos os processos incluindo os que não têm terminal associado, destacando o usuário e o comando executado.  
`ps -ef` também mostra todos os processos, mas é melhor para visualizar a relação entre eles, porque exibe PID e PPID com clareza.

**Por que um processo rodando em /tmp ou /dev/shm é altamente suspeito?**

Porque `/tmp` e `/dev/shm` são diretórios world-writable usados para arquivos temporários. Não é normal processos serem executados dali, então quando um processo aparece nesses locais, é suspeito, pois indica que algum usuário colocou um executável ali para rodar.

**Que tipo de informação útil um atacante pode extrair de argumentos de processos?**

Um atacante pode ver credenciais expostas, caminhos de arquivos sensíveis e comandos que revelam como serviços estão sendo executados. Essas informações ajudam na enumeração e na busca por privesc.

**Por que pkill deve ser evitado em operações reais?**

Porque encerrar processos diretamente é um comportamento anormal e facilmente detectado. Isso alerta sysadmins e mecanismos de detecção, prejudicando a OPSEC e podendo levar à perda de acesso.
