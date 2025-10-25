# Introdução à Análise de Redes

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno SOC do TryHackMe

## Router

Um roteador é um dispositivo de rede que encaminha dados com base em um endereço lógico. No caso das redes TCP/IP, o router encaminharia dados baseados em endereços IP de sistemas. Se estiver na sua rede doméstica e quiser visitar Google.com, o seu pedido irá para o router (o DNS converterá o nome de domínio Google.com para o endereço IP), e o seu pedido será enviado pela internet para o servidor web Google.com IP.

## Hub

Um hub é um dispositivo de rede que conecta todos os dispositivos em uma rede local ou LAN. Quando um sistema envia dados para o hub em uma porta, o hub os transmitirá para todos os outros dispositivos conectados (veja a imagem abaixo). Os Hubs podem ser referidos como dispositivos “burros” porque não compreendem quem é o destinatário pretendido dos dados que foram recebidos, pelo que os envia para todos os dispositivos.

Apesar de os dados eventualmente chegarem ao sistema pretendido, gera tráfego desnecessário e também pode permitir que os atacantes roubem dados. Se um atacante estiver conectado a um hub, sempre que um host conectado enviar dados, ele será enviado para qualquer outro host, incluindo a máquina do atacante!

## Switch 

Um switch funciona como uma versão inteligente de um hub porque realmente percebe para onde enviar dados, em vez de enviá-los a todos. Ele consegue isso usando endereços MAC como identificadores únicos para os destinatários dos dados recebidos, para que possa enviá-los para o sistema correto.

Neste diagrama abaixo, se o Computador Desktop quiser imprimir um documento, enviaria a solicitação que chegaria ao Comutador de Rede, que saberá enviá-lo para a impressora já que o computador de mesa incluirá o endereço MAC no pedido (que é obtido com o Address Resolution Protocol ou ARP).

## Bridge 

Um dispositivo de ponte de rede conecta redes separadas para torná-las em uma rede maior. Isto é diferente de um router, que permite que as redes sejam ligadas mas funcionem de forma independente. No modelo OSI, a ponte funciona na Camada 2, a camada de vínculo de dados.

## Firewall

Um firewall é um dispositivo de rede que fornece segurança de rede fundamental, monitorando o tráfego de entrada e saída e determinando se o permite ou bloqueará, com base em regras. Os firewalls podem vir em formato de software ou hardware como dispositivos físicos conectados à infra-estrutura de rede. Isto permite-nos criar redes privadas, onde só podem entrar ou sair comunicações pretendidas.

---

## tcpdump 

tcpdump -d : exibe as interfaces disponíveis

tcpdumo -i wlan0 : captura em determinada interface

### Filtros

src + ip ou dst + ip para filtrar por endereço de destino ou origem.

port + 445 : para filtrar por determinada porta.

tcpdump ftp : para filtrar por protocolo.

podemos usar "and" e "or" também.

e -c 50 é a quantidade de pacotes que irão ser capturados.

-n : evita q os ips e protas se resolvam para nomes

e -w + arquivo salva a saída da captura.

### Leitura de arquivos .pcapng

tcpdump -v -r nomedoarquivo.pcapng : quanto mais v's, mais verboso.

Cabeçalho dos pacotes

Primeira linha: mostra informações do cabeçalho IP — TTL, sinalizadores, protocolo (TCP, UDP etc.), tamanho e fragmentação.

Segunda linha: mostra endereços IP e portas de origem e destino, sinalizadores TCP (SYN, ACK, FIN etc.), números de sequência, tamanho da janela e opções.

Filtros

Você pode filtrar pacotes com base em campos do cabeçalho:

Por sinalizador TCP:

Um só: tcp[tcpflags] == tcp-push (mostra apenas pacotes PSH).

Vários: soma os valores dos bits (ex: PSH + ACK = 24 → tcp[tcpflags] == 24).

Por byte do cabeçalho:

Exemplo: icmp[0] == 8 mostra apenas ICMP Echo Request (ping).

Pode usar nomes de campos: icmp[icmptype] == 8.

Opções úteis do TCPdump

-A → mostra conteúdo em texto (ASCII).

-x → mostra dados em hexadecimal.

-X → mostra os dois.

-t, -tt, etc. → controlam o formato do timestamp.

Manipulação com comandos Unix

A saída do TCPdump é texto — dá para filtrar e processar com comandos do shell:

cut: corta campos por delimitadores.
Ex: cut -d ">" -f 1 mostra só o que vem antes do símbolo >.

awk: extrai campos por posição (separados por espaço).
Ex: awk '{print $7}' imprime o 7º campo (por exemplo, as flags TCP).

grep: procura linhas que contêm uma palavra.
Ex: grep zip mostra pacotes com “zip” no conteúdo.