---
title: bcp_getcolfmt | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_getcolfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_getcolfmt function
ms.assetid: f8bdada5-7b2d-4475-8c98-f93e9d77b130
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8c32df055ea1330fb0d1bdd32b2a3860519d2575
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73782719"
---
# <a name="bcp_getcolfmt"></a>bcp_getcolfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Usado para localizar o valor da propriedade de formato da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_getcolfmt (  
        HDBC hdbc,  
        INT field,  
        INT property,  
        void* pValue,  
        INT cbvalue,  
        INT* pcbLen);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *field*  
 É o número de coluna para o qual a propriedade é recuperada.  
  
 *property*  
 É um das constantes de propriedade.  
  
 *pValue*  
 É o ponteiro para o buffer do qual recuperar o valor dado propriedade.  
  
 *cbValue*  
 É o comprimento do buffer da propriedade em bytes.  
  
 *pcbLen*  
 Ponteiro para o comprimento dos dados que estão sendo retornados no buffer de propriedade.  
  
## <a name="returns"></a>Retorna  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 Valores da propriedade de formato da coluna são listados no tópico [bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md) . Os valores de propriedade da coluna são definidos chamando a função **bcp_setcolfmt** e a função **bcp_getcolfmt** é usada para localizar o valor da propriedade de formato da coluna.  
  
 Podem ser observadas alterações de comportamento ao conectar a um computador de servidor [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (ou posterior), na comparação com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, veja [Descoberta de metadados](../../relational-databases/native-client/features/metadata-discovery.md).  
  
## <a name="bcp_getcolfmt-support-for-enhanced-date-and-time-features"></a>Suporte de bcp_getcolfmt a recursos aprimorados de data e hora  
 Os tipos usados com a propriedade **BCP_FMT_TYPE** para tipos de data/hora são conforme especificado em [alterações de cópia em massa para tipos &#40;de data e hora aprimorados OLE DB e ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Para obter mais informações, consulte [melhorias &#40;de data e&#41;hora em ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
