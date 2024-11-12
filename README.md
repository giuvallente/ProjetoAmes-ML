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

