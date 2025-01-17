---
title: PDW status dos serviços - Analytics Platform System | Microsoft Docs
description: Parallel Data Warehouse (PDW) serviços de status para o Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3db994b4869c1b017a079b404af3d95db1316dad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960362"
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>Status dos serviços de Parallel Data Warehouse para o Analytics Platform System
O Parallel Data Warehouse **Status de serviços** página no Microsoft Analytics Platform System Configuration Manager mostra o status atual de todos os serviços do SQL Server PDW e fornece a capacidade de parar e iniciar os serviços do PDW. Isso é o único método suportado para iniciar e interromper os serviços do PDW. Observe que componentes individuais ou serviços não podem ser iniciados independentemente.  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>Para iniciar ou parar os serviços do dispositivo  
  
1.  Para iniciar os serviços do dispositivo, clique em **Appliance iniciar**.  
  
2.  Para interromper os serviços do dispositivo, clique em **parar dispositivo**.  
  
Não é necessário clicar **Apply** quando iniciar e parar os serviços de dispositivo usando **iniciar dispositivo** e **parar dispositivo**.  
  
![DWConfig Appliance PDW Services](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> Também Parando a região PDW interrompe o agente do PDW (sqldwagent) em nós. O agente do PDW exige que o nó de controle do PDW para relatar o monitoramento de integridade.  
  
## <a name="see-also"></a>Consulte também  
[Ligar o dispositivo de APS ou desligar &#40;Analytics Platform System&#41;](power-the-aps-appliance-on-or-off.md)  
  
