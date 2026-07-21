---
category: extraction
timestamp: 1780931258
plataform: webui
model: gemini-3.5-flash-extended
temperature: no control
---

# Input

## Input 1

```
Preciso realizar a extração dos dados de papers no repositório do SSRN para uma revisão sistemática da literatura, onde constam autor, título, abstract, ano, citações e se o artigo foi publicado em um periódico ou não. Pode me ajudar com isso?
```

## Input 2

```
Vamos usar a API da Elsevier para eu conseguir realizar o download em massa. Já fiz o cadastro da chave no portal de desenvolvedores da Elsevier.
```

## Input 3

```
Acredito que a solução seja buscar diretamente no OpenAlex, sem utilizar API.
```
# Reasoning

## Reasoning 1

```gemini

**Defining the Objective**

I've clarified the user's needs; the focus is extracting SSRN data for a systematic review.

**Refining Constraints and Guidelines**

I've established formatting guidelines for scannability, LaTeX usage limitations, and a strategy for handling the guide's ambiguity.

**Defining Extraction Methods**

I have determined that a Python script is necessary to circumvent SSRN's anti-scraping measures to extract required data.

**Outlining Extraction Strategies**

I am now structuring the response around three key extraction paths, detailing automation, indexer APIs, and Zotero integration.

**Identifying HTML Structure**

I have successfully pinpointed key HTML elements for scraping: titles, authors, abstracts, dates, and journal statuses.

**Mapping Data Locations**

I have clarified where key data points reside in SSRN's HTML, refining my scraping strategy significantly.

**Integrating Zotero Output**

I've outlined importing Zotero exports to Pandas, augmenting them with API data from Crossref or OpenAlex.
```

## Reasoning 2

```gemini 

**Defining the Goal**

I've established the primary objective: download SSRN paper data using the Elsevier API with the registered key.

**Discovering Elsevier's APIs**

I've learned that SSRN content within Elsevier's ecosystem is accessible through the Scopus Search API, not a dedicated SSRN API.

**Defining the Solution**

I've clarified the approach: we'll tailor a technical solution for Jerônimo, focusing on Elsevier API's indirect SSRN access.

**Refining the Query**

I've specified the Scopus Search API approach, including authentication nuances with API keys and institutional tokens.

**Crafting the Script**

I've produced a detailed, production-ready Python example, emphasizing SSRN handling and API key/token usage.

**Clarifying Data Sources**

Now, I'm documenting the distinction between SSRN and Scopus records, plus checking journal publication status.

**Constructing the Code**

I've implemented a Python script, meticulously handling API calls and data parsing, now with title, author, and year included.
```

## Reasoning 3

```gemini

**Refining Extraction Strategy**

I've decided to prioritize a direct search approach within OpenAlex, bypassing the API, per the user's advice.

**Validating Direct Search**

I've confirmed direct OpenAlex search is viable for data retrieval via its web interface.

**Refining GUI Search**

I've outlined steps for efficient SSRN searches, demonstrating direct OpenAlex GUI usage for desired metadata.
```

# Output

## Output 1

Realizar a extração de dados do **SSRN (Social Science Research Network)** para uma Revisão Sistemática da Literatura (RSL) é uma excelente estratégia para mapear preprints e literatura cinzenta. Contudo, como a plataforma pertence à Elsevier, ela não disponibiliza uma API pública aberta para buscas gerais e conta com camadas rígidas de proteção (como Cloudflare) que dificultam a raspagem de dados tradicional (_web scraping_).

Para coletar de forma estruturada os campos que você precisa (**Autor, Título, Abstract, Ano, Citações e Status de Publicação**), existem três caminhos principais.

## Comparativo de Abordagens para Extração

|**Campo Desejado**|**Abordagem 1: Scraping Direto (HTML do SSRN)**|**Abordagem 2: APIs Integradas (Scopus / OpenAlex)**|
|---|---|---|
|**Autor e Título**|Extraídos de tags `<h1>` e links de autores.|Nativos e limpos nos metadados da API.|
|**Abstract**|Capturado via classe `.abstract-text`.|Disponível na maioria dos registros indexados.|
|**Ano**|Mapeado pelas strings "Date Written" ou "Posted".|Campo estrito de data/ano de publicação.|
|**Citações**|Exige raspar o bloco dinâmico de _Metrics_.|Retornado diretamente no contador de citações.|
|**Status de Periódico**|Identificado se houver o texto _"Published in..."_.|Classificado via atributos de tipo de documento.|

