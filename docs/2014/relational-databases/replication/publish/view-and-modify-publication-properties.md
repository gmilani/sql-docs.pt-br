---
title: Exibir e modificar as propriedades da publicação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing replication properties
- modifying replication properties, articles
- articles [SQL Server replication], modifying
- publications [SQL Server replication], properties
- articles [SQL Server replication], properties
- modifying replication properties, publications
- publications [SQL Server replication], modifying
ms.assetid: 27d72ea4-bcb6-48f2-b4aa-eb1410da7efc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5053cc16734cc18c75e163fec4c06b1768e590cc
ms.sourcegitcommit: c2052b2bf7261b3294a3a40e8fed8b9e9c588c37
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/10/2019
ms.locfileid: "68941061"
---
# <a name="view-and-modify-publication-properties"></a>Visualizar e modificar as propriedades da publicação
  Este tópico descreve como exibir e modificar propriedades de publicação no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)], ou RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
-   **Para exibir e modificar propriedades de publicação, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Algumas propriedades não podem ser modificadas após uma publicação ter sido criada, e outras não podem ser modificadas se houverem assinaturas na publicação. As propriedades que não podem ser definidas são exibidas como somente leitura.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Depois que uma publicação é criada, algumas alterações de propriedade requerem um novo instantâneo. Se uma publicação tiver assinaturas, algumas alterações também exigirão que todas as assinaturas sejam reiniciadas. Para obter mais informações, consulte [Alterar propriedades da publicação e do artigo](change-publication-and-article-properties.md) e [Add Articles to and Drop Articles from Existing Publications](add-articles-to-and-drop-articles-from-existing-publications.md) (Adicionar e remover artigos para/de publicações existentes).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Exibir e modificar propriedades de publicação na caixa de diálogo **Propriedades de Publicação – \<Publicação >** , que está disponível em [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e o Replication Monitor. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
 A caixa de diálogo **Propriedades da Publicação – \<Publicação>** inclui as seguintes páginas:  
  
-   A página **Geral** inclui o nome e descrição da publicação, o nome do banco de dados, o tipo da publicação, e as configurações para expiração da assinatura.  
  
-   A página **Artigos** corresponde à página **Artigos** no Assistente para Nova Publicação. Use essa página para adicionar e excluir artigos e para alterar propriedades e filtros de coluna para artigos.  
  
-   A página **Filtrar Linhas** corresponde à página **Filtrar Linhas de Tabela** no Assistente para Nova Publicação. Use essa página para adicionar, editar e excluir filtros de linhas estáticas para todos os tipos de publicações, e para adicionar, editar e excluir filtros de linhas com parâmetros e associar filtros para publicações de mesclagem.  
  
-   A página **Instantâneo** permite que você especifique o formato e o local do instantâneo, se o instantâneo deve estar compactado e scripts para serem executados antes e depois que o instantâneo for aplicado.  
  
-   A página **Instantâneo FTP** (para publicações transacionais e de instantâneo e publicações de mesclagem para versões de Publicadores em execução antes do SQL Server 2005) permite que você especifique se os Assinantes podem baixar arquivos através de FTP (Protocolo de Transferência de Arquivo).  
  
-   A página **Instantâneo de FTP e Internet** (para publicações de mesclagem de Publicadores executando o SQL Server 2005 ou versões posteriores) permite que você especifique se os Assinantes podem baixar arquivos de instantâneo através de FTP, e se os Assinantes podem sincronizar as assinaturas através de HTTPS.  
  
-   A página **Opções de Assinatura** permite que você possa definir um número de opções que se aplicam à todas as assinaturas. As opções diferem dependendo do tipo de publicação.  
  
-   A página **Lista de Acesso à Publicação** permite que você especifique quais logons e grupos podem acessar uma publicação.  
  
-   A página **Segurança do Agente** permite que você acesse as configurações para as contas sob as quais os seguintes agentes executam e fazem conexões com os computadores em uma topologia de replicação: O Agente de Instantâneo para todas as publicações; o Log Reader Agent para todas as publicações transacionais e o Queue Reader Agent para publicações transacionais que permitem assinaturas de atualização enfileiradas.  
  
-   A página **Partições de Dados** (para publicações de mesclagem de Publicadores executando o SQL Server 2005 ou posterior) permite que você especifique se os Assinantes das publicações com filtros com parâmetros podem solicitar uma instantâneo, se um não estiver disponível. Ele também permite que você gere instantâneos para uma ou mais partições uma vez ou em uma agenda recorrente.  
  
#### <a name="to-view-and-modify-publication-properties-in-management-studio"></a>Para visualizar e modificar propriedades de publicação no Management Studio  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e expanda o nó de servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com o botão direito em uma publicação, em seguida, clique em **Propriedades**.  
  
4.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
#### <a name="to-view-and-modify-publication-properties-in-replication-monitor"></a>Para visualizar e modificar propriedades de publicação no Replication Monitor  
  
1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor e, depois, expanda um Publicador.  
  
2.  Clique com o botão direito em uma publicação, em seguida, clique em **Propriedades**.  
  
3.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Publicações podem ser modificadas e suas propriedades retornadas programaticamente usando-se procedimentos armazenados de replicação. Os procedimentos armazenados usados dependerão do tipo de publicação.  
  
#### <a name="to-view-the-properties-of-a-snapshot-or-transactional-publication"></a>Para visualizar as propriedades de uma publicação de instantâneo ou transacional  
  
1.  Execute [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql), especificando o nome da publicação para o  **\@** parâmetro de publicação. Se você não especificar esse parâmetro, as informações sobre todas as publicações no Publicador serão retornadas.  
  
#### <a name="to-change-the-properties-of-a-snapshot-or-transactional-publication"></a>Para alterar as propriedades de uma publicação de instantâneo ou transacional  
  
1.  Execute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), especificando a propriedade de publicação a ser alterada  **\@** no parâmetro Property e o novo  **\@** valor dessa propriedade no parâmetro value.  
  
    > [!NOTE]  
    >  Se a alteração exigir a geração de um novo instantâneo, você também deverá especificar um valor de **1** para  **\@force_invalidate_snapshot**e, se a alteração exigir que os assinantes sejam reinicializados, você deverá especificar um valor de **1**   **para\@force_reinit_subscription**. Para obter mais informações sobre as propriedades que, quando alteradas, exigem um novo instantâneo ou uma nova reinicialização, consulte [Alterar propriedades da publicação e do artigo](change-publication-and-article-properties.md).  
  
