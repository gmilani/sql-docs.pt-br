---
title: Interjunção (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 63de71ae82e60b8ec7d8a39e18f89e6bd2393f2d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892943"
---
# <a name="crossjoin-mdx"></a>Crossjoin (MDX)


  Retorna o produto cruzado de um ou mais conjuntos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Standard syntax  
Crossjoin(Set_Expression1 ,Set_Expression2 [,...n] )  
  
Alternate syntax  
Set_Expression1 * Set_Expression2 [* ...n]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Set_Expression2*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Comentários  
 A função de interjunção retorna o produto cruzado de dois ou mais conjuntos especificados. A ordem das tuplas no conjunto resultante depende da ordem dos conjuntos a serem unidos e da ordem de seus membros. Por exemplo, quando o primeiro conjunto consiste em {X1, X2,..., x*n*} e o segundo conjunto consistir em {Y1, Y2,..., y*n*}, o produto cruzado desses conjuntos será:  
  
 {(x1, y1), (x1, Y2),..., (x1, y*n*), (x2, y1), (x2, y2),...,  
  
 (x2, y*n*),..., (x*n*, y1), (x*n*, Y2),..., (Xn, y*n*)}  
  
> [!IMPORTANT]  
>  Se os conjuntos na junção cruzada forem compostos por tuplas de diferentes hierarquias de atributo na mesma dimensão, essa função retornará somente as tuplas que realmente existem. Para obter mais informações, consulte [Key Concepts &#40;in&#41;MDX Analysis Services](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services).  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir mostra exemplos simples de uso da função Crossjoin no eixo Colunas e Linhas de uma consulta:  
  
 `SELECT`  
  
 `[Customer].[Country].Members *`  
  
 `[Customer].[State-Province].Members`  
  
 `ON 0,`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].Members,`  
  
 `[Product].[Category].[Category].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE Measures.[Internet Sales Amount]`  
  
 O exemplo a seguir mostra a filtragem automática que ocorre quando hierarquias diferentes da mesma dimensão são unidas:  
  
 `SELECT`  
  
 `Measures.[Internet Sales Amount]`  
  
 `ON 0,`  
  
 `//Only the dates in Calendar Years 2003 and 2004 will be returned here`  
  
 `Crossjoin(`  
  
 `{[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]},`  
  
 `[Date].[Date].[Date].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 Os três exemplos a seguir retornam os mesmos resultados: o Valor de Vendas da Internet por estado para os estados dos Estados Unidos. Os dois primeiros usam as duas sintaxes de junção cruzada e o terceiro demonstra o uso da cláusula WHERE para retornar as mesmas informações.  
  
### <a name="example-1"></a>Exemplo 1  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
       [Customer].[State-Province].Members  
   ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-2"></a>Exemplo 2  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-3"></a>Exemplo 3:  
  
```  
SELECT   
   [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
