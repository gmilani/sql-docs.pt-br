---
title: Data e hora OLE DB recursos com versões anteriores do SQL Server
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 96976bac-018c-47cc-b1b2-fa9605eb55e5
author: MightyPen
ms.author: genemi
ms.custom: seo-dt-2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 100a0b6a96c9359e224e406928b03a2aa776511e
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095452"
---
# <a name="new-date-and-time-features-with-previous-sql-server-versions-ole-db"></a>Novos recursos de data e hora com versões anteriores do SQL Server (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este tópico descreve o comportamento esperado quando um aplicativo cliente que usa recursos de data e hora aprimorados se comunica com uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]e quando um cliente compilado com uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente nativo anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] envia comandos para um servidor que dá suporte a recursos de data e hora aprimorados.  
  
## <a name="down-level-client-behavior"></a>Comportamento do cliente de versão anterior  
 Os aplicativos cliente que usam uma versão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente nativo anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] veem os novos tipos de data/hora como colunas **nvarchar** . O conteúdo de coluna são representações literais. Para obter mais informações, consulte a seção "formatos de dados: cadeias de caracteres e literais" do [suporte de tipo de dados para OLE DB melhorias de data e hora](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md). O tamanho da coluna é o comprimento de literal máximo para a precisão especificada para a coluna.  
  
 As APIs de catálogo retornarão os metadados consistentes com o código de tipo de dados de nível inferior retornado ao cliente (por exemplo, **nvarchar**) e a representação de nível inferior associada (por exemplo, o formato literal apropriado). Entretanto, o nome do tipo de dados retornado será o nome de tipo [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] real.  
  
 Quando um aplicativo cliente de nível inferior é executado em um servidor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (ou posterior) no qual são feitas alterações de esquema nos tipos de data/hora, o comportamento esperado é o seguinte:  
  
|Tipo de cliente OLE DB|Tipo SQL Server 2005|SQL Server 2008 (ou posterior) tipo|Conversão de resultado (servidor para cliente)|Conversão de parâmetro (cliente para servidor)|  
|------------------------|--------------------------|---------------------------------------|--------------------------------------------|-----------------------------------------------|  
|DBTYPE_DBDATE|Datetime|data|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Campos de hora definidos como zero.|IRowsetChange falhará devido a um truncamento de cadeia de caracteres se o campo de tempo for diferente de zero.|  
|DBTYPE_DBTIME||Time(0)|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Campos de data definidos como a data atual.|IRowsetChange falhará devido ao truncamento da cadeia de caracteres se os segundos fracionários forem diferentes de zero.<br /><br /> A data é ignorada.|  
|DBTYPE_DBTIME||Time(7)|Falha-literal de tempo inválido.|OK|  
|DBTYPE_DBTIMESTAMP|||Falha-literal de tempo inválido.|OK|  
|DBTYPE_DBTIMESTAMP||Datetime2 (3)|OK|OK|  
|DBTYPE_DBTIMESTAMP||Datetime2 (7)|OK|OK|  
|DBTYPE_DBDATE|Smalldatetime|data|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Campos de hora definidos como zero.|IRowsetChange falhará devido ao truncamento da cadeia de caracteres se o campo de tempo for diferente de zero.|  
|DBTYPE_DBTIME||Time(0)|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Campos de data definidos como a data atual.|IRowsetChange falhará devido ao truncamento da cadeia de caracteres se os segundos fracionários forem diferentes de zero.<br /><br /> A data é ignorada.|  
|DBTYPE_DBTIMESTAMP||Datetime2(0)|OK|OK|  
  
 OK quer dizer que se funcionou com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], deveria continuar funcionando com o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (ou posterior).  
  
 Só as seguintes alterações de esquema comuns foram consideradas:  
  
-   Usar um novo tipo em que logicamente um aplicativo exige somente um valor de data ou hora. No entanto, o aplicativo foi forçado a usar **DateTime** ou **smalldatetime** porque tipos de data e hora separados não estavam disponíveis.  
  
-   Usar um novo tipo para obter precisão ou exatidão adicional de frações de segundos.  
  
-   Alternando para **datetime2** porque esse é o tipo de dados preferencial para data e hora.  
  
 Os aplicativos que usam metadados de servidor obtidos por meio de conjuntos de linhas de esquema ICommandWithParameters:: GetParameterInfo ou Schema para definir informações de tipo de parâmetro por meio de ICommandWithParameters:: SetParameterInfo falharão durante as conversões do cliente em que a cadeia de caracteres a representação de um tipo de origem é maior do que a representação de cadeia de caracteres do tipo de destino. Por exemplo, se uma associação de cliente usar DBTYPE_DBTIMESTAMP e a coluna de servidor for Data, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente nativo converterá o valor para "aaaa-dd-mm hh: mm: SS. fff", mas os metadados do servidor serão retornados como **nvarchar (10)** . O estouro resultante causa DBSTATUS_E_CATCONVERTVALUE. Problemas semelhantes surgem com conversões de dados por IRowsetChange, pois os metadados do conjunto de linhas são definidos a partir dos metadados do ResultSet.  
  
### <a name="parameter-and-rowset-metadata"></a>Parâmetro e metadados de conjunto de linhas  
 Esta seção descreve os metadados para parâmetros, colunas de resultado e conjuntos de linhas de esquema para clientes que são compilados com uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
#### <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 A estrutura DBPARAMINFO retorna as seguintes informações por meio do parâmetro *prgParamInfo* :  
  
