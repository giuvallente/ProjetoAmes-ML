# Machine Learning - Projeto Ames 

Este projeto tem como objetivo a construção de uma regressão sobre o dataset Ames, para além da leitura de dados e preparação simples destes.

Abaixo segue a descrição dos notebooks que compõem o projeto:

### 01. Download e Leitura do Dataset Ames

O notebook `01-LeituraDados.ipynb` contém o código para baixar e ler o dataset Ames. 

O dataset Ames é um conjunto de dados que contém informações sobre casas vendidas em Ames, Iowa, sendo constituído por 80 variáveis, as quais podem ser divididas em 3 categorias: condições dos arredores da casa, lista de características da casa e informações sobre a venda. 

Assim, neste arquivo, além de realizar o download do dataset também é realizada a transformação das variáveis categóricas em variáveis numéricas, por exemplo, a variável `Fence` que contém informações sobre o tipo de cerca da casa, foi transformada em 4 variáveis numéricas - uma para cada tipo de cerca e com uma ordem pré definida.

A transformação das variáveis categóricas em numéricas é essencial para modelos de aprendizado de máquina que não conseguem interpretar variáveis categóricas diretamente. 

Assim, transformar variáveis como `Fence` em múltiplas colunas numéricas também permite que o modelo considere a presença ou ausência de cada categoria individualmente, o que pode melhorar a interpretação e a precisão do modelo.

### 02. Análisde e Pré-processamento do Dataset Ames

O notebook `02-AnáliseDados.ipynb` contém a análise e pré-processamento do dataset Ames.

Afim de realizar o processamente do datset Ames, realizamos uma análise de praticamente todas as features que compõem nossos dados. Para isso, iniciamos pela análise das variáveis categóricas. 

O processamento das variáveis categóricas pode ser realizado de algumas formas, como:

- Remover as categorias minoritárias e registrar que o modelo desenvolvidonão é adequado para processar determinadas categorias.
- Agrupar as categorias minoritárias em uma nova categoria chamada Outros, indicando que não estamos ignorando essas propriedades, mas que não há evidências suficientes para inferir o efeito das categorias minoritárias específicas sobre o preço de venda.
- Eliminar colunas que contêm baixa variação.
- Atribuir todos os valores ausentes a uma categoria recém-criada chamada Desconhecido.

A primeira forma de processamento - a remoção de categorias minoritárias - foi utilizada para as colunas `MS.ZONING`, `STREET` e `NEIGHBORHOOD`. Assim, nosso modelo não se aplica a propriedades não residenciais, ruas de cascalho e os bairros: Blueste, Greens, GrnHill e Landmrk.

Já a segunda forma - agrupar as categorias minoritárias em uma nova categoria chamada Outros - foi utilizada para as colunas `SALE.TYPE`, `SALE.CONDITION`, `MAS.VNR.TYPE`, `MS.SUB.CLASS`, `FOUNDATION` e `ROOF.STYLE`. Para a categoria `MAS.VNR.TYPE`, também foi criada uma categoria para casas sem revestimento.

A terceira forma - eliminar colunas que contêm baixa variação - foi utilizada para as colunas `HEATING` e `ROOF.MATL`.

A quarta forma - atribuir todos os valores ausentes a uma categoria recém-criada chamada Desconhecido - foi utilizada para as colunas `GARAGE.TYPE`, a qual recebeu a categoria `No Garage` para casas sem garagem.

Além disso, as colunas `CONDITION.1` e `CONDITION.2` foram combinadas em uma única coluna, `CONDITION`, e as colunas `EXTERIOR.1st` e `EXTERIOR.2nd` foram combinadas em uma única coluna, `EXTERIOR`, com as categorias menos utilizadas agrupadas em uma única categoria.

Por último, as colunas `MISC. FEATURES` e `ALLEY` foram transformadas em colunas de booleanos, que recebem verdadeiro se a casa possui um galpão ou se está em um beco, respectivamente.

Já o processamento de variáveis ordinais pode ser realizado com algumas técnicas semelhantes, como:

- Eliminar colunas que contêm baixa variação.
- Eliminar colunas que contêm baixa adesão de respostas.
- Atribuir todos os valores ausentes a uma categoria recém-criada chamada Desconhecido.

A primeira forma - eliminar colunas que contêm baixa variação - foi utilizada para as colunas `UTILITIES`, `FIREPLACE.QU`, `GARAGE.COND` e `GARAGE.QUAL`.

A segunda forma - eliminar colunas que contêm baixa adesão de respostas - foi utilizada para a coluna `POOL.QC`.

Já a terceira forma - atribuir todos os valores ausentes a uma categoria recém-criada chamada Desconhecido - foi utilizada para a coluna `FENCE`.

