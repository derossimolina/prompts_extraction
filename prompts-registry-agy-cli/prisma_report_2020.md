# Relatório de Fluxo de Triagem PRISMA 2020

**Revisão Sistemática da Literatura:** Métodos Computacionais Aplicados à Lavagem de Dinheiro por Crime Organizado  
**Autor Principal:** Jerônimo De Rossi Molina  
**Data do Relatório:** 21 de Julho de 2026  
**Modelo de IA Utilizado:** Gemini 3.5 Flash (via Google Antigravity CLI)  
**ID do Repositório de Prompts:** `prompts-registry-agy-cli`

---

## 1. Introdução

Este relatório documenta as decisões metodológicas e o fluxo quantitativo da revisão sistemática da literatura (RSL) seguindo as diretrizes estabelecidas pela declaração **PRISMA 2020** (*Preferred Reporting Items for Systematic Reviews and Meta-Analyses*). 

A triagem inicial por título e resumo foi executada de maneira automatizada pelo agente de IA seguindo o protocolo de inclusão/exclusão (PICO-S) estruturado na versão do protocolo. Cada decisão foi registrada de forma transparente e independente com uma trilha de auditoria contendo a justificativa (*reasoning*) individual em formato JSON.

---

## 2. Etapa de Identificação (Identification)

A busca inicial nas bases de dados selecionadas (Scopus, Web of Science, SciELO) e fontes complementares (arXiv, SSRN, SocArXiv) gerou um volume consolidado de registros.

### 2.1 Busca e Consolidação Primária
Os resultados brutos importados das buscas bibliográficas totalizaram **4.223 registros**, distribuídos conforme as origens de extração compiladas no arquivo unificado:
* **Bases de Dados Principais (Scopus, Web of Science, SciELO)**
* **Repositórios de Literatura Cinzenta / Preprints (arXiv, SSRN, SocArXiv, BDTD)**

### 2.2 Deduplicação
Os 4.223 registros unificados foram submetidos a um processo algorítmico de deduplicação com base nos critérios de correspondência exata ou aproximada de DOI, título, autores e ano de publicação.
* **Registros duplicados removidos:** 1.631 registros (38,62%)
* **Registros únicos para triagem:** 2.592 registros (61,38%)

---

## 3. Etapa de Triagem (Screening)

Os **2.592 registros únicos** foram submetidos à triagem por título e resumo. A triagem foi realizada pelo agente de IA em conformidade com o protocolo.

### 3.1 Registros Excluídos (n = 2.422)
Um total de **2.422 artigos** foi excluído na primeira triagem (93,44% do corpus único). As justificativas detalhadas estão mapeadas na pasta de auditoria, categorizadas pelos seguintes motivos:
1. **Falta de Método Computacional (Critério 1 - Intervenção):** Estudos puramente qualitativos, análises jurídicas, dogmáticas ou frameworks regulatórios normativos (como tipologias clássicas do GAFI) sem modelagem associada, além de estudos econométricos descritivos sem componentes preditivos ou simulatórios.
2. **Falta de Foco em Lavagem de Dinheiro (Critério 2 - Objeto):** Artigos sobre crimes cibernéticos gerais (como ataques de ransomware), evasão fiscal comum, ou fraudes financeiras corporativas individuais sem vinculação a redes transacionais de lavagem de dinheiro.
3. **Falta de Conexão com Organização Criminosa (Critério 2 - Objeto):** Estudos focados em comportamento delituoso individual isolado, sem representação de comportamento coletivo, redes criminosas estruturadas ou facilitação organizacional de dissimulação de capitais.

### 3.2 Registros Pré-Selecionados (n = 130)
Um total de **130 artigos** foi incluído para leitura do texto completo (5,02%). Esses artigos demonstraram aplicar explicitamente técnicas computacionais relevantes (modelagem baseada em agentes - ABM, aprendizado de máquina, redes neurais, detecção em grafos - GNN, ou simulação de Monte Carlo) para analisar a lavagem de dinheiro estruturada em rede.

