---
title: Verificação de consistência | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], consistency checks
- consistency checks [ODBC]
ms.assetid: deb80efa-ad1f-4ea5-b334-9817cd279e5c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 419e338a5e96821606dc26a53a4fccecbc72ae3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125536"
---
# <a name="consistency-check"></a>Verificação de consistência
Uma verificação de consistência é executada pelo driver automaticamente sempre que um aplicativo define o campo SQL_DESC_DATA_PTR do IPD, descartar ou APD. Sempre que esse campo é definido, o driver verificará se o valor do campo SQL_DESC_TYPE e os valores aplicáveis para o campo SQL_DESC_TYPE no mesmo registro são válidos e consistentes.  
  
 O campo SQL_DESC_DATA_PTR de um IPD normalmente não estiver definido; No entanto, um aplicativo pode fazê-lo para forçar uma verificação de consistência de campos do IPD. O valor que o campo SQL_DESC_DATA_PTR do IPD é definido como não é realmente armazenado e não pode ser recuperado por uma chamada para **SQLGetDescField** ou **SQLGetDescRec**; a configuração é feita apenas para forçar o verificação de consistência. Uma verificação de consistência não pode ser executada em um IRD.  
  
 Para obter mais informações sobre a verificação de consistência, consulte [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).