## 1. Abordagem via Script Python (Web Scraping)

Se você optar por construir um script customizado para minerar as páginas de _abstract_ diretamente do SSRN, precisará simular o comportamento de um navegador para evitar bloqueios de IP.

- **Contornando o Cloudflare:** Bibliotecas tradicionais como `requests` costumam falhar no SSRN. Recomenda-se o uso do **`cloudscraper`** ou de ferramentas de automação de navegador como **`Selenium`** ou **`Playwright`** para carregar os elementos dinâmicos (como o bloco de citações).
    
- **Lógica de Captura:** O script deve primeiro coletar as URLs dos artigos a partir da página de resultados de busca e, em seguida, iterar por cada link extraindo o HTML.
    
- **Tratamento do Status:** No HTML do SSRN, quando um artigo é aceito por uma revista, a plataforma adiciona uma nota no topo ou rodapé dizendo _"Published in: [Nome do Periódico]"_. Seu script precisará de uma verificação condicional (Regex ou busca de texto simples) para identificar essa string e marcar o status como publicado.
    

## 2. Abordagem via APIs de Bases Indexadoras (Recomendado para RSL)

Para garantir a reprodutibilidade técnica exigida por protocolos como o PRISMA, a rota mais robusta é utilizar bases de dados que indexam o SSRN e possuem APIs estruturadas:

- **Scopus API:** Como a Elsevier gerencia ambas as plataformas, a API do Scopus permite buscar por artigos do SSRN (usando filtros de _Publisher_ ou _Source_). Ela entrega o pacote completo de metadados, incluindo a contagem de citações atualizada e o vínculo com periódicos caso o artigo tenha sido publicado posteriormente.
    
- **OpenAlex API:** É uma base de dados global e totalmente aberta de ecossistemas de pesquisa. Você pode fazer requisições gratuitas filtrando por documentos que tenham o SSRN como repositório original. O retorno em JSON separa perfeitamente o ano, autores, contagem de citações e se o objeto digital possui um _host_ secundário (o periódico).
    

## 3. Fluxo Semiautomatizado (Gerenciadores de Referência)

Se o volume de artigos identificados na busca inicial for de até algumas centenas, você pode acelerar o processo sem precisar programar do zero:

1. **Captura em lote:** Utilize o **Zotero** com a extensão do navegador diretamente na página de resultados do SSRN. O tradutor do Zotero extrai nativamente o título, autores, abstract e data.
    
2. **Exportação dos Metadados:** Exporte a pasta gerada no formato `.RIS` ou BibTeX.
    
3. **Tratamento e Enriquecimento:** Importe esse arquivo para um DataFrame do **Pandas** no Python. A partir dos títulos ou DOIs importados, você pode rodar um script simples e rápido apenas para consultar a contagem de citações e o status de publicação atual em uma API aberta como a do **Crossref**.
    

Qual dessas abordagens (programação direta com Python para scraping ou a integração via APIs de bases de dados) se alinha melhor com o volume de dados e com o escopo atual da sua pesquisa?

## Output 2

Excelente passo. Ter a API Key em mãos agiliza muito o processo. No ecossistema da Elsevier, os dados do SSRN (que funciona essencialmente como um servidor de preprints e working papers) são minerados programaticamente através da **Scopus Search API**.

Como você já possui a credencial (`X-ELS-APIKey`), o caminho mais eficiente é construir um script em Python utilizando as bibliotecas `requests` e `pandas`.

## Mapeamento de Campos na API da Elsevier

A resposta JSON da API do Scopus não usa exatamente os nomes convencionais em português. Veja como os dados que você precisa estão mapeados dentro da estrutura deles:

- **Autor:** Retornado na tag `dc:creator` (autor principal) ou dentro do array de autores se o escopo de busca for estendido.
    
- **Título:** Mapeado no campo `dc:title`.
    
- **Ano:** Extraído a partir do campo `prism:coverDate` (formato `AAAA-MM-DD`).
    
- **Citações:** Disponível diretamente no contador `citedby-count`.
    
- **Abstract:** Fica no campo `dc:description`. _Nota técnica:_ Dependendo do nível de acesso da sua chave (se ela é básica ou vinculada a um IP institucional/VPN universitária), a busca geral pode trazer apenas um snippet. Se isso acontecer, usamos o identificador `scopus_id` retornado para coletar o abstract completo no endpoint secundário de _Abstract Retrieval_.
    
