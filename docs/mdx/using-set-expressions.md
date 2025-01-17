---
title: Usando expressões Set | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1588d955e728830da4417160591a5c2b6c231473
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893501"
---
# <a name="using-set-expressions"></a>Usando expressões de conjunto


  Um conjunto é composto por uma lista ordenada de nenhuma ou algumas tuplas. Um conjunto que não contém nenhuma tupla é conhecido como um conjunto vazio.  
  
 A expressão completa de um conjunto consiste em nenhuma ou algumas tuplas especificadas explicitamente, entre chaves:  
  
 {[{ *Tuple_expression* | *Member_Expression* } [, { *Tuple_expression* | *Member_expression* }]...]}  
  
 As expressões de membro especificadas em uma expressão de conjunto são convertidas em expressões de tupla de um membro.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra duas expressões de conjunto usadas nos eixos Colunas e Linhas de uma consulta:  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]} ON COLUMNS,`  
  
 `{([Product].[Product Categories].[Category].&[4], [Date].[Calendar].[Calendar Year].&[2004]),`  
  
 `([Product].[Product Categories].[Category].&[1], [Date].[Calendar].[Calendar Year].&[2003]),`  
  
 `([Product].[Product Categories].[Category].&[3], [Date].[Calendar].[Calendar Year].&[2004])}`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 No eixo Colunas, o conjunto  
  
 {[Medidas].[Valor das Vendas pela Internet], [Medidas].[Valor do Imposto da Internet]}  
  
 consiste em dois membros da dimensão Medidas. No eixo Linhas, o conjunto  
  
 {([Product]. [Categorias de produto]. [Category]. & [4], [data]. [Calendário]. [Ano civil]. & [2004]),  
  
 ([Produto]. [Categorias de produto]. [Category]. & [1], [data]. [Calendário]. [Ano civil]. & [2003]),  
  
 ([Produto]. [Categorias de produto]. [Category]. & [3], [data]. [Calendário]. [Ano civil]. & [2004])}  
  
 consiste em três tuplas, cada uma contendo duas referências explícitas aos membros da hierarquia Categorias de Produto da dimensão Produto e da hierarquia Calendário da dimensão Data.  
  
 Para obter exemplos de funções que retornam conjuntos, consulte [trabalhando com membros, tuplas e &#40;conjuntos&#41;MDX](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx).  
  
## <a name="see-also"></a>Consulte também  
 [MDX &#40;de expressões&#41;](../mdx/expressions-mdx.md)  
  
  
