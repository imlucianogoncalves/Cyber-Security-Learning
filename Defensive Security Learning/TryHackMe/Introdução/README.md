# SOC Introdução

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno SOC do TryHackMe

SOC - Security Operations Center

---

Objetivos De Aprendizagem

- Construindo uma linha de base para SOC (Centro De Operações De Segurança)
- Detecção e resposta em SOC
- O papel das pessoas, dos processos e da tecnologia
- Exercício prático

## Finalidade e Componentes

O papel dele é manter a Detection e Response em dia. Ele tem algumas soluções para realizar isso, essas soluções integram toda a rede da empresa e todos os sistemas, para monitora-los a partir de um local centralizado.

Eles atuam tanto na detecção quanto na resposta, então:

### Detecção (principais pontos)

- Vulnerabilidades: fraquezas em software/sistemas que podem ser exploradas; embora nem sempre responsabilidade direta do SOC, vulnerabilidades não corrigidas aumentam o risco organizacional.

- Atividade não autorizada: identificar logins ou ações incomuns (ex.: uso de credenciais roubadas) rapidamente — sinais como local geográfico atípico ajudam na detecção.

- Violações de políticas: ações que quebram regras internas (ex.: downloads piratas, envio inseguro de dados) e que variam conforme a empresa.

- Intrusões: acessos não autorizados por exploração ou malware; exemplos incluem exploração de aplicações web ou infecção via site malicioso.

### Resposta (nível alto)

- Mitigação imediata: ao detectar um incidente, tomar medidas para limitar o impacto (bloquear acessos, isolar sistemas, etc.).

- Análise de causa raiz: investigar como o incidente ocorreu para evitar recorrência.

- Apoio do SOC: o SOC fornece detecção contínua e suporte operacional à equipe de resposta a incidentes durante contenção, erradicação e recuperação.

---

o SOC tem três pilares principais:

- Pessoas
- Processo
- Tecnologia

---

## Pessoas


 - SOC Analista (Nível 1): Qualquer coisa detectada pela segurança solução passaria por esses analistas primeiro. Estes são os primeiros respondentes a qualquer detecção. SOC Analistas de Nível 1 realizam triagem básica de alertas para determinar se uma detecção específica é prejudicial. Eles também relatam estes detecções através dos canais adequados.
-  SOC Analista (Nível 2) : Enquanto o Nível 1 faz o primeiro nível análise, algumas detecções podem exigir uma investigação mais profunda. Nível 2 Os analistas os ajudam a mergulhar mais fundo nas investigações e correlacionar o dados de várias fontes de dados para realizar uma análise adequada.
-  SOC Analista (Nível 3) :  Analistas de Nível 3 são experientes profissionais que buscam de forma proativa quaisquer indicadores de ameaça e suporte nas atividades de resposta a incidentes. A detecção de gravidade Crítica relatados por analistas de Nível 1 e Nível 2 são frequentemente incidentes de segurança que precisam de respostas detalhadas, incluindo contenção, erradicação e recuperação. É aqui que a experiência dos analistas de Nível 3 vem a calhar.
-  Engenheiro De Segurança: Todos os analistas trabalham com segurança soluções. Essas soluções precisam de implantação e configuração. Segurança Os engenheiros implantam e configuram essas soluções de segurança para garantir bom funcionamento.
-  Engenheiro De Detecção: Regras de segurança são a lógica construído atrás de soluções de segurança para detectar atividades prejudiciais. Nível 2 e 3 Os analistas costumam criar essas regras, enquanto o SOC equipe pode às vezes utilize também a função engenheiro de detecção de forma independente para isso responsabilidade.
-  SOC Gerente: O SOC Gestor gerencia os processos o SOC equipe acompanha e dá suporte. O SOC Gerente também permanece em contato com o CISO (Chief Information Security Oficial) para lhe fornecer atualizações sobre o SOC segurança atual da equipe postura e esforços.

---

## Processos do SOC

### Triagem de alertas

Esse processo serve pra determinar a gravidade do alerta e ajuda nós priorizarmos isso, tudo isso parte da resposta dos 5Ws.

Quais são os 5Ws?

**Exemplo:**

Alerta: Malware detectado no Host: GEORGE PC 

- O quê: Arquivo malicioso detectado na rede da organização.

- Quando: 5 de junho de 2024, às 13h20.

- Onde: Diretório do host “GEORGE PC”.

- Quem: Usuário George.

- Por quê: O arquivo foi baixado de um site de software pirata para usar um programa gratuitamente.

---

## Relatórios

Tais alertas prejudiciais são escalados para analistas de nível superior para uma resposta e resolução oportunas.

São escalados como **tickets** e atribuidos juntamente a capturas de telas para prova da atividade.

## Resposta a Incidentes e Forense

Algumas detecções indicam atividades altamente maliciosas e críticas, exigindo a atuação da equipe de resposta a incidentes. Em certos casos, é necessária uma análise forense detalhada para identificar a causa raiz, examinando os artefatos do sistema ou da rede.


## Tecnologia

A tecnologia ajuda, centralizando todas as informações relevantes em um sistema para que minimize o trabalho manual do SOC. Tais sistemas centralizam todas as informações de dispositivos e apps na rede e automatizam a capacidade de detecção e resposta.

**Security Information and Event Management (SIEM)**: ferramenta que recolhe logs dos vários dispositivos na rede. Com regras prédefinidas, nos da um alerta quando alguma situação não ocorre como o esperado pelas regras. Alguns SIEMs são mais construidos e oferecem tais alertas com base em comportamento do usuario.

**Endpoint Detection and Response (EDR)**: fornece para a equipe SOC visibilidade de talhada em tempo real e histórico de atividade dos dispositivos - opera no nível do endpoint e pode realizar respostas automatizadas - possui amplos recursos de detecção para endpoints, permitindo que você os investigue em detalhes e responda com um poucos cliques.


**Firewall:** A firewall funções puramente para rede segurança e atua como uma barreira entre o seu interno e externo redes (como a Internet). Monitora rede de entrada e saída tráfego e filtra qualquer tráfego não autorizado. O firewall também tem alguns regras de detecção implantadas, que nos ajudam a identificar e bloquear suspeitos tráfego antes de chegar à rede interna. 