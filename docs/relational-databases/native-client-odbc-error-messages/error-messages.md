---
title: Mensagens de erro | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 10308509004493ba68d23870a70bf878ae05b4a1
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73783460"
---
# <a name="error-messages"></a>Mensagens de erro
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O texto das mensagens retornadas pelo driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client é colocado no parâmetro *MessageText* de **SQLGetDiagRec**. A origem de um erro é indicada pelo cabeçalho da mensagem:  
  
 [Microsoft][ODBC Driver Manager]  
 São erros gerados pelo Gerenciador de Driver ODBC.  
  
 [Microsoft][ODBC Cursor Library]  
 São erros gerados pela biblioteca de cursores ODBC.  
  
 [Microsoft][SQL Server Native Client]  
 Esses erros são gerados pelo driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Se não houver outros nós com o nome de uma Net-Library nem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é sinal de que o erro foi encontrado no driver.  
  
 O [SQL Server Native Client] [*Net-Transportname*]  
 Esses erros são gerados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NET-Library, em que *net-Transportname* é o nome de exibição de um transporte de rede de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por exemplo, pipes nomeados, memória compartilhada, soquetes TCP/IP ou via). O restante da mensagem de erro contém a função Net-Library chamada e a função chamada na API de rede subjacente pela função TDS. O código de erro *pfNative* retornado com esses erros é o código de erro da pilha de protocolo de rede subjacente.  
  
 O [SQL Server Native Client] [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 São erros gerados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O restante da mensagem de erro é o texto da mensagem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O código *pfNative* retornado com esses erros é o número do erro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre uma lista de mensagens de erro (e seus números) que podem ser retornados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte as colunas descrição e erro da tabela do sistema **sysmessages** no banco de dados **mestre** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Tratando de erros e mensagens](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
