---
title: Trabalhar com perfis do agente de replicação | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], agents and profiles
- replication agent profiles [SQL Server]
- agents [SQL Server replication], profiles
- profiles [SQL Server], replication agents
ms.assetid: 9c290a88-4e9f-4a7e-aab5-4442137a9918
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 93ee480a595178627f65613b502c10e44dffc8e3
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907804"
---
# <a name="work-with-replication-agent-profiles"></a>Trabalhar com perfis do agente de replicação
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Este tópico descreve como trabalhar com perfis do Agente de Replicação no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o RMO (Replication Management Objects). O comportamento de cada agente de replicação é controlado por um conjunto de parâmetros que podem ser definidos através dos perfis de agente. Cada agente tem um perfil padrão, e alguns têm perfis adicionais predefinidos; em um determinado momento, apenas um perfil está ativo para um agente.  
  
 **Neste tópico**  
  
-   **Para trabalhar com perfis do Agente de Replicação, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
    -   Acesse a caixa de diálogo Perfis de Agente  
  
    -   Especifique um perfil para um agente  
  
    -   Crie um perfil  
  
    -   Modifique um perfil  
  
    -   Exclua um perfil  
  
     [Transact-SQL](#TsqlProcedure)  
  
    -   Crie um perfil  
  
    -   Modifique um perfil  
  
    -   Exclua um perfil  
  
    -   Use perfis de agente durante a sincronização  
  
    -   Exemplo de Transact-SQL  
  
     [Replication Management Objects](#RMOProcedure)  
  
    -   Crie um perfil  
  
    -   Modifique um perfil  
  
    -   Exclua um perfil  
  
-   **Acompanhamento:**  [depois de alterar parâmetros de agente](#FollowUp)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
###  <a name="Access_SSMS"></a> Para acessar a caixa de diálogo Perfis do Agente a partir do SQL Server Management Studio  
  
1.  Na página **Geral** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>** , clique em **Padrões de Perfil**.  

#### <a name="to-access-the-agent-profiles-dialog-box-from-replication-monitor"></a>Para acessar a caixa de diálogo Perfis do Agente a partir do Replication Monitor  
  
-   Para abrir a caixa de diálogo para todos os agentes, clique com o botão direito em um Publicador e, em seguida, clique em **Perfis do Agente**.  
  
-   Para abrir a caixa de diálogo para um único agente:  
  
    1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor, expanda um Publicador e, em seguida, clique em uma publicação.  
  
    2.  Para os perfis de Distribution Agent ou Merge Agent, clique em uma assinatura com o botão direito na guia **Todas as Assinaturas** e então clique em **Perfil do Agente**. Para outros agentes, clique com o botão direito do mouse no agente na guia **Agentes** e, em seguida, clique em **Perfil do Agente**.  
  
###  <a name="Specify_SSMS"></a> Para especificar o perfil para um agente  
  
1.  Se a caixa de diálogo **Perfis do Agente** exibir perfis para mais de um agente, selecione um agente.  
  
2.  Selecione um perfil na coluna **Padrão para Novo** da grade **Perfis do Agente** . Por padrão, o perfil só é aplicado aos agentes para publicações e assinaturas novas.  
  
3.  Para especificar que todos os agentes de um tipo selecionado para publicações ou assinaturas existentes usem esse perfil, clique em **Alterar agentes existentes**.  
  
###  <a name="Modify_SSMS"></a> Para exibir e editar os parâmetros associados a um perfil  
  
1.  Se a caixa de diálogo **Perfis do Agente** exibir perfis para mais de um agente, selecione um agente.  
  
2.  Clique no botão de propriedades ( **…** ) ao lado de um perfil.  
  
3.  Exiba os parâmetros e valores na caixa de diálogo **Propriedades do Perfil \<ProfileName>** .  
  
    -   Os parâmetros em perfis definidos pelo usuário podem ser editados; os parâmetros em perfis de sistema predefinidos não podem.  
  
    -   Para exibir todos os parâmetros de um agente, desmarque a caixa de seleção **Mostrar apenas os parâmetros usados neste perfil** . Para obter informações sobre parâmetros de agente, consulte os links no final deste tópico.  
  
4.  Clique em **Fechar**.  
  
###  <a name="Create_SSMS"></a> Para criar um perfil definido pelo usuário  
  
1.  Se a caixa de diálogo **Perfis do Agente** exibir perfis para mais de um agente, selecione um agente.  
  
2.  Clique em **Nova**.  
  
3.  Na caixa de diálogo de inicialização **Novo Perfil do Agente** , selecione um perfil existente no qual o novo perfil será baseado.  
  
4.  Na caixa de diálogo **Novo Perfil do Agente** , digite os valores nas caixas de texto **Nome** e **Descrição** .  
  
5.  Modificar parâmetros para personalizar o perfil. Para exibir todos os parâmetros de um agente, desmarque a caixa de seleção **Mostrar apenas os parâmetros usados neste perfil** . Para obter informações sobre parâmetros de agente, consulte os links no final deste tópico.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
###  <a name="Delete_SSMS"></a> Para excluir um perfil definido pelo usuário  
  
1.  Se a caixa de diálogo **Perfis do Agente** exibir perfis para mais de um agente, selecione um agente.  
  
2.  Se um perfil for associado a um ou mais agentes, altere o perfil para esses agentes:  
  
    1.  Selecione um perfil diferente na grade **Perfis do Agente** .  
  
    2.  Clique em **Alterar Agentes Existentes**.  
  
        > [!NOTE]  
        >  Isso alterará o perfil para todos os agentes do tipo selecionado para publicações ou assinaturas existentes, não apenas para os que usam o perfil que se deseja excluir.  
  
3.  Selecione o perfil a ser excluído e, em seguida, clique em **Excluir**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
###  <a name="Create_tsql"></a> Para criar um perfil novo de agente  
  
1.  No Distribuidor, execute [sp_add_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md). Especifique **\@name**, um valor igual a **1** em **\@profile_type** e um dos seguintes valores em **\@agent_type**:  
  
    -   **1** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Se esse perfil se tornar o novo perfil padrão para o tipo de agente de replicação, especifique um valor igual a **1** em **\@default**. O identificador para o novo perfil é retornado com o uso do parâmetro de saída **\@profile_id**. Isso cria um perfil novo com um conjunto de parâmetros de perfis baseado no perfil padrão para o tipo de agente especificado.  
  
2.  Depois que o perfil novo for criado, adicione, remova ou modifique os parâmetros padrão para personalizar o perfil.  
  
###  <a name="Modify_tsql"></a> Para modificar um perfil de agente existente  
  
1.  No Distribuidor, execute [sp_help_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md). Especifique um dos seguintes valores em **\@agent_type**:  
  
    -   **1** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Isso retorna todos os perfis para o tipo especificado de agente. Observe o valor de **profile_id** no conjunto de resultados para o perfil a ser alterado.  
  
2.  No Distribuidor, execute [sp_help_agent_parameter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md). Especifique o identificador de perfil da etapa 1 em **\@profile_id**. Isso retorna todos os parâmetros para o perfil. Observe o nome de qualquer parâmetro a modificar ou remover do perfil.  
  
3.  Para alterar o valor de um parâmetro em um perfil, execute [sp_change_agent_parameter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md). Especifique o identificador de perfil da etapa 1 em **\@profile_id**, o nome do parâmetro a ser alterado em **\@parameter_name** e um novo valor do parâmetro em **\@parameter_value**.  
  
    > [!NOTE]  
    >  Você não pode alterar um perfil de agente existente para se tornar o perfil padrão para um agente. Em vez disso, você deve criar um perfil novo como perfil padrão, como mostrado no procedimento anterior.  
  
4.  Para remover um parâmetro de um perfil, execute [sp_drop_agent_parameter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md). Especifique o identificador de perfil da etapa 1 em **\@profile_id** e o nome do parâmetro a ser removido em **\@parameter_name**.  
  
5.  Para adicionar um parâmetro novo a um perfil, você deve fazer o seguinte:  
  
    -   Examine a tabela do [MSagentparameterlist &#40;Transact-SQL&#41;](../../../relational-databases/system-tables/msagentparameterlist-transact-sql.md) no Distribuidor para determinar quais parâmetros de perfil podem ser definidos para cada tipo de agente.  
  
    -   No Distribuidor, execute [sp_add_agent_parameter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md). Especifique o identificador de perfil da etapa 1 em **\@profile_id**, o nome de um parâmetro válido a ser adicionado em **\@parameter_name** e o valor do parâmetro em **\@parameter_value**.  
  
###  <a name="Delete_tsql"></a> Para excluir um perfil de agente  
  
1.  No Distribuidor, execute [sp_help_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md). Especifique um dos seguintes valores em **\@agent_type**:  
  
    -   **1** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Isso retorna todos os perfis para o tipo especificado de agente. Observe o valor de **profile_id** no conjunto de resultados para o perfil a remover.  
  
2.  No Distribuidor, execute [sp_drop_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md). Especifique o identificador de perfil da etapa 1 em **\@profile_id**.  
  
###  <a name="Synch_tsql"></a> Para usar perfis de agente durante sincronização  
  
1.  No Distribuidor, execute [sp_help_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md). Especifique um dos seguintes valores em **\@agent_type**:  
  
    -   **1** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Isso retorna todos os perfis para o tipo especificado de agente. Observe o valor de **profile_name** no conjunto de resultados para o perfil a usar.  
  
2.  Se o agente for iniciado a partir do trabalho de agente, edite a etapa de trabalho que inicia o agente para especificar o valor **profile_name** obtido na etapa 1, depois do parâmetro do comando em linha **-ProfileName** . Para obter mais informações, consulte [Exibir e modificar parâmetros do prompt de comando do agente de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md).  
  
3.  Ao iniciar o agente no prompt de comando, especifique o valor **profile_name** obtido na etapa 1, depois do parâmetro da linha de comando **-ProfileName** .  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Este exemplo cria um perfil personalizado para o Agente de Mesclagem nomeado **custom_merge**, altera o valor do parâmetro **-UploadReadChangesPerBatch** , adiciona um novo parâmetro **-ExchangeType** e retorna informações sobre o perfil criado.  
  
 [!code-sql[HowTo#sp_addagentprofileparam](../../../relational-databases/replication/codesnippet/tsql/work-with-replication-ag_1.sql)]  
  
##  <a name="RMOProcedure"></a> Usando RMO  
  
###  <a name="Create_RMO"></a> Para criar um perfil novo de agente  
  
1.  Crie uma conexão para o Distribuidor usando uma instância da classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.AgentProfile> .  
  
3.  Defina as seguintes propriedades no objeto:  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> - o nome para o perfil.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AgentType%2A> - um valor <xref:Microsoft.SqlServer.Replication.AgentType> que especifica o tipo de agente de replicação para o qual está sendo criado o perfil.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criado na etapa 1.  
  
    -   (Opcional) <xref:Microsoft.SqlServer.Replication.AgentProfile.Description%2A> - uma descrição do perfil.  
  
    -   (Opcional) <xref:Microsoft.SqlServer.Replication.AgentProfile.Default%2A> - defina essa propriedade para **true** se todos os trabalhos de agente novos para essa <xref:Microsoft.SqlServer.Replication.AgentType> utilizarão, por padrão, esse perfil.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.AgentProfile.Create%2A> para criar o perfil no servidor.  
  
5.  Uma vez que o perfil existir no servidor, você poderá personalizá-lo adicionando, removendo ou modificando os valores dos parâmetros do agente de replicação.  
  
6.  Para atribuir o perfil a um trabalho de agente de replicação existente, chame o método <xref:Microsoft.SqlServer.Replication.AgentProfile.AssignToAgent%2A> . Passe o nome do banco de dados de distribuição para *distributionDBName* e a ID do trabalho para *agentID*.  
  
###  <a name="Modify_RMO"></a> Para modificar um perfil de agente existente  
  
1.  Crie uma conexão para o Distribuidor usando uma instância da classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationServer> . Passe o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criado na etapa 1.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se esse método retornar **false**, verifique se o Distribuidor existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumAgentProfiles%2A> . Passe um valor <xref:Microsoft.SqlServer.Replication.AgentType> para reduzir os perfis retornados a um tipo específico de agente de replicação.  
  
5.  Obtenha o objeto desejado <xref:Microsoft.SqlServer.Replication.AgentProfile> dos <xref:System.Collections.ArrayList>retornados, nos quais a propriedade <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> do objeto corresponda ao nome do perfil.  
  
6.  Chame um dos métodos seguintes de <xref:Microsoft.SqlServer.Replication.AgentProfile> para alterar o perfil:  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AddParameter%2A> - adiciona um parâmetro com suporte ao perfil, onde *name* é o nome parâmetro do agente de replicação e *value* é o valor especificado. Para enumerar todos os parâmetros de agente com suporte para um determinado tipo de agente, chame o método <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> . Este método retorna um <xref:System.Collections.ArrayList> de objetos <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> que representam todos os parâmetros com suporte.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.RemoveParameter%2A> - remove um parâmetro existente do perfil, onde *name* é o nome do parâmetro do agente de replicação. Para enumerar todos os parâmetros de agente atuais definidos para o perfil, chame o método <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> . Este método retorna um <xref:System.Collections.ArrayList> de objetos <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> que representam o parâmetro existente para este perfil.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.ChangeParameter%2A> - altera a configuração de um parâmetro existente no perfil, onde *name* é o nome do parâmetro do agente de replicação e *newValue* é o valor para o qual o parâmetro está sendo alterado. Para enumerar todos os parâmetros de agente atuais definidos para o perfil, chame o método <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> . Este método retorna um <xref:System.Collections.ArrayList> de objetos <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> que representam o parâmetro existente para este perfil. Para enumerar todas as configurações de parâmetro de agente com suporte, chame o método <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> . Este método retorna um <xref:System.Collections.ArrayList> de objetos <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> que representam os valores com suporte para todos os parâmetros.  
  
###  <a name="Delete_RMO"></a> Para excluir um perfil de agente  
  
1.  Crie uma conexão para o Distribuidor usando uma instância da classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.AgentProfile> . Defina o nome do perfil para <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> e o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se este método retornar **false**, o banco de dados com o nome especificado estava incorreto ou o perfil não existe no servidor.  
  
4.  Verifique se a propriedade <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A> é definida como <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.User>, o que indica um perfil de cliente. Você não deve remover um perfil que possui um valor de <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.System> para <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A>.  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.AgentProfile.Remove%2A> para remover o perfil definido pelo usuário representado por esse objeto do servidor.  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de alterar parâmetros de agente  
As alterações do parâmetro de agente entrarão em vigor na próxima vez o agente for iniciado. Se o agente ficar executando continuamente, será necessário parar e reiniciar o agente. Começando com o SQL Server 2017 CU3, algumas alterações de parâmetro de agente entram em vigor sem precisar reiniciar os agentes. 
  
## <a name="see-also"></a>Consulte Também  
 [Perfis do agente de replicação](../../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
  
