---
title: 'Coerção de tipo de dados e a anotação sql: DataType (SQLXML 4,0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- type attribute
- sql:datatype
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- xsd:type
- datatype annotation
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XSD schemas [SQLXML], mapping data types
ms.assetid: db192105-e8aa-4392-b812-9d727918c005
author: MightyPen
ms.author: genemi
ms.reviewer: ''
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fc7393d3f8f52dcbceeb9ef2ca295ef28a7b7222
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72905974"
---
# <a name="data-type-coercions-and-the-sqldatatype-annotation-sqlxml-40"></a>Coerções de tipo de dados e a anotação de sql:datatype (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Em um esquema XSD, o atributo **xsd: Type** especifica o tipo de dados XSD de um elemento ou atributo. Quando um esquema XSD é usado para extrair dados do banco de dados, o tipo de dados especificado é usado para formatar os dados.  
  
 Além de especificar um tipo XSD em um esquema, você também pode especificar um tipo de dados do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a anotação **SQL: DataType** . Os atributos **xsd: Type** e **SQL: DataType** controlam o mapeamento entre tipos de dados XSD e tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="xsdtype-attribute"></a>Atributo xsd:type  
 Você pode usar o atributo **xsd: Type** para especificar o tipo de dados XML de um atributo ou elemento que é mapeado para uma coluna. O **xsd: Type** afeta o documento que é retornado do servidor e também a consulta XPath executada. Quando uma consulta XPath é executada em um esquema de mapeamento que contém **xsd: Type**, o XPath usa o tipo de dados especificado ao processar a consulta. Para obter mais informações sobre como o XPath usa **xsd: Type**, consulte [mapeando tipos de dados XSD &#40;para tipos&#41;de dados XPath SQLXML 4,0](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md).  
  
 Em um documento retornado, todos os tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são convertidos em representações de cadeia de caracteres. Alguns tipos de dados exigem conversões adicionais. A tabela a seguir lista as conversões que são usadas para vários valores **xsd: Type** .  
  
|Tipo de dados XSD|Conversão do SQL Server|  
|-------------------|---------------------------|  
|Booliano|CONVERT(bit, COLUMN)|  
|Data|LEFT(CONVERT(nvarchar(4000), COLUMN, 126), 10)|  
|DECIMAL|CONVERT(money, COLUMN)|  
|id/idref/idrefs|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|nmtoken/nmtokens|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|time|SUBSTRING(CONVERT(nvarchar(4000), COLUMN, 126), 1+CHARINDEX(N'T', CONVERT(nvarchar(4000), COLUMN, 126)), 24)|  
|Todos os outros|Nenhuma conversão adicional|  
  
> [!NOTE]  
>  Alguns dos valores retornados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem não ser compatíveis com os tipos de dados XML que são especificados usando **xsd: Type**, porque a conversão não é possível (por exemplo, converter "XYZ" em um tipo de dados **decimal** ) ou porque o valor excede o intervalo desse tipo de dados (por exemplo,-100000 convertido em um tipo XSD **unsignedShort** ). Conversões de tipo incompatíveis podem resultar em documentos XML que não são válidos ou em erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="mapping-from-sql-server-data-types-to-xsd-data-types"></a>Mapeando dos tipos de dados do SQL Server para os tipos de dados XSD  
 A seguinte tabela mostra um mapeamento óbvio de tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para tipos de dados XSD. Se você souber o tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta tabela fornecerá o tipo XSD correspondente que você pode especificar no esquema XSD.  
  
|Tipo de dados do SQL Server|Tipo de dados XSD|  
|--------------------------|-------------------|  
|**bigint**|**Longas**|  
|**binary**|**base64Binary**|  
|**bit**|**booleano**|  
|**char**|**cadeia de caracteres**|  
|**datetime**|**dateTime**|  
|**decimal**|**decimal**|  
|**float**|**double**|  
|**image**|**base64Binary**|  
|**Int**|**Int**|  
|**money**|**decimal**|  
|**nchar**|**cadeia de caracteres**|  
|**ntext**|**cadeia de caracteres**|  
|**nvarchar**|**cadeia de caracteres**|  
|**numeric**|**decimal**|  
|**real**|**float**|  
|**smalldatetime**|**dateTime**|  
|**smallint**|**short**|  
|**smallmoney**|**decimal**|  
|**sql_variant**|**cadeia de caracteres**|  
|**sysname**|**cadeia de caracteres**|  
|**texto**|**cadeia de caracteres**|  
|**timestamp**|**dateTime**|  
|**tinyint**|**unsignedByte**|  
|**varbinary**|**base64Binary**|  
|**varchar**|**cadeia de caracteres**|  
|**uniqueidentifier**|**cadeia de caracteres**|  
  
## <a name="sqldatatype-annotation"></a>Anotação sql:datatype  
 A anotação **SQL: DataType** é usada para especificar o tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; Esta anotação deve ser especificada quando:  
  
-   Você está carregando em massa em uma coluna de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **DateTime** de um tipo **de data** **/** **hora** XSD. Nesse caso, você deve identificar o tipo de dados da coluna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando **SQL: datatype = "DateTime"** . Esta regra também se aplica a diagramas de atualização.  
  
-   Você está carregando em massa em uma coluna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo **uniqueidentifier** e o valor XSD é um GUID que inclui chaves ({e}). Quando você especifica **SQL: datatype = "uniqueidentifier"** , as chaves são removidas do valor antes de serem inseridas na coluna. Se **SQL: DataType** não for especificado, o valor será enviado com as chaves e a inserção ou atualização falhará.  
  
-   O tipo de dados XML **base64Binary** é mapeado para vários tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (**Binary**, **Image**ou **varbinary**). Para mapear o tipo de dados XML **base64Binary** para um tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] específico, use a anotação **SQL: DataType** . Essa anotação especifica o tipo de dados explícito do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da coluna para a qual o atributo é mapeado. Isto é útil quando os dados estão sendo armazenados nos bancos de dados. Ao especificar a anotação **SQL: DataType** , você pode identificar o tipo de dados explícito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Geralmente, é recomendável que você especifique **SQL: DataType** no esquema.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [Requirements for running SQLXML examples](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-xsdtype"></a>A. Especificando xsd:type  
 Este exemplo mostra como um tipo de **Data** XSD que é especificado usando o atributo **xsd: Type** no esquema afeta o documento XML resultante. O esquema fornece uma exibição XML da tabela Sales.SalesOrderHeader no banco de dados AdventureWorks.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader">  
     <xsd:complexType>  
       <xsd:attribute name="SalesOrderID" type="xsd:string" />   
       <xsd:attribute name="CustomerID"   type="xsd:string" />   
       <xsd:attribute name="OrderDate"    type="xsd:date" />   
       <xsd:attribute name="DueDate"  />   
       <xsd:attribute name="ShipDate"  type="xsd:time" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Nesse esquema de XSD, há três atributos que retornam um valor de data de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando o esquema:  
  
-   Especifica **xsd: Type = Date** no atributo **DataDoPedido** , a parte de data do valor retornado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o atributo **DataDoPedido** é exibido.  
  
-   Especifica **xsd: Type = time** no atributo **ShipDate** , a parte de hora do valor que é retornada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o atributo **ShipDate** é exibida.  
  
-   Não especifica **xsd: Type** no atributo **DueDate** , o mesmo valor que é retornado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é exibido.  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como xsdType.xml.  
  
2.  Copie o modelo a seguir e cole-o em um arquivo de texto. Salve o arquivo como xsdTypeT.xml no mesmo diretório onde você salvou xsdType.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="xsdType.xml">  
        /Order  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho de diretório especificado para o esquema de mapeamento (xsdType.xml) é relativo ao diretório onde o modelo está salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\xsdType.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  

     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o conjunto de resultados parcial:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="43659"   
         CustomerID="676"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
  <Order SalesOrderID="43660"   
         CustomerID="117"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
 ...  
</ROOT>  
```  
  
 Este é o esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader">  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="CustomerID"  />  
    <AttributeType name="OrderDate" dt:type="date" />  
    <AttributeType name="DueDate" />  
    <AttributeType name="ShipDate" dt:type="time" />  
  
    <attribute type="SalesOrderID" sql:field="OrderID" />  
    <attribute type="CustomerID" sql:field="CustomerID" />  
    <attribute type="OrderDate" sql:field="OrderDate" />  
    <attribute type="DueDate" sql:field="DueDate" />  
    <attribute type="ShipDate" sql:field="ShipDate" />  
</ElementType>  
</Schema>  
```  
  
### <a name="b-specifying-sql-data-type-using-sqldatatype"></a>b. Especificando o tipo de dados de SQL usando sql:datatype  
 Para obter um exemplo funcional, consulte o exemplo G nos [exemplos &#40;de carregamento em&#41;massa XML SQLXML 4,0](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md). Nesse exemplo, um valor de GUID que inclui "{" e "}" é carregado em massa. O esquema neste exemplo especifica **SQL: DataType** para identificar o tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como **uniqueidentifier**. Este exemplo ilustra quando **SQL: DataType** deve ser especificado no esquema.  
  
  
