# Conceitos de Networking

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

## Modelo OSI

**OSI (Open Systems Interconnection)** é um modelo conceitual - diz como as comunicações devem ocorrer em uma rede de computadores. Define a estrutura para tal comunicação - é um método teórico mas vital.

Ele é composto por 7 camadas: 

- Camada Física
- Camada De Enlace De Dados
- Camada De Rede
- Camada De Transporte
- Camada De Sessão
- Camada De Apresentação
- Camada De Aplicação

## Camada 1 - Camada Física

Trata a conexão física entre os dispositivos - inclui o meio, tal como fio, e a definiçao dos dígitos binários de 0 a 1.

Pode ser através de um sinal elétrico, óptico ou sem fio - consequentemente, precisamos de cabos de dados ou antenas, dependendo do meio físico.

Além do cabo Ethernet e do fibra-optica, exemplos do meio da camada física incluem **bandas de rádio WiFi, a banda de 2,4 GHz, A banda de 5 GHz e a banda de 6 GHz**

## Camada 2 - Camada de Data-Link (Enlace de Dados)

A camada de enlace de dados (2) define como os dispositivos de uma rede se comunicam, as regras para enviar e receber dados entre um segmento de rede.

Um segmento de rede é como um setor de uma empresa, onde temos um switch cuidando de vários computadores do setor comercial, por exemplo.

Protocolos da camada 2 incluem Ethernet (802.3) e WiFi (802.11)

No endereço MAC temos uma identificação, onde

a4:c3:f0:85:ac:2d

Os três primeiros bytes são a identificação de quem construiu essa Network Interface e o restante, o endereço daquela Network Interface.

No Wireshark, podemos ver no campo Source depois endereços MAC, o que vai receber primeiro e depois o azul - em formato de bytes.

## Camada 3 - Camada de Rede

Enquanto na camada de Data-Link (Enlace de Dados) cuidamos do envio de dados entre dois nós no mesmo segmento de rede (rede local), a camada de rede (camada 3), cuida do envio entre diferentes redes - ela lida com o endereçamento lógico e roteamento - ou seja, encontra o melhor caminho para transferir os pacote entre as diversas redes.

Exemplos de camada de rede incluem IPo (internet protocol), ICMP (internet control message protocol), VIRTUAL PRIVATE network (VPN) e IPSec e SSL/TLS VPN.

## Camada 4 - Camada de Transporte

Ela faz a divisão das mensagens em partes menores (segmentos) e depois reagrupa tudo no destino.
Também pode controlar o fluxo (para não sobrecarregar o receptor) e detectar erros na transmissão.

👉 Existem dois principais protocolos:

TCP (Transmission Control Protocol):

Confiável (garante que tudo chegue e na ordem certa).

Usa confirmação de recebimento (ACK).

Exemplo: navegação na web, e-mails, downloads.

UDP (User Datagram Protocol):

Mais rápido, mas não garante entrega.

Não faz controle de erro ou reenvio.

Exemplo: jogos online, streaming, chamadas de voz.

## Camada 5 - Camada de Sessão

Ela garante que os dados sejam enviados na ordem certa e que a conexão possa se recuperar se algo falhar.

Exemplos:

- NFS (Network File System) – permite acessar arquivos pela rede.
- RPC (Remote Procedure Call) – permite que um programa execute funções em outro computador.

## Camada 6 – Apresentação:
Essa camada prepara os dados para que a aplicação possa entendê-los.
Ela cuida de codificação, compactação e criptografia.
Exemplo: converter texto para ASCII ou Unicode, ou transformar uma imagem em JPEG, GIF ou PNG antes de enviá-la.
Quando enviamos um anexo por e-mail, o MIME é usado para codificar o arquivo em texto (ASCII) e permitir o envio.

## Camada 7 – Aplicação:
É a camada que interage diretamente com o usuário.
Ela fornece os serviços de rede usados pelos aplicativos, como navegar na web ou enviar e-mails.
Exemplos de protocolos: HTTP, FTP, DNS, SMTP, POP3, e IMAP.

# Sumário

| Número da Camada | Nome da Camada            | Função Principal                                       | Exemplos de Protocolos e Padrões                     |
|------------------:|---------------------------|--------------------------------------------------------|------------------------------------------------------|
| 7                | Camada de Aplicação       | Prestação de serviços e interfaces para aplicações     | HTTP, FTP, DNS, POP3, SMTP, IMAP                    |
| 6                | Camada de Apresentação    | Codificação, criptografia e compactação de dados       | Unicode, Mímica, JPEG, PNG, MPEG                    |
| 5                | Camada de Sessão          | Estabelecimento, manutenção e sincronização de sessões | NFS, RPC                                            |
| 4                | Camada de Transporte      | Comunicação de ponta a ponta e segmentação de dados    | UDP, TCP                                            |
| 3                | Camada de Rede            | Endereçamento lógico e roteamento entre redes          | IP, ICMP, IPSec                                     |
| 2                | Camada de Enlace de Dados | Transferência confiável de dados entre nós adjacentes  | Ethernet (802.3), WiFi (802.11)                    |
| 1                | Camada Física             | Meios físicos de transmissão de dados                  | Sinais elétricos, ópticos e sem fio                 |


