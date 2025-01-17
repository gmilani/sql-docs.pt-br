---
title: Propriedade (Erro ADO) de origem | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::get_Source
- Error::Source
- Error::GetSource
helpviewer_keywords:
- Source property [ADO Error]
ms.assetid: 4044ba15-f013-4c4c-9fe1-b4410fe9a778
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b55ebbe5a167b7d70cf606fc4e37e7ede36b486
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916901"
---
# <a name="source-property-ado-error"></a>Propriedade Source (Erro ADO)
Indica o nome do objeto ou aplicativo que originalmente gerou um erro.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um **cadeia de caracteres** valor que indica o nome de um objeto ou aplicativo.  
  
## <a name="remarks"></a>Comentários  
 Use o **fonte** propriedade em um [erro](../../../ado/reference/ado-api/error-object.md) objeto para determinar o nome do objeto ou aplicativo que originalmente gerou um erro. Isso pode ser o nome de classe do objeto ou o ID programática. Para erros no ADO, o valor da propriedade serão **ADODB.** _ObjectName_, onde *ObjectName* é o nome do objeto que disparou o erro. Para ADOX e ADO MD, o valor será **ADOX.** _ObjectName_ e **ADOMD.** _ObjectName_, respectivamente.  
  
 Com base na documentação de erro dos **fonte**, [número](../../../ado/reference/ado-api/number-property-ado.md), e [descrição](../../../ado/reference/ado-api/description-property.md) propriedades do **erro** objetos, você pode escrever código que manipulará o erro adequadamente.  
  
 O **fonte** propriedade é somente leitura para **erro** objetos.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Descrição, HelpContext, HelpFile, NativeError, número, código-fonte e exemplo de propriedades de SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Descrição, HelpContext, HelpFile, NativeError, número, código-fonte e SQLState exemplo das propriedades (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Propriedade Description](../../../ado/reference/ado-api/description-property.md)   
 [Propriedades HelpContext, HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Propriedade Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Propriedade Source (registro ADO)](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Propriedade Source (Conjunto de registros ADO)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
