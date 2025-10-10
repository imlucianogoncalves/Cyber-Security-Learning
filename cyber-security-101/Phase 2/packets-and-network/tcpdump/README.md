# TCPDUMP - Básico

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

A ferramenta tcpdump e seus libpcap são escritos em C e C++

---

Usando somente tcpdump - verificamos se ele ja esta instalado.

A primeira coisa é decidir qual interface de rede ouvir, usando `-i INTERFACE` - da pra ouvir em toodas também, usando `-i any` - você pode especificar uma interface como `-i eth0`

Um comando `ip a s` mostra as interfaces de rede disponíveis.

---

Para salvar os pacotes capturados para verificalos depois, usamod -w FILE, a extensão do arquivo é normalmente definida como .pcap - eles podem ser lidos depois usando o Wireshark.

Exemplo: 

`sudo tcpdump -i ens5 -w arquivo.pcap`

Escuta na interface ens5 e escreve no arquivo .pcap

--- 

Da pra colocar um limite de pacotes a serem escutados também, como 100, depois de receber 100 pacotes ele para sozinho, sem essa opção, ele continua para sempre. Para isso usamos -c NUMERO

`sudo tcpdump -i ens5 -w arquivo.pcap -c 50`

---

Por padrão, o tcpdump tenta resolver os pacotes com os endereços IPs amigáveis, ou seja, usando dns, se quisermos mostrar o endereõ CRU, podemos usar -n e se quisermos que até a porta não seja resolvida, como 142.250.217.46.https, podemos usar -nn

assim, aparece o endereço IPP bruto e sua porta bruta.

---

Da pra produzirmos uma saída verbosa também, para ver cada pacote chegando e indo, com -v - a cada v que adicionamos ele produzirá saída ainda mais verbosa, como -vvv

Para ler esse pacote, podemos usar o wireshark ou o próprio tcpdump, com 

`sudo tcpdump -r arquivo.pcap`

--- 

- tcpdump -i INTERFACE 	Captura pacotes em uma interface de rede específica
- tcpdump -w FILE 	Grava pacotes capturados em um arquivo
- tcpdump -r FILE 	Lê pacotes capturados de um arquivo
- tcpdump -c COUNT 	Captura um número específico de pacotes
- tcpdump -n 	Não resolva endereços IP
- tcpdump -nn 	Não resolva endereços IP e não resolva números de Protocolo
- tcpdump -v 	Exibição detalhada; a verbosidade pode ser aumentada com -vv e -vvv

---

Da pra filtrar por host também, usando host + example.com

`sudo tcpdump host example.com -w http.pcap`

Podemos filtrar por porta também, usando por + porta

`sudo tcpdump -i ens5 port 53 -n`

---

Também da pra só citar o protocolo, usando seu nome mesmo, ip, ip6, udp, tcp e icmp

---

OPERADORES LÓGICOS:


- and: Captura pacotes onde ambas as condições são verdadeiras. Por exemplo, tcpdump host 1.1.1.1 and tcp capturas tcp trânsito com host 1.1.1.1.
- or: Captura pacotes quando qualquer uma das condições é verdadeira. Por exemplo, tcpdump udp or icmp capturas UDP ou tráfego ICMP.
- not: Captura pacotes quando a condição não é verdadeira. Por exemplo, tcpdump not tcp captura todos os pacotes, exceto TCP segmentos; esperamos encontrar UDP , ICMP, e ARP pacotes entre os resultados.
