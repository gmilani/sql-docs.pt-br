---
title: Criando tabelas de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- SQL Server Native Client OLE DB provider, tables
- DBCOLUMNDESC usage
- adding tables
- CreateTable function
ms.assetid: a7b8d142-d76a-44d9-a583-86ac5109fbe8
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ab6a605e77bddbaa38ee71a0d54624c36a229f32
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73788442"
---
# <a name="creating-sql-server-tables"></a>Criando tabelas do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client expõe a função **ITableDefinition:: CreateTable** , permitindo que os consumidores criem tabelas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os consumidores usam **CreateTable** para criar tabelas permanentes nomeadas pelo consumidor e tabelas permanentes ou temporárias com nomes exclusivos gerados pelo provedor de OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Quando o consumidor chama **ITableDefinition:: CreateTable**, se o valor da propriedade DBPROP_TBL_TEMPTABLE for VARIANT_TRUE, o provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB gerará um nome de tabela temporário para o consumidor. O consumidor define o parâmetro *pTableID* do método **CreateTable** como NULL. As tabelas temporárias com nomes gerados pelo provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo não aparecem no conjunto de linhas de **tabelas** , mas podem ser acessadas por meio da interface **IOpenRowset** .  
  
 Quando os consumidores especificam o nome da tabela no membro *pwszName* da União *uname* no parâmetro *pTableID* , o provedor de OLE DB do cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com esse nome. As restrições de nomeação de tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se aplicam, e o nome da tabela pode indicar uma tabela permanente, ou uma tabela temporária local ou global. Para obter mais informações, confira [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md). O parâmetro *ppTableID* pode ser NULL.  
  
 O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client pode gerar os nomes de tabelas permanentes ou temporárias. Quando o consumidor define o parâmetro *pTableID* como nulo e define *ppTableID* para apontar para um\*de DBID válido, o provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native retorna o nome gerado da tabela no membro *pwszName* de *uname* a União da DBID apontada pelo valor de *ppTableID*. Para criar uma tabela nomeada do provedor de OLE DB de cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o consumidor inclui a propriedade de tabela OLE DB DBPROP_TBL_TEMPTABLE em um conjunto de propriedades de tabela referenciado no parâmetro *rgPropertySets* . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB nativo do cliente – as tabelas temporárias nomeadas são locais.  
  
 **CreateTable** retornará DB_E_BADTABLEID se o membro *eKind* do parâmetro *pTableID* não indicar DBKIND_NAME.  
  
## <a name="dbcolumndesc-usage"></a>Uso de DBCOLUMNDESC  
 O consumidor pode indicar um tipo de dados de coluna usando o membro *pwszTypeName* ou o membro *wType*. Se o consumidor especificar o tipo de dados em *pwszTypeName*, o provedor de OLE DB do cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ignorará o valor de *wType*.  
  
 Se estiver usando o membro *pwszTypeName*, o consumidor especificará o tipo de dados usando nomes de tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os nomes de tipo de dados válidos são aqueles retornados na coluna de TYPE_NAME do conjunto de linhas de esquema de PROVIDER_TYPES.  
  
 O provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo reconhece um subconjunto de valores de DBTYPE de OLE DB enumerados no membro *wType* . Para obter mais informações, consulte [mapeamento de tipo de dados em ITableDefinition](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md).  
  