# Modelo TCP/IP

Esse é um modelo real, implementado e usado no dia a dia.


- Camada De Aplicação : As camadas de aplicação, Apresentação e sessão do modelo OSI, ou seja, as camadas 5, 6 e 7, são agrupadas na camada de aplicação no TCP / Modelo IP.
- Camada De Transporte : Esta é a camada 4.
- Camada Internet : Esta é a camada 3. A camada de rede do modelo OSI é chamada de camada de Internet no TCP / Modelo IP.
- Camada De Ligação : Esta é a camada 2.

## Endereços IP

Endereços privados:

- 10.0.0.0 - 10.255.255.255 ( 10/8)
- 172.16.0.0 - 172.31.255.255 ( 172.16/12)
- 192.168.0.0 - 192.168.255.255 ( 192.168/16)


10, 172, 192 - privados

## UDP

**AGE NA CAMADA 4**

Sem confirmação de recebimento, precisa de IP + Porta para determinar processo de envio e recebimento.

Mesmo sem confirmação de recebimento, é uma opção mais barata e mais rápida.

È como enviar uma carta para uma pessoa.

## TCP

**AGE NA CAMADA 4**

O TCP é orientado a conexão - ele usa vários mecanismos para garantir a entrega confiável dos dados enviados pelos processos nos hosts em redes.

Sendo um rapaz orientado a conexão, precisa do estabelecimento de uma conexão TCP antes de qualquer dado ser enviado.

Cada octeto de dados possui um número de sequências, isso garante que os dados estão chegando em ordem. Ficaria estranho se eu recebesse o pacote com o número 1 e depois o 300, não? O correto é o número sequencial certinho.

A conexão TCP funciona no fluxo do three ways hadnshake. São utilizados alguns sinalizadores, sendo eles:

SYN (Synchronise)

ACK (Acknowledgment)

Os pacotes são enviados da seguinte forma:

- Pacote SYN -> Inicia a conexão enviando um pacote SYN: esse pacote tem o número sequencial escolhido aleatóriamente pelo cliente

- Pacote SYN-ACK -> o servidor responde com um pacote SYN-ACK: que adicione o número de sequencia inicial escolhido aleatóriamente pelo servidor

- Pacote ACK -> o handshake de três vias é concluído quando o cliente envia um pacote ACK para confirmar a recepção do pacote SYN-ACK


# Encapsulamento


O encapsulamento é um conceito essencial, pois permite que cada camada se concentre em sua função pretendida. Na imagem abaixo, temos os quatro passos a seguir:

    Dados de Aplicação : Tudo começa quando o usuário insere os dados que deseja enviar no aplicativo. Por exemplo, você escreve um e-mail ou uma mensagem instantânea e aperta o botão enviar. O aplicativo Formata esses dados e passa a enviá-los de acordo com o protocolo de aplicação utilizado, utilizando a camada abaixo dele, a camada de transporte.
    Segmento ou datagrama do protocolo de transporte : A camada de transporte, como TCP ou UDP , Adiciona as informações de cabeçalho adequadas e cria o TCP segmento (ou UDP datagrama ). Esse segmento é enviado para a camada abaixo dele, a camada de rede.
    Pacote de rede : A camada de rede, ou seja, a camada de Internet, adiciona um cabeçalho IP ao recebido TCP segmento ou UDP datagrama. Então, este IP pacote é enviado para a camada abaixo dela, a camada de enlace de dados.
    Quadro de enlace de dados : A Ethernet ou WiFi recebe o pacote IP e adiciona o cabeçalho e trailer adequados, criando um quadro .

Começamos com os dados do aplicativo. Na camada de transporte, adicionamos um TCP ou UDP cabeçalho para criar um TCP segmento ou UDP datagrama . Novamente, na camada de rede, adicionamos o cabeçalho IP adequado para obter um Pacote IP que pode ser roteado pela Internet. Por fim, adicionamos o cabeçalho e o trailer apropriados para obter um quadro WiFi ou Ethernet na camada de link. 

# Telnet (!IMPORTANTE!)

Telnet (teletype network) - é um protocolo de rede para conemxão de terminal remota. Permite que executemos comandos de texto remotamente.

Podemos nos conectar a qualquer servidor escutando uma porta TCP.

- servidor echo:7 - ecoa tudo o que vc envia
- servidor diurno:13 - manda o dia e hora atuais
- web http:80 - serve páginas web


TELNET no Web HTTP ->

conectamos e enviamos a requisição

GET / HTTP/1.1
Host: nomedohost.com.br
Enter

e ele nos retorna a requisição;