---
title: Estrutura SSVARIANT | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
ms.assetid: d13c6aa6-bd49-467a-9093-495df8f1e2d9
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2298bbbfcdb4c0245d9b932152c21f39d7e884f0
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73770740"
---
# <a name="ssvariant-structure"></a>Estrutura SSVARIANT
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A estrutura **SSVARIANT** , que é definida em sqlncli. h, corresponde a um valor DBTYPE_SQLVARIANT no provedor OLEDB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 **SSVARIANT** é uma União discriminadora. Dependendo do valor do membro vt, o consumidor pode determinar qual membro deve ser lido. Os valores vt correspondem aos tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, a estrutura **SSVARIANT** pode manter qualquer tipo do SQL Server. Para obter mais informações sobre a estrutura de dados para tipos de OLE DB padrão, consulte [indicadores de tipo](https://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Comentários  
 Quando DataTypeCompat==80, vários subtipos **SSVARIANT** se tornam cadeias de caracteres. Por exemplo, os seguintes valores vt serão exibidos em **SSVARIANT** como VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Quando DateTypeCompat == 0, estes tipos aparecerão no seu formulário nativo.  
  
 Para obter mais informações sobre SSPROP_INIT_DATATYPECOMPATIBILITY, consulte [usando palavras-chave da cadeia de conexão com SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 O arquivo sqlncli. h contém macros de acesso variante que simplificam a desreferência dos tipos de membro na estrutura **SSVARIANT** . Um exemplo é V_SS_DATETIMEOFFSET que você pode usar da seguinte maneira:  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Para obter o conjunto completo de macros de acesso para cada membro da estrutura **SSVARIANT** , consulte o arquivo sqlncli. Hi.  
  
 A seguinte tabela descreve os membros da estrutura **SSVARIANT**:  
  
|Membro|Indicador de tipo OLE DB|Tipo de dados OLE DB C|valor vt|Comentários|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||Especifica o tipo de valor contido no struct **SSVARIANT**.|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|Dá suporte ao tipo de dados **tinyint**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|sShortIntVal|DBTYPE_I2|**SHORT**|**VT_SS_I2**|Dá suporte ao tipo de dados **smallint**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|Dá suporte ao tipo de dados **int**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|Dá suporte ao tipo de dados **bigint**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|Dá suporte ao tipo de dados **real**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|Dá suporte ao tipo de dados **float**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|Dá suporte aos tipos de dados **Money** e **smallmoney**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|Dá suporte ao tipo de dados **bit**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|Dá suporte ao tipo de dados **uniqueidentifier**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|Dá suporte ao tipo de dados **numérico**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|Dá suporte ao tipo de dados **date**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|Dá suporte aos tipos de dados **smalldatetime**, **datetime**e **datetime2**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|Dá suporte ao tipo de dados **time**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Inclui os seguintes membros:<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**byte**) especifica a escala para o valor de *tTime2Val* .|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|Dá suporte ao tipo de dados **datetime2**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Inclui os seguintes membros:<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**byte**) especifica a escala para o valor de *tsDataTimeVal* .|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|Dá suporte ao tipo de dados **datetimeoffset**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Inclui os seguintes membros:<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**byte**) especifica a escala para o valor de *tsoDateTimeOffsetVal* .|  
|NCharVal|Não existe um indicador de tipo OLE DB correspondente.|**struct _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|Dá suporte aos tipos de dados **nchar** e **nvarchar**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Inclui os seguintes membros:<br /><br /> *sActualLength* (**Short**) especifica o comprimento real para a cadeia de caracteres para a qual *pwchNCharVal* aponta. Não inclui o zero final.<br /><br /> *sMaxLength* (**Short**) especifica o comprimento máximo da cadeia de caracteres para a qual *pwchNCharVal* aponta.<br /><br /> Ponteiro *pwchNCharVal* (**WCHAR** \*) para a cadeia de caracteres.<br /><br /> Membros não utilizados: *rgbReserved*, *dwReserved*e *pwchReserved*.|  
|CharVal|Não existe um indicador de tipo OLE DB correspondente.|**struct _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|Dá suporte aos tipos de dados **Char** e **varchar**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Inclui os seguintes membros:<br /><br /> *sActualLength* (**Short**) especifica o comprimento real para a cadeia de caracteres para a qual *pchCharVal* aponta. Não inclui o zero final.<br /><br /> *sMaxLength* (**Short**) especifica o comprimento máximo da cadeia de caracteres para a qual *pchCharVal* aponta.<br /><br /> *pchCharVal* (**Char** \*) ponteiro para a cadeia de caracteres.<br /><br /> Membros não usados:<br /><br /> *rgbReserved*, *dwReserved*e *pwchReserved*.|  
|BinaryVal|Não existe um indicador de tipo OLE DB correspondente.|**struct _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|Dá suporte aos tipos de dados **Binary** e **varbinary**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Inclui os seguintes membros:<br /><br /> *sActualLength* (**Short**) especifica o comprimento real para os dados aos quais o *prgbBinaryVal* aponta.<br /><br /> *sMaxLength* (**Short**) especifica o comprimento máximo para os dados aos quais o *prgbBinaryVal* aponta.<br /><br /> Ponteiro *prgbBinaryVal* (**byte** \*) para os dados binários.<br /><br /> Membro não usado: *dwReserved*.|  
|Não conhecido como|UNUSED|UNUSED|UNUSED|UNUSED|  
|BLOBType|UNUSED|UNUSED|UNUSED|UNUSED|  
  
## <a name="see-also"></a>Consulte também  
 [Tipos &#40;de dados OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