### 3.3 Casos Limítrofes / Dúvidas (n = 40)
Um subgrupo de **40 artigos** (1,54%) foi marcado como `Uncertain` (Dúvida). Estes consistem em modelos computacionais de detecção de fraudes financeiras transacionais gerais, onde a caracterização da "organização criminosa" é implícita ou ambígua. Seguindo o protocolo de auditoria, estes casos foram sinalizados para adjudicação humana obrigatória antes da leitura de texto completo.

---

## 4. Diagrama de Fluxo PRISMA 2020

Abaixo está a representação gráfica do fluxo de informação ao longo das diferentes fases da revisão sistemática:

```
#####################################################################################
#                                                                                   #
#   IDENTIFICAÇÃO                                                                   #
#   ┌────────────────────────────────────────┐                                      #
#   │ Registros identificados nas buscas     │                                      #
#   │ (Bases primárias e complementares)     │                                      #
#   │ n = 4.223                              │                                      #
#   └───────────────────┬────────────────────┘                                      #
#                       │                                                           #
#                       ▼                                                           #
#   ┌────────────────────────────────────────┐                                      #
#   │ Registros removidos antes da triagem:  │                                      #
#   │ - Duplicatas removidas                 │                                      #
#   │   n = 1.631                            │                                      #
#   └───────────────────┬────────────────────┘                                      #
#                       │                                                           #
#                       ▼                                                           #
#   TRIAGEM                                                                         #
#   ┌────────────────────────────────────────┐                                      #
#   │ Registros únicos triados               │                                      #
#   │ (Por título e resumo)                  │                                      #
#   │ n = 2.592                              │                                      #
#   └───────────────────┬────────────────────┘                                      #
#                       │                                                           #
#                       ├─────────────────────────────┐                             #
#                       │                             ▼                             #
#                       │                    ┌──────────────────────────────────┐   #
#                       │                    │ Registros excluídos pelo agente: │   #
#                       │                    │ - Sem método computacional       │   #
#                       │                    │ - Sem foco em lavagem de dinheiro│   #
#                       │                    │ - Sem foco em crime organizado   │   #
#                       │                    │ n = 2.422                        │   #
#                       │                    └──────────────────────────────────┘   #
#                       ▼                                                           #
#   ELEGIBILIDADE                                                                   #
#   ┌────────────────────────────────────────┐                                      #
#   │ Registros pré-selecionados para        │                                      #
#   │ leitura de texto completo              │                                      #
#   │ n = 170                                │                                      #
#   │   (- 130 Incluídos pelo agente)        │                                      #
#   │   (- 40 Casos limítrofes / dúvidas)    │                                      #
#   └───────────────────┬────────────────────┘                                      #
#                       │                                                           #
#                       ▼                                                           #
#   ┌────────────────────────────────────────┐                                      #
#   │ Adjudicação Humana e Avaliação         │                                      #
#   │ (Processo de decisão em andamento)     │                                      #
#   └────────────────────────────────────────┘                                      #
#                                                                                   #
#####################################################################################
```

---

## 5. Próximas Etapas e Confiabilidade

Para consolidar a validade da triagem final:
1. **Adjudicação:** O pesquisador principal avaliará individualmente os 40 registros classificados como `Uncertain` (disponibilizados no arquivo `screening_report.md` com suas respectivas justificativas detalhadas), decidindo pela inclusão ou exclusão definitiva.
2. **Replicabilidade:** A integridade das justificativas de exclusão poderá ser auditada de forma independente através da reexecução da *Skill* `srl-aml-agent` por um segundo modelo independente para cálculo do Kappa de Cohen de confiabilidade inter-avaliador.
3. **Leitura de Texto Completo:** Os artigos aceitos serão avaliados integralmente segundo o protocolo adaptado CASP de qualidade de modelos computacionais.
