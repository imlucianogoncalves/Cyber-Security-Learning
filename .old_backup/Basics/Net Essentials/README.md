# Network Essentials

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

Objetivo de aprender sobre:

- DCHP
- ARP
- NAT
- ICMP
    - Ping
    - Traceroute

## DHCP

Sempre que vamos usar uma rede, precisamos no mínimo de:

- Endereço IP junto com máscara de sub-rede
- Roteador (ou gateway)
- DNS servidor

Configurar essas opções manualmente são boas, especialmente pra servidores (não bão precisar mudar de rede). Além disso, eles precisam de informações fixam para acesso de terceiros.

Porém, automatizar o processo de configurar novos dispositivos tem suas vantegens, como nos poupar do trabalho de config manual - conflitos de endereço (quando dois recebem o msm endereço IP).

O DHCP serve pra isso, ele é um protocolo de nível de aplicativo que depende de UDP - o servidor escuta em UDP na porta 67, e o cliente envia de UDP na porta 68 - seu pc e celular te DHCP como padrão.

D - Disvoer
O - Offer
R - Request
A - Acknowledge


O DHCP segue essas 4 etapas, descobrir, oferecer, solicitar e reconhecer.

1- DHCP Discover: O cliente manda um DHCPDISCOVER buscando o servidor DHCP local, se houver.
2- DHCP Offer: O servidor responde com uma mensagem DHCPOFFER com um endereço IP disponível para o cliente aceitar.
3- O cliente responde com uma mensagem DHCPREQUEST para indicar que aceitou o IP oferecido.
4- DHCP Acknowledge: O servidor responde com uma mensagem DHCPACK para confirmar que o endereço IP oferecido agora está atribuído a este cliente.

## ARP - Address Resolution Protocol

Possibilita encontrar o endereço MAC de outro dispositivo na Ethernet.

O ARP tem um processo para reconhecer o endereço MAC de outro host na rede. Como ele faz? Com o ARP.

Exemplo: 

- O computador A tem o IP 192.168.66.89
- Ele quer se comunicar com o computador B, que tem o IP 192.168.66.1

Como o A só sabe o IP do B, ele envia uma mensagem ARP perguntando:

- “Quem tem o IP 192.168.66.1? Me diga seu endereço MAC!”

Essa mensagem é enviada para todos os dispositivos da rede (broadcast), usando o endereço MAC especial ff:ff:ff:ff:ff:ff.

O computador B vê a mensagem e responde:

- “Eu sou o 192.168.66.1, e meu endereço MAC é [xx:xx:xx:xx:xx:xx].”

Depois disso, o computador A guarda essa informação em uma tabela (chamada tabela ARP) e, a partir daí, consegue se comunicar diretamente com o B usando o endereço MAC dele.

*O ARP ASK e o ARP ANSWER* não é encapsulado dentro de um UDP ou IP - ele é encapsulado diretamente dentro de um quadro Ethernet.

O ARP é considerado da **camada 2** por que lida com endereços MAC.

## ICMP - Troubleshooting de redes.

O Internet Control Message Protocol (ICMP) é usado principalmente apra diagósticos de rede e relatórios de erros. Dois comandos são populares dependem do ICMP e são fundamentais na solução de problemas de rede e na segurança da rede.

- ping: usa o ICMP  para testar a conectividade a um sistema de destino e mede o round tripe time (RTT). Vẽ se o alvo tá vivo e em quanto tempo ele responde.
- traceroute: ele é chamado de traceroute em linux e tracert em windows usa ICMP para descobrir a rota do alvo.

### Ping

Funcona como o jogo ping-pong, jogamos a bola para ele (com o ICMP dentro de um pacote IP), e ele nos responde, com outro pacote IP ocm um ICMP dentro, só que com a resposta - o ping calcula se chegou e em quanto tempo chegou.

### Tracceroute

O protocolo IP tem um campo chamado TTL (time-to-live) que indica o número máximo de roteadores pelos quais um pacote PODE viajar antes de ser descartado.

O roteador diminui os pacotes TTL por um antes de envia-lo, quando o TTL chega a zero, o roteador descarta o pacote e envia um ICMP time exceeded.

## Routing Protocols:


- OSPF (Open Shortest Path First) : OSPF é um protocolo de roteamento que permite que os roteadores compartilhem informações sobre a topologia da rede e calculem os caminhos mais eficientes para a transmissão de dados. Ele faz isso fazendo com que os roteadores troquem atualizações sobre o estado de seus links e redes conectados. Dessa forma, cada roteador possui um mapa completo da rede e pode determinar as melhores rotas para chegar a qualquer destino.

- EIGRP (Enhanced Interior Gateway Routing Protocol) : EIGRP é um protocolo de roteamento proprietário da Cisco que combina aspectos de diferentes algoritmos de roteamento. Ele permite que os roteadores compartilhem informações sobre as redes que podem alcançar e o custo (como largura de banda ou atraso) associado a essas rotas. Em seguida, os roteadores usam essas informações para escolher os caminhos mais eficientes para a transmissão de dados.

- BGP (Border Gateway Protocol) : O BGP é o protocolo de roteamento principal usado na Internet. Ele permite que diferentes redes (como as de provedores de Serviços de Internet) troquem informações de roteamento e estabeleçam caminhos para que os dados trafeguem entre essas redes. O BGP ajuda a garantir que os dados possam ser roteados com eficiência pela Internet, mesmo ao atravessar várias redes.

- RIP (Routing Information Protocol) : RIP é um protocolo de roteamento simples frequentemente usado em redes pequenas. Os roteadores que executam o RIP compartilham informações sobre as redes que podem alcançar e o número de saltos (roteadores) necessários para chegar lá. Como resultado, cada roteador constrói uma tabela de roteamento com base nessas informações, escolhendo as rotas com o menor número de saltos para chegar a cada destino.
