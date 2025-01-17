---
title: Suspender um banco de dados de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.suspenddatamove.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], suspending a database
- Availability Groups [SQL Server], databases
ms.assetid: 86858982-6af1-4e80-9a93-87451f0d7ee9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7c428d9141acfaca3e8ec7876e62b733c30ec161
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797956"
---
# <a name="suspend-an-availability-database-sql-server"></a>Suspender um banco de dados de disponibilidade (SQL Server)
  Você pode suspender um banco de dados de disponibilidade no [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Observe que um comando para suspender precisa ser emitido na instância do servidor que hospeda o banco de dados para ser suspenso ou retomado.  
  
 O efeito de um comando de suspensão depende de se você suspende um banco de dados secundário ou um banco de dados primário, da seguinte maneira:  
  
|Banco de dados suspenso|Efeito do comando de suspensão|  
|------------------------|-------------------------------|  
|Banco de dados secundário|Somente o banco de dados secundário local é suspenso e seu estado de sincronização torna-se NOT SYNCHRONIZING. Outros bancos de dados secundários não são afetados. O banco de dados suspenso para de receber e aplicar dados (registros de log) e começa ficar desatualizado em relação ao banco de dados primário. Conexões existentes nas secundários legíveis permanecem utilizáveis. Novas conexões para o banco de dados suspenso na secundário legível não serão permitidas até que o movimento de dados seja continuado.<br /><br /> O banco de dados primário permanece disponível. Se você suspender cada um dos bancos de dados secundários correspondentes, o banco de dados primário será executado exposto.<br /><br /> **\*\* Importante \*\*** Enquanto um banco de dados secundário permanece suspenso, a fila de envio do banco de dados primário correspondente acumula registros de log de transação não enviados. As conexões para a réplica secundária retornam dados que estavam disponíveis no momento em que o movimento de dados foi suspenso.|  
|Banco de dados primário|O banco de dados primário para o movimento de dados para todos os bancos de dados secundários conectados. O banco de dados primário continua sendo executado em um modo exposto. O banco de dados primário permanece disponível para clientes, e as conexões existentes em um banco de dados secundário legível permanecem utilizáveis e novas conexões podem ser feitas.|  
  
> [!NOTE]  
>  Suspender um banco de dados secundário AlwaysOn não afetam diretamente a disponibilidade do banco de dados primário. Porém, suspender um banco de dados secundário pode afetar os recursos de redundância e failover para o banco de dados primário. Isto está em contraste com o espelhamento de banco de dados, onde o estado de espelhamento é suspenso no banco de dados espelho e no banco de dados principal. Suspender um banco de dados secundário AlwaysOn suspende o movimento de dados em todos os bancos de dados secundários correspondentes, e os recursos de failover e a redundância são eliminados para esse banco de dados até que o banco de dados primário seja retomado.  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para suspender um banco de dados usando:**  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Acompanhamento:** [evitando um log de transações cheio](#FollowUp)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e Restrições  
 O comando SUSPEND retorna assim que é aceito pela réplica que hospeda o banco de dados de destino, mas, na verdade, a suspensão do banco de dados ocorre de forma assíncrona.  
  
###  <a name="Prerequisites"></a> Prerequisites  
 Você deve estar conectado à instância de servidor que hospeda o banco de dados a ser suspenso. Para suspender um banco de dados primários e os bancos de dados secundários correspondentes, conecte-se à instância de servidor que hospeda a réplica primária. Para suspender um banco de dados secundário deixando o banco de dados primário disponível, conecte-se à réplica secundária.  
  
###  <a name="Recommendations"></a> Recomendações  
 Durante gargalos, a suspensão de um ou mais bancos de dados secundários brevemente poderá ser útil para melhorar temporariamente o desempenho na réplica primária. Desde que um banco de dados secundário permaneça suspenso, o log de transações do banco de dados primário correspondente não poderá ser truncado. Isso faz com que os registros de log sejam acumulados no banco de dados primário. Portanto, é recomendável retomar ou remover um banco de dados secundário suspenso rapidamente. Para obter mais informações, consulte [Acompanhamento: evitando um log de transações cheio](#FollowUp), posteriormente neste tópico.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para suspender um banco de dados**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica de disponibilidade na qual você deseja suspender um banco de dados e expanda a árvore de servidores. Para obter mais informações, consulte [Pré-requisitos](#Prerequisites)anteriormente neste tópico.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Expanda o grupo de disponibilidade.  
  
4.  Expanda o nó **Bancos de dados de Disponibilidade** , clique com o botão direito do mouse no banco de dados e clique **Suspender a Movimentação de Dados**.  
  
5.  Na caixa de diálogo **Suspender a Movimentação de Dados** , clique em **OK**.  
  
     O Pesquisador de Objetos indica que o banco de dados está suspenso alterando o ícone de banco de dados para exibir um indicador de pausa.  
  
> [!NOTE]  
>  Para suspender bancos de dados adicionais neste local de réplica, repita as etapas 4 e 5 para cada banco de dados.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 **Para suspender um banco de dados**  
  
1.  Conecte-se à instância do servidor que hospeda a réplica cujo banco de dados você deseja suspender. Para obter mais informações, consulte [Pré-requisitos](#Prerequisites)anteriormente neste tópico.  
  
2.  Suspenda o banco de dados usando a seguinte instrução [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-hadr):  
  
     ALTER DATABASE *database_name* SET HADR SUSPEND  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para suspender um banco de dados**  
  
1.  Altere o diretório (`cd`) para a instância do servidor que hospeda a réplica cujo banco de dados você deseja suspender. Para obter mais informações, consulte [Pré-requisitos](#Prerequisites)anteriormente neste tópico.  
  
2.  Use o cmdlet `Suspend-SqlAvailabilityDatabase` para suspender o grupo de disponibilidade.  
  
     Por exemplo, o comando a seguir suspende a sincronização de dados para o banco de dados de disponibilidade `MyDb3` no grupo de disponibilidade `MyAg` na instância de servidor denominada `Computer\Instance`.  
  
    ```powershell
    Suspend-SqlAvailabilityDatabase -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\Databases\MyDb3  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet `Get-Help` no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> Follow Up: Avoiding a Full Transaction Log  
 Normalmente, quando um ponto de verificação automático é executado em um banco de dados, seu log de transações é truncado àquele ponto de verificação após o próximo backup de log. Porém, enquanto um banco de dados secundário está suspenso, todos os registros de log atuais permanecem ativos no banco de dados primário. Se o log de transações ficar cheio (por ter atingido seu tamanho máximo ou porque a instância de servidor ficou sem espaço), o banco de dados não poderá executar mais nenhuma atualização.  
  
 Para evitar esse problema, você deverá proceder da seguinte maneira:  
  
-   Adicionar mais espaço de log para o banco de dados primário.  
  
-   Retomar o banco de dados secundário antes de o log ficar cheio. Para obter mais informações, consulte [Retomar um banco de dados de disponibilidade &#40;SQL Server&#41;](resume-an-availability-database-sql-server.md).  
  
-   Remover um banco de dados secundário. Para obter mais informações, veja [Remover um banco de dados secundário de um grupo de disponibilidade &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md).  
  
 **Para solucionar problemas de um log de transações completo**  
  
-   [Solução de problemas em um log de transação completa &#40;Erro do SQL Server 9002&#41;](../../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
##  <a name="RelatedTasks"></a> Tarefas Relacionadas  
  
-   [Retomar um banco de dados de disponibilidade &#40;SQL Server&#41;](resume-an-availability-database-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do &#40;grupos de disponibilidade AlwaysOn&#41; SQL Server](overview-of-always-on-availability-groups-sql-server.md)    
 [Retomar um banco de dados de disponibilidade &#40;SQL Server&#41;](resume-an-availability-database-sql-server.md)  
