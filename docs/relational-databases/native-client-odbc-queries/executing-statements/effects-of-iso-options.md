---
title: Efeitos das opções ISO | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ISO options (ODBC)
- ODBC applications, ISO options
- ODBC applications, statements
- SQL Server Native Client ODBC driver, ISO options
- statements [ODBC], ISO options
ms.assetid: 813f1397-fa0b-45ec-a718-e13fe2fb88ac
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 43347e4fcf517dc52c8791dc81220a8990e1655d
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779871"
---
# <a name="effects-of-iso-options"></a>Efeitos das opções ISO
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O padrão ODBC corresponde bastante ao padrão ISO e os aplicativos ODBC esperam o comportamento padrão de um driver ODBC. Para fazer com que seu comportamento esteja de acordo com isso definido no padrão ODBC, o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client sempre usa as opções ISO disponíveis na versão do SQL Server com a qual ele se conecta.  
  
 Quando o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se conecta a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o servidor detecta que o cliente está usando o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e define várias opções no.  
  
 O próprio driver emite estas instruções; o aplicativo ODBC não faz nada para solicitá-las. A configuração dessas opções permite que os aplicativos ODBC que usam o driver sejam mais portáteis, pois o comportamento do servidor corresponde então ao padrão ISO.  
  
 Em geral, os aplicativos baseados na DB-Library não ativam essas opções. Os sites que observam comportamento diferente entre os clientes ODBC ou de biblioteca de banco de BD ao executar a mesma instrução SQL não devem assumir que isso aponta para um problema com o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Eles devem primeiro executar novamente a instrução no ambiente de biblioteca de banco de usuários com as mesmas opções SET que seriam usadas pelo driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
 Como as opções SET podem ser ativadas e desativadas a qualquer momento por usuários e aplicativos, os desenvolvedores de procedimentos armazenados e de gatilhos também devem tomar o cuidado de testar seus procedimentos e gatilhos com as opções SET listadas acima ativadas e desativadas. Isso garante que os procedimentos e gatilhos funcionem corretamente, independentemente das opções que uma conexão específica possa ter ativado ao invocar o procedimento ou o gatilho. Os gatilhos ou os procedimentos armazenados que necessitam de uma determinada configuração para uma dessas opções deve emitir uma instrução SET no início do gatilho ou do procedimento armazenado. Essa instrução SET permanece em vigor apenas para a execução do gatilho ou do procedimento armazenado; quando o procedimento ou o gatilho é concluído, a configuração original é restaurada.  
  
 Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], uma quarta opção SET, CONCAT_NULL_YIELDS_NULL, também é ativada. O driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client não definirá essas opções em se AnsiNPW = no for especificado na fonte de dados ou em [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) ou [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md).  
  
 Assim como as opções ISO observadas anteriormente, o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client não ativará a opção QUOTED_IDENTIFIER em se Quotid = NO for especificado na fonte de dados ou em **SQLDriverConnect** ou **SQLBrowseConnect**.  
  
 Para permitir que o driver saiba o estado atual das opções SET, os aplicativos ODBC não devem usar a instrução SET do [!INCLUDE[tsql](../../../includes/tsql-md.md)] para definir essas opções. Eles devem definir essas opções usando apenas a fonte de dados ou as opções de conexão. Se o aplicativo emitir instruções SET, o driver poderá gerar instruções SQL incorretas.  
  
## <a name="see-also"></a>Consulte também  
 [Executando instruções &#40; &#41; ODBC](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
   [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)  
 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)  
  
  
