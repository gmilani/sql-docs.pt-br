---
title: Plotar dados em um eixo secundário (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 094f39bf-3634-4852-9fc3-3adec4b266e5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 86d73f2ab16bdb7ee801e333f3a75c96a2a1c360
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65578185"
---
# <a name="plot-data-on-a-secondary-axis-report-builder-and-ssrs"></a>Plotar dados em um eixo secundário (Construtor de Relatórios e SSRS)

O gráfico possui dois tipos de eixo: primário e secundário. O eixo secundário é útil ao comparar dois conjuntos de valores com dois intervalos de dados distintos que compartilham uma categoria em comum.  
  
 Por exemplo, suponha que você tenha um gráfico que calcula Receita versus Imposto referente ao ano de 2008. Nesse caso, o período de 2008 é comum para os dois conjuntos de valores. No entanto, quando as duas séries são plotadas no mesmo eixo y, não podemos fazer uma comparação útil porque a escala do eixo y é otimizada para os valores maiores no conjunto de dados. Se mostrarmos Receita no eixo primário, e Imposto no eixo secundário, poderemos exibir cada série em seu próprio eixo y com sua própria escala de valores. A série ainda compartilha um eixo x comum.  
  
 Em situações em que existam mais de duas séries a serem comparadas, considere uma abordagem diferente para comparação e exibição de várias séries em um gráfico. Para obter mais informações, consulte [Várias séries em um gráfico](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md).  
  
 Um exemplo deste gráfico está disponível como um relatório de exemplo. Para obter mais informações sobre como baixar esse relatório de exemplo e outros, consulte [Relatórios de exemplo do Construtor de Relatórios e do Designer de Relatórios](https://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-plot-a-series-on-the-secondary-axis"></a>Para plotar uma série no eixo secundário  
  
1.  Clique com o botão direito do mouse na série no gráfico ou em um campo na área **Valores** que você deseja exibir no eixo secundário e clique em **Propriedades da Série**. A caixa de diálogo **Propriedades da Série** é exibida.  
  
2.  Clique em **Eixo e Área do Gráfico**e selecione qual dos eixos secundários você deseja habilitar, o eixo de valor ou o eixo de categoria.  

## <a name="next-steps"></a>Próximas etapas

[Formatando rótulos de eixo em um gráfico](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
[Especificar um intervalo de eixo](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