- **Status de Periódico:** No Scopus, registros nativos do SSRN aparecem com o campo `prism:aggregationType` como "Journal" ou "Preprint" e `subtypeDescription` como "Preprint" ou "Article". Quando o artigo do SSRN é publicado formalmente em uma revista científica, a Elsevier costuma indexar a versão final como um novo registro do tipo "Article", vinculando-a ao periódico correspondente.
    

## Script Base para Extração em Massa

Para isolar os artigos vindos especificamente do SSRN dentro do Scopus, utilizamos o identificador de fonte do repositório na query (como o título da fonte: `SRCTITLE("SSRN Electronic Journal")` ou seu ISSN correspondente `1556-5068`).

O modelo abaixo estrutura a requisição inicial e organiza os dados em um DataFrame pronto para exportação:

```python

import requests
import pandas as pd

# Substitua com as suas credenciais do portal de desenvolvedores
API_KEY = "SUA_API_KEY_AQUI"

# Se estiver usando a VPN da universidade ou na rede interna, o 'insttoken' 
# pode ser necessário para liberar acesso completo aos abstracts. Caso contrário, deixe vazio.
INST_TOKEN = "" 

url = "https://api.elsevier.com/content/search/scopus"

headers = {
    "X-ELS-APIKey": API_KEY,
    "Accept": "application/json"
}
if INST_TOKEN:
    headers["X-ELS-Insttoken"] = INST_TOKEN

# Query de exemplo: filtra pelo SSRN e busca termos específicos no título/abstract/palavras-chave
# Substitua "innovation ecosystems" pelo seu termo de busca da RSL
query = 'SRCTITLE("SSRN Electronic Journal") AND TITLE-ABS-KEY("innovation ecosystems")'

params = {
    "query": query,
    "count": 25,        # Quantidade de registros por requisição (máximo padrão é 25 ou 100)
    "start": 0,         # Ponto de partida para a paginação
    "view": "COMPLETE"  # Solicita o conjunto completo de metadados (incluindo abstracts)
}

all_papers = []

response = requests.get(url, headers=headers, params=params)

if response.status_code == 200:
    data = response.json()
    entries = data.get("search-results", {}).get("entry", [])
    
    for entry in entries:
        # Extração e tratamento dos metadados
        title = entry.get("dc:title", "N/A")
        author = entry.get("dc:creator", "N/A")
        
        # Tratamento da data para obter o ano
        cover_date = entry.get("prism:coverDate", "")
        year = cover_date.split("-")[0] if cover_date else "N/A"
        
        citations = entry.get("citedby-count", 0)
        abstract = entry.get("dc:description", "N/A")
        
        # Identificadores de tipo de publicação
        agg_type = entry.get("prism:aggregationType", "N/A")
        subtype = entry.get("subtypeDescription", "N/A")
        
        all_papers.append({
            "Autor": author,
            "Título": title,
            "Abstract": abstract,
            "Ano": year,
            "Citações": citations,
            "Tipo_Agregação": agg_type,
            "Subtipo": subtype
        })
        
    # Transforma em DataFrame para manipulação
    df = pd.DataFrame(all_papers)
    print(f"Sucesso! {len(df)} artigos extraídos nesta chamada.")
else:
    print(f"Erro na requisição: {response.status_code} - {response.text}")
```

## Próximos Passos para o Volume da RSL

Como revisões sistemáticas costumam lidar com centenas ou milhares de resultados, o script final precisará de uma **lógica de paginação automática** (um loop `while` que incrementa o parâmetro `"start"` somando o valor de `"count"` até atingir o total indicado pela API em `"opensearch:totalResults"`).

Você prefere que avancemos estruturando esse loop completo de paginação automática com tratamento de erros para salvar os dados diretamente em um arquivo local (como CSV), ou quer validar primeiro a sintaxe da sua string de busca para o Scopus?

## Output 3

Essa é uma excelente virada de estratégia! A interface gráfica (Web UI) do **OpenAlex** é hoje uma das ferramentas mais poderosas e amigáveis para Revisões Sistemáticas da Literatura (RSL). Ela permite construir buscas complexas e fazer a extração direta para arquivos estruturados (**CSV** ou **RIS**) sem que você precise digitar uma única linha de código ou lidar com chaves de acesso.

