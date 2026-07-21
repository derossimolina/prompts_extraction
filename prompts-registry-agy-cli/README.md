# Registro de Prompts e Trilha de Auditoria (Title and Abstract Screening)

Este diretório contém o registro detalhado de todas as interações e decisões tomadas durante a etapa de triagem de títulos e resumos (*Title and Abstract Screening*) para a Revisão Sistemática da Literatura (RSL) sobre **Métodos Computacionais Aplicados à Lavagem de Dinheiro por Crime Organizado**.

## Finalidade e Metodologia

Para garantir a **auditorabilidade, replicabilidade, confiabilidade e validade** das decisões de triagem (evitando vieses de seleção e garantindo transparência), cada um dos **2.592 artigos** da base unificada e deduplicada foi submetido individualmente a um crivo automatizado baseado no protocolo PICO-S registrado.

O resultado de cada triagem é documentado de forma estruturada em formato JSON na subpasta `./screening/`.

## Estrutura do Repositório

```
/prompt-registry/
├── README.md              ← Esta explicação metodológica geral
├── screening_report.md    ← Relatório estatístico consolidado e listagem de artigos incluídos/dúvidas
└── screening/             ← Arquivos JSON individuais de auditoria (2592 arquivos)
    ├── PROMPT-SCREENING-0001-2026-07-20-GEMINI_3_5_FLASH.json
    ├── PROMPT-SCREENING-0002-2026-07-20-GEMINI_3_5_FLASH.json
    └── ...
```

## Resumo Estatístico da Triagem

* **Total de Artigos Triados:** 2.592
* **Artigos Incluídos (Include):** 130 (5,02%) - Avançam para leitura de texto completo
* **Artigos em Dúvida (Uncertain):** 40 (1,54%) - Encaminhados para adjudicação humana
* **Artigos Excluídos (Exclude):** 2.422 (93,44%) - Não atendem aos critérios mínimos

## Estrutura do Log de Auditoria (JSON)

Cada arquivo de auditoria em `./screening/` contém:
1. **Metadados da Execução:** ID do prompt, timestamp ISO 8601, plataforma (`Google Antigravity`), modelo (`Gemini 3.5 Flash`), temperatura (`0.1`) e versão da *Skill*.
2. **Dados de Entrada (`input`):** Título, autores, ano de publicação, DOI, fonte e abstract do artigo analisado.
3. **Dados de Saída (`output`):** Decisão final (`Include`, `Exclude` ou `Uncertain`), lista de critérios atendidos ou falhos, e justificativa contextualizada (*reasoning*) em português.
4. **Decisão Humana (`human_decision`):** Estado de validação do pesquisador supervisor (padrão: `pending`).

## Protocolo de Auditoria e Replicabilidade

1. **Adjudicação de Dúvidas:** Os 40 artigos sinalizados como `Uncertain` devem ser abertos no relatório ou em seus respectivos arquivos JSON para a decisão final do pesquisador principal.
2. **Auditoria por Amostragem:** O orientador principal efetuará a conferência aleatória de 10% dos arquivos classificados como `Exclude`.
3. **Replicabilidade:** A integridade lógica das justificativas pode ser auditada por scripts de processamento de texto ou reexecutada com um modelo secundário, utilizando o cálculo do coeficiente de Kappa de Cohen para medir a concordância entre rodadas paralelas.
