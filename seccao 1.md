Este projeto possui um conjunto de dados genómicos e dados ómicos de amostras de pacientes com cancro, dados estes que pretendemos analisar com base no conteúdo lecionado.

# SECÇÃO 1

Nesta etapa, foi necessário entender o objetivo do estudo, bem como as diversas variáveis presentes, para aplicar o pré-processamento adequado.
Primeiramente, converteu-se a variável "Hugo_Symbol" como index da nossa tabela de dados, ao invés da numeração inicial das linhas, e procedeu-se à eliminação da coluna "Entrez_Gene_ID" porque não se justificava ter 2 atributos referentes a "Id" dos genes. De seguida, com recurso à função "dropna", eliminou-se as linhas que apresentavam pelo menos um missing value.

Aqui, optou-se por eliminar apenas as linhas e não as colunas, uma vez que estas últimas são referentes às amostras do estudo. Posteriormente, retirou-se os duplicados existentes nas colunas. A realização deste passo levou à necessidade de tirar a variável "Hugo_Symbol" como index. Foi possível verificar que não existiam duplicados, uma vez que o número de colunas de manteve igual. Por fim, confirmou-se a inexistência de valores nulos.


No que diz respeito aos metadados, temos 2 ficheiros, 1 referente aos pacientes e outro referente às amostras. Primeiramente, aplicou-se o pré-processamento ao ficheiro dos pacientes. 
Numa etapa inicial, selecionou-se apenas as linhas a partir da 5º posição e definiu-se os nomes das colunas com base nos valores presentes na 4º linha. A esta nova tabela, aplicou-se a função “describe”, de modo a observar as estatísticas descritivas do dataframe.  
Assim, para cada coluna observou-se informações relativas: à contagem dos valores dessa variável; ao número de valores únicos; ao valor mais verificado (moda); e a frequência com que a moda aparece.

Seguidamente, realizou-se algumas etapas de pré-processamento similares às do primeiro ficheiro. De forma a retirar os missing values, recorreu-se, uma vez mais, à função “dropna”. Contudo, neste caso, a eliminação diz respeito às colunas que apresentassem todos os seus valores como NaN. 
Para além disso, percebeu-se que a coluna “DAYS_TO_INITIAL_PATHOLOGIC_DIAGNOSIS” continha todos os seus valores a zero, logo procedeu-se à sua eliminação. Posteriormente, analisou-se a presença de colunas repetidas. 

Observando atentamente, foi possível confirmar que as colunas “OS_MONTHS” e “DSS_MONTHS” eram iguais. Dado o extenso número de linhas e a dificuldade em analisar todas elas, construiu-se um ciclo if, no qual caso se verifique que efetivamente as colunas são iguais, elimina-se a “DSS_MONTHS”. 
Por último, apagou-se as colunas que apresentavam todos os valores iguais, uma vez que não fornecem informação variada. Para o caso em estudo, variáveis que não apresentem variações nos seus valores não são relevantes, pois não introduzem informação que permita tirar conclusões.
Importante notar que o número de linhas se manteve intacto e que apenas se eliminou colunas. Isto porque as linhas são variáveis únicas relativas ao ID do paciente e não queremos reduzir o número de doentes em estudo. Já as colunas dizem respeito a variáveis em análise, sendo que aquelas que não possuem informação útil são eliminadas.


Passando para o ficheiro relativo às amostras, também aqui se selecionou apenas a informação a partir da 5º linha (inclusive) e moveu-se a informação da 3º linha para colunas, tendo-se renomeado as mesmas. De forma análoga ao ficheiro anterior, aplicou-se a função “describe” para serem geradas as estatísticas descritivas do dataframe. 
De seguida, aplicou-se a função “dropna” para eliminar eventuais colunas com missing values, mas tais não existiam. Para além disso, foi-se verificar as colunas que apresentavam todos os valores iguais, procedendo-se à respetiva eliminação. 


A etapa seguinte consistiu na união dos 2 ficheiros de metadados: data_patient e data_sample. Tal como esperado, o número de linhas final não apresentou variações, pois as informações contidas nestas são iguais nas duas tabelas (Patient Identifier). 
Ora, como o index da tabela era o “Patient Identifier” e a 1º coluna era o “Sample_ID” e ambas são variáveis únicas, não se justifica possuir duas colunas com informação semelhante. Assim, optou-se por colocar a “Sample_ID” como index e retirar a coluna “Patient Identifier”. 
Esta substituição não levou a perda de nenhuma informação, pois através do ID único de cada amostra é possível associar o doente correspondente, que também contêm um ID único. 
Seguidamente, recorreu-se à função “loc” para comparar o ficheiro resultante da união com o ficheiro dos dados, de modo a obter apenas as colunas que se encontram neste último (data). Tal permite manter as informações coincidentes. 


