---
title: Especificar contagens de objetos (Assistente de Design de agregação) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.calculatingobjectcounts.f1
ms.assetid: 305d9d79-d1ab-4704-a7b5-3283842b3996
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d616997d3764aad42691d9ef3c213d553b5f311
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068304"
---
# <a name="specify-object-counts-aggregation-design-wizard"></a>Especificar Contagens de Objetos (Assistente de Design de Agregação)
  Use a página **Especificar Contagens de Objetos** para calcular a contagem de objetos no cubo automaticamente ou para inserir contagens estimadas manualmente. O Assistente de Design de Agregação usa a contagem de objetos para estimar requisitos de armazenamento.  
  
## <a name="options"></a>Opções  
 **Objetos Cube**  
 Exibe as dimensões e os atributos do cubo. Somente os atributos que não têm seus `AggregationUsage` propriedade definida como `None` na **revisar uso de agregação** página do assistente são exibidos, porque esses são os únicos atributos que exigem que as contagens sejam especificadas.  
  
 **Contagem estimada**  
 Exibe o número estimado de linhas no grupo de medidas e as contagens de membros de atributo estimadas nas dimensões do banco de dados. Você pode digitar um valor a ser usado como a contagem estimada ou calcular os valores da contagem estimada. Para calcular os valores da contagem, digite `0` no campo e, em seguida, clique **contagem**. Os campos que já exibem uma contagem não são atualizados.  
  
 **Contagem de partições**  
 (Opcional) Digite o número estimado de linhas no grupo de medidas e digite as contagens de membros de atributo estimadas nas partições.  
  
 **Count**  
 Calcula e popula novamente os valores na coluna **Contagem estimada** para todos os campos vazios. Os campos que já exibem uma contagem não são atualizados.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda de F1 do Assistente de Design de agregação](aggregation-design-wizard-f1-help.md)   
 [Assistentes do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
