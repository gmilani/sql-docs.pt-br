---
title: SQLSetDescField | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetDescField function
ms.assetid: de4bed15-15be-4825-994c-1046255e725a
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a37821dff5176dfcb42cfd0a9f6424dfcc3f1938
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73785700"
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQLSetDescField pode ser usado para definir campos de descritor para parâmetros com valor de tabela e colunas de parâmetro com valor de tabela. Para obter informações sobre os campos disponíveis, consulte [campos de descritor de parâmetro com valor de tabela](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md) e [campos de descritor para colunas constituintes de parâmetro com valor de tabela](../../relational-databases/native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md).  
  
## <a name="remarks"></a>Comentários  
 As colunas do parâmetro com valor de tabela ficam disponíveis somente quando o campo do cabeçalho do descritor SQL_SOPT_SS_PARAM_FOCUS é definido como o ordinal de um registro que tenha SQL_DESC_TYPE definido como SQL_SS_TABLE. Para obter mais informações sobre SQL_SPOT_SS_PARAM_FOCUS, consulte [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Se for feita uma tentativa de definir SQL_SOPT_SS_PARAM_FOCUS para o ordinal de um parâmetro que não seja um parâmetro com valor de tabela, SQLSetStmtAttr retornará SQL_ERROR e um registro de diagnóstico será criado com SQLSTATE = HY024 e a mensagem "valor de atributo inválido". SQL_SOPT_SS_PARAM_FOCUS não é alterado quando SQL_ERROR é retornado.  
  
 A definição de SQL_SOPT_SS_PARAM_FOCUS como 0 restaura o acesso a registros de descritor para parâmetros.  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros &#40;com valor&#41;de tabela ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>Suporte do SQLSetDescField a recursos aprimorados de data e hora  
 Os recursos de data/hora foram aprimorados no ODBC. Para obter informações sobre o campo de descritor fornecido para os novos tipos de data/hora, consulte [Parameter and Result Metadata](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md).  
  
 Para obter mais informações, consulte [melhorias &#40;de data e&#41;hora em ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>Suporte de SQLSetDescField a UDTs grandes do CLR  
 O SQLSetDescField dá suporte a UDTs (tipos definidos pelo usuário) CLR grandes. Para obter mais informações, consulte [ &#40;ODBC&#41;grandes tipos de CLR definidos pelo usuário](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>Suporte de SQLSetDescField a colunas esparsas  
 SQLSetDecField pode ser usado para definir SQL_SOPT_SS_NAME_SCOPE no descritor de parâmetro do aplicativo (APD) para os valores SQL_SS_NAME_SCOPE_EXTENDED e SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET.  
  
 Para obter mais informações, consulte [colunas esparsas &#40;dão suporte a ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
   [SQLSetDescField](https://go.microsoft.com/fwlink/?LinkId=80705)  
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
