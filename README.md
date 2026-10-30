⛽ Inteligência de Dados para Gestão e Previsão de Preços de Combustíveis

Projeto acadêmico interdisciplinar desenvolvido para as disciplinas de Visualização de Dados e Aprendizado de Máquina Supervisionado, da Universidade Federal da Paraíba (UFPB).

O projeto tem como objetivo desenvolver uma solução de apoio à tomada de decisão para a gestão e o acompanhamento dos preços de combustíveis, utilizando dados públicos da Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP), técnicas de análise e visualização de dados e modelos de aprendizado de máquina supervisionado.

📌 Sobre o projeto

O projeto foi desenvolvido a partir de uma demanda apresentada pela empresa Forno Nobre, que atua no setor de panificação, produção e distribuição de alimentos.

O demandante, Moacir, gerente de uma das filiais, é responsável por acompanhar os custos relacionados aos combustíveis utilizados nas atividades da unidade e repassar essas informações ao proprietário e CEO da empresa, Jader.

A partir dessa necessidade, surgiu a proposta de desenvolver uma solução que permita organizar, analisar e visualizar informações sobre os preços dos combustíveis, além de utilizar modelos preditivos para estimar valores e auxiliar no planejamento.

A solução integra duas áreas da Ciência de Dados:

Visualização de Dados: organização, exploração e apresentação de informações por meio de análises, indicadores e visualizações que facilitem a interpretação dos dados.

Aprendizado de Máquina Supervisionado: desenvolvimento e avaliação de modelos de regressão capazes de estimar preços de combustíveis a partir de características disponíveis na base histórica.

🎯 Objetivos

Objetivo geral

Desenvolver uma solução de inteligência de dados para apoiar o acompanhamento e o planejamento dos custos com combustíveis, utilizando dados públicos, técnicas de visualização e modelos de aprendizado de máquina supervisionado.

Objetivos específicos

Obter e organizar dados públicos de preços de combustíveis disponibilizados pela ANP.

Realizar auditoria e análise da qualidade dos dados.

Identificar e tratar inconsistências, duplicidades e valores ausentes.

Estruturar uma base analítica para utilização nas análises.

Explorar os dados por meio de estatísticas e visualizações.

Desenvolver uma estrutura de análise que facilite a interpretação da variação dos preços.

Construir modelos de regressão para estimar preços de combustíveis.

Comparar o desempenho dos modelos com abordagens de referência (baselines).

Avaliar os resultados por meio de métricas de erro e diagnóstico dos resíduos.

Fornecer informações que possam auxiliar o acompanhamento dos preços e o planejamento financeiro da organização.

🗂️ Fonte de dados

A principal fonte utilizada no projeto é a Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP), por meio de seus arquivos públicos de séries históricas de preços de combustíveis.

Fonte oficial:

https://www.gov.br/anp/pt-br/centrais-de-conteudo/dados-abertos/serie-historica-de-precos-de-combustiveis

Os dados apresentam informações relacionadas aos preços de revenda de combustíveis em diferentes localidades e períodos, permitindo realizar análises sobre o comportamento dos preços ao longo do tempo.

Período analisado: janeiro de 2024 a junho de 2026.

Os dados utilizados são públicos e não incluem informações financeiras internas ou registros individuais de abastecimento da empresa.

🔎 Etapas de desenvolvimento

O desenvolvimento do projeto foi organizado em etapas, desde a obtenção dos dados até a avaliação dos resultados do modelo.

1. Obtenção e exploração dos dados

Inicialmente, foram obtidos os arquivos disponibilizados pela ANP. Em seguida, foi realizada uma exploração inicial para compreender a estrutura da base, suas dimensões, variáveis, tipos de dados e características gerais.

2. Auditoria e preparação dos dados

Foi realizada uma auditoria para identificar problemas de qualidade e preparar a base para as análises e a modelagem.

Entre os procedimentos realizados, destacam-se:

Verificação de registros duplicados.

Identificação de valores ausentes.

Verificação de valores inválidos.

Padronização dos nomes das colunas.

Adequação dos tipos de dados.

Organização das informações temporais.

Preparação das variáveis utilizadas na modelagem.

Resultado da auditoria:

Descrição

Quantidade

Registros iniciais

2.134.685

Registros finais

2.125.555

Registros removidos

9.130

Entre os problemas identificados, destacam-se 9.129 registros duplicados e uma ocorrência removida por apresentar inconsistência relacionada à data ou ao preço.

