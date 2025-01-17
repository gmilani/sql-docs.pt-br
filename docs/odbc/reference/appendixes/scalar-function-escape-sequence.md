---
title: Sequência de Escape de função escalar | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36e108fcc61b2390d5fd72ac4ad322778ccfb4b2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057069"
---
# <a name="scalar-function-escape-sequence"></a>Sequência de escape de função escalar
ODBC usa sequências de escape para funções escalares. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação BNF, a sintaxe é:  
  
 *ODBC escalar-função escape* :: =  
  
 *Iniciador do ODBC-esc* fn *função escalar ODBC esc terminador*  
  
 *scalar-function* ::= *function-name* (*argument-list*)  
  
 (As definições para os não terminais *nome da função* e *nome da função* (*lista de argumentos*) são derivados da lista de funções escalares em [ Apêndice e: Funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).)  
  
 *Iniciador do ODBC-esc* :: = {  
  
 *Terminador de esc ODBC* :: =}  
  
 Para determinar se a fonte de dados oferece suporte aos procedimentos e o driver dá suporte a sintaxe de invocação de procedimento ODBC, um aplicativo pode chamar **SQLGetInfo**. Para obter mais informações, consulte [apêndice e: Funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).
