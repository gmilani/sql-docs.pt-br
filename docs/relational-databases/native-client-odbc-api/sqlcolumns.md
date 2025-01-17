---
title: SQLColumns | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColumns function
ms.assetid: 69d3af44-8196-43ab-8037-cdd06207b171
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 58209d617d7978ff4ed6da486bd5c89c076c05af
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73787418"
---
# <a name="sqlcolumns"></a>SQLColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLColumns** retorna SQL_SUCCESS se os valores existem ou não para os parâmetros *CatalogName*, *TableName*ou *ColumnName* . **SQLFetch** retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
> [!NOTE]  
>  Para tipos de valores grandes, os parâmetros de todos os comprimentos serão retornados com um valor SQL_SS_LENGTH_UNLIMITED.  
  
 **SQLColumns** pode ser executado em um cursor de servidor estático. Uma tentativa de executar **SQLColumns** em um cursor atualizável (dinâmico ou de conjunto de chaves) retornará SQL_SUCCESS_WITH_INFO indicando que o tipo de cursor foi alterado.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte ao relatório de informações de tabelas em servidores vinculados, aceitando um nome de duas partes para o parâmetro *CatalogName* : *Linked_Server_Name.Catalog_Name*.  
  
 Para ODBC 2. os aplicativos *x* que não usam Curingas em *TableName*, **SQLColumns** retornam informações sobre todas as tabelas cujos nomes correspondem a *TableName* e pertencem ao usuário atual. Se o usuário atual não possuir nenhuma tabela cujo nome corresponda ao parâmetro *TableName* , **SQLColumns** retornará informações sobre todas as tabelas pertencentes a outros usuários em que o nome da tabela corresponde ao parâmetro *TableName* . Para ODBC 2. os aplicativos *x* que usam Curingas **retornam** todas as tabelas cujos nomes correspondem a *TableName*. Para ODBC 3. os aplicativos *x* **SQLColumns** retorna todas as tabelas cujos nomes correspondem a *TableName* , independentemente do proprietário, ou se são usados curingas.  
  
 A tabela a seguir lista as colunas retornadas pelo conjunto de resultados:  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|DATA_TYPE|Retorna SQL_VARCHAR, SQL_VARBINARY ou SQL_WVARCHAR para os tipos de dados **varchar (max)** .|  
|TYPE_NAME|Retorna "varchar", "varbinary" ou "nvarchar" para os tipos de dados **varchar (max)** , **varbinary (max)** e **nvarchar (max)** .|  
|COLUMN_SIZE|Retorna SQL_SS_LENGTH_UNLIMITED para os tipos de dados **varchar (max)** indicando que o tamanho da coluna é ilimitado.|  
|BUFFER_LENGTH|Retorna SQL_SS_LENGTH_UNLIMITED para os tipos de dados **varchar (max)** indicando que o tamanho do buffer é ilimitado.|  
|SQL_DATA_TYPE|Retorna SQL_VARCHAR, SQL_VARBINARY ou SQL_WVARCHAR para os tipos de dados **varchar (max)** .|  
|CHAR_OCTET_LENGTH|Retorna o comprimento máximo de uma coluna char ou binary. Retorna 0 para indicar que o tamanho é ilimitado.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|Retorna o nome do catálogo no qual é definido o nome de uma coleção de esquemas XML. Se não for possível localizar o nome do catálogo, essa variável conterá uma cadeia de caracteres vazia.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|Retorna o nome do esquema no qual é definido o nome de uma coleção de esquemas XML. Se não for possível localizar o nome do esquema, essa variável conterá uma cadeia de caracteres vazia.|  
|SS_XML_SCHEMACOLLECTION_NAME|Retorna o nome de uma coleção de esquemas XML. Se não for possível localizar o nome, essa variável conterá uma cadeia de caracteres vazia.|  
|SS_UDT_CATALOG_NAME|O nome do catálogo que contém o UDT (tipo definido pelo usuário).|  
|SS_UDT_SCHEMA_NAME|O nome do esquema que contém o UDT.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|O nome qualificado do assembly do UDT.|  
  
 Para UDTs, a coluna de TYPE_NAME existente é usada para indicar o nome do UDT; Portanto, nenhuma coluna adicional para ela deve ser adicionada ao conjunto de resultados de **SQLColumns** ou [SQLProcedureColumns](../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md). O DATA_TYPE de uma coluna ou parâmetro UDT é SQL_SS_UDT.  
  
 Para o UDT de parâmetros, você pode usar os novos descritores específicos do driver definidos acima para obter ou definir as propriedades extra de metadados de um UDT, caso o servidor retorne ou exija essas informações.  
  
 Quando um cliente se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e chama SQLColumns, usar valores nulos ou curingas para o parâmetro de entrada do catálogo não retornará informações de outros catálogos. Em vez disso, serão retornadas apenas informações sobre o catálogo atual. O cliente pode primeiro chamar SQLTables para determinar em qual catálogo a tabela desejada está localizada. Em seguida, o cliente pode usar esse valor de catálogo para o parâmetro de entrada do catálogo em sua chamada para SQLColumns para recuperar informações sobre as colunas nessa tabela.  
  
