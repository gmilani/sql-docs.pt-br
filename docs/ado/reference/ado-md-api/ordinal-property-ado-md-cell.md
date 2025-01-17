---
title: Propriedade ordinal (célula do ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 194b72ce66eb2efdc3a246f24948b01c790f7b8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949371"
---
# <a name="ordinal-property-ado-md-cell"></a>Propriedade Ordinal (Célula do ADO MD)
Identifica exclusivamente um [célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md) por sua posição dentro de um conjunto de células.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **longo** inteiro e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 O valor da célula ordinal identifica exclusivamente a célula dentro de um conjunto de células. Conceitualmente, as células são numeradas em um conjunto de células como se fosse o conjunto de células uma *p*-matriz dimensional, onde *p* é o número de [eixos](../../../ado/reference/ado-md-api/axes-collection-ado-md.md). As células são numeradas a partir do zero na ordem de linha principal. Aqui está a fórmula para calcular o número ordinal de uma célula:  
  
 O valor da célula ordinal que pode ser usado com o [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propriedade da [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto para recuperar rapidamente o [célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo Axis (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Propriedade item (conjunto de células do ADO MD)](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Propriedade Ordinal (Posição do ADO MD)](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)
