---
title: "Método SetValue (classe ClientSettingsGeneralFlag) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: SetValue Method (ClientSettingsGeneralFlag Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: SetValue method
ms.assetid: 34443689-a0e0-4668-a811-17532c6fd271
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 01d281c30ea34ad6a17e59578bfd64a9b3a93fe3
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="setvalue-method-clientsettingsgeneralflag-class"></a>Método SetValue (classe ClientSettingsGeneralFlag)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Define todos os valores do sinalizador referenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.SetValue(Value)  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Um objeto da [classe ClientSettingsGeneralFlag](../../../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md) que representa um sinalizador geral para as configurações de servidor.  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Description|  
|---------------|-----------------|  
|*Value*|Um valor booliano que especifica o valor do sinalizador.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor **uint32** , que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Configurar protocolos de cliente](http://technet.microsoft.com/library/ms181035.aspx)  
  
  