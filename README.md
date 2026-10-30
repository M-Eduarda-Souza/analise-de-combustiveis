# Inteligência de Dados para Gestão e Previsão de Preços de Combustíveis

Projeto acadêmico interdisciplinar desenvolvido para as disciplinas de Visualização de Dados e Aprendizado de Máquina Supervisionado, da Universidade Federal da Paraíba (UFPB).

O projeto tem como objetivo desenvolver uma solução de apoio à tomada de decisão para a gestão e o acompanhamento dos preços de combustíveis, utilizando dados públicos da Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP), técnicas de análise e visualização de dados e modelos de aprendizado de máquina supervisionado.

## 1. Sobre o projeto

O projeto foi desenvolvido a partir de uma demanda apresentada pela empresa Forno Nobre, que atua no setor de panificação, produção e distribuição de alimentos.

O demandante, Moacir, gerente de uma das filiais, é responsável por acompanhar os custos relacionados aos combustíveis utilizados nas atividades da unidade e repassar essas informações à administração da empresa.

A partir dessa necessidade, surgiu a proposta de desenvolver uma solução que permita organizar, analisar e visualizar informações sobre os preços dos combustíveis, além de utilizar modelos de regressão para estimar valores e auxiliar no planejamento.

O projeto contempla duas áreas da Ciência de Dados:

*Visualização de Dados:* organização, exploração e apresentação de informações por meio de análises, indicadores e visualizações.

*Aprendizado de Máquina Supervisionado:* desenvolvimento e avaliação de modelos de regressão capazes de estimar preços de combustíveis a partir das características disponíveis na base histórica.

## 2. Objetivos

### Objetivo geral

Desenvolver uma solução de inteligência de dados para apoiar o acompanhamento e o planejamento dos custos com combustíveis, utilizando dados públicos, técnicas de visualização e modelos de aprendizado de máquina supervisionado.

### Objetivos específicos

- Obter e organizar dados públicos de preços de combustíveis disponibilizados pela ANP.
- Realizar auditoria e análise da qualidade dos dados.
- Identificar e tratar inconsistências, duplicidades e valores ausentes.
- Estruturar uma base analítica para utilização nas análises.
- Explorar os dados por meio de estatísticas e visualizações.
- Analisar diferenças de preços entre produtos, localidades e períodos.
- Desenvolver um modelo de regressão para estimar preços de combustíveis.
- Comparar o desempenho do modelo com abordagens de referência (baselines).
- Avaliar os resultados por meio de métricas de erro e diagnóstico dos resíduos.
- Fornecer informações que possam auxiliar o acompanhamento dos preços e o planejamento financeiro da organização.

## 3. Fonte de dados

A principal fonte utilizada no projeto é a Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP), por meio de seus arquivos públicos de séries históricas de preços de combustíveis.

