---
title: TopCount (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e0f607f3111c150bff3d5dc562c77901a381bedc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036606"
---
# <a name="topcount-mdx"></a>TopCount (MDX)


  Classifica um conjunto em ordem decrescente e retorna o número especificado de elementos com os valores mais altos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TopCount(Set_Expression,Count [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Count*  
 Uma expressão numérica válida que especifica o número de tuplas a ser retornado.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão numérica for especificada, o **TopCount** função classificará, em ordem decrescente, as tuplas no conjunto especificado pelo conjunto especificado de acordo com o valor especificado pela expressão numérica, conforme avaliado sobre especificado Defina. Depois de classificar o conjunto, o **TopCount** função, em seguida, retorna o número especificado de tuplas com o valor mais alto.  
  
> [!IMPORTANT]  
>  Como o [BottomCount](../mdx/bottomcount-mdx.md) função, o **TopCount** função sempre quebra a hierarquia.  
  
 Se uma expressão numérica não for especificada, a função retornará o conjunto de membros em ordem natural, sem qualquer classificação, se comportando como a [Head (MDX)](../mdx/head-mdx.md) função.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna as 10 datas mais significativas classificadas por Valor de Vendas pela Internet:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `TOPCOUNT([Date].[Date].[Date].MEMBERS, 10, [Measures].[Internet Sales Amount])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 O exemplo a seguir retorna, para a categoria Bicicleta, os cinco primeiros membros do conjunto que contém todas as combinações de membros do nível Cidade na hierarquia Geografia na dimensão Geografia, bem como todos os anos fiscais da hierarquia Fiscal da dimensão Data, ordenados pela medida Valor das Vendas do Revendedor (começando com os membros desse conjunto com o maior número de vendas).  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopCount  
   ({[Geography].[Geography].[City].Members   
      *[Date].[Fiscal].[Fiscal Year].Members}  
   , 5  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].Bikes)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
