---
title: A réplica de disponibilidade está desconectada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.agdashboard.arp2connected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 1a2162d3-54fb-4356-b349-effbdc15a5a4
caps.latest.revision: 10
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: fb94df7f1a442dcb3dc25193a38d055ccc15e446
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122470"
---
# <a name="availability-replica-is-disconnected"></a>A réplica de disponibilidade está desconectada
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado da Conexão da Réplica de Disponibilidade|  
|**Problema**|A réplica de disponibilidade está desconectada.|  
|**Categoria**|**Crítico**|  
|**Faceta**|Réplica de disponibilidade|  
  
## <a name="description"></a>Description  
 Esta política verifica o estado da conexão entre as réplicas de disponibilidade. O estado da política é não íntegro quando o estado de conexão da réplica de disponibilidade é DISCONNECTED. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre possíveis causas e soluções estão localizadas em [A réplica de disponibilidade está desconectada](http://go.microsoft.com/fwlink/p/?LinkId=220857) no TechNet Wiki.  
  
## <a name="possible-causes"></a>Causas possíveis  
 A réplica secundária não está conectada à réplica primária. O estado de conexão é DISCONNECTED. Esse problema pode ter sido causado pelo seguinte:  
  
-   A porta de conexão pode estar em conflito com outro aplicativo.  
  
-   O tipo de criptografia ou algoritmo é incompatível.  
  
-   O ponto de extremidade de conexão foi excluído ou não foi iniciado.  
  
-   O transporte está desconectado.  
  
## <a name="possible-solutions"></a>Soluções possíveis  
 Estas são as possíveis soluções para este problema:  
  
-   Verifique a configuração de ponto de extremidade de espelhamento de banco de dados para as instâncias da réplica primária e secundária e atualize a configuração incompatível.  
  
-   Verifique se a porta está em conflito, e se estiver, altere o número da porta.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade do AlwaysOn &#40;do SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  