*Fonte oficial:* [Série Histórica de Preços de Combustíveis — ANP](https://www.gov.br/anp/pt-br/centrais-de-conteudo/dados-abertos/serie-historica-de-precos-de-combustiveis?utm_source=chatgpt.com)

*Período analisado:* janeiro de 2024 a junho de 2026.

Os dados apresentam informações relacionadas aos preços de revenda de combustíveis em diferentes localidades e períodos.

Os arquivos utilizados são públicos e não incluem informações financeiras internas ou registros individuais de abastecimento da empresa.

As orientações para localizar os dados utilizados estão disponíveis em:

dados_usados/onde_encontrar.txt

## 4. Auditoria e preparação dos dados

Inicialmente, foram obtidos os arquivos disponibilizados pela ANP. Em seguida, foi realizada uma exploração para identificar as características da base e possíveis problemas de qualidade.

Entre os procedimentos realizados, destacam-se:

- Verificação de registros duplicados.
- Identificação de valores ausentes.
- Verificação de valores inválidos.
- Padronização dos nomes das colunas.
- Adequação dos tipos de dados.
- Organização das informações temporais.
- Preparação das variáveis utilizadas na modelagem.

### Resultado da auditoria

| Descrição | Quantidade |
|---|---:|
| Registros iniciais | 2.134.685 |
| Registros finais | 2.125.555 |
| Registros removidos | 9.130 |

Entre os problemas identificados, destacam-se 9.129 registros duplicados e uma ocorrência removida por apresentar inconsistência relacionada à data ou ao preço.

Também foram identificadas variáveis com elevada quantidade de informações ausentes, como Valor de Compra e Complemento.

## 5. Visualização e análise dos dados

Na disciplina de Visualização de Dados, o projeto contempla a organização e apresentação das informações para facilitar a compreensão do comportamento dos preços dos combustíveis.

A exploração dos dados permite observar características da base, comparar categorias e localidades e identificar variações ao longo do período analisado.

As visualizações e análises exploratórias são apoiadas pela utilização de Python, Pandas e Matplotlib.

Os materiais gráficos disponíveis no repositório estão organizados na pasta:

docs/graficos/

## 6. Aprendizado de Máquina Supervisionado

O problema foi estruturado como uma tarefa de regressão, utilizando como variável-alvo o preço de venda do combustível, representado pela coluna valor_de_venda.

O primeiro modelo implementado foi uma Árvore de Decisão para Regressão (DecisionTreeRegressor).

### 6.1. Variáveis preditoras

*Variáveis categóricas:*

- Região (regiao_sigla)
- Estado (estado_sigla)
- Produto (produto)
- Bandeira (bandeira)
- Tipo de bandeira (tipo_bandeira)

*Variáveis numéricas:*

- Ano da coleta (ano_coleta)
- Mês da coleta (mes_coleta)

A preparação das variáveis foi organizada utilizando Pipeline e ColumnTransformer, com tratamento de valores ausentes, padronização de variáveis numéricas e codificação das variáveis categóricas por meio de OneHotEncoder.

### 6.2. Configuração do modelo

| Parâmetro | Configuração |
|---|---|
| Algoritmo | DecisionTreeRegressor |
| Profundidade máxima | 10 |
| Semente aleatória | 42 |
| Validação cruzada | TimeSeriesSplit |
| Número de divisões | 5 |

A configuração inicial não passou por uma busca automatizada de hiperparâmetros.

## 7. Particionamento e validação

Foi utilizada uma divisão cronológica dos dados, respeitando a ordem temporal dos registros.

| Conjunto | Proporção aproximada | Período |
|---|---:|---|
| Treinamento | 70% | 01/01/2024 a 01/10/2025 |
| Validação | 15% | 02/10/2025 a 16/02/2026 |
| Teste | 15% | 17/02/2026 a 30/06/2026 |

Também foi realizada validação cruzada temporal utilizando TimeSeriesSplit, com cinco divisões.

A avaliação final foi realizada no conjunto de teste, separado dos dados utilizados no treinamento.

## 8. Baselines

Foram utilizadas duas abordagens de referência para comparar o desempenho do modelo supervisionado.

*Baseline trivial:* utiliza a média da variável-alvo calculada a partir do conjunto de treinamento para gerar previsões constantes.

*Baseline operacional proposto:* utiliza a mediana histórica do preço de venda por estado e produto, calculada com os dados de treinamento, com uma referência global para situações sem correspondência.

O baseline operacional representa uma regra de referência proposta para o projeto, não um procedimento de previsão já utilizado pela empresa.

## 9. Avaliação dos resultados

Foram utilizadas duas métricas de avaliação:

- *MAE (Mean Absolute Error):* erro absoluto médio entre os valores reais e previstos.
- *RMSE (Root Mean Squared Error):* raiz do erro quadrático médio, que atribui maior peso aos erros mais elevados.

O MAE foi adotado como métrica principal por permitir interpretar diretamente a diferença média entre o preço estimado e o observado, em reais por litro.

### 9.1. Comparação dos modelos

Os resultados obtidos no conjunto de teste foram:

| Abordagem | MAE (R$/litro) | RMSE (R$/litro) |
|---|---:|---:|
| Baseline trivial | 1,1393 | 1,2593 |
| Baseline operacional proposto | 0,7124 | 0,8582 |
| Árvore de decisão | *0,5507* | *0,6993* |

A árvore de decisão apresentou desempenho superior aos dois baselines nas métricas utilizadas.

Em relação ao MAE, houve uma redução aproximada de 22,7% em comparação com o baseline operacional proposto e de 51,7% em comparação com o baseline trivial.

### 9.2. Validação cruzada temporal

Na validação cruzada temporal, o modelo apresentou:

| Indicador | Resultado |
|---|---:|
| MAE médio | R$ 0,2866/litro |
| Desvio-padrão do MAE | R$ 0,0638/litro |

O MAE obtido no conjunto de teste foi superior à média observada na validação cruzada, indicando dificuldades de generalização para determinados períodos posteriores ao treinamento.

### 9.3. Diagnóstico dos resíduos

A análise dos resíduos foi utilizada para identificar padrões de erro e observações com maiores diferenças entre os valores reais e estimados.

Considerando o resíduo como a diferença entre o valor real e o valor previsto, foram observados os seguintes resultados:

| Estatística | Resultado |
|---|---:|
| Média dos resíduos | 0,4502 |
| Mediana dos resíduos | 0,4099 |
| Desvio-padrão | 0,5351 |
| Maior erro absoluto | 3,7099 |

A predominância de resíduos positivos indica tendência de subestimação dos preços no conjunto de teste.

Uma das observações com maior erro apresentou preço real de R$ 9,99/litro e previsão aproximada de R$ 6,28/litro.

Esses resultados mostram que o modelo ainda apresenta limitações para representar determinadas variações de preços.

## 10. Limitações do projeto

Apesar dos resultados obtidos, algumas limitações precisam ser consideradas:

- Os dados representam preços de revenda pesquisados pela ANP, não necessariamente os valores efetivamente pagos pela empresa.
- A variável Valor de Compra apresenta 100% de valores ausentes na base auditada.
- O modelo utiliza informações geográficas e temporais gerais, sem identificar individualmente os estabelecimentos.
- As variáveis não contemplam informações específicas sobre consumo, rotas, abastecimentos e despesas da filial.
- O modelo utiliza ano e mês como características temporais, sem incorporar diretamente históricos recentes de preços.
- Embora a demanda original considere decisões com horizonte semanal, o modelo atual estima preços de registros individuais, não realizando uma previsão semanal propriamente dita.
- O desempenho no conjunto de teste foi inferior ao observado na validação cruzada.
- A configuração inicial da árvore de decisão não passou por otimização automatizada de hiperparâmetros.

Dessa forma, os resultados devem ser interpretados como uma ferramenta inicial de apoio à análise dos preços, não como garantia de economia ou previsão exata dos custos da organização.

## 11. Tecnologias utilizadas

| Tecnologia | Aplicação |
|---|---|
| Python | Linguagem principal do projeto |
| Pandas | Manipulação e análise dos dados |
| NumPy | Operações numéricas |
| Matplotlib | Construção de visualizações |
| Scikit-learn | Desenvolvimento e avaliação dos modelos |
| Jupyter Notebook | Desenvolvimento e execução das análises |
| ANP | Fonte pública dos dados |

## 12. Estrutura do repositório

A organização dos arquivos publicados segue a estrutura abaixo:

text
analise-de-combustiveis/
│
├── dados_usados/
│   └── onde_encontrar.txt
│
├── docs/
│   ├── graficos/
│   ├── E03_LeticiaSousa_MariaEduardaSouza_escuta_canvas (1).pdf
│   └── E04_LeticiaSousa_MariaEduardaSouza_dados_baseline.pdf
│
├── notebooks/
│   └── auditoria_dados.ipynb
│
├── .gitignore
│
└── README.md


A pasta dados_usados contém orientações relacionadas à obtenção dos dados utilizados.

A pasta docs reúne a documentação acadêmica e os materiais gráficos do projeto.

A pasta notebooks contém o notebook de auditoria, preparação, modelagem e avaliação.

## 13. Como executar o projeto

Para reproduzir as análises, é necessário possuir Python instalado e um ambiente capaz de executar notebooks Jupyter.

### 13.1. Clonar o repositório

bash
git clone https://github.com/M-Eduarda-Souza/analise-de-combustiveis.git


### 13.2. Acessar a pasta do projeto

bash
cd analise-de-combustiveis


### 13.3. Instalar as bibliotecas

bash
pip install pandas numpy matplotlib scikit-learn jupyter


Caso o notebook utilize bibliotecas adicionais, elas também deverão ser instaladas.

### 13.4. Obter os dados

Consultar o arquivo:

text
dados_usados/onde_encontrar.txt


Os arquivos originais podem ser obtidos na página de séries históricas de preços de combustíveis da ANP.

Antes de executar o notebook, é necessário disponibilizar os arquivos de dados nos caminhos utilizados pelas células de leitura.

Os arquivos devem preservar o formato esperado pelo código, incluindo o separador de colunas utilizado na leitura dos dados.

### 13.5. Executar o notebook

Na pasta do repositório, executar:

bash
jupyter notebook


Em seguida, abrir o arquivo:

text
notebooks/auditoria_dados.ipynb


Executar as células sequencialmente, desde a leitura dos dados até a avaliação do modelo.

*Observação:* a execução depende da disponibilidade dos arquivos originais da ANP e da correspondência entre os caminhos utilizados no notebook e a localização dos arquivos no ambiente de execução.

## 14. Documentação acadêmica

O repositório reúne documentos desenvolvidos ao longo das entregas do projeto.

*Entrega 3 — Escuta do demandante e Canvas de ML*

Documento referente ao levantamento da demanda, à identificação do problema e à estruturação inicial da proposta.

*Entrega 4 — Dados e baseline*

Documento referente à preparação dos dados, à auditoria e à construção das abordagens iniciais de referência.

*Entrega 5 — Pacote da Avaliação 1*

Relatório de consolidação da decisão, formulação, dados, partição, baselines, modelo supervisionado, avaliação, diagnóstico e limitações.

O relatório final da Entrega 5 deverá ser incluído na pasta docs após sua conclusão.

## 15. Possibilidades de evolução

Como continuidade do projeto, algumas melhorias podem ampliar a utilidade da solução:

- Desenvolver um painel interativo de BI para acompanhamento dos preços.
- Incorporar informações mais específicas sobre localidades e estabelecimentos.
- Testar outros algoritmos de regressão e realizar otimização de hiperparâmetros.
- Incorporar variáveis históricas para melhorar a capacidade de previsão temporal.
- Utilizar dados internos de abastecimento da Forno Nobre, caso haja autorização e disponibilidade.
- Desenvolver estimativas de despesas futuras a partir do histórico real de consumo da empresa.
- Comparar previsões com os valores efetivamente observados ao longo do tempo.

## 16. Equipe

Projeto desenvolvido por:

- Letícia Sousa
- Maria Eduarda Souza
- Marina Moraes

*Instituição:* Universidade Federal da Paraíba (UFPB).

*Curso:* Ciência de Dados para Negócios.

*Disciplinas:*
- Visualização de Dados.
- Aprendizado de Máquina Supervisionado.

*Período:* 2026.2.

## 17. Uso de Inteligência Artificial

Durante o desenvolvimento do projeto, foi utilizado o ChatGPT, da OpenAI, como ferramenta de apoio à organização das etapas do trabalho, à compreensão do funcionamento do modelo de aprendizado de máquina e à interpretação das exigências das entregas.

A ferramenta também auxiliou na identificação e correção de erros durante a implementação do código, além de contribuir para a organização e revisão dos textos e da documentação.

As sugestões fornecidas foram analisadas pela equipe, que permaneceu responsável pelas decisões tomadas, pela implementação e pela conferência dos resultados apresentados.

## 18. Referências

*Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP).* Série Histórica de Preços de Combustíveis. Disponível no portal oficial da ANP.

*Scikit-learn.* Machine Learning in Python. Documentação oficial.

*Pandas.* Python Data Analysis Library. Documentação oficial.

*Matplotlib.* Visualization with Python. Documentação oficial.

---

Projeto acadêmico desenvolvido para fins de estudo, análise de dados e aplicação de técnicas de aprendizado de máquina supervisionado.