## <a name="sqlcolumns-and-table-valued-parameters"></a>SQLColumns e parâmetros com valor de tabela  
 O conjunto de resultados retornado por SQLColumns depende da configuração de SQL_SOPT_SS_NAME_SCOPE. Para obter mais informações, consulte [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). As colunas a seguir foram adicionadas para parâmetros com valor de tabela:  
  
|Nome da coluna|Tipo de dados|Sumário|  
|-----------------|---------------|--------------|  
|SS_IS_COMPUTED|Smallint|Para uma coluna em um TABLE_TYPE, será SQL_TRUE se a coluna for uma coluna computada; caso contrário, SQL_FALSE.|  
|SS_IS_IDENTITY|Smallint|SQL_TRUE se a coluna for uma coluna de identidade; caso contrário, SQL_FALSE.|  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros &#40;com valor&#41;de tabela ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlcolumns-support-for-enhanced-date-and-time-features"></a>Suporte de SQLColumns a recursos aprimorados de data e hora  
 Para obter informações sobre os valores retornados para tipos de data/hora, consulte [Catálogo de metadados](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obter mais informações, consulte [melhorias &#40;de data e&#41;hora em ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlcolumns-support-for-large-clr-udts"></a>Suporte de SQLColumns para UDTs CLR grandes  
 **SQLColumns** dá suporte a UDTs (tipos definidos pelo usuário) CLR grandes. Para obter mais informações, consulte [ &#40;ODBC&#41;grandes tipos de CLR definidos pelo usuário](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlcolumns-support-for-sparse-columns"></a>Suporte de SQLColumns para colunas esparsas  
 Duas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] colunas específicas foram adicionadas ao conjunto de resultados para SQLColumns:  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|SS_IS_SPARSE|**Smallint**|Se a coluna for uma coluna esparsa, será SQL_TRUE; caso contrário, SQL_FALSE.|  
|SS_IS_COLUMN_SET|**Smallint**|Se a coluna for a **column_set** coluna, isso será SQL_TRUE; caso contrário, SQL_FALSE.|  
  
 Em conformidade com a especificação ODBC, SS_IS_SPARSE e SS_IS_COLUMN_SET aparecem antes de todas as colunas específicas do driver que foram adicionadas a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versões anteriores à [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]e depois de todas as colunas exigidas pelo próprio ODBC.  
  
 O conjunto de resultados retornado por SQLColumns depende da configuração de SQL_SOPT_SS_NAME_SCOPE. Para obter mais informações, consulte [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Para obter mais informações sobre colunas esparsas no ODBC, consulte [colunas &#40;esparsas suportam ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Função Sqlcolumns](https://go.microsoft.com/fwlink/?LinkId=59336)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
