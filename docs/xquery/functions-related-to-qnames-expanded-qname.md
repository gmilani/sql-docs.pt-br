---
title: expanded-QName (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expanded-QName function
- fn:expanded-QName function
ms.assetid: b8377042-95cc-467b-9ada-fe43cebf4bc3
author: rothja
ms.author: jroth
ms.openlocfilehash: 7c50409ea35809c52de718a8281bf76f75a5a0e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004588"
---
# <a name="functions-related-to-qnames---expanded-qname"></a>Funções Relacionadas a QNames – expanded-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna um valor do tipo xs: QName com o namespace URI especificado na *$paramURI* e o nome local especificado na *$paramLocal*. Se *$paramURI* é a cadeia de caracteres vazia ou a sequência vazia, ele não representará um namespace.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
fn:expanded-QName($paramURI as xs:string?, $paramLocal as xs:string?) as xs:QName?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$paramURI*  
 É o namespace URI para o QName.  
  
 *$paramLocal*  
 É a parte do nome local do QName.  
  
## <a name="remarks"></a>Comentários  
 O seguinte se aplica para o **expanded-QName()** função:  
  
-   Se o *$paramLocal* valor especificado não estiver na forma léxica correta do tipo xs: NCName, a sequência vazia será retornada e representa um erro dinâmico.  
  
-   Não é oferecido suporte à conversão do tipo xs:QName em qualquer outro tipo no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Por isso, o **expanded-QName()** função não pode ser usada na construção XML. Por exemplo, quando você estiver construindo um nó, como `<e> expanded-QName(...) </e>`, o valor precisa ser não digitado. Isso exigiria que você convertesse o valor de tipo xs:QName retornado por `expanded-QName()` para xdt:untypedAtomic. Porém, não é oferecido suporte para isso. Em um exemplo posterior neste tópico é oferecida uma solução.  
  
-   Você pode modificar ou comparar os valores de tipo QName existentes. Por exemplo, `/root[1]/e[1] eq expanded-QName("http://nsURI" "myNS")` compara o valor do elemento <`e`>, com o QName retornado pela **expanded-QName()** função.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery contra instâncias XML armazenadas em várias **xml** colunas de tipo a [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] banco de dados.  
  
### <a name="a-replacing-a-qname-type-node-value"></a>A. Substituindo um valor de nó do tipo QName  
 Este exemplo ilustra como você pode modificar o valor de um nó de elemento do tipo QName. O exemplo executa o seguinte:  
  
-   Cria uma coleção de esquemas XML que define um elemento do tipo QName.  
  
-   Cria uma tabela com uma **xml** coluna de tipo usando a coleção de esquemas XML.  
  
-   Salva uma instância XML na tabela.  
  
-   Usa o **Modify ()** método do tipo de dados xml para modificar o valor do elemento de tipo QName na instância. O **expanded-QName()** função é usada para gerar o novo valor de tipo QName.  
  
```  
-- If XML schema collection (if exists)  
-- drop xml schema collection SC  
-- go  
-- Create XML schema collection  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
    xmlns:xs="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="QNameXSD"   
      xmlns:xqo="QNameXSD" elementFormDefault="qualified">  
      <element name="Root" type="xqo:rootType" />  
      <complexType name="rootType">  
            <sequence minOccurs="1" maxOccurs="1">  
                        <element name="ElemQN" type="xs:QName" />  
            </sequence>  
      </complexType>  
</schema>'  
go  
-- Create table.  
CREATE TABLE T( XmlCol xml(SC) )  
-- Insert sample XML instnace  
INSERT INTO T VALUES ('  
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
      <ElemQN>ns:someName</ElemQN>  
</Root>')  
go  
-- Verify the insertion  
SELECT * from T  
go  
-- Result  
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
  <ElemQN>ns:someName</ElemQN>  
</Root>   
```  
  
 Na consulta a seguir, o <`ElemQN`> valor do elemento é substituído usando o **Modify ()** método de tipo de dados xml e substitua o valor de XML DML, conforme mostrado.  
  
```  
-- the value.  
UPDATE T   
SET XmlCol.modify('  
  declare default element namespace "QNameXSD";   
  replace value of /Root[1]/ElemQN   
  with expanded-QName("https://myURI", "myLocalName") ')  
go  
-- Verify the result  
SELECT * from T  
go  
```  
  
 Este é o resultado. Observe que o elemento <`ElemQN`> de QName tipo agora tem um novo valor:  
  
```  
<Root xmlns="QNameXSD" xmlns:ns="urn">  
  <ElemQN xmlns:p1="https://myURI">p1:myLocalName</ElemQN>  
</Root>  
```  
  
 As instruções a seguir removem os objetos usados no exemplo.  
  
```  
-- Cleanup  
DROP TABLE T  
go  
drop xml schema collection SC  
go  
```  
  
### <a name="b-dealing-with-the-limitations-when-using-the-expanded-qname-function"></a>B. Tratando as limitações ao usar a função expanded-QName()  
 O **expanded-QName** função não pode ser usada na construção XML. O exemplo a seguir ilustra essa situação. Para solucionar essa limitação, o exemplo primeiro insere um nó e, em seguida, modifica o nó.  
  
```  
-- if exists drop the table T  
--drop table T  
-- go  
-- Create XML schema collection  
-- DROP XML SCHEMA COLLECTION SC  
-- go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
 -- Create table T with a typed xml column (using the XML schema collection)  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- Insert an XML instance.  
insert into T values ('<root xmlns:a="https://someURI">a:b</root>')  
 go  
-- Verify  
SELECT *   
FROM T  
```  
  
 A tentativa a seguir adiciona outro <`root`> elemento, mas falha, porque não há suporte para a função expanded-QName() na construção XML.  
  
```  
update T SET xmlCol.modify('  
insert <root>{expanded-QName("http://ns","someLocalName")}</root> as last into / ')  
go  
```  
  
 Uma solução para isso é primeiro inserir uma instância com um valor para o <`root`> elemento e, em seguida, modificá-lo. Neste exemplo, um valor inicial nulo é usado quando o <`root`> elemento é inserido. A coleção de esquemas XML neste exemplo permite um valor nulo para o <`root`> elemento.  
  
```  
update T SET xmlCol.modify('  
insert <root xsi:nil="true"/> as last into / ')  
go  
-- now replace the nil value with another QName.  
update T SET xmlCol.modify('  
replace value of /root[last()] with expanded-QName("http://ns","someLocalName") ')  
go  
 -- verify   
SELECT * FROM T  
go  
-- result  
<root>b</root>  
```  
  
 `<root xmlns:a="https://someURI">a:b</root>`  
  
 `<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p1="http://ns">p1:someLocalName</root>`  
  
 Você pode comparar o valor QName, como mostrado na consulta a seguir. A consulta retorna apenas o <`root`> elementos cujos valores correspondem ao QName de tipo de valor retornado pela **expanded-QName()** função.  
  
```  
SELECT xmlCol.query('  
    for $i in /root  
    return  
       if ($i eq expanded-QName("http://ns","someLocalName") ) then  
          $i  
       else  
          ()')  
FROM T  
```  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Há uma limitação: O **expanded-QName()** função aceita a sequência vazia como o segundo argumento e retorna vazia em vez de gerar um erro de tempo de execução quando o segundo argumento estiver incorreto.  
  
## <a name="see-also"></a>Consulte também  
 [Funções relacionadas a QNames &#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
