---
title: Nível de isolamento da transação do cursor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- isolation levels [ODBC]
- ODBC applications, row versioning
- cursors [ODBC], isolation levels
- ODBC cursors, isolation levels
- row versioning [SQL Server], ODBC
ms.assetid: 0c6663a4-5a25-44aa-8fe4-e35af9bf4a83
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 92d9eb8bb09065290c99f3cb9894208a7613b984
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784101"
---
# <a name="cursor-transaction-isolation-level"></a>Nível de isolamento da transação de cursor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O comportamento de bloqueio completo de cursores se baseia em uma interação entre atributos de simultaneidade e o nível de isolamento da transação definidos pelo cliente. Os clientes ODBC definem o nível de isolamento da transação usando os atributos [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) SQL_ATTR_TXN_ISOLATION ou SQL_COPT_SS_TXN_ISOLATION. O comportamento de bloqueio de um ambiente de cursor específico é determinado pela combinação dos comportamentos de bloqueio das opções de nível de isolamento da transação e de simultaneidade.  
  
 Os seguintes níveis de isolamento da transação de cursor têm suporte pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client:  
  
-   Leitura confirmada (SQL_TXN_READ_COMMITTED)  
  
-   Leitura não confirmada (SQL_TXN_READ_UNCOMMITTED)  
  
-   Leitura repetível (SQL_TXN_REPEATABLE_READ)  
  
-   Serializável (SQL_TXN_SERIALIZABLE)  
  
-   Instantâneo (SQL_TXN_SS_SNAPSHOT)  
  
 Observe que a API ODBC especifica níveis de isolamento de transação adicionais, mas eles não têm suporte pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou pelo driver ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do cursor](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
