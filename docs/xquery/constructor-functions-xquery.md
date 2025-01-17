---
title: Funções de construtor (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- constructor functions [XQuery]
ms.assetid: 98562d0e-d0e0-4f62-b001-90acbac67277
author: rothja
ms.author: jroth
ms.openlocfilehash: 7f64c9ff6664410983d9c3ce7ebdbf07e493ca03
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038995"
---
# <a name="constructor-functions-xquery"></a>Funções do construtor (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  De uma entrada especificada, as funções do construtor criam instâncias de qualquer tipo atômico interno XSD definido pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TYP($atomicvalue as xdt:anyAtomicType?  
  
) as TYP?  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *$strval*  
 A cadeia de caracteres que será convertida.  
  
 *TYP*  
 Qualquer tipo XSD interno.  
  
## <a name="remarks"></a>Comentários  
 Há suporte para construtores de tipos base e XSD derivados atômicos. No entanto, os subtipos **xs: Duration**, que inclui **XDT: yearmonthduration e XDT: daytimeduration**, e **xs: QName**, **xs: NMTOKEN**, e **xs: Notation** não têm suporte. Tipos atômicos definidos pelo usuário, que estejam disponíveis nas coleções de esquemas associadas também estarão disponíveis, desde que eles sejam direta ou indiretamente derivados dos tipos a seguir.  
  
#### <a name="supported-base-types"></a>Tipos de base com suporte  
 Esses são os tipos base com suporte:  
  
-   xs:string  
  
-   xs:boolean  
  
-   xs:decimal  
  
-   xs:float  
  
-   xs:double  
  
-   xs:duration  
  
-   xs:dateTime  
  
-   xs:time  
  
-   xs:date  
  
-   xs:gYearMonth  
  
-   xs:gYear  
  
-   xs:gMonthDay  
  
-   xs:gDay  
  
-   xs:gMonth  
  
-   xs:hexBinary  
  
-   xs:base64Binary  
  
-   xs:anyURI  
  
#### <a name="supported-derived-types"></a>Tipos derivados com suporte  
 Estes são os tipos derivados com suporte:  
  
-   xs:normalizedString  
  
-   xs:token  
  
-   xs:language  
  
-   xs:Name  
  
-   xs:NCName  
  
-   xs:ID  
  
-   xs:IDREF  
  
-   xs:ENTITY  
  
-   xs:integer  
  
-   xs:nonPositiveInteger  
  
-   xs:negativeInteger  
  
-   xs:long  
  
-   xs:int  
  
-   xs:short  
  
-   xs:byte  
  
-   xs:nonNegativeInteger  
  
-   xs:unsignedLong  
  
-   xs:unsignedInt  
  
-   xs:unsignedShort  
  
-   xs:unsignedByte  
  
-   xs:positiveInteger  
  
 O SQL Server também oferece suporte para dobra constante para invocações de funções de construção nas seguintes maneiras:  
  
-   Se o argumento for uma cadeia de caracteres literal, a expressão será avaliada durante a compilação. Quando o valor não atender às restrições de tipo, um erro estático será gerado.  
  
-   Se o argumento for um literal de outro tipo, a expressão será avaliada durante a compilação. Quando o valor não atender às restrições de tipo, uma sequência vazia será retornada.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery contra instâncias XML armazenadas em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
### <a name="a-using-the-datetime-xquery-function-to-retrieve-older-product-descriptions"></a>A. Usando a função dateTime() XQuery para recuperar descrições de produtos mais antigos  
 Neste exemplo, um documento XML de exemplo é atribuído pela primeira vez para um **xml** variável de tipo. Este documento contém três exemplos <`ProductDescription`> elementos, com cada um deles contendo um <`DateCreated`> elemento filho.  
  
 A variável é então consultada para recuperar apenas aquelas descrições de produtos que tenham sido criados antes de uma data específica. Para fins de comparação, a consulta usa o **xs:dateTime()** a função de construtor para digitar as datas.  
  
```  
declare @x xml  
set @x = '<root>  
<ProductDescription ProductID="1" >  
  <DateCreated DateValue="2000-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription  ProductID="2" >  
  <DateCreated DateValue="2001-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription ProductID="3" >  
  <DateCreated DateValue="2002-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
</root>'  
  
select @x.query('  
     for $PD in  /root/ProductDescription  
     where xs:dateTime(data( ($PD/DateCreated/@DateValue)[1] )) < xs:dateTime("2001-01-01T00:00:00Z")  
     return  
        element Product  
       {   
        ( attribute ProductID { data($PD/@ProductID ) },  
        attribute DateCreated { data( ($PD/DateCreated/@DateValue)[1] ) } )  
        }  
 ')  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O FOR... Estrutura de loop em que é usada para recuperar o \<ProductDescription > elemento que satisfaz a condição especificada na cláusula WHERE.  
  
-   O **DateTime ()** função de construtor é usada para construir **dateTime** digite valores para que eles possam ser comparados adequadamente.  
  
-   A consulta então constrói o XML resultante. Como você está construindo uma sequência de atributos, vírgulas e parênteses são usados na construção XML.  
  
 Esse é o resultado:  
  
```  
<Product   
   ProductID="1"   
   DateCreated="2000-01-01T00:00:00Z"/>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Construção XML &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
