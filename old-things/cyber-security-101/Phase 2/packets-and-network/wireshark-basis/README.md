# Wireshark - Básico

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe


O Wireshark é uma ferramenta de análise de pacotes - nela conseguimos analisar todas as partes de um protocolo, cada etapa, camada e dados, criptografados ou não.

O Wireshark é uma das mais fodas ferramentas de análise de tráfego - vários propositos para seu uso:

- Detecção e solução de problemas de rede - como pontos de falha de carga de rede e congestionamento.
- Detecção de anomalias de segurança, hosts invasores, uso anormal de portas e tráfego suspeito.
- Investigar e aprender detalhes do protocolo, como códigos de resposta e dados de carga útil.

O Wireshark colore os pacotes em ordem de diferentes condições e protocolo para detectar anomalias e protocolos em capturas.

---

Dentro do Wireshark, podemos fazer diversas coisas - o que foi passado na primeira aula dessa base, foi que podemos ver várias informações na plataforma, como nome do arquivo de análise, como mesclar arquivos *.pcapng*, como verificar integridade, ver as anotações de tal arquivo, total de pacotes capturados, etc.

--- 

## Dissecção de pacotes

Os pacotes consistem de 5 a 7 camadas baseadas no modelo OSI.

Quando clicamos em um detalhe de um pacote, ele destaca a parte correspondente no painel de bytes do pacote.

Olhando detalhadamente para o painel de detalhes, temos:

- Quadro, pacote
- Fonte [MAC]
- Fonte [IP]
- Protocolo
- Erros de Protocolo
- Protocolo de APlicativo 
- Dados de aplicativo.

---

O quadro / pacote (Camada 1) 0 - Isso mostra qual pacote / quadro vc tá olhando com detalhes específicos a camada física do modelo OSI.

Fonte [MAC] (Camada 2) - isso mostra os endereços MAC de origem de destino; da camada de elnace de dados do moselo OSI.

Fonte [IP] (Camada 3) - mostra os endereços IPv4 de origem e destino; da camada de rede do modelo OSI.

Protocolo (Camada 4) - mostra os detalhes do protocolo usado (UDP / TCP) e portas de origem e destino; da camada de transporte do modelo OSI.

Erros de Protocolo - continuação da 4a camada mostra segmentos específicos de TCP - que precisava ser remontado (só é possível em TCP, pois em UDP não temos tal verificação)

Protocolos de Aplicação - (camada 5) - mostra detalhes específicos do protocolo usado, como HTTP, FTP e SMB - da camada de aplicação do modelo OSI.

Dados da aplicação - extensão da 5a camada pode mostrar os dados específicos da aplicação.

**TTL - FICA DENTRO DO PACOTE IP**

**ETAG - FICA DENTRO DO HTTP**

## Navegação de pacotes

Cada pacote/ quadro tem um ID.

Para ir para determinado, selecinar no Menu **GO** > **To packet**

---

Para achar um pacote pelo seu conteúdo - podemos usar outra fature -> **Edit -> Find Packet**

Os filtros mais usados são strng e regex. Não diferencia minúsculas de maíusculas - mas pode habilitar isso.

Da pra selecionar ONDE buscar, como packet lis (coluna debaixo esquerdo) - packet details (dentro dos itens) e em packet bytes (os hexadecimais da direita)

--- 

Da pra marcar os pacotes de interesse pra que eles fiquem destacados, via menu - > Edit -> Mark Packet ou com o botão direto e Mark Packet.

---

Da pra adicionar comentários em pacotes, pra realizar anotações, citar pontes importantes / suspeitos para outros analistas, etc -> ao contrário da marcação, esses ppodem permanecer dentro do arquivo até q alguém remova.

---

Da pra exportar os pacotes em **File > Export Specified Packets**

---

Também da pra exportar objetos, como DICOM, HTTP, FMI, SMB e TFTP

---

Da pra mudar o formato da data de exibição em View -> Time Display Format

---

EM Analysis -> Expert Information -> temos algumas coisas detalhadas sobre os pacotes no geral, como flags.

Temos em azul, informações sobre o fluxo de trabalho uzual

Ciano, eventos notáveis como códigos de erro de apps.

Amarelo avisos como códigos de erro incomuns ou declaração de problemas

Vermelhos - pacotes malformados - erro.

## Filtragem de pacotes

Para filtrar uma rota específica, do IPv4 X para IPv4 Y - podemos clicar  com o botão direito no pacote -> usar como filtro e aplicar.

Também da pra analisar todo o tipo de interação entre dois endereços IP. Com o botão direito -> Conversation Filter -> e o método -> TCP

Da pra colorir toda uma inteção entre hosts também, em com botão direito e Colorize Conversation.

!!!! MUITO IMPORTANTE !!!!

Para ver o conteúdo dos pacotes, como HTTP - podemos ver a Stream, assim podemos ver a requisição e a repsosta em uma nova tab.