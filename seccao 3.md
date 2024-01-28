# Secção 3
Para responder ao objetivo de avaliar a distribuição de subtipos de cancro, utilizou-se técnicas de aprendizagem super-visionada. Dessa forma, conseguimos analisar e comparar valores de previsão através de características como accuracy. Os modelos de aprendizagem que abordamos foram: KNN (K - Nearest Neighbors), árvores de decisão, SVM (Support Vector Machine), random forest e naive bayes.

Em relação às métricas de erro, usamos a cross validation, matriz de confusão, accuracy, precisão e sensibilidade.

#### Modelos de Aprendizagem super-visionada

O primeiro passo constituiu em separar os dados de entrada e saída, sendo os primeiros referentes a todas as colunas exceto as duas últimas e os dados de saída referentes a apenas a última coluna.
De seguida foi necessário dividir os nossos dados em treino(70%) e teste(30%). Decidimos construir um gráfico para visualizar a distribuição dos dados de treino, assim como imprimimos os seus valores.

O primeiro modelo de aprendizagem foi o KNN, o respetivo modelo tem como função a captura de padrões, nos dados de entrada, que posteriormente podem ser usados para realizar previsões ou tomar decisões sobre novos dados. Sempre que o realizamos acrescentamos um parâmetro de cálculo de accuracy e cross validation.

O segundo modelo foi o Decision Tree, a árvore de decisão divide o conjunto de dados com base nos diferentes subtypes,neste caso, selecionando o atributo que melhor separa os dados em subconjuntos mais homogéneos. Mais uma vez os cálculos de accuracy e cross validation foram executados.

O terceiro modelo de aprendizagem foi o Support Vector Machine (SVM), este, tem como objetivo encontrar o hiperplano de separação que melhor divide os pontos de dados das diferentes classes no espaço dimensional. À semelhança dos casos anteriores, calculou-se o cross validation.

O quarto modelo foi o Random Forest, uma técnica de ensemble que combina múltiplas árvores de decisão num único modelo mais robusto e geralmente mais preciso. Analogamente, determinamos o cross validation.

Por fim, analisamos o modelo Naive Bayes, um modelo que se baseia, como o nome indica, no teorema de Bayes, que descreve como calcular a probabilidade condicional de uma hipótese (classe) dado um conjunto de evidências. Neste caso, apenas a accuracy foi determinada.

Decidiu-se ainda, criar um novo modelo com base nos melhores modelos anteriormente testados, sendo eles Random Forest (0.729), Decision Tree (0.721) e o Naive Bayes(0.710). Obtendo assim, um valor de cross validation de 0.725, que não superou o maior valor registado de 0.729.

#### Métricas de Erro

As métricas de erro são utilizadas para avaliar o desempenho de modelos de aprendizagem pelos conjuntos de dados de teste. Elas fornecem uma medida quantitativa de quão bem o modelo está a realizar as suas previsões em relação aos valores reais.

Realizamos as seguintes métricas para todos os modelos: cross validation, matriz de confusão, accuracy, precisão e sensibilidade.

O cross validation (CV) é uma técnica usada para avaliar o desempenho de um modelo num conjunto de dados de teste, dividindo os dados em k partes iguais e treinando o modelo k vezes.
Já a matriz de confusão é a tabela que descreve o desempenho de um modelo de classificação, mostrando o número de verdadeiros positivos (TP), falsos positivos (FP), verdadeiros negativos (TN) e falsos negativos (FN). Para além disso, permite uma análise mais detalhada do desempenho do modelo, destacando as previsões corretas e os erros cometidos, no nosso caso, nos diferentes subtipos de cancro.
O cálculo da accuracy (Acc) reflete a proporção de previsões corretas feitas pelo modelo em relação ao total de previsões, fornecendo uma medida geral do quão bem o modelo está a classificar os dados corretamente, independentemente da label.
E por fim, a precisão e a sensibilidade (Recall). A primeira consiste na proporção de verdadeiros positivos (TP) em relação ao total de previsões positivas feitas pelo modelo (TP + FP). Enquanto que, a segunda refere-se à proporção de verdadeiros positivos (TP) em relação ao total de instâncias positivas reais na população (TP + FN).

#### Conclusão

Deste modo, podemos concluir que à semelhança do caso anterior, o modelo Random Forest foi o que obteve melhores resultados (CV: 0.73; Acc: 0.74; Precision: 0.78; Recall: 0.74), ou seja, é o melhor modelo para cumprir o nosso objetivo.

Porém, dado o número reduzido de dados com que os modelos foram treinados, não é possível assegurar a total fiabilidade do modelo que apresentou melhor desempenho.























