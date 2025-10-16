# Powershell

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

Os comandos do Powershell são chamados de cmdlets - e são orientados a objetos.

Ele funciona numa vibe de verbo + noun - para consolidar, vamos usar esses exemplos:

**[Get-Content]** - recupera o conteudo de um arquivo e o exibe no console. (pegar - conteudo)

**[Set-Location]** - muda o diretório, como o cd.

**[Get-Command]** - mostra todos os comandos disponíveis para usar naquele ambiente.

Para filtrar a lista do Get-Command baseando-se em filtros de tipo, podemos usasr **[Get-Command -CommandType "Function"]**

**[Get-Help + comando"]** mostra a ajuda sober aquele comando, é como um man do Linux.

**[Get-Alias"]** mostra todos os aliases que temos disponíveis.

**[Find-Module -Name "PowerShell*" ]** procura em repositorios comando extras pra adicionar baseados em powershell.

**[Install-Module -Name "PowerShellGet"]** depois de encontrado, ele instala com o nome do repositório.


## Trabalhando com arquivos e andando pelos diretórios.

**[Get-ChildItem]** - funciona como um ls - exibe as pastas e / ou arquivos filhos do diretório que vc está.

Podemos passar o atributo **-Path + ".\Diretório** para ver os filhos de uma pasta em específico.

---

**[Set-Location -Path ".\Documents"]** este grande rapaz funciona como o CD do Linux - passamos o set-locaiton, citando q vamos mudar de diretório. Passamos o parametro -Path + Caminho pra específicar pra onde queremos ir.

---

Um pouco complicado para criar um novo diretório ou arquivo - fazemos da seguinte maneira

**[New-Item ".\nome-ou-caminho\arquivo-ou-pasta" --ItemType "Directory"]** - assim criamos dentro da pasta que estamos, uma pasta nome-ou-caminho e dentro dela uma outra pasta chamada arquivo-ou-pasta - o tipo passado foi directory - o que os torna pastas.

Para arquivo, o **[-ItemType "File"]**

---

Para remover diretórios ou arquivos, usamos

**[Remove-Item -Path ".\Caminho"]** 

---

Para copiar itens, podemos usar 

**[Copy-Item -Path ".\pasta-do-arquivo\arquivo.txt" -Destination ".\pasta-destino\nome-do-arquivo.txt"]**

---

Para exibir o conteúdo do item 

**[Get-Content -Path ".\pasta\arquivo.txt"]**

ou 

**[Get-Content arquivo.txt]**

## Canalização, filtragem e classificação de dados 

A canalização funciona exatamente igual no Linux onde usamos "|" para executar outro comando, como ls -la | grep "desktop"

Exemplo de uso no PowerShell:

**[Get-ChildItem | Sort-Object Length]** - assim, exibimos os itens da pasta e organizados por tamanho

Para filtrar por outros tipos de dados, como extensão de arquivo, podemos usar outro comando, que é:

**[Get-ChildItem | Where-Object -Property "Extension" -eq ".txt" ]** o que acontece aqui? eu passo o pipe com um where-object (onde o objeto, tiver a propriedade extension igual a .txt)


-eq significa equal to - igual a, temos outros também:


    -ne: " não igual ". Esse operador pode ser usado para excluir objetos dos resultados com base em critérios especificados.
    -gt: " maior que ". Este operador filtrará apenas objetos que excedam um valor especificado. É importante notar que esta é uma comparação estrita, o que significa que os objetos que são iguais ao valor especificado serão excluídos dos resultados.
    -ge: " maior ou igual a ". Esta é a versão não estrita do operador anterior. Uma combinação de -gt e -eq.
    -lt: " menor que ". Como sua contraparte, "maior que", este é um operador estrito. Incluirá apenas objetos que estão estritamente abaixo de um determinado valor.
    -le: " menor ou igual a ". Assim como sua contraparte -ge, esta é a versão não estrita do operador anterior. Uma combinação de -lt e -eq.


um outro legal, é o -like, onde passamos tipo um regex, onde tiver aquela palavra, mesmo que não seja ela igual 100%.

**[| Select-Object Name,Length ]** seleciona as colunas que vc quer ver
 

 ## Informações do sistema

**[Get-ComputerInfo]** é igual ao systeminfo - mostra as informações gerais do sistema.

 **[Get-LocalUser]** mostra os usuarios naquela máquina local

  **[Get-NetIPConfiguration]** é igual ao ipconfig - mostra as informações gerais da rede.

  **[Get-NetIPAddress]** mostra coisas sobre os ENDEREÇOS na rede


## Processos e analise do sistema em tempo real

**[Get-Process]** mostra todos os processos em execução.

**[Get-Service]** mostra todos os serviços e seu status, parado ou rodando - usado bastante pra solução de problemas MAS também na parte forense visando serviços anômalos nosistema.

**[Get-NetTCPConnection]** - bom pra forense tbm, mostra endpoints locais e remotos - bom pra ver backdors ocultos ou conexões com servidores externos.

**[Get-FileHash -Path .\ship-flag.txt]** gera hash do artigo para verificar adulteração, integridade de arquivo.  