# Network Fundamentals

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

# Modelo OSI

O modelo OSI (Open System Interconnection Model) é um modelo que dita como todos os dispositivos em uma rede enviaração, receberação e interpretarão os dados.

Ele é usado para que, dispositivos com diferentes designs e arquiteturas possam comunicar-se entre sí por seguir o modelo padrão.

*Ele tem 7 camadas e é organizado normalmente da 7 para a 1.*

- 1 Physical Layey
- 2 Data Link Layer
- 3 Network Layer
- 4 Transport Layer
- 5 Session Layer
- 6 Presentation Layer
- 7 Application Layer.

## 1. A Camada Física (Physical Layer)

Essa é a camada mais baixa e lida com sinais elétricos para transmitir dados entre sí. Um exemplo é os cabos Ethernet.

## 2. A Camada de Enlace de Dados (Data Link Layer)

Essa camada se concentra no endereçamento físico da transmissão.

Ela recebe um pacote da camada de rede **(3. Network Layer)** e adiciona no endpoint do endereço MAC do receptor.

Dentro de cada computador tem uma NIC (Network Interface Card) que vem com um endereço MAC exclusivo.

A camada de **enlace de dados** também é responsável por apresentar os dados em um formato adequado para a transmissão.

## 2. A Camada de Rede (Network Layer)

Aqui acontece o processo de roteamento e remontagem de dados.

Primeiro, o roteamento simplesmente determina o caminho mais ideal no qual esses blocos de dados devem ser enviados 

**Obs**: *Como ativar o Waze para pegar um caminho mais rápido*

Essa camada já tem alguns protocolos que decidem esses melhores caminhos, mas só saberemos disso aqui na camada de rede.

Os protocolos são: **OSPF (Open Shortest Path First) e RIP (Routing Information Protocol)**

Os fatores que decidem a rota a ser seguida são:

- Qual o caminho mais curto? *Ou seja, tem a menor quantidade de dispositivos que o pacote precisa percorrer*
- Qual é o caminho mais confiável? *Ou seja, os pacotes já foram perdidos nesse caminho antes?*
- Qual caminho tem a conexão física mais rápida? *Qual caminho está utilizando cabo coaxial (cobre - mais lento) e qual está usando cabo de fibra óptica (mais rapido?)*

Nessa camada tudo é tratado a partir de endereços IP. 

Se um roteador tem a capacidade de entregar pacotes usando endereços de IP, eles são chamados de Dispositivos de Camada 3.

## 4. A Camada de Transporte (Transport Layer)

Dados são enviados a partir de um dos 2 protocolos

- TCP - Transmission Control Protocol
- UDP - 

TCP é bom pois transmite confiabilidade e garantia - ele garante que os dados sejam enviados e recebidos.

Além disso, garante que os pacotes na camada de sessão (5) tenham sido recebidos e montados na mesma ordem.

Utilizado para 

- Compartilhamento de arquivos
- Navegação na internet
- Envio de e-mail

(Precisam que os dados sejam recebidos precisamente e completamente)

O UDP (User Datagrama Protocol), diferente do TCP só envia e pronto. Não verifica recebimento, nâo verifica integridade nem nada.

Ele é bem rápido e não mantém a conexão constante como o TCP

> *UDP é útil em situações em que há pequenos pedaços de dados sendo enviados. Por exemplo, protocolos usados para descobrir dispositivos ( ARP e DHCP que discutimos em Sala 2-Introdução à LAN) ou arquivos maiores, como streaming de vídeo (onde não há problema se alguma parte do vídeo estiver pixelada. Pixels são apenas pedaços perdidos de dados!)*

## 5. A Camada de Sessão (Session Layer)

A sessão, que funciona depois que os dados sejam corretamente traduzidos ou formatados a partir da camada de apresentação (camada 6) - mantém uma conexão com o dispositivo para qual os dados estão sendo enviados ou recebidos.

Enquanto houver conexão, haverá sessão.

Ela também fecha a conexão caso dê um "timeout".

## 6. A Camada de Apresentação (Presentation Layer)

Aqui ocorre a traduçao dos dados para a camada de Aplicação (camada 7) - mesmo que usemos navegadores diferentes, clientes de e-mails diferentes, precisamos que os dados sejam os mesmos e sejam vistos da mesma maneira.

Assim age essa camada, traduzindo e tratando os dados recebidos.