Por fim, as colunas `GARAGE.FINISH`, `BSMT.COND`, `BSMT.QUAL`, `BSMT.EXPOSURE`, `BSMT.FIN.TYPE.1` e `BSMT.FIN.TYPE.2` foram transformadas em colunas nominais, com a categoria `NO GARAGE` para casas sem garagem e `NA` para as casas que não obtivémos resposta acerca do porão ou da existência deste.

A última etapa do processamento é a análise das variáveis contínuas. 

Para esta última etapa realizamos algumas verificações como: a coluna `GARAGE.YR.BLT` possuía como valores anos futuros à coleta dos dados para este dataset, então criamos uma nova coluna chamada `GARAGE.AGE` que representa a idade da garagem e preenchemos os valores faltantes com a média. Realizamos o mesmo procedimento para as colunas `YEAR.BUILT` e `YEAR.REMOD.ADD`, criando as colunas `HOUSE.AGE` e `REMOD.AGE`, respectivamente.

Além disso, a coluna `SALES.PRICE` foi transformada em logaritmo na base 10. 

Por fim, a coluna `LOT.FRONTAGE` foi preenchida com a média e a coluna `MAS.VNR.AREA` foi preenchida com zero, já que os valores faltantes representam as casas que não possuem uma área do revestimento de alvenaria na fachada da casa.

### 03. Análise dos Modelos de Predição do Valor de Venda das Casas do Dataset Ames

O notebook `03-ModelosPredicao.ipynb` contém dois modelos de predição do valor de venda das casas do dataset Ames, o modelo `Random Forest` e o modelo `Ridge`.

O primeiro passo para a construção dos modelos foi identificar todas as variáveis categóricas. Assim, as variáveis categóricas nominais - categóricas sem ordem entre as categoria - foram transformadas em variáveis dummy, ou seja, cada categoria foi transformada em uma coluna binária. Já as variáveis categóricas ordinais - categóricas com ordem entre as categorias - foram transformadas em variáveis numéricas, com as categorias recebendo valores inteiros de acordo com a ordem.

Em seguida, realizamos a divisão do dataset em treino e teste, com 75% dos dados sendo utilizados para treino e 25% para teste.

Então, podemos iniciar a construção dos modelos. Para ambos os modelos realizamos o ajuste dos hiperparâmetros utilizando a técnica de `Grid Search`, que consiste em testar todas as combinações possíveis de hiperparâmetros e escolher a combinação que resulta no melhor desempenho do modelo, além de evitar o overfitting.	

Assim, para o modelo `Random Forest` ajustamos os hiperparâmetros `n_estimators` e `max_depth`. Já para o modelo `Ridge` ajustamos o hiperparâmetro `alpha`.

Desta forma, escolhemos o modelo que obteve como `scoring` o maior valor de `neg_mean_squared_error`, visto que o objetivo do modelo é minimizar o erro quadrático médio (MSE). Assim, o modelo `Ridge` com o hiparâmetro `alpha` igual a 100 foi o escolhido.

Por fim, treinamos o modelo escolhido com todos os dados de treino e realizamos a predição do valor de venda das casas do dataset Ames, o que nos resultou em um erro quadrático médio de 0.0038.

### Conclusões Finais

O modelo de regressão Ridge foi o escolhido para a predição do valor de venda das casas do dataset Ames, com um erro quadrático médio de 0.0038. 

Assim, o modelo mostra um desempenho razoavelmente bom. O MSE indica o quão distante, em média, as previsões do modelo estão dos valores reais, e um valor mais baixo sugere um modelo mais preciso.

Desta forma, podemos trazer como consequências do desempenho do modelo final para a aplicação de negócios o fato das previsões de preço poderem estar relativamente próximas dos valores reais, o que pode ser útil para agentes imobiliários, avaliadores ou investidores ao tentar estimar o valor de venda das casas. Contudo, um MSE de 0.0038 indica que o modelo tem uma tendência a errar um pouco, o que pode levar a subestimações ou superestimações do preço de venda das casas. Em negócios, isso pode afetar a confiança dos clientes ou investidores, além de afetar a estratégia de precificação.

Por fim, podemos também obter uma maior noção acerca de quais variáveis trazem um maior impacto no valor de venda das casas. Assim, o nosso modelo escolhido revela que a variável `OVERALL.QUAL` é a que mais impacta no valor de venda das casas, seguida pelas variáveis `GR.LIV.AREA` e `OVERALL.COND`. Além disso, também podemos colocar a prova, por exemplo, que quanto mais velha for a casa, menor será o seu valor de venda.

### Autores

Giúlia Gomes Vallente <br>
Julia Almeida Silva <br>



