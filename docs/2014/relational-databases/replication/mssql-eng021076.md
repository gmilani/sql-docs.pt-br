---
title: MSSQL_ENG021076 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021076 error
ms.assetid: 612e5c59-ba3e-49c3-a3df-56bac3d850a2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 23bd163d63fa3939e35facc49cb3be7f8f07ff91
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63023213"
---
# <a name="mssqleng021076"></a>MSSQL_ENG021076
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|21076|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O instantâneo inicial do artigo '%s' ainda não está disponível.|  
  
## <a name="explanation"></a>Explicação  
 O erro MSSQL_ENG021076 pode ser gerado se o Distribution Agent for iniciado antes do Snapshot Agent terminar de gerar o instantâneo. Esse erro só será gerado se a publicação possuir um único artigo. Se a publicação possuir mais de um artigo, será gerado o erro MSSQL_ENG021075. Para obter mais informações, consulte [MSSQL_ENG021075](mssql-eng021075.md).  
  
## <a name="user-action"></a>Ação do usuário  
 Se o Snapshot Agent da publicação não for iniciado até que a assinatura seja criada, ou se não tiver sido iniciado desde que você optou por reiniciar a assinatura, inicie o Snapshot Agent e aguarde sua conclusão antes de iniciar o Distribution Agent. Para obter mais informações, consulte [Create and Apply the Snapshot](create-and-apply-the-snapshot.md) (Criar e aplicar o instantâneo).  
  
 Se o Agente de Instantâneo não for concluído, verifique o histórico do Agente de Instantâneo em relação a erros e faça o diagnóstico. Para obter informações sobre exibir detalhes de status e de erro do agente no Replication Monitor, confira [Exibir informações e executar tarefas usando o Replication Monitor](monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 Se o erro continuar ocorrendo, aumente o log do agente e especifique um arquivo de saída para o log. Dependendo do contexto do erro, isso poderá fornecer as etapas que levaram ao erro e/ou as mensagens de erros adicionais.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)  
  
  
