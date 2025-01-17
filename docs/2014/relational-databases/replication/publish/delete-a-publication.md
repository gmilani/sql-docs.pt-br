---
title: Excluir uma publicação | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- removing publications
- publications [SQL Server replication], deleting
- articles [SQL Server replication], deleting
- deleting publications
ms.assetid: 408a1360-12ee-4896-ac94-482ae839593b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fa08a7f84cd413f1212cc73d4242b5da70fd33eb
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882286"
---
# <a name="delete-a-publication"></a>Delete a Publication
  Este tópico descreve como excluir uma publicação no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Para excluir uma publicação, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Exclua publicações da pasta **Publicações Locais** no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-delete-a-publication"></a>Para excluir uma publicação  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com o botão direito na publicação que você deseja excluir e clique em **Excluir**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 As publicações podem ser excluídas programaticamente usando procedimentos armazenados de replicação. Os procedimentos armazenados que você usar dependerão do tipo de publicação a ser excluída.  
  
> [!NOTE]  
>  Excluir uma publicação não remove objetos publicados do banco de dados de publicação ou objetos correspondentes do banco de dados de assinatura. Use o comando `DROP <object>` para remover esses objetos manualmente, se necessário.  
  
#### <a name="to-delete-a-snapshot-or-transactional-publication"></a>Para excluir uma publicação de instantâneo ou transacional  
  
1.  Siga um destes procedimentos:  
  
    -   Para excluir uma única publicação, execute [sp_droppublication](/sql/relational-databases/system-stored-procedures/sp-droppublication-transact-sql) no Publicador do banco de dados de publicação.  
  
    -   Para excluir todas as publicações e remover todos os objetos de replicação de um banco de dados publicado, execute [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) no Publicador. Especifique um valor de `tran` para **\@tipo**. (Opcional) Se o Distribuidor não puder ser acessado ou se o status do banco de dados for suspeito ou estiver offline, especifique um valor igual a **1** em **\@force**. (Opcional) Especifique o nome do banco de dados em **\@dbname** se [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) não for executado no banco de dados de publicação.  
  
        > [!NOTE]  
        >  A especificação de um valor igual a **1** em **\@force** pode manter objetos de publicação relacionados à replicação no banco de dados.  
  
2.  (Opcional) Se esse banco de dados não tiver outras publicações, execute [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql) para desabilitar a publicação do banco de dados atual usando replicação de instantâneo ou transacional.  
  
3.  (Opcional) No Assinante no banco de dados de assinatura, execute [sp_subscription_cleanup](/sql/relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql) para remover quaisquer metadados de replicação remanescentes no banco de dados de assinatura.  
  
#### <a name="to-delete-a-merge-publication"></a>Para excluir uma publicação de mesclagem  
  
1.  Siga um destes procedimentos:  
  
    -   Para excluir uma única publicação, execute [sp_dropmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql) no Publicador do banco de dados de publicação.  
  
    -   Para excluir todas as publicações e remover todos os objetos de replicação de um banco de dados publicado, execute [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) no Publicador. Especifique um valor de `merge` para **\@tipo**. (Opcional) Se o Distribuidor não puder ser acessado ou se o status do banco de dados for suspeito ou estiver offline, especifique um valor igual a **1** em **\@force**. (Opcional) Especifique o nome do banco de dados em **\@dbname** se [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) não for executado no banco de dados de publicação.  
  
        > [!NOTE]  
        >  A especificação de um valor igual a **1** em **\@force** pode manter objetos de publicação relacionados à replicação no banco de dados.  
  
2.  (Opcional) Se esse banco de dados não tiver outras publicações, execute [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql) para desabilitar a publicação do banco de dados atual usando replicação de mesclagem.  
  
3.  (Opcional) No Assinante no banco de dados de assinatura, execute [sp_mergesubscription_cleanup &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql) para remover quaisquer metadados de replicação remanescentes no banco de dados de assinatura.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Este exemplo mostra como remover uma publicação transacional e desabilitar publicação transacional para um banco de dados. Este exemplo pressupõe que todas as assinaturas foram previamente removidas. Para obter mais informações, consulte [Delete a Pull Subscription](../delete-a-pull-subscription.md) ou [Delete a Push Subscription](../delete-a-push-subscription.md).  
  
 [!code-sql[HowTo#sp_droppublication](../../../snippets/tsql/SQL15/replication/howto/tsql/droptranpub.sql#sp_droppublication)]  
  
 Este exemplo mostra como remover uma publicação de mesclagem e desabilitar publicação de mesclagem para um banco de dados. Este exemplo pressupõe que todas as assinaturas foram previamente removidas. Para obter mais informações, consulte [Delete a Pull Subscription](../delete-a-pull-subscription.md) ou [Delete a Push Subscription](../delete-a-push-subscription.md).  
  
 [!code-sql[HowTo#sp_dropmergepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/dropmergepub.sql#sp_dropmergepublication)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 É possível excluir publicações de forma programada usando o RMO (Replication Management Objects). As classes de RMO usadas para remover uma publicação dependem do tipo de publicação a ser removida.  
  
#### <a name="to-remove-a-snapshot-or-transactional-publication"></a>Para remover uma publicação transacional ou instantâneo  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPublication> .  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para a publicação, e a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a conexão criada na etapa 1.  
  
4.  Verifique a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para saber se a publicação existe. Se o valor dessa propriedade for `false`, as propriedades de publicação na etapa 3 foram definidas incorretamente ou a publicação não existe.  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> .  
  
6.  (Opcional) Se nenhuma outra publicação transacional existir para esse banco de dados, ele pode ser desabilitado para a publicação transacional, como se segue:  
  
    1.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> . Defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a instância de <xref:Microsoft.SqlServer.Management.Common.ServerConnection> na etapa 1.  
  
    2.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se esse método retorna `false`, confirme que o banco de dados existe.  
  
    3.  Defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> como `false`.  
  
    4.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> .  
  
7.  Feche as conexões.  
  
#### <a name="to-remove-a-merge-publication"></a>Para remover uma publicação de mesclagem  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> .  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para a publicação, e a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a conexão criada na etapa 1.  
  
4.  Verifique a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para saber se a publicação existe. Se o valor dessa propriedade for `false`, as propriedades de publicação na etapa 3 foram definidas incorretamente ou a publicação não existe.  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> .  
  
6.  (Opcional) Se nenhuma outra publicação de mesclagem existir para esse banco de dados, ele pode ser desabilitado para a publicação de mesclagem, como se segue:  
  
    1.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> . Defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a instância de <xref:Microsoft.SqlServer.Management.Common.ServerConnection> na etapa 1.  
  
    2.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se esse método retornar `false`, verifique se o banco de dados existe.  
  
    3.  Defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> como `false`.  
  
    4.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> .  
  
7.  Feche as conexões.  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 O exemplo a seguir exclui uma publicação transacional. Se nenhuma outra publicação transacional existir para esse banco de dados, a publicação transacional será também desabilitada.  
  
 [!code-csharp[HowTo#rmo_DropTranPub](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_droptranpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPub](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_droptranpub)]  
  
 O exemplo a seguir exclui uma publicação de mesclagem. Se nenhuma outra publicação de mesclagem existir para esse banco de dados, a publicação de mesclagem será também desabilitada.  
  
 [!code-csharp[HowTo#rmo_DropMergePub](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_dropmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePub](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_dropmergepub)]  
  
## <a name="see-also"></a>Consulte também  
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Publicar dados e objetos de banco de dados](publish-data-and-database-objects.md)  
  
  
