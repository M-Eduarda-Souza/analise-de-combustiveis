ANÁLISE DE PREÇOS DE COMBUSTÍVEIS

Projeto desenvolvido para as disciplinas de Visualização de Dados e Aprendizado de Máquina Supervisionado, do curso de Ciência de Dados para Negócios da Universidade Federal da Paraíba (UFPB).

1. SOBRE O PROJETO

O projeto surgiu a partir de uma demanda da empresa Forno Nobre, que trabalha com produção e distribuição de alimentos.

Atualmente, a filial acompanha os gastos com combustíveis por meio dos comprovantes de abastecimento dos motoristas, que são registrados nas planilhas de despesas. Entretanto, não existe um acompanhamento específico da variação dos preços.

A partir disso, nosso grupo decidiu trabalhar com os dados públicos da Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP), buscando analisar os preços dos combustíveis e desenvolver um modelo que possa auxiliar no acompanhamento desses valores.

O projeto também envolve a disciplina de Visualização de Dados, na qual trabalhamos com a exploração dos dados e a apresentação das informações por meio de gráficos e análises.

2. OBJETIVO

Nosso objetivo é analisar os preços dos combustíveis e desenvolver um modelo de regressão que consiga estimar os valores de venda a partir das informações disponíveis na base.

Além disso, buscamos identificar possíveis problemas nos dados, realizar os tratamentos necessários e comparar os resultados do modelo com métodos mais simples.

3. BASE DE DADOS

Utilizamos dados públicos disponibilizados pela ANP, referentes aos preços de revenda de combustíveis em diferentes regiões do Brasil.

O período considerado foi de janeiro de 2024 a junho de 2026.

Os dados podem ser encontrados na página de séries históricas de preços de combustíveis da ANP.

As orientações para localizar os arquivos utilizados estão disponíveis em:

dados_usados/onde_encontrar.txt

Como não tivemos acesso aos registros internos de abastecimento da empresa, utilizamos os dados da ANP como referência para o desenvolvimento do projeto.

4. AUDITORIA E PREPARAÇÃO DOS DADOS

Antes de desenvolver o modelo, realizamos uma auditoria para verificar a qualidade dos dados.

Nessa etapa, analisamos registros duplicados, valores ausentes, possíveis inconsistências, tipos das variáveis e organização das informações.

A base inicial apresentava 2.134.685 registros. Após os tratamentos, permanecemos com 2.125.555 registros, totalizando 9.130 remoções.

Desse total, 9.129 registros eram duplicados e um apresentava inconsistência relacionada à data ou ao preço.

Também identificamos variáveis com muitos valores ausentes, como Valor de Compra e Complemento.

Após a auditoria, organizamos as variáveis necessárias para a etapa de modelagem.

5. MODELO UTILIZADO

Para a primeira etapa de modelagem supervisionada, utilizamos uma Árvore de Decisão para Regressão (DecisionTreeRegressor).

A variável que buscamos estimar é o preço de venda do combustível, representado no código por valor_de_venda.

As variáveis utilizadas como entrada foram:

Região (regiao_sigla)

Estado (estado_sigla)

Produto (produto)

Bandeira (bandeira)

Tipo de bandeira (tipo_bandeira)

Ano da coleta (ano_coleta)

Mês da coleta (mes_coleta)

Para preparar essas variáveis, utilizamos Pipeline e ColumnTransformer, incluindo o tratamento de valores ausentes, a padronização das variáveis numéricas e a transformação das variáveis categóricas.

O modelo foi configurado com profundidade máxima igual a 10 e random_state igual a 42.

6. DIVISÃO DOS DADOS

Realizamos uma divisão temporal dos dados para separar os conjuntos de treinamento, validação e teste.

A divisão foi feita considerando aproximadamente 70% das datas para treinamento, 15% para validação e 15% para teste.

Os períodos ficaram organizados da seguinte forma:

Treinamento: 01/01/2024 a 01/10/2025.

Validação: 02/10/2025 a 16/02/2026.

Teste: 17/02/2026 a 30/06/2026.

Também utilizamos validação cruzada temporal com cinco divisões, por meio do TimeSeriesSplit.

7. BASELINES

Para avaliar o desempenho do modelo, utilizamos duas abordagens de referência.

O primeiro baseline foi o trivial, que utiliza a média dos preços do conjunto de treinamento como previsão.

O segundo foi um baseline operacional proposto pelo grupo, utilizando a mediana histórica dos preços por estado e produto.

Essa segunda abordagem foi construída como uma referência para o projeto, não sendo um método já utilizado pela empresa.

Os dois baselines foram comparados com a árvore de decisão no mesmo conjunto de teste.

8. RESULTADOS

Para avaliar os resultados, utilizamos o MAE como métrica principal e o RMSE como métrica complementar.

Os resultados encontrados no conjunto de teste foram:

Baseline trivial:
MAE: 1,1393
RMSE: 1,2593

Baseline operacional:
MAE: 0,7124
RMSE: 0,8582

Árvore de decisão:
MAE: 0,5507
RMSE: 0,6993

A árvore de decisão apresentou os menores erros entre as três abordagens.

Em comparação com o baseline operacional, o modelo apresentou uma redução de aproximadamente 22,7% no MAE. Em relação ao baseline trivial, a redução foi de aproximadamente 51,7%.

Na validação cruzada temporal, encontramos um MAE médio de 0,2866, com desvio-padrão de 0,0638.

Entretanto, o resultado obtido no conjunto de teste foi inferior ao observado durante a validação cruzada, mostrando que o modelo ainda apresenta dificuldades para estimar os preços em determinados períodos.

9. ANÁLISE DOS ERROS

Também realizamos uma análise dos resíduos para observar as diferenças entre os preços reais e os valores estimados.

Os resultados encontrados foram:

Média dos resíduos: 0,4502.

Mediana dos resíduos: 0,4099.

Desvio-padrão: 0,5351.

Maior erro absoluto: 3,7099.

Observamos que o modelo apresentou uma tendência de estimar preços abaixo dos valores reais no conjunto de teste.

Um dos maiores erros ocorreu em um registro com preço real de R$ 9,99 e valor estimado de aproximadamente R$ 6,28.

Esses resultados mostram que, apesar de superar os baselines, o modelo ainda precisa de melhorias.

10. LIMITAÇÕES

Uma das principais limitações é que utilizamos dados nacionais da ANP, que não representam necessariamente os preços pagos pela empresa.

Além disso, o modelo não considera informações específicas da filial, como consumo dos veículos, quantidade de combustível utilizada, rotas e despesas reais de abastecimento.

Outra limitação é que o modelo utiliza características gerais dos registros, como localização, produto e período da coleta, sem considerar diretamente os preços observados nas semanas anteriores.

Embora a demanda inicial envolva o acompanhamento semanal dos preços, o modelo desenvolvido nesta etapa estima valores de registros individuais e ainda não realiza uma previsão específica para a semana seguinte.

Por isso, entendemos que os resultados representam uma primeira etapa do projeto e que o modelo ainda não deve ser utilizado como única referência para decisões de abastecimento.

11. FERRAMENTAS UTILIZADAS

Durante o desenvolvimento do projeto, utilizamos:

Python, para trabalhar com os dados e desenvolver o modelo