Também foram identificadas variáveis com elevada quantidade de informações ausentes, como Valor de Compra e Complemento.

3. Visualização e análise dos dados

Na disciplina de Visualização de Dados, o projeto contempla a organização e apresentação das informações para facilitar a compreensão do comportamento dos preços dos combustíveis.

A exploração dos dados permite observar características da base, comparar categorias e localidades e identificar variações ao longo do período analisado.

As visualizações e análises exploratórias são apoiadas pela utilização de Python, Pandas e Matplotlib.

A proposta de aplicação é transformar os dados em informações úteis para o acompanhamento dos preços e a elaboração de análises que apoiem as decisões da organização.

4. Desenvolvimento do aprendizado de máquina supervisionado

Na disciplina de Aprendizado de Máquina Supervisionado, foi desenvolvido um problema de regressão, utilizando como variável-alvo o preço de venda do combustível (valor_de_venda).

O primeiro modelo implementado foi o Decision Tree Regressor (Árvore de Decisão para Regressão).

Foram utilizadas como variáveis preditoras:

Variáveis categóricas:

Região (regiao_sigla);

Estado (estado_sigla);

Produto (produto);

Bandeira (bandeira);

Tipo de bandeira (tipo_bandeira).

Variáveis numéricas:

Ano da coleta (ano_coleta);

Mês da coleta (mes_coleta).

A preparação das variáveis foi organizada utilizando Pipeline e ColumnTransformer, com imputação de valores ausentes e codificação das variáveis categóricas por meio de OneHotEncoder.

Configuração do modelo:

Algoritmo: DecisionTreeRegressor.

Profundidade máxima: 10 (max_depth=10).

Semente aleatória: 42 (random_state=42).

5. Particionamento e validação

Para avaliar o desempenho do modelo de acordo com a ordem temporal dos registros, foi utilizada uma divisão cronológica dos dados:

Treinamento: 70%.

Validação: 15%.

Teste: 15%.

Também foi realizada validação cruzada temporal utilizando TimeSeriesSplit, com cinco divisões.

Esse procedimento permite avaliar o comportamento do modelo em diferentes períodos, respeitando a sequência temporal dos dados e evitando a utilização de informações futuras no treinamento.

6. Avaliação dos modelos

Foram utilizadas abordagens de referência (baselines) para estabelecer parâmetros de comparação com o modelo supervisionado.

As métricas utilizadas foram:

MAE (Mean Absolute Error): mede o erro absoluto médio entre os valores reais e previstos.

RMSE (Root Mean Squared Error): mede a raiz do erro quadrático médio, atribuindo maior peso aos erros mais elevados.

Também foi realizado o diagnóstico dos resíduos, permitindo observar a distribuição dos erros e identificar possíveis tendências de superestimação ou subestimação dos preços.

📊 Resultados obtidos

Na avaliação realizada sobre o conjunto de teste, foram obtidos os seguintes resultados:

Modelo

MAE (R$)

RMSE (R$)

Baseline trivial

1,1393

1,2593

Baseline operacional

0,7124

0,8582

Árvore de decisão

0,5507

0,6993

Os resultados indicam que a árvore de decisão apresentou desempenho superior aos dois baselines utilizados, considerando as métricas MAE e RMSE.

Na validação cruzada temporal, o modelo apresentou:

MAE médio: R$ 0,2866.

Desvio-padrão: R$ 0,0638.

Entretanto, o desempenho no conjunto de teste foi inferior ao observado na validação cruzada, indicando que o modelo ainda apresenta dificuldades para acompanhar determinadas variações dos preços em períodos posteriores ao treinamento.

Esses resultados reforçam a importância de avaliar o modelo em dados que representem períodos futuros e de considerar suas limitações antes de utilizá-lo em decisões operacionais.

⚠️ Limitações do projeto

Apesar dos resultados obtidos, algumas limitações precisam ser consideradas:

Os dados utilizados representam preços de revenda pesquisados pela ANP e não necessariamente os valores efetivamente pagos pela empresa.

A variável Valor de Compra apresenta 100% de valores ausentes na base auditada.

O modelo utiliza informações geográficas e temporais gerais, sem identificar individualmente os estabelecimentos.

As variáveis utilizadas não contemplam informações específicas sobre consumo, rotas, abastecimentos e despesas da filial.

