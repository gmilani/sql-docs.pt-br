---
title: Líder (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cc4d362fbc7656e9427548a352b32d5d8297071e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905738"
---
# <a name="lead-mdx"></a>Lead (MDX)


  Retorna o membro que é um número especificado de posições que seguem um membro especificado junto ao nível do membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.Lead( Index )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Index*  
 Uma expressão numérica válida que especifica várias posições de membro.  
  
## <a name="remarks"></a>Comentários  
 As posições de membros em um nível são determinadas pela ordem natural da hierarquia de atributo. A numeração das posições se baseia em zero.  
  
 Se o lead especificado for zero (0), o **levar** função retorna o membro especificado.  
  
 Se o lead especificado for negativo, o **levar** função retorna um membro anterior.  
  
 `Lead(1)` é equivalente a [NextMember](../mdx/nextmember-mdx.md) função. `Lead(-1)` é equivalente a [PrevMember](../mdx/prevmember-mdx.md) função.  
  
 O **levar** função é semelhante ao [latência](../mdx/lag-mdx.md) funcionar, exceto que o **retardo** função procura na direção oposta a **levar** função. Ou seja, `Lead(n)` é equivalente a `Lag(-n)`.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o valor para dezembro de 2001:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(-2) ON 0  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna o valor para março de 2002:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
