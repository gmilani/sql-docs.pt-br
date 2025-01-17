---
title: Remover um ouvinte do grupo de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.removeaglistener.default.f1
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
ms.assetid: fd9bba9a-d29f-4c23-8ecd-aaa049ed5f1b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 049296ff601296edbd990fe9ea70aef3efa8c44b
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782863"
---
# <a name="remove-an-availability-group-listener-sql-server"></a>Remover um ouvinte de grupo de disponibilidade (SQL Server)
  Este tópico descreve como remover um ouvinte de grupo de disponibilidade em um grupo de disponibilidade AlwaysOn usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para remover um ouvinte usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Prerequisites  
  
-   Você deve estar conectado à instância do servidor que hospeda a réplica primária.  
  
###  <a name="Recommendations"></a> Recomendações  
 Antes de excluir um ouvinte de grupo de disponibilidade, é recomendável verificar se nenhum aplicativo o está usando.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para remover um ouvinte de grupo de disponibilidade**  
  
1.  No Pesquisador de Objetos, conecte-se à instância do servidor que hospeda a réplica primária e clique no nome do servidor para expandir a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Expanda o nó do grupo de disponibilidade e expanda o nó **Ouvintes de Grupos de Disponibilidade** .  
  
4.  Clique com o botão direito do mouse no ouvinte a ser removido e selecione o comando **Excluir** .  
  
5.  Isso abre a caixa de diálogo **Remover Ouvinte do Grupo de Disponibilidade** . Para obter mais informações, consulte [Remover ouvinte do grupo de disponibilidade](#AgListenerPropertiesDialog), posteriormente neste tópico.  
  
###  <a name="AgListenerPropertiesDialog"></a> Remover Ouvinte do Grupo de Disponibilidade (caixa de diálogo)  
 **Name**  
 O nome do ouvinte a ser removido.  
  
 **Resultado**  
 Exibe um link, **Êxito** ou **Erro**, em que você pode clicar para obter mais informações.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 **Para remover um ouvinte de grupo de disponibilidade**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária.  
  
2.  Use a instrução [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) , da seguinte maneira:  
  
     ALTER AVAILABILITY GROUP *group_name* remover ouvinte **' *`dns_name`* '**  
  
     em que *group_name* é o nome do grupo de disponibilidade, e *dns_name* é o nome DNS do ouvinte do grupo de disponibilidade.  
  
     O exemplo a seguir exclui o ouvinte do grupo de disponibilidade `AccountsAG` . O nome DNS é AccountsAG_Listener.  
  
    ```sql
    ALTER AVAILABILITY GROUP AccountsAG REMOVE LISTENER 'AccountsAG_Listener';  
    ```  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para remover um ouvinte de grupo de disponibilidade**  
  
1.  Defina o padrão (`cd`) para a instância de servidor que hospeda a réplica primária.  
  
2.  Use o cmdlet `Remove-Item` interno para remover um ouvinte. Por exemplo, o comando a seguir remove um ouvinte denominado `MyListener` de um grupo de disponibilidade denominado `MyAg`.  
  
    ```powershell
    Remove-Item SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AGListeners\MyListener  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet `Get-Help` no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
##  <a name="RelatedTasks"></a> Tarefas Relacionadas  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Exibir propriedades do ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](view-availability-group-listener-properties-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do &#40;grupos de disponibilidade AlwaysOn&#41; SQL Server](overview-of-always-on-availability-groups-sql-server.md)    
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)  