#### <a name="to-view-the-properties-of-a-merge-publication"></a>Para visualizar as propriedades de uma publicação de mesclagem  
  
1.  Execute [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql), especificando o nome da publicação para o  **\@** parâmetro de publicação. Se você não especificar esse parâmetro, as informações sobre todas as publicações no Publicador serão retornadas.  
  
#### <a name="to-change-the-properties-of-a-merge-publication"></a>Para alterar as propriedades de uma publicação de mesclagem  
  
1.  Execute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), especificando a propriedade de publicação que está sendo  **\@** alterada no parâmetro Property e o novo  **\@** valor dessa propriedade no parâmetro value.  
  
    > [!NOTE]  
    >  Se a alteração exigir a geração de um novo instantâneo, você também deverá especificar um valor de **1** para  **\@force_invalidate_snapshot**e, se a alteração exigir que os assinantes sejam reinicializados, você deverá especificar um valor de **1 para force_reinit_subscription para** obter mais informações sobre as propriedades que, quando alteradas, exigem um novo instantâneo ou reinicialização, consulte [alterar propriedades da publicação e do artigo](change-publication-and-article-properties.md).  **\@**  
  
#### <a name="to-view-the-properties-of-a-snapshot"></a>Para visualizar as propriedades de um instantâneo  
  
1.  Execute [sp_helppublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql), especificando o nome da publicação para o  **\@** parâmetro de publicação.  
  
#### <a name="to-change-the-properties-of-a-snapshot"></a>Para alterar as propriedades de um instantâneo  
  
