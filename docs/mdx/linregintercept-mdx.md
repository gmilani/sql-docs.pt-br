---
title: LinRegIntercept (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 30d3fd98995c24498af9376db19087b2018394e3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905579"
---
# <a name="linregintercept-mdx"></a>Função LinRegIntercept (MDX)


  Calcula a regressão linear de um conjunto e retorna o valor da interseção x na linha de regressão, y = ax + b.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
LinRegIntercept(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression_y*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo y.  
  
 *Numeric_Expression_x*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo x.  
  
## <a name="remarks"></a>Comentários  
 A regressão linear, que usa o método dos mínimos quadrados, calcula a equação de uma linha de regressão (ou seja, a linha mais adequada para uma série de pontos). A linha de regressão tem a seguinte equação, em que um é a inclinação e b é a interceptação:  
  
 y = ax+b  
  
 O **LinRegIntercept** função avalia o conjunto especificado em relação a primeira expressão numérica para obter os valores para o eixo y. Em seguida, a função avalia o conjunto especificado em relação à segunda expressão numérica, se especificada, para obter os valores para o eixo x. Se a segunda expressão numérica não for especificada, a função utilizará o contexto atual das células no conjunto especificado como valores para o eixo x. A não especificação do argumento de eixo x geralmente é usada com a dimensão Tempo.  
  
 Depois de obter o conjunto de pontos, o **LinRegIntercept** função retorna a interceptação da linha de regressão (b na equação anterior).  
  
> [!NOTE]  
>  O **LinRegIntercept** função ignora células vazias ou células que contêm texto ou valores lógicos. Porém, a função contém células com valores zero.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a interceptação de uma linha de regressão para as medidas de vendas de unidade e vendas de loja.  
  
```  
LinRegIntercept(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
