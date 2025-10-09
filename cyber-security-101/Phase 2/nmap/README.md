# NMAP - Básico

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

Nmap é um scanner de rede de código aberto

*DICA: SEMPRE USAR O NMAP COMO SUDO*

---

Temos várias maneiras de específicar nossos alvos

1. FAIXA DE IP: podemos usar um "entre" usando o caracter "-": Vamos supor que quero escanear todos os IPs de 192.168.0.1 a 192.68.0.10 - usamos **192.168.0.1-10**

2. SUB-REDE IP: Podemos escanear toda uma sub-rede usando 192.168.0.1/24 - assim, vai equivaler como 192.168.0.0-255

3. HOSTNAME: especificar um destino por hostname, por exemplo: example.thm.

---

Para verificar em uma rede os hosts online, tem a opção -sn, que envia um ping scan.

---

Escaneando uma rede local em busca de hosts ativos:

`nmap -sn 192.168.66.0/24`

È legal saber do resultado disso por que nos retorna o endereço MAC dos dispositivos, ao qual podemos verificar os fornecedores da placa de rede e identificar o tipo de dispositivo de destino.

Quando fazemos essa analise, o NMAP envia ARP REQUEST, quando um dispositivo responde, o nmap rotula com "Host está ativo"

---

E para descobrir hosts externos, como o NMAP faz? Visando que como ele não faz parte da rede local do alvo, ele não pode enviar pacotes ARP?

Envia pacotes ICMP, icmp timestapm e tcp (com tags SYN e ACK) respectivamente.

---

`nmap -sL 192.168.0.1/24` lista todos os hosts a serem verificados SEM digitaza-los de verdade, ajuda a confirmar os destinos antes de executar a verificação real.

--- 

`-sn` atua mais quieto dentro da rede, sem fazer muito barulho.

---


## PORT SCANNING

TCP tem 65535 portas como padrão

---

-sT tenta realizar o aperto de três vias com CADA uma das portas daquele host, se uma der certo, ele fecha a conexão.

---

SYN SCAN (Stealth)

Realiza uma varredura mais quita, enviando apena so pacote SYN e nunca completando o aperto de três mãos.

A vantagem é que conduz a menos logs e é relativamente mais furtivo.

--- 

Para procurar por serviços UDP, podemos usar -sU

---

NMAP verifica as 1.000 portas por padrão, mas temos como limitar tal número.

`-F` é o modo rápido, verifica as top 100 portas mais comuns

`-[range]` - verifica um intervalo de portas, por exemplo `-p10-1024` enquanto `-p-25` faz a varredura das potas entre 1 e 25.

Já o `-p-` verifica todas as 65 mil portas disponíveis.

---

## Detecção de Versão

Podemos usar `-O` para que o NMAP tente identificar a versão da OS, mas isso não é preciso.

`-sV` ativa a detecção de versão - MUUITO bom pra identificar informações sobre o alvo.

Podemos usar juntos `-O -sV`, mas da pra diminuir e usar `-A` que executa a versão do OS, varredura de versão, tracerouter, etc.

---

Alguns hosts podem falar q n estão disponíveis quando enviamos o primeiro pacote de descoberta, então pra pular isso, podemos usar `-Pn` que trata todos os hosts como ativo.

---

## Velocidade

Podemos configurar a velocidade da varrerura com 5 níveis, sendo eles:

- T0 (paranóico) 
- T1 (sorrateira)
- T2 (educado)
- T3 (normal)
- T4 (agressivo)

## Saída

Para verbose, usamos 

-v, -vv, -vvv

Para depuração TOTAL, podemos usar -d passando um número que vai até no máximo -d9

Para salvar o resultado da varredura, podemos usar alguns jeitos:


* -oN <filename> - Saída Normal
* -oX <filename> - XML saída
* -oG <filename> - grep- saída capaz (útil para grep e awk)
* -oA <basename> - Saída em todos os principais formatos


