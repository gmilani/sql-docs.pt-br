---
title: sp_mergecleanupmetadata (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergecleanupmetadata_TSQL
- sp_mergecleanupmetadata
helpviewer_keywords:
- sp_mergecleanupmetadata
ms.assetid: 892f8628-4cbe-4cc3-b959-ed45ffc24064
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0196993f863d973e14834f7eb3b93b797a825ac4
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907332"
---
# <a name="sp_mergecleanupmetadata-transact-sql"></a>sp_mergecleanupmetadata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Deve ser usado somente em topologias de replicação que incluem servidores que executam versões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. o **sp_mergecleanupmetadata** permite que os administradores limpem os metadados nas tabelas do sistema **MSmerge_genhistory**, **MSmerge_contents** e **MSmerge_tombstone** . Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` é o nome da publicação. a *publicação* é **sysname**, com um padrão de **%** , que limpa os metadados de todas as publicações. A publicação já deve existir se explicitamente especificada.  
  
`[ @reinitialize_subscriber = ] 'subscriber'` especifica se o Assinante deve ser reinicializado. o *assinante* é **nvarchar (5)** , pode ser **true** ou **false**, com um padrão de **true**. Se **for true**, as assinaturas serão marcadas para reinicialização. Se **for false**, as assinaturas não serão marcadas para reinicialização.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_mergecleanupmetadata** deve ser usado somente em topologias de replicação que incluem servidores que executam versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. Topologias que só incluem o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 ou versão posterior deveriam usar limpeza automática de metadados com base em retenção. Ao executar esse procedimento armazenado, tenha cuidado com o crescimento potencialmente grande e necessário do arquivo de log no computador em que o procedimento armazenado está sendo executado.  
  
> [!CAUTION]
>  Depois que **sp_mergecleanupmetadata** é executado, por padrão, todas as assinaturas nos assinantes de publicações que têm metadados armazenados em **MSmerge_genhistory**, **MSmerge_contents** e **MSmerge_tombstone** são marcadas para reinicialização, todas as alterações pendentes no Assinante são perdidas e o instantâneo atual é marcado como obsoleto.  
> 
> [!NOTE]
>  Se houver várias publicações em um banco de dados e qualquer uma dessas publicações usar um período de retenção de publicação infinita ( **\@retenção**=**0**), executar **sp_mergecleanupmetadata** não limpará a mesclagem metadados de controle de alterações de replicação para o banco de dados. Por esse motivo, use a retenção de publicação infinita com precaução.  
  
 Ao executar esse procedimento armazenado, você pode escolher se deseja reinicializar os assinantes definindo o parâmetro **\@reinitialize_subscriber** como **true** (o padrão) ou **false**. Se **sp_mergecleanupmetadata** for executado com o parâmetro **\@Reinitialize_subscriber** definido como **true**, um instantâneo será reaplicado no Assinante, mesmo que a assinatura tenha sido criada sem um instantâneo inicial (por exemplo, se os dados e o esquema do instantâneo foram aplicados manualmente ou já existiam no Assinante). Definir o parâmetro como **false** deve ser usado com cautela, porque se a publicação não for reinicializada, você deverá garantir que os dados no Publicador e no Assinante sejam sincronizados.  
  
 Independentemente do valor de **\@reinitialize_subscriber**, **sp_mergecleanupmetadata** falhará se houver processos de mesclagem em andamento que estejam tentando carregar alterações em um Publicador ou em um assinante de republicação no momento em que o armazenamento procedimento é invocado.  
  
 **Executando sp_mergecleanupmetadata com \@reinitialize_subscriber = TRUE:**  
  
1.  É recomendado, mas não exigido, que você interrompa todas as atualizações nos bancos de dados de publicação e assinatura. Se a atualização continuar, qualquer atualização feita no Assinante desde a última mesclagem será perdida quando a publicação for reiniciada, mas a convergência dos dados será mantida.  
  
2.  Execute uma mesclagem executando o Agente de Mesclagem. Recomendamos que você use a opção de linha de comando **-Validate** Agent em cada assinante ao executar o agente de mesclagem. Se você estiver executando mesclagens de modo contínuo, consulte *considerações especiais para mesclagens de modo contínuo* mais adiante nesta seção.  
  
3.  Depois que todas as mesclagens forem concluídas, execute **sp_mergecleanupmetadata**.  
  
4.  Execute **sp_reinitmergepullsubscription** em todos os assinantes usando a assinatura de pull nomeada ou anônima para garantir a convergência de dados.  
  
5.  Se você estiver executando mesclagens de modo contínuo, consulte *considerações especiais para mesclagens de modo contínuo* mais adiante nesta seção.  
  
6.  Gere novamente arquivos de instantâneo para todas as publicações de mesclagem envolvidas em todos os níveis. Se tentar fazer a mesclagem sem primeiro gerar novamente o instantâneo, você será solicitado a gerar o instantâneo novamente.  
  
7.  Faça um backup do banco de dados de publicação. Falha nesse procedimento pode causar uma falha de mesclagem depois da restauração de um banco de dados de publicação.  
  
 **Executando sp_mergecleanupmetadata com \@reinitialize_subscriber = FALSE:**  
  
1.  Interrompa **todas** as atualizações para os bancos de dados de publicação e de assinatura.  
  
2.  Execute uma mesclagem executando o Agente de Mesclagem. Recomendamos que você use a opção de linha de comando **-Validate** Agent em cada assinante ao executar o agente de mesclagem. Se você estiver executando mesclagens de modo contínuo, consulte *considerações especiais para mesclagens de modo contínuo* mais adiante nesta seção.  
  
3.  Depois que todas as mesclagens forem concluídas, execute **sp_mergecleanupmetadata**.  
  
4.  Se você estiver executando mesclagens de modo contínuo, consulte *considerações especiais para mesclagens de modo contínuo* mais adiante nesta seção.  
  
5.  Gere novamente arquivos de instantâneo para todas as publicações de mesclagem envolvidas em todos os níveis. Se tentar fazer a mesclagem sem primeiro gerar novamente o instantâneo, você será solicitado a gerar o instantâneo novamente.  
  
6.  Faça um backup do banco de dados de publicação. Falha nesse procedimento pode causar uma falha de mesclagem depois da restauração de um banco de dados de publicação.  

 **Considerações especiais para mesclagens de modo contínuo**  
  
 Se você estiver executando mesclagens do modo contínuo, deverá:  
  
-   Pare o Agente de Mesclagem e, em seguida, execute outra mesclagem sem o parâmetro **-Continuous** especificado.  
  
-   Desative a publicação com **sp_changemergepublication** para garantir que as mesclagens de modo contínuo que são sondadas para o status da publicação falhem.  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 Quando você concluiu a etapa 3 da execução do **sp_mergecleanupmetadata**, retome as mesclagens do modo contínuo com base em como elas foram interrompidas. Ou:  
  
-   Adicione o parâmetro **-Continuous** de volta para o agente de mesclagem.  
  
-   Reative a publicação com **sp_changemergepublication.**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **db_owner** podem executar **sp_mergecleanupmetadata**.  
  
 Para usar esse procedimento armazenado, o Publicador deve estar executando o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Os assinantes devem estar executando [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7,0, Service Pack 2.  
  
## <a name="see-also"></a>Consulte Também  
 [ &#40;Transact-SQL&#41; MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)  
 [ &#40;MSmerge_contents Transact-&#41; SQL](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)  
 [Transact &#40;-SQL MSmerge_tombstone&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  