O modelo utiliza ano e mês como características temporais, sem incorporar diretamente tendências recentes ou históricos de preços anteriores.

O desempenho apresentou redução no conjunto de teste em comparação com a validação cruzada.

A configuração inicial da árvore de decisão não passou por uma busca automatizada de hiperparâmetros.

Dessa forma, os resultados devem ser interpretados como uma ferramenta inicial de apoio à análise dos preços, não como garantia de economia ou previsão exata dos custos da organização.

🛠️ Tecnologias e ferramentas

As principais tecnologias utilizadas no desenvolvimento e na análise dos dados são:

Tecnologia

Aplicação

Python

Linguagem principal do projeto

Pandas

Manipulação e análise dos dados

NumPy

Operações numéricas

Matplotlib

Construção de visualizações

Scikit-learn

Desenvolvimento e avaliação dos modelos de aprendizado de máquina

Jupyter Notebook

Desenvolvimento, documentação e execução das análises

ANP

Fonte pública dos dados

📁 Estrutura do projeto

A organização do repositório segue a seguinte estrutura proposta:

projeto-combustiveis/
│
├── dados/
│   ├── bruto/
│   │   └── arquivos_originais_ANP.csv
│   │
│   └── processado/
│       └── base_tratada.csv
│
├── notebooks/
│   └── auditoria_dados_corrigido.ipynb
│
├── docs/
│   └── relatorios_e_documentacao/
│
├── src/
│   └── funcoes.py
│
├── README.md
│
└── requirements.txt

A estrutura apresenta a organização dos arquivos do projeto. Os nomes dos arquivos e diretórios devem corresponder aos efetivamente presentes no repositório.

▶️ Como executar o projeto

Para reproduzir as análises, é necessário possuir Python instalado e um ambiente capaz de executar notebooks Jupyter.

1. Clonar o repositório

git clone URL_DO_REPOSITORIO

2. Entrar na pasta do projeto

cd projeto-combustiveis

3. Instalar as bibliotecas necessárias

pip install pandas numpy matplotlib scikit-learn jupyter

4. Disponibilizar os dados

Os arquivos CSV originais da ANP devem ser colocados na pasta:

dados/bruto/

Os arquivos devem manter o formato esperado pelo notebook, incluindo o separador de colunas utilizado na leitura dos dados (;).

5. Executar o notebook

jupyter notebook

Em seguida, abrir o notebook de auditoria e modelagem disponível na pasta notebooks/ e executar as células sequencialmente.

Observação: a execução depende da disponibilidade dos arquivos de dados originais ou de suas versões processadas, conforme os caminhos utilizados no notebook.

🔮 Possibilidades de evolução

Como continuidade do projeto, algumas melhorias podem ampliar a utilidade da solução:

Desenvolver um painel interativo de BI para acompanhamento dos preços.

Incorporar informações mais específicas sobre localidades e estabelecimentos.

Testar outros algoritmos de regressão e realizar otimização de hiperparâmetros.

Incorporar variáveis históricas para melhorar a capacidade de previsão temporal.

Utilizar dados internos de abastecimento da Forno Nobre, caso haja autorização e disponibilidade.

Desenvolver estimativas de despesas futuras a partir do histórico real de consumo da empresa.

Comparar previsões com os valores efetivamente observados ao longo do tempo.

👥 Equipe

Projeto desenvolvido por:

Letícia Sousa

Maria Eduarda Souza

Marina Moraes

Instituição: Universidade Federal da Paraíba (UFPB)

Disciplinas:

Visualização de Dados.

Aprendizado de Máquina Supervisionado.

Período: 2026.2

📚 Referências

AGÊNCIA NACIONAL DO PETRÓLEO, GÁS NATURAL E BIOCOMBUSTÍVEIS (ANP). Série Histórica de Preços de Combustíveis. Disponível em: https://www.gov.br/anp/pt-br/centrais-de-conteudo/dados-abertos/serie-historica-de-precos-de-combustiveis.

SCIKIT-LEARN. Machine Learning in Python. Documentação oficial. Disponível em: https://scikit-learn.org/.

PANDAS. Python Data Analysis Library. Documentação oficial. Disponível em: https://pandas.pydata.org/.

MATPLOTLIB. Visualization with Python. Documentação oficial. Disponível em: https://matplotlib.org/.

Projeto acadêmico desenvolvido para fins de estudo, análise de dados e aplicação de técnicas de aprendizado de máquina supervisionado.
