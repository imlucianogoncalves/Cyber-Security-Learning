# Windows Command Line

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

## Informações básicas do sistema.

**[ver]** mostra a versão do sistema.

**[systeminfo]** mostra as informações detalhadas do sistema : importante, para ver a versão geral, hardware, usuario, etc.

**[| more]** aplica paginação no retorno de um comando

**[cls]** limpa a tela.

**[comando + help]** mostra ajuda sobre o comando.

## Soluções de problemas de rede

**[ipconfig]** - informações de rede, como IPv4, máscara de sub-rede, gateway padrão.

**[ipconfig /all]** mostra uma visão geral de sua configuração de rede.

podemos ver Registros DNS, Habilitação do DHCP, etc.

**[ping target_add]** pra solução de problemas, verificando se o destinatário responde através do envio de um pacote ICMP

**[tracert target_add]** traça todo o caminho percorrido para chegar no endereço alvo

**[nslookup target_add]** procura por um host para aquele determinado endereço. podemos adicionar um endereço personalizado para fazer a requisição, como nslookup target_add 1.1.1.1

**[netstat]** mostra as conexões ao qual o computador está associada, netstat -abont mostra as conexões, processos, endereço ip, estado, etc.

## Directories

**[cd]** funciona como o pwd do linux - mostra o diretório atual

**[dir]** funciona como o ls do linux - mostrando os diretórios e arquivos - parametro /a é como o -a do linux - mostra arquivos e diretórios escondidos.

**[tree]** mostra de forma formatada os diretórios e subdiretórios de onde vc está.

**[cd e mkdir]** são iguais ao linux, porém para remover, ao invés de rm, usamos **[rmdir]** que remove todo o diretório.

## Files

**[copy arquivo1.txt arquivo2.txt]** para copiar arquivos

**[move]** para mover

**[del / erase]** para remover arquivo.

Da pra usar * pra aplicar um filtro na ação, como **[copy *.md C:\Markdown]**, copia todos osarquivos com .md para a pasta em específico.

# Tarefas

**[tasklist]** mostra os processos em andamento.

exemplo: 

**[tasklist /FI "imagename eq sshd.exe"]** mostra o processo que tem a coluna imagename = sshd.exe

para fechar um processo usamos

[**taskkill /PID target_pid**]


## EXTRAS

**[chkdsk]** checa o sistema e disco por erros

**[sfc /scannow]** scanea os arquivos do sistema por erros e os repara se possível.

## **/?** esse é o mestre.