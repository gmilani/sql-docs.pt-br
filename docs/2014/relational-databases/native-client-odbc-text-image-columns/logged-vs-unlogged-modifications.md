---
title: Conectado vs. Registradas modificações | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d5c73288c57a834008f4d09ad098ad1b41183e76
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130329"
---
# <a name="logged-vs-unlogged-modifications"></a>Conectado vs. Modificações registradas
  Um aplicativo pode solicitar que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client não registre em log **texto**, **ntext**, e **imagem** modificações. No entanto, tome cuidado ao usar essa opção. Ele deve ser usado apenas para essas situações em que o **texto**, **ntext**, ou **imagem** dados não são críticos e os proprietários de dados estão dispostos a sacrificar a capacidade de recuperar dados para alto desempenho.  
  
 O log de **texto**, **ntext**, e **imagem** modificações é controlado pela chamada [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) com o  *Atributo* parâmetro definido como sql_sopt_ss _ TEXTPTR_LOGGING e *ValuePtr* definido como SQL_TL_ON ou SQL_TL_OFF.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando colunas Text e Image](managing-text-and-image-columns.md)  
  
  