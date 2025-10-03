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

