---
title: sys.DM os_nodes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_nodes
- dm_os_nodes_TSQL
- dm_os_nodes
- sys.dm_os_nodes_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_nodes dynamic management view
ms.assetid: c768b67c-82a4-47f5-850b-0ea282358d50
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5cf36f7156f9297231fc232e8fecafee5e77427c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosnodes-transact-sql"></a>sys.dm_os_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Um componente interno denominado SQLOS cria estruturas de nó que imitam a localidade do processador de hardware. Essas estruturas podem ser alteradas usando NUMA temporário para criar layouts de nó personalizados.  
  
 A tabela seguinte fornece informações sobre esses nós.  
  
> **Observação:** para chamar esse DMV do [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_nodes**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|node_id|**smallint**|ID do nó.|  
|node_state_desc|**nvarchar(256)**|Descrição do estado do nó. Os valores são exibidos primeiro com os valores mutuamente exclusivos, seguidos pelos valores combinados. Por exemplo:<br /><br /> Online, Thread Resources Low, Lazy Preemptive<br /><br /> Há quatro valores node_state_desc mutuamente exclusivos. Eles são listados com suas descrições.<br /><br /> ONLINE: O nó está online<br /><br /> OFFLINE: O nó está offline<br /><br /> OCIOSO: Nó não tem nenhuma solicitação de trabalho pendente e entrou em um estado ocioso.<br /><br /> IDLE_READY: O nó não tem nenhuma solicitação de trabalho pendente e está pronto para um estado ocioso.<br /><br /> Há cinco valores combináveis de node_state_desc, listados abaixo e suas descrições.<br /><br /> DAC: Este nó é reservado para a Conexão administrativa dedicada.<br /><br /> THREAD_RESOURCES_LOW: Nenhum thread novo pode ser criado neste nó devido a uma condição de memória insuficiente.<br /><br /> HOT ADDED: Indica que os nós foram adicionados em resposta a um quente evento de CPU.|  
|memory_object_address|**varbinary (8)**|Endereço de objeto de memória associado a esse nó. Relação um para um para sys.dm_os_memory_objects.memory_object_address.|  
|memory_clerk_address|**varbinary (8)**|Endereço de administrador de memória associado a este nó. Relação um para um para sys.dm_os_memory_clerks.memory_clerk_address.|  
|io_completion_worker_address|**varbinary (8)**|Endereço de trabalhador atribuído à conclusão de E/S deste nó. Relação um para um para sys.dm_os_workers.worker_address.|  
|memory_node_id|**smallint**|ID do nó de memória ao qual este nó pertence. Relação muitos para um para sys.dm_os_memory_nodes.memory_node_id.|  
|cpu_affinity_mask|**bigint**|Bitmap que identifica as CPUs às quais este nó está associado.|  
|online_scheduler_count|**smallint**|Número de agendadores online que são gerenciados por este nó.|  
|idle_scheduler_count|**smallint**|Número de agendadores online que não têm nenhum trabalhador ativo.|  
|active_worker_count|**int**|Número de trabalhadores que estão ativos em todos os agendadores gerenciados por este nó.|  
|avg_load_balance|**int**|Média do número de trabalhos para cada agendador neste nó.|  
|timer_task_affinity_mask|**bigint**|Bitmap que identifica os agendadores que podem ter trabalhos de timer atribuídos.|  
|permanent_task_affinity_mask|**bigint**|Bitmap que identifica os agendadores que podem ter trabalhos permanentes atribuídos.|  
|resource_monitor_state|**bit**|Cada nó possui um monitor de recursos atribuído. O monitor de recursos pode estar sendo executando ou em estado ocioso. O valor 1 indica que está sendo executado; o valor 0 indica que está em estado ocioso.|  
|online_scheduler_mask|**bigint**|Identifica a máscara de afinidade de processo para este nó.|  
|processor_group|**smallint**|Identifica o grupo de processadores para este nó.|  
|cpu_count |**int** |Número de CPUs disponíveis para este nó. |
|pdw_node_id|**int**|O identificador para o nó que essa distribuição é no.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Permissões  
Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, requer o `VIEW DATABASE STATE` no banco de dados. Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, requer o **administrador do servidor** ou um **administrador do Active Directory do Azure** conta.  
  
## <a name="see-also"></a>Consulte também  
  
 [Sistema operacional SQL Server relacionadas exibições de gerenciamento dinâmico &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  

