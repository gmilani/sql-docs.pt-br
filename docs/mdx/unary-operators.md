---
title: Operadores unários | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9ec9ac3eef28c4deae08d577487599575852c132
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893551"
---
# <a name="unary-operators"></a>Operadores unários


  Na linguagem MDX, os operadores unários executam uma operação em um operando único, como retornar o valor negativo ou positivo de uma expressão numérica.  
  
 O MDX oferece suporte aos operadores unários listados na tabela a seguir.  
  
|Operator|Descrição|  
|--------------|-----------------|  
|[- (Negativo)](../mdx/negative-mdx.md)|Retorna o valor negativo de uma expressão numérica.|  
|[+ (Positivo)](../mdx/positive-mdx.md)|Retorna o valor positivo de uma expressão numérica.|  
  
 O exemplo a seguir demonstra o uso de um operador unário para retornar o valor negativo de uma medida:  
  
```  
WITH   
   MEMBER [Measures].[NegDiscountAmount] AS  
   -[Measures].[Discount Amount]  
SELECT   
   {[Measures].[Discount Amount],[Measures].[NegDiscountAmount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 Além disso, o MDX usa operadores unários especiais para determinar a operação de agregação executada pela função [RollupChildren](../mdx/rollupchildren-mdx.md) . Para obter mais informações sobre esses operadores unários especiais, consulte [Adicionar uma agregação personalizada a uma dimensão](https://docs.microsoft.com/analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension).  
  
## <a name="see-also"></a>Consulte também  
 [Sintaxe &#40;de MDX de operadores&#41;](../mdx/operators-mdx-syntax.md)  
  
  