A última etapa desta secção tinha como intuito selecionar algumas variáveis relevantes para a análise e gerar alguns gráficos que ilustrassem as principais características dos dados e metadados. Deste modo, as variáveis escolhidas foram: Subtype, Grade, Age e DFS_Status (Disease Free Status). 
A primeira é referente aos subtipos de cancro existentes e que, portanto, podem ser diagnosticados nos pacientes analisados. Por sua vez, a segunda variável avalia o grau do cancro, auxiliando nas conclusões sobre qual o grau mais comum e os motivos para tais. Já a variável “Age” dá uma noção das faixas etárias mais suscetíveis ao desenvolvimento desta doença, podendo-se levantar a questão do porquê de tal se verificar. 
Por último, escolheu-se a variável “Disease Free Status” para perceber os casos de sucesso de tratamento e a percentagem de doentes reincidentes. Contudo, antes de criarmos alguns gráficos que permitam retirar conclusões, teve-se de garantir que as variáveis selecionadas têm o pré-processamento adequado.

Assim, começando pela variável “Subtype” fomos verificar a existência de valores nulos. 
A função aplicada nesta etapa retornou um total de 20 valores nulos, tendo-se posteriormente eliminado os mesmos. Analogamente, analisou-se as restantes variáveis selecionadas, eliminando-se os valores nulos caso estes existissem. 

Concluído este passo, construiu-se um gráfico de cores para a variável “Subtype”, onde se comprovou que o subtipo de cancro mais comum é o 'UCEC_CN_LOW', contrariamente ao 'UCEC_POLE’, que é o menos verificado. De forma similar à anterior, construiu-se um gráfico para a variável “Grade”, de onde se conclui que o grau mais constatado é o G3 e que o menos constatado é o High Grade.

Ora, atendendo à lógica dos gráficos obtidos, tentou-se aplicar a mesma à variável “Age”. Porém, dado a imensa diversidade de dados, o gráfico mostrou-se pouco conclusivo e bastante confuso. Como tal, decidiu-se que dividir a variável idade em intervalos de tempo e recorrer a um gráfico de barras para obter resultados mais conclusivos. Durante esta etapa, foi ainda necessário converter a variável em análise para inteiro, pois esta encontrava-se como “object”. 
Feitas as devidas alterações através da função “astype”, construiu-se então o gráfico para as seguintes faixas etárias: [0,25], [25,40], [40,65], [65, 100]. O resultado obtido, apresentava uma das faixas etárias sem valores e as restantes bastante concentradas. Assim, decidiu-se reajustar os intervalos escolhidos, tendo-se obtido um gráfico com uma melhor distribuição.
A partir deste, foi possível verificar que os pacientes do estudo se encontram maioritariamente na faixa etária dos 50 anos aos 65 anos. 

Por sua vez, para a variável “DFS_STATUS”, comprovou-se que a quantidade de pessoas que se tornam reincidentes no cancro são muito menores do que aquelas que ficaram completamente tratadas. 

Ora, após a análise de cada uma desta variáveis individualmente, optou-se por gerar outros gráficos, nos quais poderíamos comparar vários parâmetros e retirar outras conclusões importantes através das suas conexões.

O primeiro escolhido compara o grau da doença com o “Disease Free Status”. Analisando atentamente, pode-se afirmar que o grau 3 é o que apresenta mais doentes tratados com sucesso, mas também é o grau que apresenta maior reincidência. Tal pode ser justificado pelo facto de o G3 ter sido o grau mais verificado na análise do gráfico feito anteriormente. 

De seguida, comparou-se o “Disease Free Status” com a Idade. Observando os resultados, constata-se que a faixa etária dos 30 anos aos 40 anos não apresenta reincidência após tratamento. Para além disso, a faixa etária com mais sucesso nos tratamentos, mas também com maior reincidência é a dos 50 anos aos 65 anos. 
Uma vez mais, tal pode ser justificado dado a maioria dos pacientes ter idades contidas nesse intervalo.

Optou-se ainda por criar um gráfico relativo ao subtipo e ao grau. 
Os resultados obtidos demonstram que: para o subtipo “UCEC_CN_HIGH” o G3 é o que apresenta maior incidência; para o subtipo “UCEC_CN_LOW” é o grau 1 o mais verificado; já no subtipo “USEC_MSI” foi o grau 3; e por último, no subtipo “UCEC_POLE” também foi o grau 3. 

Por último, analisou-se o subtipo juntamente com a idade. Analisando os dados, pode-se afirmar que para o subtipo “UCEC_UC_HIGH”, a faixa etária com maior incidência é a dos 65 aos 80. Já para os restantes subtipos, foi a faixa etária dos 50 anos aos 65 anos.
Tal como dito anteriormente, sendo esta a faixa etária predominante nos dados, é justificável que seja o intervalo de dados com maior incidência em quase todos os subtipos de cancro.
