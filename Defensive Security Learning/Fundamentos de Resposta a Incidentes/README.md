# Fundamentos de Resposta a Incidentes

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno SOC do TryHackMe

Objetivos De Aprendizagem

- Visão geral do que são incidentes e seus níveis de gravidade
- Tipos comuns de incidentes
- Fases de resposta a Incidentes de SANS e NIST Frameworks
- Ferramentas para detecção e resposta a incidentes, juntamente com o papel dos PlayBooks
- Plano De Resposta A Incidentes

---

## Tipos de Incidentes de Segurança Cibernética

Embora muitas atividades maliciosas no ambiente digital sejam rotuladas genericamente como “hacking”, a segurança cibernética classifica incidentes em categorias específicas, cada uma com características e impactos distintos.

### 1. Infecções por Malware
- **Definição:** Programas maliciosos que podem comprometer sistemas, redes ou aplicativos.  
- **Vetores comuns:** Arquivos de texto, documentos, executáveis, anexos de e-mail.  
- **Impacto:** Pode variar desde perda de dados até comprometimento completo do sistema.  

### 2. Brechas de Segurança (Security Breaches)
- **Definição:** Acesso não autorizado a dados confidenciais.  
- **Importância:** Crítico para empresas que dependem da proteção de informações sensíveis.  
- **Exemplo:** Um invasor obtendo acesso a registros financeiros internos.  

### 3. Vazamentos de Dados (Data Leaks)
- **Definição:** Exposição de informações confidenciais a entidades não autorizadas.  
- **Causas:** Podem ser intencionais (ataques) ou acidentais (erro humano, má configuração).  
- **Impacto:** Danos reputacionais, chantagem, exploração de informações.  

### 4. Ataques Internos (Insider Attacks)
- **Definição:** Incidentes originados de dentro da organização.  
- **Exemplo:** Funcionário descontente infectando a rede com malware via USB.  
- **Risco:** Insiders têm acesso privilegiado, tornando ataques internos altamente perigosos.  

### 5. Ataques de Negação de Serviço (DoS / Denial of Service)
- **Definição:** Inundação de sistemas ou redes com solicitações falsas, tornando-os indisponíveis.  
- **Objetivo:** Comprometer a **disponibilidade**, um dos pilares da segurança cibernética (Confidencialidade, Integridade, Disponibilidade).  
- **Impacto:** Paralisação de serviços críticos, mesmo que os dados permaneçam seguros.  

### Observações Gerais
- Cada tipo de incidente tem **potencial único de impacto**.  
- A gravidade depende do contexto da vítima; o mesmo incidente pode ser crítico para uma organização e irrelevante para outra.  
- **Exemplo:** Um vazamento de dados pode ser insignificante para uma empresa, mas um ataque DoS pode comprometer totalmente suas operações.


---

# Estruturas de Resposta a Incidentes

Lidar com diferentes tipos de incidentes em um ambiente corporativo exige **processos estruturados**. Organizações populares como **SANS** e **NIST** desenvolveram frameworks amplamente utilizados para orientar a resposta a incidentes de forma eficaz.

---

## 1. SANS Incident Response Framework (PICERL)

O framework SANS possui **6 fases**, lembradas pelo acrônimo **PICERL**:

| Fase | Explicação | Exemplo |
|------|------------|---------|
| **Preparação** | Construir recursos necessários para lidar com incidentes, incluindo equipes e planos de resposta, além de implementar soluções de segurança. | Treinamento de colaboradores sobre phishing e-mails. |
| **Identificação** | Detectar comportamentos anormais que possam indicar um incidente, utilizando monitoramento e técnicas de análise. | Detectar tráfego incomum em um host comprometido por um anexo malicioso de phishing. |
| **Contenção** | Minimizar o impacto isolando sistemas comprometidos ou desabilitando contas afetadas. | Isolar o host da rede para evitar movimentação lateral do invasor. |
| **Erradicação** | Remover a ameaça do ambiente comprometido e garantir que o sistema esteja limpo. | Executar varredura profunda de malware para eliminar software malicioso. |
| **Recuperação** | Restaurar sistemas afetados a partir de backups ou reconstrução, garantindo funcionalidade segura. | Reconfigurar host comprometido e restaurar dados a partir de backup. |
| **Lições Aprendidas** | Revisar o incidente para identificar lacunas e melhorar processos futuros. | Reunião pós-incidente para analisar causa raiz e aprimorar a segurança. |

---

## 2. NIST Incident Response Framework

O framework NIST é semelhante ao SANS, mas com **4 fases principais**:

1. **Preparação** – Equipamentos, políticas, treinamento e medidas preventivas.
2. **Detecção e Análise** – Identificação de incidentes e avaliação do impacto.
3. **Contenção, Erradicação e Recuperação** – Minimizar danos, eliminar ameaças e restaurar sistemas.
4. **Atividades Pós-Incidente** – Revisão, documentação e melhoria contínua.

> Nota: A principal diferença é que o NIST combina algumas fases do SANS (como Contenção, Erradicação e Recuperação) em uma etapa única.

---

## 3. Plano de Resposta a Incidentes

As organizações formalizam seus processos em um **Plano de Resposta a Incidentes**, documento aprovado pela alta administração que descreve procedimentos antes, durante e após um incidente.

### Componentes principais:
- Funções e responsabilidades de cada membro da equipe.
- Metodologia de resposta a incidentes.
- Plano de comunicação com stakeholders, incluindo autoridades legais.
- Caminho de escalonamento a ser seguido para diferentes tipos de incidentes.

---

Para identificar tais incidentes, podemos usar:

- SIEM : A segurança da Informação e gestão de eventos Solução ( SIEM ) coleta todos os logs importantes em um local centralizado e os correlaciona para identificar incidentes.
- AV : Antivírus ( AV ) detecta programas maliciosos conhecidos em um sistema e verifica regularmente o seu sistema para estes.
- EDR : Detecção e Resposta de Endpoint ( EDR ) é implantado em todos os sistemas, protegendo-o contra algum nível avançado ameaças. Essa solução também pode conter e erradicar a ameaça. 