Como o OpenAlex indexa de forma aberta o ecossistema global de pesquisas (incluindo o SSRN), você consegue mapear tudo visualmente. Veja como estruturar essa extração direto na plataforma:

## Passo a Passo para Extração na Interface do OpenAlex

### 1. Filtrando pelo Repositório (SSRN)

Para garantir que você está minerando apenas os registros do SSRN, utilize os filtros de fontes (_Sources_) da interface:

- Acesse [openalex.org](https://openalex.org/) e clique na barra de busca de **Works** (Trabalhos).
    
- No painel lateral de filtros, adicione um filtro por **Source**.
    
- Busque por **"SSRN Electronic Journal"** ou **"Social Science Research Network"** e selecione-o. Isso isolará a base do SSRN.
    

### 2. Adicionando os Termos da RSL

Na barra principal de busca, insira os termos e operadores booleanos da sua pesquisa (ex: `"innovation ecosystems" AND "public management"`). A interface do OpenAlex processará a busca combinando o filtro do SSRN com as suas palavras-chave no título e no abstract simultaneamente.

## Como os Seus 6 Campos Virão no CSV

Ao clicar no botão de **Export** (geralmente localizado no canto superior direito dos resultados) e escolher o formato **CSV**, o arquivo gerado trará colunas específicas que atendem perfeitamente aos seus critérios:

|**Campo Desejado**|**Coluna Correspondente no CSV do OpenAlex**|**Comportamento no OpenAlex**|
|---|---|---|
|**Autor**|`authorships` / `author.display_name`|Traz a lista de autores formatada, frequentemente associada às suas respectivas instituições.|
|**Título**|`title`|Título completo e limpo do documento.|
|**Abstract**|`abstract`|Disponível na exportação se o registro contiver o resumo indexado.|
|**Ano**|`publication_year`|Ano de publicação em formato numérico direto, pronto para filtros cronológicos.|
|**Citações**|`cited_by_count`|O OpenAlex atualiza essa contagem constantemente com base em toda a sua rede aberta.|
|**Status de Periódico**|`locations` / `primary_location.source.type`|**O grande trunfo do OpenAlex** (explicado em detalhes abaixo).|

### Decifrando o Status: O Artigo foi para um Periódico?

Uma das maiores vantagens de usar o OpenAlex sem código para essa análise é a forma como eles gerenciam **"Locations"** (Locais de Hospedagem).

> No OpenAlex, se um preprint do SSRN foi aceito e publicado posteriormente em uma revista científica tradicional, eles **não criam dois registros separados**. Eles mesclam os dados em um único "Work" que passa a ter múltiplas localizações.

Ao analisar o CSV exportado, você saberá o status olhando para duas colunas:

1. **`primary_location.source.type`**: Se o artigo continua apenas como um working paper/preprint no SSRN, essa coluna indicará `repository`. Se ele já foi publicado formalmente e a versão final da revista foi indexada, essa coluna mudará para `journal`.
    
2. **`locations`**: Esta coluna lista todos os lugares onde o texto está disponível. Se houver mais de uma URL (uma apontando para o `ssrn.com` e outra para o site de uma editora como `sciencedirect.com` ou `springer.com`), significa que o artigo evoluiu de preprint para um artigo de periódico publicado.
    

O OpenAlex enviará o link para download do arquivo CSV diretamente para o seu e-mail caso o volume de resultados seja muito alto.

Você já tem a string de busca final estruturada em blocos booleanos (AND/OR) para aplicar direto nos filtros da plataforma?
# Human Decision

Com base no resultado da busca em GenAI, utilizei plugin do Zotero, primeiramente com indicado, porém essa alternativa não funcionou a contento. Desse modo a alternativa foi utilizar a API da Scopus para realizar o download em massa. 

A abordagem do [[#Output 2]] não funcionou também, sendo que a abordagem buscando dentro do OpenAlex se tornou mais interessante. Portanto, se utilizou a abordagem sugerida no [[#Output 3]], visto que traz os registros do SSRN de forma mais eficiente. 

> **Nota**: não é permitido no OpenAlex usar asterisco ($\text{*}$) como _wildcard_ para buscar termos em plural ou derivações. A sugestão da própria plataforma é trabalhar com proximidade usando o descritor `~3`, sendo o número os graus de proximidade do termo. Optou-se por usar o descritor de proximidade `~4` para todos os termos com asterisco. Este último não funcionou a contento, retirando-se e mantendo a expressão sem nenhum descritor ou _wildcard_. 