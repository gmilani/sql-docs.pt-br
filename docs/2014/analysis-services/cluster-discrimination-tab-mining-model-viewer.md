---
title: Guia discriminação (Visualizador do modelo de mineração) do cluster | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.discrimination.f1
ms.assetid: ae7cfff7-ab1c-4cf5-9a91-97b21d15d85f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1d55f61d9255d19f22fffb7380785a2ada1a2763
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087895"
---
# <a name="cluster-discrimination-tab-mining-model-viewer"></a>Guia Distinção de Cluster (Visualizador do Modelo de Mineração)
  Use a guia **Distinção de Cluster** para comparar dois clusters existentes em um modelo de clustering. Você pode ver como as diferentes combinações de atributos e valores são representadas dentro dos clusters.  
  
 **Para obter mais informações:** [Algoritmo Microsoft Clustering](data-mining/microsoft-clustering-algorithm.md), [procurar um modelo usando o Visualizador de Cluster da Microsoft](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do Visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração dentre eles na estrutura de mineração atual. O modelo de mineração será aberto no visualizador associado.  
  
 **Visualizador**  
 Escolha um visualizador a ser utilizado para explorar o modelo de mineração selecionado. Você pode usar o visualizador personalizado para modelos de clustering, ou Visualizador de Conteúdo de Mineração da [!INCLUDE[msCoName](../includes/msconame-md.md)] . Você também pode usar visualizadores de plug-in se houver.  
  
 **Cluster 1**  
 Selecione um cluster, para que você possa compará-lo com outro cluster.  
  
 **Cluster 2**  
 Selecione um segundo cluster da lista de clusters no modelo de mineração para comparar com o **Cluster 1**. Você também pode comparar um cluster com seu complemento, ou seja, todos os casos no modelo exceto os que estiverem no cluster selecionado.  
  
 **Pontuações de distinção para \<cluster 1 > e \<cluster 2 >**  
 As colunas no gráfico fornecem informações sobre como cada par atributo-valor está relacionado com os dois clusters selecionados.  
  
|||  
|-|-|  
|**Variáveis**|Um atributo no modelo de mineração.|  
|**Valores**|Um valor do atributo selecionado em **Variáveis**.|  
|**Favorece \<cluster 1 >**|O gráfico de barra à esquerda representa a probabilidade de o par atributo-valor selecionado ser representativo do cluster selecionado em **Cluster 1**. Você pode passar o mouse sobre a barra para ver o valor, representado como uma porcentagem. Observe que, mesmo se o valor for zero, ele não significa que o valor do atributo estará necessariamente faltando do cluster, assim que a distribuição favorece fortemente um cluster em detrimento do outro.|  
|**Favorece \<cluster 2 >**|O gráfico de barra à direita representa a probabilidade de o par atributo-valor selecionado ser representativo do cluster selecionado em **Cluster 2**.|  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores do modelo de mineração &#40; Designer do modelo de mineração de dados &#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do modelo de Mineração de dados](data-mining/data-mining-model-viewers.md)  
  
  
