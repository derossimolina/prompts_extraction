# Computational Methods Applied to Money Laundering by Organized Crime: GenAI Policy Extraction

**Main Protocol**
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20562470.svg)](https://doi.org/10.5281/zenodo.20562470)

**Prompt Extraction Policy**
(DOI forthcoming)

This repository is part a systematic literature review (SLR), named "Computational Methods Applied to Money Laundering by Organized Crime", under thesis project, named "Anti-money laudering Simulating Framework: A Generative Agent Based Modelling for Support Financial Institutions" (forthcoming).

Here we commit all prompts-extractions used by researcher to support SLR's extraction, screening and synthesized. All [policy](./policy.md) are at `policy.md`file, in this README we summarized main steps to register this policy. If you want to check all SLR protocol, this is published at Zenodo. 

# Introduction

A policy for prompt extraction is established in this protocol, aiming at replicability, transparency, ethics, and bias suppression. However, LLMs are not driven by deterministic models, operating on **non-deterministic** patterns, which means results are not granularly reproducible by third parties. The guarantee of replicability is not linked directly to the output, but rather to the **procedure** applied in its construction.

# Prompt Collection

When using LLM models focused on iteration and interaction with the user through chat, the prompts used (inputs) as well as the results (outputs) will be extracted at each conversation or step. They will be stored according to a specific metadata structure in markdown format (`*.md`).

## Metadata structure and human decision

Our metadata structure are divided with **categories**, **timestamp** for register data and time, **plataform** and LLM **model**, **temperature**, **input** natural language data, **reasoning** and **output** as result. All prompts are screening for human decision, to maintain replicability, transparency, and publicity.

## Unique ID

All files are follow strictly a unique identification, to traceability for other researchers conduct same or fork this policy or protocol.

# Commit Messages

All commit messages are song name, that everyone can check it on music streaming service or YouTube. This name songs follow alphabetical order, initiated with A, after that B, and so on.

# Disclaimer IAG

## Disclaimer for Protocol

> In accordance with the guidelines for the use of Artificial Intelligence issued by the Brazilian Federal Agency for Support and Evaluation of Graduate Education (CAPES), the National Council for Scientific and Technological Development (CNPq), the Brazilian Academy of Management (ANPAD), and the AI Use Guidelines of the Universidade de Caxias do Sul (UCS), this protocol made use of generative artificial intelligence (GenAI) to support the drafting, structuring, and critical review of its methodological components. The tool employed was Claude (Anthropic), model Claude Sonnet 4.6, accessed on June 3, 2026. Human supervision was exercised over all methodological decisions, and the intellectual responsibility for the protocol's content rests entirely with the authors. This study was financed in part by the Coordenação de Aperfeiçoamento de Pessoal de Nível Superior – Brasil (CAPES) – Finance Code 001.

# References

Cacciamani, G. E., Chu, T. N., Sanford, D. I., Abreu, A., Duddalwar, V., Oberai, A., Kuo, C.-C. J., Liu, X., Denniston, A. K., Vasey, B., McCulloch, P., Wolff, R. F., Mallett, S., Mongan, J., Kahn, C. E., Sounderajah, V., Darzi, A., Dahm, P., Moons, K. G. M., … Hung, A. J. (2023). PRISMA AI reporting guidelines for systematic reviews and meta-analyses on AI in healthcare. Nature Medicine, 29(1), 14–15. https://doi.org/10.1038/s41591-022-02139-w

De Rossi Molina, J., Panizzon, M., & Perini, R. (2026). Computational Methods Applied to Money Laundering by Organized Crime: SRL Protocol. Zenodo. https://doi.org/10.5281/zenodo.20562470

Moons, K. G. M., Damen, J. A. A., Kaul, T., Hooft, L., Andaur Navarro, C., Dhiman, P., Beam, A. L., Van Calster, B., Celi, L. A., Denaxas, S., Denniston, A. K., Ghassemi, M., Heinze, G., Kengne, A. P., Maier-Hein, L., Liu, X., Logullo, P., McCradden, M. D., Liu, N., … Van Smeden, M. (2025). PROBAST+AI: An updated quality, risk of bias, and applicability assessment tool for prediction models using regression or artificial intelligence methods. BMJ, 388, e082505. https://doi.org/10.1136/bmj-2024-082505

Williams, R. I., Clark, L. A., Clark, W. R., & Raffo, D. M. (2021). Re-examining systematic literature review in management research: Additional benefits and execution protocols. European Management Journal, 39(4), 521–533. https://doi.org/10.1016/j.emj.2020.09.007
