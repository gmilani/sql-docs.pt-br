---
title: Informações da publicação, agentes (publicação de instantâneo) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.downlevelagents.snapshot.f1
ms.assetid: 599ff80b-392c-43aa-9db2-dc4ed33d4f6e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 47b334cf08e126308544ec2126c96f7da0bed932
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770021"
---
# <a name="publication-information-agents-snapshot-publication"></a>Informações da Publicação, Agentes (publicação de instantâneo)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  A guia **Agentes** exibe informações resumidas sobre o Snapshot Agent para a publicação selecionada.  
  
## <a name="options"></a>Opções  
 Para obter informações mais detalhadas e tarefas relacionadas ao Snapshot Agent, clique com o botão direito do mouse na linha do agente e clique em uma opção no menu de atalho. Para alterar a forma como a grade exibe os dados, clique com o botão direito do mouse na grade e clique em uma destas opções:  
  
-   **Classificar**: classifique uma ou mais colunas na caixa de diálogo **Classificar Colunas**.  
  
-   **Escolher Colunas para Mostrar**: selecione quais colunas devem ser exibidas e a ordem em que devem ser exibidas, na caixa de diálogo **Selecionar Colunas**.  
  
-   **Filtrar**: filtre linhas na grade com base em valores de colunas da caixa de diálogo **Configurações de Filtro**.  
  
-   **Limpar Filtro**: Limpe todas as configurações de filtro para a grade.  
  
 As configurações de filtro são específicas de cada grade. A seleção e a classificação da coluna são aplicadas a todas as grades do mesmo tipo, como a grade de publicações de cada Publicador.  
  
 **Status**  
 O status do Snapshot Agent. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro  
  
-   Tentando novamente comandos com falha  
  
-   Não está sendo executado  
  
-   Concluído  
  
 **Agente**  
 O Snapshot Agent. Essa é a única publicação associada a uma publicação de instantâneo. O Distribution Agent é associado com assinaturas para essa publicação. Para obter mais informações, confira [Exibir informações e executar tarefas usando o Replication Monitor](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 **Última Hora de Início**  
 A última vez que o agente foi iniciado.  
  
 **Duration**  
 O tempo durante o qual o agente foi executado. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total, se o agente foi executado anteriormente.  
  
 **Última Ação**  
 A última ação executada durante a execução mais recente do agente.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas usando o Replication Monitor](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
