# OSINT

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

## Pesquisas avançadas no Google:

- **"frase exata"** as aspas duplas indicam que vc está procurando páginas com a palavra ou frase EXATA.

- **site:** permite específicar o domínio ao qual você está buscando auqela informação, pode ser usado como: **site:tryhackme.com success stories**

- **-** o sinal de menos, exclui determinada palavra-chave da pesquisa, como **pyramids -tourism**

- **filetype:** específica o tipo de arquivo que você pesquisa por. Podemos pesquisar por PDF, DOC, XLS, PPT, etc. **filetype:ppt cyber security**

## Shodan

É um mecanismo de busca de dispositivos conectados à internet.

Podemos pesquisar, por exemplo, quais servidores ainda usam o Apache em sua versão 2.4.1, simplesmente digitando **apache 2.4.1**, ele nos dara uma lista com país, IP do servidor, etc.

## Censys 

O Censys, diferente do Shodan, concentra-se conectados a internet, sites, certificados e outros ativos da internet.

Ele é bom para:

- Enumerar domínios em uso
- Auditar portas e serviços abertos
- Descobrir ativos invasoers

## VirusTotal

Verifica virus a partir de URL e/ou arquivo - pode não ser preciso.

## Have I been Pwned?

Ele verifica, a partir do seu e-mail se você teve informações vazadas em vazamentos de hackers - como suas senhas, credenciais, etc.

# CVE

CVEs (Common Vulnerabilities and Exposures) é uma espécie de dicionário das vulnerabilidades. A cada vulnerabilidade é atribuido um CVE ID com um formato padronizado como **CVE-2024-29988**

## EXPLOIT DATABASE

O Exploit Database lista códigos de exploração de vários autores; alguns desses códigos de exploração são testados e marcados como verificados. 