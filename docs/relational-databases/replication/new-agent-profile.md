---
title: Novo perfil de agente | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.profiles.newperfprofile.f1
helpviewer_keywords:
- New Agent Profile dialog box
ms.assetid: ebf59330-a421-45a5-9020-0484a96852bc
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 10ddecc4e3c81d48a2824eb48e48495e4f2dec1d
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68764937"
---
# <a name="new-agent-profile"></a>Novo Perfil de Agente
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Use a caixa de diálogo **Novo Perfil de Agente** para criar um novo perfil. Novos perfis sempre são baseados em perfis existentes, mas eles podem ser modificados para atender aos requisitos do aplicativo. Depois que um perfil é criado ele pode ser aplicado a trabalhos de agentes futuros e existentes na caixa de diálogo **Perfis de Agente** . Os valores de parâmetro de agente podem ser editados na caixa de diálogo \<**AgentProfileName> Propriedades**.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Insira um nome para o perfil.  
  
 **Descrição**  
 Insira uma descrição para o perfil.  
  
 **Parâmetro**  
 Os parâmetros de agente incluídos no perfil. O perfil no qual o perfil novo é baseado não especifica necessariamente um valor para cada parâmetro. Para consultar todos os parâmetros válidos de um determinado agente, desmarque a caixa de seleção **Mostrar apenas os parâmetros usados neste perfil** . Para obter descrições de cada parâmetro, consulte.  
  
-   [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
-   [Agente do Leitor de Log de Replicação](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [Agente de Mesclagem de Replicação](../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [Agente de Leitor de Fila de Replicação](../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
 **Valor padrão**  
 O valor padrão para cada parâmetro de agente.  
  
 **Value**  
 O valor especificado para o parâmetro no perfil no qual o perfil novo é baseado. Edite esse campo para obter qualquer valor de parâmetro que você queira alterar.  
  
 **Mostrar apenas os parâmetros usados neste perfil**  
 Desmarque para mostrar todos os parâmetros válidos para um determinado agente.  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhar com perfis do Agente de Replicação](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Perfis do agente de replicação](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  
