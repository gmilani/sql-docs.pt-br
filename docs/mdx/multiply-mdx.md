---
title: '* (Multiplicação) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 396dded86adfe8faa6b6ad58b5eb8174d4323726
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088422"
---
# <a name="-multiply-mdx"></a>* (Multiplicação) (MDX)


  Realiza uma operação aritmética que multiplica dois números.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Numeric_Expression * Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Numeric_Expression*  
 Uma linguagem MDX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor com o tipo de dados do parâmetro com prioridade maior.  
  
## <a name="remarks"></a>Comentários  
 As duas expressões devem ser do mesmo tipo de dados ou uma expressão deve poder ser convertida implicitamente no tipo de dados da outra expressão. Se uma expressão for avaliada como um valor nulo, o operador retornará um valor nulo.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