|Tipo de parâmetro|wType|ulParamSize|bPrecision|bScale|  
|--------------------|-----------|-----------------|----------------|------------|  
|DATE|DBTYPE_WSTR|10|~0|~0|  
|time|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
 Note que alguns destes intervalos de valor não são contínuos; por exemplo, 9 está faltando em 8,10..16. Isso se deve à adição de um ponto decimal quando a precisão fracionária é maior que zero.  
  
#### <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 As seguintes colunas são retornadas:  
  
|Tipo de coluna|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE, DBCOLUMN_DATETIMEPRECISION|  
|-----------------|--------------------|--------------------------|-------------------------|--------------------------------------------------|  
|DATE|DBTYPE_WSTR|10|NULL|NULL|  
|time|DBTYPE_WSTR|8, 10..16|NULL|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|NULL|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|NULL|NULL|  
  
#### <a name="columnsinfogetcolumninfo"></a>ColumnsInfo::GetColumnInfo  
 A estrutura de DBCOLUMNINFO retorna as seguintes informações:  
  
|Tipo de parâmetro|wType|ulColumnSize|bPrecision|bScale|  
|--------------------|-----------|------------------|----------------|------------|  
|DATE|DBTYPE_WSTR|10|~0|~0|  
|time(1..7)|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
### <a name="schema-rowsets"></a>Schema Rowsets  
 Esta seção aborda metadados para parâmetros, colunas de resultados e conjuntos de linhas de esquema para novos tipos de dados. Essas informações são úteis é que você tem um provedor de cliente desenvolvido usando ferramentas anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
#### <a name="columns-rowset"></a>Conjunto de linhas de COLUMNS  
 Os valores de coluna a seguir são retornados para tipos de data/hora:  
  
|Tipo de coluna|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|DATETIME_PRECISION|  
|-----------------|----------------|--------------------------------|------------------------------|-------------------------|  
|DATE|DBTYPE_WSTR|10|20|NULL|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|0|  
|Datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|3|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|NULL|  
  
#### <a name="procedure_parameters-rowset"></a>Conjunto de linhas de PROCEDURE_PARAMETERS  
 Os valores de coluna a seguir são retornados para tipos de data/hora:  
  
|Tipo de coluna|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|TYPE_NAME<br /><br /> LOCAL_TYPE_NAME|  
|-----------------|----------------|--------------------------------|------------------------------|--------------------------------------|  
|DATE|DBTYPE_WSTR|10|20|DATE|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|time|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|smalldatetime|  
|Datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|Datetime|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|datetime2|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|datetimeoffset|  
  
#### <a name="provider_types-rowset"></a>Conjunto de linhas de PROVIDER_TYPES  
 As linhas a seguir são retornadas para tipos de data/hora:  
  
|Tipo -><br /><br /> Column|DATE|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|DATE|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_WSTR|DBTYPE_WSTR|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_WSTR|DBTYPE_WSTR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|DATE|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_TRUE|VARIANT_FALSE|VARIANT_FALSE|  
|IS_FIXEDLENGTH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
  
## <a name="down-level-server-behavior"></a>Comportamento de servidor de versão anterior  
 Quando conectado a um servidor de uma versão anterior à [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], qualquer tentativa de usar os novos nomes de tipo de servidor (por exemplo, com ICommandWithParameters:: SetParameterInfo ou ITableDefinition:: CreateTable) resultará em DB_E_BADTYPENAME.  
  
 Se novos tipos forem associados para parâmetros ou resultados sem o uso de um nome de tipo, e o novo tipo for usado para especificar o tipo de servidor implicitamente ou se não houver nenhuma conversão válida do tipo de servidor no tipo de cliente, DB_E_ERRORSOCCURRED será retornado e DBBINDSTATUS_UNSUPPORTED_CONVERSION será definido como o status de associação para o acessador usado em Execute.  
  
 Se houver uma conversão de cliente aceita do tipo de buffer no tipo de servidor para a versão do servidor na conexão, todos os tipos de buffer do cliente poderão ser usados. Nesse contexto, o *tipo de servidor* significa o tipo especificado por ICommandWithParameters:: SetParameterInfo ou implícito pelo tipo de buffer se ICommandWithParameters:: SetParameterInfo não for chamado. Isto significa que DBTYPE_DBTIME2 e DBTYPE_DBTIMESTAMPOFFSET poderão ser usados com servidores de versões anteriores ou quando DataTypeCompatibility=80, se a conversão de cliente em um tipo de servidor aceito for bem-sucedida. Obviamente, se o tipo de servidor estiver correto, um erro ainda poderá ser relatado pelo servidor se ele não puder executar uma conversão implícita no tipo de servidor real.  
  
## <a name="ssprop_init_datatypecompatibility-behavior"></a>Comportamento de SSPROP_INIT_DATATYPECOMPATIBILITY  
 Quando SSPROP_INIT_DATATYPECOMPATIBILITY é definido como SSPROPVAL_DATATYPECOMPATIBILITY_SQL2000, os novos tipos de data/hora e metadados associados aparecem para os clientes conforme eles aparecem para clientes de nível inferior, conforme descrito em [alterações de cópia em massa para tipos &#40;de data e&#41;hora aprimorados OLE DB e ODBC](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
## <a name="comparability-for-irowsetfind"></a>Comparações de IRowsetFind  
 Todos os operadores de comparação são permitidos para os novos tipos de data/hora, porque eles aparecem como tipos de cadeia de caracteres, em vez de tipos de data/hora.  
  
## <a name="see-also"></a>Consulte também  
 [Melhorias de data e hora &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
