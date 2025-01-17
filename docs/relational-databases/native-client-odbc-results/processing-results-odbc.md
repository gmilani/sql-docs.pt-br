---
title: Processando resultados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], about result sets
- SQLRowCount function
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- COMPUTE clause
- result sets [ODBC]
- COMPUTE BY clause
ms.assetid: 61a8db19-6571-47dd-84e8-fcc97cb60b45
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7949d646ac8890a9f4a5631de991168f9a0997e4
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73778975"
---
# <a name="processing-results-odbc"></a>Processando resultados (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Depois que um aplicativo envia uma instrução SQL, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna qualquer dado resultante como um ou mais conjuntos de resultados. Um conjunto de resultados é um conjunto de linhas e colunas que correspondem aos critérios da consulta. As instruções SELECT, funções de catálogo e alguns procedimentos armazenados geram um conjunto de resultados disponibilizado para um aplicativo no formato tabular. Se a instrução SQL executada for um procedimento armazenado, um lote contendo vários comandos ou uma instrução SELECT contendo palavras-chave, haverá vários conjuntos de resultados a serem processados.  
  
 As funções de catálogo ODBC também podem recuperar dados. Por exemplo, [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md) recupera dados sobre colunas na fonte de dados. Esses conjuntos de resultados podem conter zero ou mais linhas.  
  
 Outras instruções SQL, como GRANT ou REVOKE, não retornam conjuntos de resultados. Para essas instruções, o código de retorno de **SQLExecute** ou **SQLExecDirect** geralmente é a única indicação de que a instrução foi bem-sucedida.  
  
 Cada instrução INSERT, UPDATE e DELETE retorna um conjunto de resultados que contém apenas o número de linhas afetado pela modificação. Essa contagem é disponibilizada quando o aplicativo chama [SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md). ODBC 3. os aplicativos *x* devem chamar **SQLRowCount** para recuperar o conjunto de resultados ou [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) para cancelá-lo. Quando um aplicativo executa um lote ou procedimento armazenado que contém várias instruções INSERT, UPDATE ou DELETE, o conjunto de resultados de cada instrução de modificação deve ser processado usando **SQLRowCount** ou cancelado usando **SQLMoreResults**. Essas contagens podem ser canceladas incluindo uma instrução SET NOCOUNT ON no lote ou no procedimento armazenado.  
  
 O Transact-SQL inclui a instrução SET NOCOUNT. Quando a opção NOCOUNT é definida em, SQL Server não retorna as contagens das linhas afetadas por uma instrução e **SQLRowCount** retorna 0. A versão do driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client introduz uma opção [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) específica do driver, SQL_SOPT_SS_NOCOUNT_STATUS, para relatar se a opção NOCOUNT está ativada ou desativada. Sempre que **SQLRowCount** retorna 0, o aplicativo deve testar SQL_SOPT_SS_NOCOUNT_STATUS. Se SQL_NC_ON for retornado, o valor de 0 de **SQLRowCount** indicará apenas que SQL Server não retornou uma contagem de linhas. Se SQL_NC_OFF for retornado, significa que NOCOUNT está desativado e o valor de 0 de **SQLRowCount** indica que a instrução não afetou nenhuma linha. Os aplicativos não devem exibir o valor de **SQLRowCount** quando SQL_SOPT_SS_NOCOUNT_STATUS for SQL_NC_OFF. Lotes ou procedimentos armazenados grandes podem conter várias instruções SET NOCOUNT, de forma que os programadores não podem supor que SQL_SOPT_SS_NOCOUNT_STATUS permaneça constante. A opção deve ser testada cada vez que **SQLRowCount** retornar 0.  
  
 Várias outras instruções Transact-SQL retornam seus dados em mensagens e não em conjuntos de resultados. Quando o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client recebe essas mensagens, ele retorna SQL_SUCCESS_WITH_INFO para permitir que o aplicativo saiba que as mensagens informativas estão disponíveis. O aplicativo pode então chamar **SQLGetDiagRec** para recuperar essas mensagens. As instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que funcionam deste modo são as seguintes:  
  
-   DBCC  
  
-   SET SHOWPLAN (disponível com versões anteriores do SQL Server)  
  
-   SET STATISTICS  
  
-   PRINT  
  
-   RAISERROR  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client retorna SQL_ERROR em um RAISERROR com uma severidade de 11 ou superior. Se a severidade do RAISERROR for 19 ou superior, a conexão também será descartada.  
  
 Para processar os conjuntos de resultados a partir de uma instrução SQL, o aplicativo:  
  
-   Determina as características do conjunto de resultados.  
  
-   Associa as colunas às variáveis do programa.  
  
-   Recupera um único valor, uma linha inteira de valores ou várias linhas de valores.  
  
-   Testa se há mais conjuntos de resultados e, se houver, faz loops de volta para determinar as características do novo conjunto de resultados.  
  
 O processo de recuperação de linhas da fonte de dados e de seu retorno ao aplicativo é chamado de busca.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Determinando as características de um ODBC &#40;do conjunto de resultados&#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
-   [Atribuindo armazenamento](../../relational-databases/native-client-odbc-results/assigning-storage.md)  
  
-   [Buscando dados de resultados](../../relational-databases/native-client-odbc-results/fetching-result-data.md)  
  
-   [Mapeando tipos &#40;de dados ODBC&#41;](../../relational-databases/native-client-odbc-results/mapping-data-types-odbc.md)  
  
-   [Uso do tipo de dados](../../relational-databases/native-client-odbc-results/data-type-usage.md)  
  
-   [Tradução automática de dados de caracteres](../../relational-databases/native-client-odbc-results/autotranslation-of-character-data.md)  
  
## <a name="see-also"></a>Consulte também  
 [  &#40;SQL Server Native Client&#41; ODBC](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
 [Tópicos &#40;de instruções de processamento de resultados ODBC&#41;](https://msdn.microsoft.com/library/772d9064-c91d-4cac-8b60-fcc16bf76e10)  
  
  
