---
title: '&amp; (AND bit a bit) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- AND, bitwise AND
- '& (bitwise AND)'
- bitwise AND (&)
ms.assetid: 06d2958e-66a5-44d8-8bc4-56209ebe1ff2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 295affd0b03368d8156bec8e3b7193f3ce0684ac
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71290310"
---
# <a name="amp-bitwise-and-ssis-expression"></a>&amp; (AND bit a bit) (Expressão SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Executa uma operação AND de bit a bit de dois valores de inteiro. Compara cada bit de seu primeiro operando com o bit correspondente de seu segundo operando. Se ambos os bits forem 1, o bit de resultado correspondente será definido como 1. Caso contrário, o bit de resultado correspondente é definido como zero (0).  
  
 Ambas as condições devem ser um tipo de dados inteiro assinado ou ambas as condições devem ser um tipo de dados inteiro não assinado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
integer_expression1 & integer_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *integer_expression1, integer_expression2*  
 É qualquer expressão válida de um tipo de dados inteiro assinado ou não assinado. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinado por tipos de dados dos dois argumentos. Para obter mais informações, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Remarks  
 Se qualquer condição for nula, o resultado de expressão será nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo executa uma operação AND de bit a bit entre as colunas **NumberA** e **NumberB**. **NumberA** contém 3 (0000011) e a coluna **NumberB** contém 7 (00000111).  
  
```  
NumberA & NumberB  
```  
  
 A expressão é avaliada como 3 (00000011).  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000011  
  
 Este exemplo executa uma operação AND de bit a bit entre as colunas **ReorderPoint** e **SafetyStockLevel** .  
  
```  
ReorderPoint & SafetyStockLevel  
```  
  
 Se **ReorderPoint** for 10 e **SafetyStockLevel** for 8, a expressão será avaliada como 8 (00001000).  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001000  
  
 Este exemplo executa uma operação AND de bit a bit entre dois inteiros.  
  
```  
3 & 5   
```  
  
 A expressão é avaliada como 1 (00000001).  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000001  
  
## <a name="see-also"></a>Consulte Também  
 [&& &#40;AND lógico&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/logical-and-ssis-expression.md)   
 [Precedência de operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