1.  Execute [sp_changepublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql), especificando uma ou mais das propriedades de instantâneo novas para os parâmetros de instantâneo apropriados.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Esse exemplo de replicação transacional retorna as propriedades da publicação.  
  
 [!code-sql[HowTo#sp_helppublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changetranpub.sql#sp_helppublication)]  
  
 Esse exemplo de replicação transacional desabilita a replicação de esquema para a publicação.  
  
 [!code-sql[HowTo#sp_changepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changetranpub.sql#sp_changepublication)]  
  
 Esse exemplo de replicação de mesclagem retorna as propriedades da publicação.  
  
 [!code-sql[HowTo#sp_helpmergepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changemergepub.sql#sp_helpmergepublication)]  
  
 Esse exemplo de replicação de mesclagem desabilita a replicação de esquema para a publicação.  
  
 [!code-sql[HowTo#sp_changemergepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changemergepub.sql#sp_changemergepublication)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Você pode modificar as publicações e acessar suas propriedades programaticamente, usando o RMO (Replication Management Objects). As classes RMO que você usa para visualizar ou modificar as propriedades da publicação, dependem do tipo da publicação.  
  
#### <a name="to-view-or-modify-properties-of-a-snapshot-or-transactional-publication"></a>Para visualizar ou modificar as propriedades de um instantâneo ou publicação transacional  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPublication> , defina <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e propriedades <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para a publicação, e defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a conexão criada no etapa 1.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar `false`, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  (Opcional) Para alterar as propriedades, defina um novo valor para uma ou mais propriedades definíveis. Use o operador lógico AND (`&` no Microsoft Visual C# e `And` no Microsoft Visual Basic) para determinar se um dado valor <xref:Microsoft.SqlServer.Replication.PublicationAttributes> está definido para a propriedade <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> . Use o operador OR de lógica inclusiva (`|` no Visual C# e `Or` no Visual Basic) e o operador OR de lógica exclusiva (`^` no Visual C# e `Xor` no Visual Basic) para alterar os valores <xref:Microsoft.SqlServer.Replication.PublicationAttributes> para a propriedade <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> .  
  
5.  (Opcional) Se você especificar um valor de `true`  para  <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar as alterações no servidor. (Opcional) Se você especificar um valor de `false` para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (padrão), as alterações serão enviadas imediatamente ao servidor.  
  
#### <a name="to-view-or-modify-properties-of-a-merge-publication"></a>Para visualizar ou modificar as propriedades de uma publicação de mesclagem  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> , defina <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e propriedades <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para a publicação, e defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a conexão criada no etapa 1.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar `false`, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  (Opcional) Para alterar as propriedades, defina um novo valor para uma ou mais propriedades definíveis. Use o operador AND lógico (`&` no Visual C# e `And` no Visual Basic) para determinar se um dado valor <xref:Microsoft.SqlServer.Replication.PublicationAttributes> está definido para a propriedade <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> . Use o operador OR de lógica inclusiva (`|` no Visual C# e `Or` no Visual Basic) e o operador OR de lógica exclusiva (`^` no Visual C# e `Xor` no Visual Basic) para alterar os valores <xref:Microsoft.SqlServer.Replication.PublicationAttributes> para a propriedade <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> .  
  
5.  (Opcional) Se você especificar um valor de `true`  para  <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar as alterações no servidor. (Opcional) Se você especificar um valor de `false` para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (padrão), as alterações serão enviadas imediatamente ao servidor.  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo define atributos de publicação para uma publicação transacional. As alterações são armazenadas em cache até que sejam explicitamente enviadas ao servidor.  
  
 [!code-csharp[HowTo#rmo_ChangeTranPub_cached](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changetranpub_cached)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeTranPub_cached](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changetranpub_cached)]  
  
 Esse exemplo desabilita a replicação DDL para uma publicação de mesclagem.  
  
 [!code-csharp[HowTo#rmo_ChangeMergePub_ddl](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changemergepub_ddl)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergePub_ddl](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changemergepub_ddl)]  
  
## <a name="see-also"></a>Consulte também  
 [Publicar dados e objetos de banco de dados](publish-data-and-database-objects.md)   
 [Alterar propriedades da publicação e do artigo](change-publication-and-article-properties.md)   
 [Fazer alterações de esquema em bancos de dados de publicação](make-schema-changes-on-publication-databases.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Adicionar e remover artigos de uma publicação](add-articles-to-and-drop-articles-from-a-publication.md)   
 [Exibir informações e executar tarefas usando o Replication Monitor](../monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Exibir e modificar as propriedades do artigo](view-and-modify-article-properties.md)  
  
  
