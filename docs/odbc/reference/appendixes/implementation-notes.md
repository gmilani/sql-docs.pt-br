---
title: Notas de implementação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 95b60ba35a867135cfc1f823e08b1a99f0262ca9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135740"
---
# <a name="implementation-notes"></a>Notas de implementação
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Esta seção descreve como a biblioteca de cursores ODBC é implementada. Ele descreve como a biblioteca de cursores mantém seu cache, executa instruções SQL e implementa funções ODBC.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Cache de biblioteca de cursores](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [Processando instruções SQL](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [Funções ODBC e a biblioteca de cursores](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
