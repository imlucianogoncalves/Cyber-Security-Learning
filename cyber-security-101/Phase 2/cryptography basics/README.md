# Critografia - Básico

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

Objetivos, entender: 

- Termos-chave de criptografia
- Importância da criptografia
- Cifra De César
- Cifras simétricas padrão
- Cifras assimétricas comuns
- Matemática básica comumente usada em criptografia 

A criptografia é usada para proteger a confidencialidade, integridade e autenticidade.

---

Cenários que usamos criptografia hoje em dia:

- Quando fazemos login em determinado site, meu tráfego está criptografado para não ser interceptado.

- Quando se conectamos por SSH, o cliente e o servidor estabelecem um túnel criptografado para que ninguém possa espionar sua sessao.

- Serviços bancários online, verifica o certificado do servidor remoto pra garantir autenticidade.

- Quando baixamos um arquivo, pra verificar se ele foi baixado corretamente tem funções de hash.

---

Quando guardamos dados de cartões de crédito, devemos mante-los armazenados de forma criptografada e ao ser transmitido também, isso segundo o PCI DSS (Padrão de Segurança de Dados do Setor de Cartões de Pagamento)

---

Exemplo simples, temos um texto "plain text" que quremos enviar e criptografar, pra isso precisamos de uma chave, a função de criptografia retorna um texto cifrado, a função de criptografia faz parte da cifra, uma cifra é um algoritmo para converter um texto simples em um texto cifrado e vice-versa.

Para recuperar o texto simples, devemos passar o texto cifrado junto com a chave adequada através da função de descriptografia, que nos daria o texto simples original.

---

- Plaintext: mensagens ou dados originais e legíveis antes de serem criptografados, pode ser doc, imagem, mídia ou qualquer outro binário.

- Texto cifrado: É a versão embaralhada e ilegível da mensaem após a criptografia, idealmente não podemos obter nenhuma info sobre o texto simples original, exceto seu tamanho aproximadao.

- Cifra é um algoritmo ou método para converter texto simples em texto cifrado e vice-versa. Uma cifra geralmente é desenvolvida por um matemático.

- Chave é uma cadeia de bits que a cifra usa para criptografar ou descriptografar dados. Em geral, a cifra usada é de conhecimento público; no entanto, a chave deve permanecer secreta, a menos que seja a chave pública em criptografia assimétrica. Visitaremos a criptografia assimétrica em uma tarefa posterior.

- Criptografia é o processo de conversão de texto simples em texto cifrado usando uma cifra e uma chave. Ao contrário da chave, a escolha da cifra é divulgada.

- Descriptografia é o processo inverso de criptografia, convertendo o texto cifrado de volta em texto simples usando uma cifra e uma chave. Embora a cifra fosse de conhecimento público, recuperar o texto simples sem o conhecimento da chave deveria ser impossível (inviável). 

---

A criptografia existe desde o Egito Antigo (1900 a.C.), mas uma das mais simples e conhecidas é a Cifra de César, criada no século I a.C. Ela funciona deslocando cada letra do texto por um número fixo — por exemplo, com deslocamento de 3, “TRYHACKME” vira “WUBKDFNPH”.

Para descriptografar, basta deslocar as letras no sentido oposto. Porém, essa cifra é fácil de quebrar, pois há apenas 25 chaves possíveis, tornando-a vulnerável a ataques de força bruta.

Apesar de ser insegura hoje, a Cifra de César é um marco na história da criptografia, que também inclui métodos mais avançados como a Cifra de Vigenère, a Máquina Enigma e o One-Time Pad;

---

# Criptografia simétrica

Ela usa a msm chave pra criptografar e descriptografar o conteúdo, pode ser meio complicado compartilhar a chave, perde um pouco do fator segurança.

- DES foi adotado como padrão em 1977 e usa uma chave de 56 bits. Com o avanço do poder computacional, em 1999, a DES chave foi quebrada com sucesso em menos de 24 horas, motivando a mudança para 3DES.

- 3DES é DES aplicado três vezes; consequentemente, o tamanho da chave é de 168 bits, embora a segurança efetiva seja de 112 bits. 3DES foi mais um ad - solução hoc quando DES não era mais considerado seguro. 3DES foi preterido em 2019 e deve ser substituído por AES ; no entanto, ainda pode ser encontrado em alguns sistemas legados.

- AES foi adotado como padrão em 2001. Seu tamanho de chave pode ser de 128, 192 ou 256 bits.

---

# Criptografia assimétrica

Já a assimétrica, usa uma para criptografar e outra para descriptografar. - criptografa usando a chave pública; 

As duas chaves são chamadas de chave pública e chave privada.

