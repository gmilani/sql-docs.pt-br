---
title: Alocar identificadores e conectar-se ao SQL Server (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- handles [ODBC]
- handles [ODBC], connection
- handles [ODBC], about handles
ms.assetid: 6172cd52-9c9a-467d-992f-def07f3f3bb1
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ce294636c4d01a143b640126832bc6cca31ece14
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73782072"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>Alocar identificadores e se conectar ao SQL Server (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>Para alocar identificadores e se conectar ao SQL Server  
  
1.  Inclua o arquivos de cabeçalho ODBC Sql.h, Sqlext.h, Sqltypes.h.  
  
2.  Inclua o arquivo de cabeçalho específico do driver do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Odbcss.h.  
  
3.  Chame [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) com um **handletype** de SQL_HANDLE_ENV para inicializar o ODBC e alocar um identificador de ambiente.  
  
4.  Chame [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) com o **atributo** definido como SQL_ATTR_ODBC_VERSION e **ValuePtr** definido como SQL_OV_ODBC3 para indicar que o aplicativo usará chamadas de função de formato ODBC 3. x.  
  
5.  Opcionalmente, chame [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) para definir outras opções de ambiente ou chame [SQLGetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=58403) para obter opções de ambiente.  
  
6.  Chame [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) com um **handletype** de SQL_HANDLE_DBC para alocar um identificador de conexão.  
  
7.  Opcionalmente, chame [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) para definir opções de conexão ou chame [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) para obter opções de conexão.  
  
8.  Chame o SQLConnect para usar uma fonte de dados existente para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Ou  
  
     Chame [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) para usar uma cadeia de conexão para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Uma cadeia de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] completa mínima tem uma de duas formas:  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     Se a cadeia de conexão não for concluída, **SQLDriverConnect** poderá solicitar as informações necessárias. Isso é controlado pelo valor especificado para o parâmetro *DriverCompletion* .  
  
     \- ou –  
  
     Chame [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) várias vezes de maneira iterativa para criar a cadeia de conexão e conectar-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
9. Opcionalmente, chame [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md) para obter atributos de driver e comportamento para a fonte de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
10. Aloque e use instruções.  
  
11. Chame SQLDisconnect para desconectar de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e tornar o identificador de conexão disponível para uma nova conexão.  
  
12. Chame [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) com um **handletype** de SQL_HANDLE_DBC para liberar o identificador de conexão.  
  
13. Chame **SQLFreeHandle** com um **handletype** de SQL_HANDLE_ENV para liberar o identificador do ambiente.  
  
> [!IMPORTANT]  
>  Quando possível, use a Autenticação do Windows. Se a Autenticação do Windows não estiver disponível, solicite aos usuários que digitem suas credenciais em tempo de execução. Evite armazenar as credenciais em um arquivo. Se for necessário manter as credenciais, criptografe-as com a [Win32 crypto API](https://go.microsoft.com/fwlink/?LinkId=64532)(em inglês).  
  
## <a name="example"></a>Exemplo  
 Este exemplo mostra uma chamada para **SQLDriverConnect** para se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem a necessidade de uma fonte de dados ODBC existente. Ao passar uma cadeia de conexão incompleta para **SQLDriverConnect**, isso faz com que o driver ODBC solicite ao usuário que insira as informações ausentes.  
  
```  
#define MAXBUFLEN   255  
  
SQLHENV      henv = SQL_NULL_HENV;  
SQLHDBC      hdbc1 = SQL_NULL_HDBC;  
SQLHSTMT      hstmt1 = SQL_NULL_HSTMT;  
  
SQLCHAR      ConnStrIn[MAXBUFLEN] =  
         "DRIVER={SQL Server Native Client 10.0};SERVER=MyServer";  
  
SQLCHAR      ConnStrOut[MAXBUFLEN];  
SQLSMALLINT   cbConnStrOut = 0;  
  
// Make connection without data source. Ask that driver   
// prompt if insufficient information. Driver returns  
// SQL_ERROR and application prompts user  
// for missing information. Window handle not needed for  
// SQL_DRIVER_NOPROMPT.  
retcode = SQLDriverConnect(hdbc1,      // Connection handle  
                  NULL,         // Window handle  
                  ConnStrIn,      // Input connect string  
                  SQL_NTS,         // Null-terminated string  
                  ConnStrOut,      // Address of output buffer  
                  MAXBUFLEN,      // Size of output buffer  
                  &cbConnStrOut,   // Address of output length  
                  SQL_DRIVER_PROMPT);  
```  
  
  
