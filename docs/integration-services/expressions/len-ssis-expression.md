---
title: LEN (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- LEN function
- number of characters
ms.assetid: d961398b-e4d0-4936-be17-8f4c5882a640
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4f84bb32435afe7cbe52cea6ed25f59940dbd42c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297523"
---
# <a name="len-ssis-expression"></a>LEN (Expressão SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Retorna o número de caracteres em uma expressão character. Se a cadeia de caracteres incluir espaços em branco à esquerda e à direita, a função os incluirá na contagem. LEN retorna valores idênticos para a mesma cadeia de caracteres de byte único e duplo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
LEN(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É a expressão a ser avaliada.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 O argumento *character_expression* pode ser um tipo de dados DT_WSTR, DT_TEXT, DT_NTEXT ou DT_IMAGE. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Se *character_expression* for um literal de cadeia de caracteres ou uma coluna de dados com o tipo de dados DT_STR, ele será implicitamente convertido para o tipo de dados DT_WSTR antes de LEN executar sua operação. Outros tipos de dados devem ser explicitamente convertidos para o tipo de dados DT_WSTR. Para obter mais informações, consulte [Cast &#40;Expressão do SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Se o argumento transmitido para a função LEN tiver um tipo de dados BLOB (Binary Large Object Block), como DT_TEXT, DT_NTEXT ou DT_IMAGE, a função retornará uma contagem de bytes.  
  
 LEN retornará um resultado nulo se o argumento for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo retorna o comprimento de uma literal de cadeia de caracteres. O resultado de retorno é 12.  
  
```  
LEN("Ball Bearing")  
```  
  
 Este exemplo retorna a diferença entre o comprimento de valores nas colunas **FirstName** e **LastName** .  
  
```  
LEN(FirstName) - LEN(LastName)  
```  
  
 Retorna o comprimento de um nome do computador que usa a variável de Sistema **MachineName**.  
  
```  
LEN(@MachineName)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
