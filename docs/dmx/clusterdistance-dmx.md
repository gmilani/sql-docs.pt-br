---
title: ClusterDistance (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 523c57811ca29956edc3c18b8143844732c163b6
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892391"
---
# <a name="clusterdistance-dmx"></a>ClusterDistance (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  A função **ClusterDistance** retorna a distância do caso de entrada do cluster especificado ou, se nenhum cluster for especificado, a distância do caso de entrada do cluster mais provável.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ClusterDistance([<ClusterID expression>])  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 Essa função só pode ser usada se o modelo de mineração de dados subjacente oferecer suporte a clustering. A função pode ser usada com qualquer tipo de modelo de clusterização (EM, K-Means etc.), mas o resultado será diferente de acordo com o algoritmo.  
  
## <a name="return-type"></a>Tipo de retorno  
 Valor escalar.  
  
## <a name="remarks"></a>Comentários  
 A função **ClusterDistance** retorna a distância entre o caso de entrada e o cluster que tem a probabilidade mais alta para esse caso de entrada.  
  
 No caso da clusterização K-Means, como qualquer caso pode pertencer a apenas um cluster, com um peso de associação de 1.0, a distância do cluster sempre será 0. No entanto, em K-Means, pressupõe-se que cada cluster tem um centroide. Para obter o valor do centroide, consulte ou procure a tabela aninhada NODE_DISTRIBUTION no conteúdo do modelo de mineração. Para obter mais informações, consulte [Conteúdo do modelo de mineração para modelos de clustering &#40;Analysis Services – Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining).  
  
 No caso do método de clusterização de EM padrão, todos os pontos dentro do cluster são considerados igualmente prováveis; portanto, por design, não há centroide para o cluster. O valor de **ClusterDistance** entre um caso específico e um determinado cluster *N* é calculado da seguinte maneira:  
  
 ClusterDistance (N) = 1-(membershipWeight (N))  
  
 Ou:  
  
 ClusterDistance (N) = 1-ClusterProbability (N))  
  
## <a name="related-prediction-functions"></a>Funções de previsão relacionadas  
 O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornece as seguintes funções adicionais para consultar modelos de clusterização:  
  
-   Use a [função &#40;DMX&#41; do cluster](../dmx/cluster-dmx.md) para retornar o cluster mais provável.  
  
-   Use a [função &#40;DMX&#41; ClusterProbability](../dmx/clusterprobability-dmx.md) para obter a probabilidade de que um caso pertença a um cluster específico. Este valor serve como o inverso da distância de cluster.  
  
-   Use a [função &#40;DMX&#41; de PredictHistogram](../dmx/predicthistogram-dmx.md) para retornar um histograma da probabilidade do caso de entrada existente em cada um dos clusters do modelo.  
  
-   Use a [função &#40;DMX&#41; PredictCaseLikelihood](../dmx/predictcaselikelihood-dmx.md) para retornar uma medida de 0 a 1 que indica a probabilidade de que um caso de entrada deve existir Considerando o modelo aprendido pelo algoritmo.  
  
## <a name="example1-obtaining-cluster-distance-to-the-most-likely-cluster"></a>Example1 Obtendo a distância do cluster para o cluster mais provável  
 O exemplo a seguir retorna a distância do caso especificado para o cluster ao qual o caso provavelmente pertence.  
  
```  
SELECT  
    ClusterDistance()  
FROM  
    [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
    '2-5 Miles' AS [Commute Distance],  
    'Graduate Degree' AS [Education],  
    0 AS [Number Cars Owned],  
    0 AS [Number Children At Home]) AS t  
```  
  
 Resultados do exemplo:  
  
|Expressão|  
|----------------|  
|0.0477390930705145|  
  
 Para descobrir qual é esse cluster, você pode substituir  `Cluster` for `ClusterDistance` no exemplo anterior.  
  
 Resultados do exemplo:  
  
|$CLUSTER|  
|--------------|  
|Cluster 6|  
  
## <a name="example2-obtaining-distance-to-a-specified-cluster"></a>Example2 Obtendo distância para um cluster especificado  
 A sintaxe a seguir usa o conjunto de linhas do esquema de conteúdo do modelo de mineração para retornar a lista de IDs de nó e legendas de nó para os clusters que existem no modelo de mineração. Em seguida, você pode usar a legenda do nó como o argumento do identificador de cluster na função **ClusterDistance** .  
  
```  
SELECT NODE_UNIQUE_NAME, NODE_CAPTION   
FROM <model>.CONTENT   
WHERE NODE_TYPE = 5  
```  
  
 Resultados do exemplo:  
  
|NODE_UNIQUE_NAME|NODE_CAPTION|  
|------------------------|-------------------|  
|001|Cluster 1|  
|002|Cluster 2|  
  
 A sintaxe a seguir retorna a distância do caso especificado do cluster rotulado como Cluster 2.  
  
```  
SELECT  
    ClusterDistance('Cluster 2')  
AS [Cluster 2 Distance]  
FROM [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
    '2-5 Miles' AS [Commute Distance],  
    'Graduate Degree' AS [Education],  
    0 AS [Number Cars Owned],  
    0 AS [Number Children At Home]) AS t  
```  
  
 Resultados do exemplo:  
  
|Distância do Cluster 2|  
|------------------------|  
|0.97008209236394|  
  
## <a name="see-also"></a>Consulte também  
 [Cluster &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [Referência da função &#40;DMX&#41; das extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Conteúdo do modelo de mineração para modelos de clustering &#40;Analysis Services – Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining)  
  
  
