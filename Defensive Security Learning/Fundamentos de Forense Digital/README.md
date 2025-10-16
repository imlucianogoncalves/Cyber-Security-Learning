# Fundamentos de Forense Digital

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno SOC do TryHackMe

A parte de forense digital utiliza ferramentas e técnicas para investigar dispositivos digitais minuciosamente após qualquer crime para encontrar e analisar provas para ações legais necessárias.

Objetivos De Aprendizagem

- Fases da Perícia digital
- Tipos de forense digital
- Procedimento de aquisição de provas
- Windows forense
- Resolvendo um caso forense

---

As fases de toda investigação forense digital, são:

- Collection (coleta)
- Examination (exame)
- Analysis (análise)
- Reporting (relatório)

## 1. Coleta 

Aqui, coletamos todo o tipo de informação de todas as fontes disponíveis, como laptops, câmeras, usbs, etc. Isso é necessário para garantir que os dados originais não sejam adulterados posteriormente.

## 2. Exame

Nessa parte, é importante filtrarmos os dados coletados, pois na maioria das vezes tais dados vem em quantidades massivas que levariam muito tempo para análise singular. Então o investigador filtra de acordo com a relevância e os joga para o próximo passo.

## 3. Análise

Nessa parte, extraimos dados e os correlacionamos com as evidências. O objetivo vária muito dependendo do cenário.

## 4. Relatórios

Nessa parte, apresentamos a metodologia de extração usada e tais conclusões sob as evidências. Aqui é bom deixar em linguagem executiva, não exclusivamente técnica.

---

Alguns tipos de forense digital:


- Computação forense: O tipo mais comum de digital forense é computação forense, que diz respeito à investigação de computadores, os dispositivos mais utilizados em crimes.
- Forense móvel: Forense móvel envolve investigando dispositivos móveis e extraindo evidências como chamada registros, mensagens de texto, localizações de GPS e muito mais.
- Forense de redes: Esta área da perícia abrange investigação além dos dispositivos individuais. Inclui toda a rede. A maioria das evidências encontradas nas redes é o tráfego de rede logs.
- Banco de dados forense: Muitos dados críticos são armazenados em bancos de dados dedicados. Forense de banco de dados investiga qualquer intrusão em esses bancos de dados que resultam em modificação ou exfiltração de dados.
- Cloud forensics: Cloud forensics é o tipo de forense que envolve investigar dados armazenados na nuvem infraestrutura. Esse tipo de perícia às vezes fica complicado para o investigadores, pois há poucas evidências sobre infraestruturas em nuvem.
- E-mail forense: E-mail, o mais comum método de comunicação entre profissionais, tornou-se parte importante da Perícia digital. Os e-mails são investigados para determinar se eles fazem parte de phishing ou campanhas fraudulentas.


---

## Aquisição de Provas

### Autorização

Autorização: a equipe forense deve obter autorização antes de coletar qualquer dado, por que nesses itens normalmente há diversos dados sensíveis tanto empresárias quanto pessoais. Precisamos garantir autorização para atuar dentro da lei.

### Cadeia de Custódia

Imagine que você coleta uma prova e ela aparece diferente ou simplesmente desaparece depois de alguns dias - ninguém poderá ser incriminado por que não há um documento confiável para aquilo.

Isso é resolvido usando um documento de cadeia de custódioa, ele é um documento formal contendo todos os detalhes das provas, normalmente contém:

- Descrição da prova (nome, tipo).
- Nome dos indivíduos que recolheram as provas.
- Data e hora da coleta de provas.
- Local de armazenamento de cada prova.
- Tempos de acesso e o registro individual que acessou as provas.

Isso garante um rastro adequado de evidência e ajuda a preserva-las, ainda comprova integridade e confiabilidade das provas em juízo.

### Uso de Bloqueadores de Escrita

Os bloqueadores de escrita são uma parte essencial da equipe forense digital toolbox. Suponha que você esteja coletando evidências do disco rígido de um suspeito e anexando o disco rígido à estação de trabalho forense.

Enquanto o coleta ocorre, algumas tarefas em segundo plano na estação de trabalho forense podem alterar os carimbos de data / hora dos arquivos no disco rígido. Isso pode causar entraves durante a análise, acabando por produzir resultados incorretos. Suponha que os dados tenham sido coletados do disco rígido usando um bloqueador de gravação no mesmo cenário.

Desta vez, o disco rígido do suspeito permaneceria em seu estado original, pois o bloqueador de gravação pode bloquear qualquer evidência ações de alteração. 

## Windows Forense

Quando estamos analisando sistemas operacionais, é comum obtermos a iso (image) dos sistemas, que nada mais é uma copia integra de determinadas partes.

São dois tipos principais:

- Imagens de disco: que não são são voláteis, ou seja, se eu reiniciar a máquina elas permanecerão lá, como imagens, videos, documentos, histórico de nav, etc.

- Imagens de memória: logs, registros de conexões, programas em execução - esse ja é volátil, se reiniciarmos o computador perderemos tais informações, então é a prioridade principal ao extrair a imagem do sistema.

---

### Ferramentas para Windows Forense

FTK Imager: Ferramenta para criar imagens de disco de Windows e analisar seu conteúdo; interface gráfica fácil de usar; serve para aquisição e análise.

Autopsy: Plataforma forense open-source para analisar imagens de disco; permite busca por palavras-chave, recuperação de arquivos excluídos, análise de metadados e detecção de inconsistências.

DumpIt: Ferramenta de linha de comando para capturar imagens de memória de sistemas Windows.

Volatilidade: Ferramenta open-source para análise de imagens de memória; usa plugins para examinar artefatos específicos; suporta Windows, Linux, macOS e Android.