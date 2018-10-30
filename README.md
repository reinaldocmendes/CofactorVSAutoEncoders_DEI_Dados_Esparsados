# CofactorVSAutoEncoders_DEI_Dados_Esparsados
Resultados comparativos do CoFactor Vs AutoEncoder's com matrizes utilizando Distância Euclideana Invertida

# Definição dos Dados - Descritivo
Os valores apresentados nos gráficos, correspondem aos resultados obtidos do Algoritmo CoFactor. A Barra amarela correponde a entrada padrão dos dados, no qual o algoritmo trabalha com a co-ocorrência de itens. As demais barras correpondem a entrada gerada atráves do procedimento a descrito abaixo.

# Redes Neurais Convolutivas
O dataset de imagens (ml20m) foi aplicado a quatro redes neurais convolutivas para extração de suas features. Foram elas Resnet50, Vgg16, Vgg19 e Xception. Uma vez que essas features foram extraídas, uma segunda feature foi extraída de informações textuais do mesmo dataset utilizando uma rede neural chamada Doc2vec.

Cada feature extraídas da imagens foram concatenadas com a feature de informações textuais, gerando um novo vetor de features.

Resnet50+Doc2Vec / Vgg16+Doc2Vec / Vgg19+Doc2Vec / Xception+Doc2Vec

# AutoEnconder's
Cada vetor de features "concatenado" foi aplicado a um tipo de AutoEnconder com o objetivo de gerar uma nova representação do vetor de features original. Os autoencoder's utilizados foram Sparse AutoEncoder, Convolutional AutoEnconder (CAE) e Varitional AutoEncoder (VAE).

As representações geradas do vetor de featuares concatenado, após aplicadas nos autoencoder's foram:

10% - Uma representação com 10% do tamanho do vetor original

20% - Uma representação com 20% do tamanho do vetor original

30% - Uma representação com 30% do tamanho do vetor original

40% - Uma representação com 40% do tamanho do vetor original

50% - Uma representação com 50% do tamanho do vetor original

60% - Uma representação com 60% do tamanho do vetor original

70% - Uma representação com 70% do tamanho do vetor original

80% - Uma representação com 80% do tamanho do vetor original

90% - Uma representação com 90% do tamanho do vetor original

100% - Uma representação com 100% do tamanho do vetor original

# Matriz de Similaridade
Foi gerado uma matrix de similaridade entre os vetores de características (vetor final gerado a partir do AutoEncoder) utilizando o método da "Distância Euclideana". Para os resultados apresentados nesse documento foi utilizado uma "Distância Euclideana Invertida Não Normalizada", ou seja, valores muito proxímos de zero (ou zero) corresponde a vetores que não possuem similaridade nenhum, em contrapartida quanto maior for o valor maior é a similaridade entre os itens.

### Ajuste de sparsidade
Para realização experimental algumas similaridades tiveram seus valores modificados para 0 (zero), ou seja, similaridade nula, e acordo com as seguintes observações:

* File "Resultados_CoFactor_Vs_CAE_inv_less_5.ipynb":  Similaridade <= 5 
* File "Resultados_CoFactor_Vs_CAE_inv_less_10.ipynb": Similaridade <= 10
* File "Resultados_CoFactor_Vs_VAE_inv_less_70_pct.ipynb": Similaridade <= (70% do maior valor)
* File "Resultados_CoFactor_Vs_VAE_inv_less_80_pct.ipynb": Similaridade <= (80% do maior valor)
* File "Resultados_CoFactor_Vs_VAE_inv_less_95_pct.ipynb": Similaridade <= (95% do maior valor)
* File "Resultados_CoFactor_Vs_VAE_inv_less_98_pct.ipynb": Similaridade <= (98% do maior valor)

Obs: O maior valor encontrado na matriz de similaridade corresponde a similaridade do vetor com ele mesmo.

# Metricas de Avaliação
Medidas de avaliação (ranked-based) foram utilizadas para medir o desempenho da recomendação do algoritmo ao mudar seu dataset de entrada em comparação com o dataset original proposto (co-ocorrência).

Para cada usuário, todas as métricas comparam a classficação prevista de itens "não observados" com sua classificação real. As medidas utilizadas foram Recall, NDCG e Map.

Nos resultados apresentados nos gráficos que seguem, foram considerados nos experimentos um "ranked list" de tamanhos fixados em: 10, 20, 50 e 100, para cada medida de avaliação, por exemplo, NDCG@20 significado que foi considerado um ranked list dos 20 itens no topo da lista.

# Análise Geral


## CAE
Nós Gráficos construidos atráves das matrizes geradas pelo o AutoEncoder "CAE" é possível verificar que mesmo alterando o tipo da rede neural (vgg's, resnet ou xception) eles apresentam um comportamento bastante similar.

Para a métrica "Recall" quanto maior o valor de @k melhor o resultado.

Para métrica NDCG, os valores de @k entre 10 e 50 tem resultados similares, no entanto, para um @k de 100 o desempenho do algoritmo aumenta consideravelmente. Na métrica de avaliação MAP o algoritmo tem um comportamento contrário ao Recall, quanto maior o valor de @k pior foi seu desempenho.

### Tornar o DataSet mais esparso não foi suficiente para modificar significativamente os resultados.¶

* Em todas as Comparações o BaseLine (CoFactor) utilizado apresentou melhor resultado do que as representações propostas do vetor original.
