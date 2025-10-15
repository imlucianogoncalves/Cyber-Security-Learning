# Web Application - Básico

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

Objetivos De Aprendizagem

Ao completar esta sala, você irá:

- Entenda o que é uma aplicação web e como ela é executada em um navegador web.
- Divida os componentes de uma URL e veja como ela ajuda a acessar os recursos da web.
- Saiba como HTTP solicitações e Respostas funcionam.
- Familiarize-se com os diferentes tipos de HTTP métodos de solicitação.
- Entenda o que é diferente HTTP códigos de resposta significam.
- Confira como HTTP os cabeçalhos funcionam e por que eles são importantes para a segurança.

---

## WAF

Web Application Firewall -> Ajuda a filtrar solicitações perigosas e forneçe um elemento de proteção.

## Mensagens HTTP

![Imagem HTTP](images/overview.png)

As mensagens HTTP, existem dois tipos, os HTTP Requests, que o usuario envia para o servidor

e o HTTP Response, que o servidor envia para o usuario.

---

## HTTP Request

![Imagem HTTP](images/http-request.png)

O **HTTP Request** é o que um usuairo envia para o servidor web quando quer interagir com determinado conteúdo ou arquivo. Então o usuario, pede "permissão" para ver a página /sobre, por exemplo, e o que servidor responde com a permissão e com o conteúdo em texto propriamente dito.


---

## 🔹 HTTP Métodos

### **GET**
- Busca dados do servidor **sem alterar** nada.  
- ⚠️ Evite expor dados sensíveis (tokens, senhas).  
- **Risco:** exposição de informações em texto claro.

### **POST**
- Envia dados para o servidor (criar/atualizar).  
- ⚠️ Sempre **valide e sanitize** entradas.  
- **Risco:** ataques de **SQL Injection** e **XSS**.

### **PUT**
- Substitui ou atualiza um recurso existente.  
- ⚠️ Exija **autorização** antes de aceitar.  
- **Risco:** modificações indevidas.

### **DELETE**
- Remove um recurso do servidor.  
- ⚠️ Apenas usuários autorizados devem poder excluir.  
- **Risco:** perda de dados.

### **PATCH**
- Atualiza **parte** de um recurso.  
- ⚠️ Valide os dados enviados.  
- **Risco:** inconsistências no sistema.

### **HEAD**
- Igual ao GET, mas retorna **somente cabeçalhos**.  
- **Uso:** verificar metadados sem baixar conteúdo.

### **OPTIONS**
- Mostra **métodos permitidos** em um recurso.  
- **Uso:** ajuda o cliente a entender permissões.

### **TRACE**
- Mostra métodos permitidos (para depuração).  
- ⚠️ Normalmente desativado por **motivos de segurança**.

### **CONNECT**
- Cria uma **conexão segura** (ex: HTTPS).  
- **Importante:** base da comunicação criptografada.

---

## 🌐 URL Path

Define **onde** o recurso solicitado está localizado.

Exemplo:

➡️ Caminho: `/api/users/123`

**Boas práticas:**
- ✅ Valide o caminho para evitar acesso não autorizado  
- ✅ Higienize para prevenir injeções  
- ✅ Proteja dados sensíveis com avaliações de privacidade  

---

## ⚙️ HTTP Versão

Mostra o **protocolo usado** na comunicação entre cliente e servidor.

| Versão | Ano | Características principais |
|--------|------|-----------------------------|
| **HTTP/0.9** | 1991 | Apenas solicitações GET |
| **HTTP/1.0** | 1996 | Suporte a cabeçalhos e cache |
| **HTTP/1.1** | 1997 | Conexões persistentes, transferência fragmentada |
| **HTTP/2** | 2015 | Multiplexação, compactação e priorização |
| **HTTP/3** | 2022 | Baseado em QUIC, mais rápido e seguro |

🟢 **HTTP/2 e HTTP/3** → mais rápidos e seguros  
🔵 **HTTP/1.1** → ainda o mais utilizado por compatibilidade

---

✅ **Resumo:**  
A linha de solicitação define **o que**, **onde** e **como** o cliente quer interagir com o servidor.  
Segurança depende de **validação, autorização e atualização de protocolo**.


---

## Cabeçalhos da Request

| Cabeçalho da Solicitação | Exemplo                                                                 | Descrição                                                                                             |
|--------------------------|-------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| Host                     | `Host: tryhackme.com`                                                   | Especifica o nome do servidor web para o qual a solicitação se destina.                               |
| User-Agent               | `User-Agent: Mozilla/5.0`                                               | Informa ao servidor o agente cliente (navegador, biblioteca HTTP, etc.) que originou a requisição.    |
| Referer                  | `Referer: https://www.google.com/`                                      | Indica a URL de onde a solicitação foi iniciada (página anterior).                                    |
| Cookie                   | `Cookie: user_type=student; room=introtowebapplication; room_status=in_progress` | Armazena pares nome=valor enviados pelo navegador com dados de sessão/preferências.                   |
| Content-Type             | `Content-Type: application/json`                                        | Descreve o tipo/formato dos dados no corpo da requisição (ex.: `application/json`, `text/html`).      |


---

## Corpo da Solicitação — resumo MUITO SIMPLES

Em requisições que enviam dados (ex: POST, PUT), os dados ficam no corpo da solicitação.

Formatos comuns:

URL encoded — pares key=value&....

`name=Aleksandra&age=27`

form-data (multipart) — usado para uploads (arquivos + campos).

```
--boundary
Content-Disposition: form-data; name="file"; filename="img.jpg"
[dados binários]
--boundary--
```

JSON — objeto { "name":"Aleksandra", "age":27 }.
`{"name":"Aleksandra","age":27}`

XML — dados em tags <user>...</user>.
`<user><name>Aleksandra</name><age>27</age></user>`

---

## HTTP Responses

Cabeçalhos de segurança para as aplicações.

### Content-Security-Policy ( CSP ) 

A header CSP é uma camada de segurança que ajuda a evitar ataques de Cross-Site Scripting por meio de configurar páginas que serão tratadas como confiáveis.

Tesmos várias opções de uso, sendo elas:

 `Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.tryhackme.com; style-src 'self'`

Vemos o uso de:

- default-src
    - que especifica a Política padrão de self, que significa apenas o site atual.

- script-src
    - que especifica a Política de onde os scripts podem ser carregados, que é self junto com os scripts hospedados em https://cdn.tryhackme.com

- style-src
    - que especifica a política para onde as folhas de estilo CSS de estilo podem ser carregadas do site atual (self) 

---