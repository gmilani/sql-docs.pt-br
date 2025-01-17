---
title: sys. dm_os_tasks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_tasks
- sys.dm_os_tasks_TSQL
- dm_os_tasks_TSQL
- dm_os_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_tasks dynamic management view
ms.assetid: 180a3c41-e71b-4670-819d-85ea7ef98bac
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 086065aa79ca6fba7ad84e5b7e7f99f6f462f7dd
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2019
ms.locfileid: "74164902"
---
# <a name="sysdm_os_tasks-transact-sql"></a>sys.dm_os_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada tarefa que está ativa na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Uma tarefa é a unidade básica de execução no SQL Server. Exemplos de tarefas incluem uma consulta, um logon, um logoff e tarefas do sistema, como atividade de limpeza de fantasma, atividade de ponto de verificação, gravador de log, atividade de refazer paralela. Para obter mais informações sobre tarefas, consulte o [Guia de arquitetura de threads e tarefas](../../relational-databases/thread-and-task-architecture-guide.md).
  
> [!NOTE]  
> Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **Sys. dm_pdw_nodes_os_tasks**.  
  
|Nome da coluna|Data type|Descrição|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary(8)**|Endereço de memória do objeto.|  
|**task_state**|**nvarchar(60)**|O estado da tarefa. Pode ser um dos seguintes:<br /><br /> PENDING: Esperando por um thread de trabalho.<br /><br /> RUNNABLE: Executável, mas esperando receber um quantum.<br /><br /> RUNNING: Atualmente em execução no agendador.<br /><br /> SUSPENDED: Tem um trabalhador, mas está esperando por um evento.<br /><br /> DONE: Concluído.<br /><br /> SPINLOOP: Preso em um spinlock.|  
|**context_switches_count**|**int**|Número de alternâncias de contexto de agendador que esta tarefa completou.|  
|**pending_io_count**|**int**|Número de E/Ss físicas executadas por esta tarefa.|  
|**pending_io_byte_count**|**bigint**|Contagem total de bytes de E/Ss que são executadas por esta tarefa.|  
|**pending_io_byte_average**|**int**|Contagem média de bytes de E/Ss que são executadas por esta tarefa.|  
|**scheduler_id**|**int**|ID do agendador pai. Este é um identificador das informações de agendador para esta tarefa. Para obter mais informações, consulte [Sys. &#40;DM_OS_SCHEDULERS Transact-&#41;SQL](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).|  
|**session_id**|**smallint**|ID da sessão que está associado à tarefa.|  
|**exec_context_id**|**int**|ID do contexto de execução que está associado à tarefa.|  
|**request_id**|**int**|ID da solicitação da tarefa. Para obter mais informações, consulte [Sys. &#40;DM_EXEC_REQUESTS Transact-&#41;SQL](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|**worker_address**|**varbinary(8)**|Endereço de memória do trabalhador que está executando a tarefa.<br /><br /> NULL = A tarefa está esperando que um trabalhador possa ser executado ou a execução da tarefa foi recém-concluída.<br /><br /> Para obter mais informações, consulte [Sys. &#40;DM_OS_WORKERS Transact-&#41;SQL](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|**host_address**|**varbinary(8)**|Endereço de memória do host.<br /><br /> 0 = A hospedagem não foi usada para criar a tarefa. Isto ajuda a identificar o host que foi usado para criar esta tarefa.<br /><br /> Para obter mais informações, consulte [Sys. &#40;DM_OS_HOSTS Transact-&#41;SQL](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md).|  
|**parent_task_address**|**varbinary(8)**|Endereço de memória da tarefa que é pai do objeto.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões
No [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer a permissão `VIEW SERVER STATE`.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a permissão `VIEW DATABASE STATE` no banco de dados. Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   

## <a name="examples"></a>Exemplos  
  
### <a name="a-monitoring-parallel-requests"></a>A. Monitorando solicitações paralelas  
 Para solicitações executadas em paralelo, você verá várias linhas para a mesma combinação de (\<**session_id**>, \<**request_id**>). Use a consulta a seguir para localizar a [opção de configuração de servidor definir o grau máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) para todas as solicitações ativas.  
  
> [!NOTE]  
>  Um **request_id** é exclusivo dentro de uma sessão.  
  
```  
SELECT  
    task_address,  
    task_state,  
    context_switches_count,  
    pending_io_count,  
    pending_io_byte_count,  
    pending_io_byte_average,  
    scheduler_id,  
    session_id,  
    exec_context_id,  
    request_id,  
    worker_address,  
    host_address  
  FROM sys.dm_os_tasks  
  ORDER BY session_id, request_id;  
```  
  
### <a name="b-associating-session-ids-with-windows-threads"></a>b. Associando IDs de sessão a threads do Windows  
 Você pode usar a consulta a seguir para associar um valor de ID de sessão a um ID de thread do Windows. Depois, poderá monitorar o desempenho do thread no Monitor de Desempenho do Windows. A consulta a seguir não retorna informações de sessões que estão suspensas.  
  
```  
SELECT STasks.session_id, SThreads.os_thread_id  
  FROM sys.dm_os_tasks AS STasks  
  INNER JOIN sys.dm_os_threads AS SThreads  
    ON STasks.worker_address = SThreads.worker_address  
  WHERE STasks.session_id IS NOT NULL  
  ORDER BY STasks.session_id;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
[SQL Server exibições &#40;de&#41; gerenciamento dinâmico relacionadas ao sistema operacional](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)    
[Guia de arquitetura de thread e tarefa](../../relational-databases/thread-and-task-architecture-guide.md)     
  