> [!NOTE]  
>  **CreateTable** retornará DB_E_BADTYPE se o consumidor definir o membro *pTypeInfo* ou *pclsid* para especificar o tipo de dados de coluna.  
  
 O consumidor especifica o nome da coluna no membro *pwszName* da união *uName* do membro *dbcid* de DBCOLUMNDESC. O nome da coluna é especificado como uma cadeia de caracteres Unicode. O membro *eKind* de *dbcid* precisa ser DBKIND_NAME. **CreateTable** retornará DB_E_BADCOLUMNID se *eKind* for inválido, se *pwszName* for NULL ou se o valor de *pwszName* não for um identificador válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Todas as propriedades de coluna estão disponíveis em todas as colunas definidas para a tabela. **CreateTable** poderá retornar DB_S_ERRORSOCCURRED ou DB_E_ERRORSOCCURRED se os valores de propriedade forem definidos em conflito. **CreateTable** retornará um erro quando as configurações de propriedade de coluna inválidas causarem uma falha na criação de tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 As propriedades de coluna em um DBCOLUMNDESC são interpretadas da seguinte maneira.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|Leitura/gravação: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE Descrição: define a propriedade de identidade na coluna criada. Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a propriedade de identidade é válida para uma única coluna de uma tabela. A definição da propriedade como VARIANT_TRUE para mais de uma única coluna gera um erro quando o provedor de OLE DB do cliente nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta criar a tabela no servidor.<br /><br /> A propriedade de identidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] só é válida para os tipos **integer**, **numeric** e **decimal** quando a escala é 0. Definir a propriedade como VARIANT_TRUE em uma coluna de qualquer outro tipo de dados gera um erro quando o provedor de OLE DB cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo tenta criar a tabela no servidor.<br /><br /> O provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo retorna DB_S_ERRORSOCCURRED quando DBPROP_COL_AUTOINCREMENT e DBPROP_COL_NULLABLE são VARIANT_TRUE e o *dwOption* de DBPROP_COL_NULLABLE não é DBPROPOPTIONS_REQUIRED. DB_E_ERRORSOCCURRED é retornado quando DBPROP_COL_AUTOINCREMENT e DBPROP_COL_NULLABLE são VARIANT_TRUE e *dwOption* de DBPROP_COL_NULLABLE é igual a DBPROPOPTIONS_REQUIRED. A coluna é definida com a propriedade de identidade [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o membro *dwStatus* de DBPROP_COL_NULLABLE é definido como DBPROPSTATUS_CONFLICTING.|  
|DBPROP_COL_DEFAULT|Leitura/gravação: leitura/gravação<br /><br /> Padrão: nenhum<br /><br /> Descrição: Cria uma restrição [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DEFAULT para a coluna.<br /><br /> O membro *vValue* de DBPROP pode ser qualquer um dentre inúmeros tipos. O membro *vValue.vt* deve especificar um tipo compatível com o tipo de dados da coluna. Por exemplo, a definição de BSTR N/A como o valor padrão para uma coluna definida como DBTYPE_WSTR é uma correspondência compatível. Definir o mesmo padrão em uma coluna definida como DBTYPE_R8 gera um erro quando o provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo tenta criar a tabela no servidor.|  
|DBPROP_COL_DESCRIPTION|Leitura/gravação: leitura/gravação<br /><br /> Padrão: nenhum<br /><br /> Descrição: a propriedade de coluna DBPROP_COL_DESCRIPTION não é implementada pelo provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.<br /><br /> O membro *dwStatus* da estrutura DBPROP retorna DBPROPSTATUS_NOTSUPPORTED quando o consumidor tenta gravar o valor da propriedade.<br /><br /> A definição da propriedade não constitui um erro fatal para o provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Se todos os outros valores de parâmetro forem válidos, será criada a tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|DBPROP_COL_FIXEDLENGTH|Leitura/gravação: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: o provedor de OLE DB do cliente nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa DBPROP_COL_FIXEDLENGTH para determinar o mapeamento de tipo de dados quando o consumidor define o tipo de dados de uma coluna usando o membro *wType* do DBCOLUMNDESC. Para obter mais informações, consulte [mapeamento de tipo de dados em ITableDefinition](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md).|  
|DBPROP_COL_NULLABLE|Leitura/gravação: leitura/gravação<br /><br /> Padrão: nenhum<br /><br /> Descrição: ao criar a tabela, o provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo indica se a coluna deve aceitar valores nulos se a propriedade estiver definida. Quando a propriedade não é definida, a capacidade da coluna de aceitar NULL como valor é determinado pela opção de banco de dados padrão ANSI_NULLS do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> O provedor de OLE DB de cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é um provedor compatível com ISO. Sessões conectadas exibem comportamentos de ISO. Se o consumidor não definir DBPROP_COL_NULLABLE, as colunas aceitarão valores nulos.|  
|DBPROP_COL_PRIMARYKEY|Leitura/gravação: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE Descrição: quando VARIANT_TRUE, o provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB cria a coluna com uma restrição PRIMARY KEY.<br /><br /> Quando definido como uma propriedade de coluna, só uma única coluna pode determinar a restrição. Definir a propriedade VARIANT_TRUE para mais de uma única coluna retorna um erro quando o provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo tenta criar a tabela de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Observação: o consumidor pode usar **IIndexDefinition::CreateIndex** para criar uma restrição de PRIMARY KEY em duas ou mais colunas.<br /><br /> O provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo retorna DB_S_ERRORSOCCURRED quando DBPROP_COL_PRIMARYKEY e DBPROP_COL_UNIQUE são VARIANT_TRUE e o *dwOption* de DBPROP_COL_UNIQUE não é DBPROPOPTIONS_REQUIRED.<br /><br /> DB_E_ERRORSOCCURRED é retornado quando DBPROP_COL_PRIMARYKEY e DBPROP_COL_UNIQUE são VARIANT_TRUE e *dwOption* de DBPROP_COL_UNIQUE é igual a DBPROPOPTIONS_REQUIRED. A coluna é definida com a propriedade de identidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o membro *dwStatus* de DBPROP_COL_PRIMARYKEY é definido como DBPROPSTATUS_CONFLICTING.<br /><br /> O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client retorna um erro quando DBPROP_COL_PRIMARYKEY e DBPROP_COL_NULLABLE são VARIANT_TRUE.<br /><br /> O provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo retorna um erro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando o consumidor tenta criar uma restrição de chave primária em uma coluna de tipo de dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inválido. Não podem ser definidas restrições de PRIMARY KEY em colunas criadas com os tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]bit **,** text **,** ntext**e**image**do**.|  
|DBPROP_COL_UNIQUE|Leitura/gravação: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE Descrição: aplica uma restrição UNIQUE do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à coluna.<br /><br /> Quando definido como uma propriedade de coluna, a restrição só é aplicada em uma única coluna. O consumidor pode usar **IIndexDefinition::CreateIndex** para aplicar uma restrição de UNIQUE nos valores combinados de duas ou mais colunas.<br /><br /> O provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo retorna DB_S_ERRORSOCCURRED quando DBPROP_COL_PRIMARYKEY e DBPROP_COL_UNIQUE são VARIANT_TRUE e *dwOption* não é DBPROPOPTIONS_REQUIRED.<br /><br /> DB_E_ERRORSOCCURRED é retornado quando DBPROP_COL_PRIMARYKEY e DBPROP_COL_UNIQUE são VARIANT_TRUE e *dwOption* é igual a DBPROPOPTIONS_REQUIRED. A coluna é definida com a propriedade de identidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o membro *dwStatus* de DBPROP_COL_PRIMARYKEY é definido como DBPROPSTATUS_CONFLICTING.<br /><br /> O provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo retorna DB_S_ERRORSOCCURRED quando DBPROP_COL_NULLABLE e DBPROP_COL_UNIQUE são VARIANT_TRUE e *dwOption* não é DBPROPOPTIONS_REQUIRED.<br /><br /> DB_E_ERRORSOCCURRED é retornado quando DBPROP_COL_NULLABLE e DBPROP_COL_UNIQUE são VARIANT_TRUE e *dwOption* é igual a DBPROPOPTIONS_REQUIRED. A coluna é definida com a propriedade de identidade [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o membro *dwStatus* de DBPROP_COL_NULLABLE é definido como DBPROPSTATUS_CONFLICTING.<br /><br /> O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client retorna um erro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando o consumidor tenta criar uma restrição UNIQUE em uma coluna de tipo de dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inválida. Não é possível definir restrições de UNIQUE em colunas criadas com o tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]bit**do**.|  
  
 Quando o consumidor chama **ITableDefinition:: CreateTable**, o provedor de OLE DB do cliente nativo da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta as propriedades da tabela da seguinte maneira.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|Leitura/gravação: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE Descrição: por padrão, o provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo cria tabelas nomeadas pelo consumidor. Quando VARIANT_TRUE, o provedor de OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client gera um nome de tabela temporário para o consumidor. O consumidor define o parâmetro *pTableID* de **CreateTable** como NULL. O parâmetro *ppTableID* precisa conter um ponteiro válido.|  
  
 Se o consumidor solicitar que um conjunto de linhas seja aberto em uma tabela criada com êxito, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB do cliente nativo abrirá um conjunto de linhas com suporte do cursor. Qualquer propriedade de conjunto de linhas pode ser indicada nos conjuntos de propriedade passados.  
  
 O exemplo a seguir cria uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
// This CREATE TABLE statement shows the details of the table created by   
// the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//    CONSTRAINT PK_OrderDetails  
//         PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
// The PRIMARY KEY constraint is created in an additional example.  
HRESULT CreateTable  
    (  
    ITableDefinition* pITableDefinition  
    )  
    {  
    DBID            dbidTable;  
    const ULONG     nCols = 5;  
    ULONG           nCol;  
    ULONG           nProp;  
    DBCOLUMNDESC    dbcoldesc[nCols];  
  
    HRESULT         hr;  
  
    // Set up column descriptions. First, set default property values for  
    //  the columns.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbcoldesc[nCol].pwszTypeName = NULL;  
        dbcoldesc[nCol].pTypeInfo = NULL;  
        dbcoldesc[nCol].rgPropertySets = new DBPROPSET;  
        dbcoldesc[nCol].pclsid = NULL;  
        dbcoldesc[nCol].cPropertySets = 1;  
        dbcoldesc[nCol].ulColumnSize = 0;  
        dbcoldesc[nCol].dbcid.eKind = DBKIND_NAME;  
        dbcoldesc[nCol].wType = DBTYPE_I4;  
        dbcoldesc[nCol].bPrecision = 0;  
        dbcoldesc[nCol].bScale = 0;  
  
        dbcoldesc[nCol].rgPropertySets[0].rgProperties =   
            new DBPROP[NCOLPROPS_MAX];  
        dbcoldesc[nCol].rgPropertySets[0].cProperties = NCOLPROPS_MAX;  
        dbcoldesc[nCol].rgPropertySets[0].guidPropertySet =  
            DBPROPSET_COLUMN;  
  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                dwOptions = DBPROPOPTIONS_REQUIRED;  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].colid  
                 = DB_NULLID;  
  
            VariantInit(  
                &(dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                    vValue));  
  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt = VT_BOOL;  
            }  
        }  
  
    // Set the column-specific information.  
    dbcoldesc[0].dbcid.uName.pwszName = L"OrderID";  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[0].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[1].dbcid.uName.pwszName = L"ProductID";  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[1].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[2].dbcid.uName.pwszName = L"UnitPrice";  
    dbcoldesc[2].wType = DBTYPE_CY;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[2].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[3].dbcid.uName.pwszName = L"Quantity";  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[3].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[4].dbcid.uName.pwszName = L"Discount";  
    dbcoldesc[4].wType = DBTYPE_NUMERIC;  
    dbcoldesc[4].bPrecision = 2;  
    dbcoldesc[4].bScale = 2;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].dwPropertyID =   
        DBPROP_COL_DEFAULT;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.vt = VT_BSTR;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.bstrVal =  
        SysAllocString(L"0");  
    dbcoldesc[4].rgPropertySets[0].cProperties = 2;  
  
    // Set up the dbid for OrderDetails.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    if (FAILED(hr = pITableDefinition->CreateTable(NULL, &dbidTable,  
        nCols, dbcoldesc, NULL, 0, NULL, NULL, NULL)))  
        {  
        DumpError(pITableDefinition, IID_ITableDefinition);  
        goto SAFE_EXIT;  
        }  
  
SAFE_EXIT:  
    // Clean up dynamic allocation in the property sets.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            if (dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt == VT_BSTR)  
                {  
                SysFreeString(dbcoldesc[nCol].rgPropertySets[0].  
                    rgProperties[nProp].vValue.bstrVal);  
                }  
            }  
  
        delete [] dbcoldesc[nCol].rgPropertySets[0].rgProperties;  
        delete [] dbcoldesc[nCol].rgPropertySets;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
