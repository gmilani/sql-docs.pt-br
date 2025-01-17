---
title: Categoria de evento Broker | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Broker event category
- Broker event category [SQL Server]
- event classes [SQL Server], Broker event category
ms.assetid: 470dc93c-0dda-4d89-829b-937738d59b31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9918aca57caaef0dc460e810f5ed5ca2d1106ac3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62663805"
---
# <a name="broker-event-category"></a>Categoria de evento Broker
  A categoria de evento **Broker** contém eventos gerais do Service Broker.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Classe de evento Broker:Activation](broker-activation-event-class.md)|Um evento gerado quando um monitor de fila inicia um procedimento armazenado de ativação.|  
|[Classe de evento Broker:Connection](broker-connection-event-class.md)|Um evento gerado para informar o status de uma conexão de transporte gerenciada pelo Service Broker.|  
|[Classe de evento Broker:Conversation](broker-conversation-event-class.md)|Um evento gerado para reportar o progresso de uma conversa.|  
|[Classe de evento Broker:Conversation Group](broker-conversation-group-event-class.md)|Um evento gerado quando o banco de dados cria ou descarta um grupo de conversa.|  
|[Classe de evento Broker:Corrupted Message](broker-corrupted-message-event-class.md)|Um evento gerado para informar que o banco de dados recebeu uma mensagem corrompida.|  
|[Classe de evento Broker:Forwarded Message Dropped](broker-forwarded-message-dropped-event-class.md)|Um evento gerado quando o SQL Server descarta uma mensagem do Service Broker que deveria ter sido encaminhada.|  
|[Classe de evento Broker:Forwarded Message Sent](broker-forwarded-message-sent-event-class.md)|Um evento gerado quando o SQL Server encaminha uma mensagem do Service Broker.|  
|[Classe de evento Broker:Message Classify](broker-message-classify-event-class.md)|Um evento gerado quando o Service Broker determina o roteamento de uma mensagem.|  
|[Classe de evento Broker:Message Drop](broker-message-drop-event-class.md)|Um evento gerado quando o Service Broker é incapaz de reter uma mensagem recebida que deveria ter sido entregue a um serviço dessa instância.|  
|[Agente: Classe de evento Remote Message Ack](broker-remote-message-ack-event-class.md)|Um evento gerado quando o Service Broker envia ou recebe uma confirmação de mensagem.|  
  
 Também são fornecidos dois eventos de auditoria de segurança para o Service Broker. Para obter mais informações sobre esses eventos, consulte [Classe de evento Audit Broker Login](audit-broker-login-event-class.md) e [Classe de evento Audit Broker Conversation](audit-broker-conversation-event-class.md).  
  
## <a name="see-also"></a>Consulte também  
 [Categoria de evento de auditoria de segurança](https://docs.microsoft.com/bi-reference/trace-events/security-audit-event-category)  
  
  