Recursos de segurança, como HTTPS ocorrem nessa camada.

## 7. A Camada de Aplicação (Application Layer)

Essa é a mais conhecida, aplicativos, navegadores, ftps, oferecem uma GUI (Graphical User Interface) onde o usuario pode interagir com os dados enviados e/ou recebidos.

Também tem o DNS, que lida em como os endereços dos sites são convertidos em endereços IP.

# Pacotes e Frames

Um **pacote** é um pedaço de dados da camada 3 (a camada de rede) do Modelo OSI - tem infos como: cabeçalho IP e carga útil.

O quadro, contudo, é usado na camada 2 (enlace de dados) que, encapsula o **pacote** e adiciona a informação adicional tal como endereços MAC.

Essse processo se chama encapsulamento - é seguro assumir que quando estamos falando de qualquer coisa sobre endereços IP, estamos falando de **pacotes** e quando as infos de encapsulamento são removidas, são quadros.

**Algumas headers padrões de um pacote:**

- **Time to live** - temporizador de expiração, pra que ele não fique indefinidamente na rede e não consiga alcançar um host ou sair do sistema.
- **Checksum** - verifica a integridade: se o conteúdo do pacote for alterado durante a transmissão, o valor calculado não corresponderá ao esperado, indicando corrupção 
- **Source Address** - o endereço IP que enviou o pacote, ele permite que o destinatário saiba para onde responder.
- **Destination Address** - para onde ele está sendo enviado - próximo destino que os dados devem alcançar.

## TCP / IP

O TCP/IP é uma versão resumida do modelo OSI. Contendo apenas 4 camadas:

- Aplicação 
- Transportes
- Internet
- Network Interface

**Ele é baseado em conexão** - deve estabelecer conexão entre o cliente e um dispositivo que atua como servidor.

Sendo ele baseado em conexão, ele garante que os dados enviados sejam recebidos na outra porta - esse processo se chama handshake de três vias, ou (three ways handshake).

Pq é bom?

- integridade de dados
- evita bagunça na ordem de envio e recebimento
- confiabilidade.

---

Como funciona o handshake de três vias?

### 1. SYN

Pacote inicial enviado por um cliente, usado para iniciar uma conexão e sincronizar dois dispositivos juntos.

### 2. SYN/ACK

Enviado pelo servidor para confirmar a tentativa de sincronização do cliente.

### 3. ACK

Pode ser usado pelo cliente e/ou servidor para confirmar que uma série de mensagems / pacotes foram recebidos com sucesso.

### 4. DATA

Depois da conexão ser estabelecida, os dados (como bytes de um arquivo) são enviados atráves de uma mensagem "DATA".

### 5. FIN 

Pacote usado para limpar corretamente a conexão depois de concluída.

### # RST

Finaliza abruptamente a conexão - é o último recurso: indica se o serviço ou aplicativo n estiverem funcionando corretamente ou se apresentar falhas.


## Fechando a conexão TCP

Ele fecha quando um dispositivo determinar que o outro recebeu todos os dados com êxito.

Prioridade fechar a conexão TCP o mais rápido possível - reserva recursos do sistema no dispositivo.

O dispositivo envia um pacote **FIN** para fechar a conexão,

Então ficaria:

- Cliente: FIN - quero terminar
- Servidor: ACK - tendi
- Servidor: FIN - bora terminar então
- CLiente: ACK - blz


# UDP / IP

Não precisa de conexão constante, não tem handshake de três vias, nem qualquer sinc.

É stateless.

# Portas 

São entre 0 e 65535.

Tem algumas portas padrão para facilitar uso.

- **FTP (File Transfer Protocol) : 21** - compartilhamento de arquivos - modelo cliente-servidor (vc baixa de um servidor)

- **SSH (Secure Shell) : 22** - Entra em sistemas em uma relação baseada em texto para gerenciamento

- **HyperText Transfer Protocol (HTTP):80**	 - WWW, navegadores web, mostra texto, imagens e videos.

- **HyperText Transfer Protocol Secure (HTTPS):443** - mesma coisa do de cima, mas mais seguro usando encriptação	

- **Server Message Block (SMB):445** - 
igual ao FTP, mas não é client-server, então vc pode compartilhar com a impressora, por ex.
- **Remote Desktop Protocol (RDP):3389** - tipo o SSH, mas com uma interface visual, igual usar aqueles app de acesso remoto.