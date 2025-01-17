---
title: Posicionamento do conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdce4c7b08a8b15cdb0a9ee1111a216aeef005bf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924439"
---
# <a name="recordset-positioning"></a>Posicionamento do conjunto de registros
Use o **AbsolutePosition** propriedade para mover para um registro, com base em sua posição ordinal na **Recordset** objeto, ou para determinar a posição ordinal do registro atual. O provedor deve oferecer suporte a funcionalidade apropriada para essa propriedade estar disponível.  
  
 **Exemplo de AbsolutePosition** é baseado em 1 e é igual a 1 quando o registro atual é o primeiro registro na **conjunto de registros**. Conforme mencionado anteriormente, você pode obter o número total de registros na **conjunto de registros** objeto o **RecordCount** propriedade.  
  
 Quando você define o **AbsolutePosition** propriedade, mesmo se for para um registro no cache atual, ADO recarrega o cache com um novo grupo de registros que começam com o registro especificado. O **CacheSize** propriedade determina o tamanho desse grupo.  
  
> [!NOTE]
>  Você não deve usar o **AbsolutePosition** a propriedade como um número de registro de substituto. A posição de um determinado registro muda quando você exclui um registro anterior. Também não há nenhuma garantia de que um determinado registro têm a mesma **AbsolutePosition** se o **Recordset** objeto será novamente consultado ou reaberto. Indicadores são a maneira recomendada de reter e retornar para uma determinada posição e são a única maneira de posicionamento em todos os tipos de **Recordset** objetos.
