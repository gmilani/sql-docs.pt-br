---
title: PredictCaseLikelihood (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0302af7f2241f3e158e8fa95691544c6fdf2dfac
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893924"
---
# <a name="predictcaselikelihood-dmx"></a>PredictCaseLikelihood (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Esta função retorna a probabilidade de um caso de entrada se ajustar no modelo existente. Usado somente com modelos de cluster.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PredictCaseLikelihood([NORMALIZED|NONNORMALIZED])  
```  
  
## <a name="arguments"></a>Argumentos  
 NORMALIZED  
 O valor de retorno contém a probabilidade do caso com o modelo dividido pela probabilidade do caso sem o modelo.  
  
 NONNORMALIZED  
 O valor de retorno contém a probabilidade bruta do caso, que é o produto das probabilidades dos atributos de caso.  
  
## <a name="applies-to"></a>Aplica-se a  
 Modelos criados usando os algoritmos clustering e [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[msCoName](../includes/msconame-md.md)] clustering de sequência.  
  
## <a name="return-type"></a>Tipo de retorno  
 Número de ponto flutuante da dupla precisão entre 0 e 1. Um número próximo de 1 indica que o caso tem uma alta probabilidade de ocorrer neste modelo. Um número próximo de 0 indica que o caso tem pouca probabilidade de ocorrer neste modelo.  
  
## <a name="remarks"></a>Comentários  
 Por padrão, o resultado da função **PredictCaseLikelihood** é normalizado. Em geral, os valores normalizados são mais úteis à medida que o número de atributos de um caso aumenta e as diferenças entre as probabilidades brutas de quaisquer dois casos tornam-se muito menores.  
  
 A seguinte equação é usada para calcular os valores normalizados, determinados x e y:  
  
-   x = probabilidade do caso baseada no modelo de cluster  
  
-   y = probabilidade de caso marginal, calculada como a probabilidade de log do caso com base na contagem dos casos de treinamento  
  
-   Z = exp (log (x)-log (Y))  
  
 Normalizado = (z/(1 + z))  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a probabilidade de o caso específico ocorrer no modelo de cluster, que é baseado no banco de dados [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW.  
  
```  
SELECT  
  PredictCaseLikelihood() AS Default_Likelihood,  
  PredictCaseLikelihood(NORMALIZED) AS Normalized_Likelihood,  
  PredictCaseLikelihood(NONNORMALIZED) AS Raw_Likelihood,  
FROM  
  [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 Resultados esperados:  
  
|Default_Likelihood|Normalized_Likelihood|Raw_Likelihood|  
|-------------------------|----------------------------|---------------------|  
|6.30672792729321E-08|6.30672792729321E-08|9.5824454056846E-48|  
  
 A diferença entre esses resultados demonstra o efeito da normalização. O valor bruto de **CaseLikelihood** sugere que a probabilidade do caso seja de cerca de 20%; no entanto, quando você normaliza os resultados, fica claro que a probabilidade do caso é muito baixa.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Referência da função &#40;DMX&#41; das extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funções &#40;de previsão gerais DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
