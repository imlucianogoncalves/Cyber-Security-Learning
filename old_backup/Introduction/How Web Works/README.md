# Como a Web Funciona

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

## DNS (Domain Name System)

DNS traduz o endereço de IP em um texto legível para melhor compreensão.

### A RECORD

É os registros que resolvem para endereços IPv4 - por ex: 104.26.10.229 

### AAAA

Resolvem para endereços IPv6 - por ex: 2606:4700:20:: 681a:be5 

### CNAME

Retorna outro domínio, por ex:

mail.empresa.com.br -> mail.umbler.com.br

### REGISTROS MX

Endereços dos servidores de e-mail. Tbm vem com um número para prioridade - se um dos servidores MX cair, o outro entrará.

### REGISTRO TXT

Dados baseados em texto armazenados, como listar servidores que podem escrever e-mails em nome de X domínio.

### Como Funciona o DNS

1. **Verificação local:**  
   Quando você acessa um domínio, seu computador primeiro verifica seu **cache local**. Se o endereço já foi pesquisado recentemente, ele é usado imediatamente.

2. **Servidor Recursivo:**  
   Caso não esteja no cache local, a solicitação vai para um **servidor DNS recursivo** (geralmente do seu ISP, mas pode ser personalizado).  
   - Se o servidor recursivo tiver o domínio em cache, ele retorna a resposta.  
   - Caso contrário, ele inicia a busca pelos **servidores raiz** da Internet.

3. **Servidores Raiz:**  
   Os servidores raiz direcionam a solicitação para o **servidor TLD** correto, baseado no domínio de nível superior (ex.: `.com`, `.org`).

4. **Servidor TLD:**  
   O servidor TLD aponta para o **servidor autoritativo** responsável pelo domínio solicitado.

5. **Servidor Autoritativo:**  
   Este servidor contém os **registros DNS** do domínio (ex.: `A`, `CNAME`, `MX`) e responde ao servidor recursivo.

6. **Resposta e Cache:**  
   - O servidor recursivo guarda a resposta em seu cache para futuras consultas.  
   - O computador original recebe a resposta e também a armazena temporariamente.  
   - Cada registro DNS tem um **TTL (Time to Live)** que define quanto tempo ele deve ser mantido em cache antes de ser consultado novamente.

**Resumo:** O DNS funciona como uma cadeia de consultas: cache local → servidor recursivo → raiz → TLD → autoritativo → resposta, com caching para acelerar futuras solicitações.


## HTTP e HTTPS

HTTP (HyperText Transfer Protocol) é usado sempre que você visualiza um site - é um conjunto de regras utilizadas para comunicação com servidores web, sejam elas HTML, imagens, videos, etc.

HTTPS (HyperText Transfer Protocol Secure) é a versão segura do HTTP - os dados são criptografados para não serem interceptados e também se certificar que vc está falando com o servidor certo.

URL (Uniform Resource Locator)

- **Esquema (Protocolo):** Define como acessar o recurso, por exemplo: `HTTP`, `HTTPS`, `FTP`.

- **Usuário:** Credenciais de login se necessário (nome de usuário e senha).

- **Host:** Nome de domínio ou endereço IP do servidor.

- **Porto:** Porta de conexão. Exemplo: `80` para HTTP, `443` para HTTPS. Pode ser qualquer número de `1` a `65535`.

- **Caminho:** Local ou arquivo específico que você quer acessar.

- **Query String:** Informações adicionais enviadas ao caminho.  
Exemplo: `/blog?id=1` indica que deseja o artigo com `id=1`.

- **Fragmento:** Referência a uma seção específica da página.  
Exemplo: `#secao2` aponta diretamente para uma parte do conteúdo.

### Métodos HTTP

#### GET Request

Obter informações de um servidor web

#### POST Request

Enviar dados ao servidor e potencialmente criar novos registros.

#### PUT Request

Enviar dados para atualizar informações de um registro

#### DELETE Request

Excluir informações / registros de um servidor web

### Cabeçalhos

#### Cabeçalhos De Solicitação Comuns 

São cabaçelhos enviados do cliente para o servidor.

- **Host:** O endereço do HOST ao qual você quer realizar a requisição.
- **User-Agent:** Informações sobre seu navegador, ajuda para ajustes de compatibilidade.
- **Content-Length:** Quantos dados esperar daquela solicitação - para garantir q nao falta nada.
- **Accept-Enconding:** quais tipos de métodos de compactação o servidor suporta
- **Cookie:** Dados enviados ao servidor para ajudar lembrar suas infos.

#### Cabeçalhos De Resposta Comuns

- **Set-Cookie:** dados enviados pelo servidor que o navegador armazena e retorna em cada requisição.  
- **Cache-Control:** define por quanto tempo a resposta pode ser armazenada no cache.  
- **Content-Type:** indica o tipo de dado retornado (HTML, CSS, JS, imagem, PDF, vídeo, etc.).  
- **Content-Encoding:** mostra como os dados foram compactados para envio.
