---
title: Mapeando tipos de dados XSD para tipos de dados XPath (SQLXML 4.0) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- XPath queries [SQLXML], mapping data types
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XPath data types [SQLXML]
- XSD schemas [SQLXML], mapping data types
ms.assetid: ced1a95e-18d4-4a5a-8da8-dbb6d58bbd45
caps.latest.revision: "24"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 19ce96f9e7c7731b669f5186a1b038bade09646e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>Mapeando tipos de dados XSD para tipos de dados XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Quando uma consulta XPath é executada em um esquema XSD e o tipo XSD é especificado no **xsd: Type** atributo, o XPath usa o tipo de dados especificado quando processa a consulta.  
  
 O tipo de dados XPath de um nó é derivado do tipo de dados XSD no esquema, conforme mostra tabela a seguir. (O nó de EmployeeID é usado para fins meramente ilustrativos.)  
  
|Tipo de dados XSD|Tipo de dados XDR|Equivalente<br /><br /> tipos de dados XPath|SQL Server<br /><br /> conversão que é usada|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**Base64Binary**<br /><br /> **HexBinary**|**Nenhuma**<br /><br /> **bin.base64bin.hex**|**Não aplicável**|Nenhuma<br /><br /> EmployeeID|  
|**Booliano**|**booleano**|**booleano**|CONVERT(bit, EmployeeID)|  
|**Decimal, inteiro, float, byte, short, int, long, float, double, unsignedByte, unsignedShort, unsignedInt, unsignedLong**|**número, int, float, i1, i2, i4, i8, r4, r8ui1, ui2, ui4, ui8**|**número**|CONVERT(float(53), EmployeeID)|  
|**ID, idref, idrefsentity, entidades, notação, nmtoken, nmtokens, DateTime, string, AnyURI**|**ID, idref, idrefsentity, entidades, enumeração, notação, nmtoken, nmtokens, char, dateTime, dateTime.tz, string, uri, uuid**|**cadeia de caracteres**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**decimal**|**Fixed 14.4**|**Não aplicável (não há nenhum tipo de dados no XPath equivalente ao tipo de dados XDR Fixed 14.4.)**|CONVERT(money, EmployeeID)|  
|**date**|**date**|**cadeia de caracteres**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**time**|**time**<br /><br /> **time.TZ**|**cadeia de caracteres**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  