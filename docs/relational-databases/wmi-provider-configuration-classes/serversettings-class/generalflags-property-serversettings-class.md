---
title: Propriedade GeneralFlags (ServerSettings)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- GeneralFlags Property (ServerSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- GeneralFlags property
ms.assetid: 129bff8d-d2bc-4297-952f-d0a919d169f7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bd79263e09f1b3eccb4a4efff0ed8ecd036fcc9d
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659297"
---
# <a name="generalflags-property-serversettings-class"></a>Propriedade GeneralFlags (classe ServerSettings)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém os sinalizadores gerais associados com o a instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.GeneralFlags [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe ServerSettings](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md) que representa as configurações de servidor em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Uma matriz de objetos da [classe ServerSettingsGeneralFlag](../../../relational-databases/wmi-provider-configuration-classes/serversettingsgeneralflag-class/serversettingsgeneralflag-class.md) que especificam os sinalizadores gerais associados com a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Configurando protocolos de rede do servidor e bibliotecas net](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
