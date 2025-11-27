# Burp Suite - Básico

## Pra que serve?

O Burp Suite consegue interceptar o tráfego de uma requisição, possibilitando mudarmos a maneira a qual ela é enviada.

## Features que ele nos fornece

- Proxy : O Burp Proxy é o aspecto mais conhecido do Burp Suite . Ele permite a interceptação e modificação de solicitações e respostas ao interagir com aplicativos da web.

- Repetidor : Outro recurso bem conhecido. O repetidor permite para capturar, modificar e reenviar a mesma solicitação várias vezes. Esta funcionalidade é particularmente útil ao criar cargas úteis por meio de tentativa e erro (por exemplo, em SQLi - Structured Query Language Injection) ou testar a funcionalidade de um endpoint para vulnerabilidades.

- Intruso : Apesar das limitações de taxa no Burp Suite Comunidade, Intruder permite para pulverizar endpoints com solicitações. É comumente utilizado para ataques de força bruta ou endpoints de fuzzing.

- Decodificador : O decodificador oferece um serviço valioso para transformação de dados. Ele pode decodificar dados capturados informações ou codificar cargas úteis antes de enviá-las ao alvo. Enquanto Existem serviços alternativos para este propósito, aproveitando o Decoder dentro O Burp Suite pode ser altamente eficiente.

- Comparador : Como o nome sugere, o Comparador permite a comparação de dois dados no nível de palavra ou byte. não exclusivo do Burp Suite , a capacidade de enviar dados potencialmente grandes segmentos diretamente para uma ferramenta de comparação com um único atalho de teclado acelera significativamente o processo.

- Sequenciador : O sequenciador é normalmente empregado ao avaliar a aleatoriedade de tokens, como cookies de sessão valores ou outros dados supostamente gerados aleatoriamente. Se o algoritmo usado para gerar esses valores carece de aleatoriedade segura, pode expor caminhos para ataques devastadores.

---

## Proxy 

Permite-nos interceptar as solicitações e respostas, podemos editar e enviar direto, ou também podemos enviar para outras ferramentas, como o Intruder.

## Aba Target 

Podemos usar essa aba para ver um mapa do site completo, com estrutura de pastas disponíveis, etc.

Na sub-aba "Issue definitions" podemos ver uma lista bem grande de certas vulnerabilidades que o Burp nos da.

---

Essa aula foi bem básica, apresentou coisas relacionadas a configuração da ferramenta, etc - no fim realizei uma simulação de ataque XSS, burlamos a verificação no front-end e injetamos um código javascript.

