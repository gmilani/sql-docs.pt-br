---
title: sys. dm _pdw_nodes_exec_query_profiles (Transact-SQL) | Microsoft Docs
description: Exibição de gerenciamento dinâmico que pode ser usada para monitorar o progresso da consulta data warehouse em tempo real enquanto a consulta está em execução.
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 7237e7f7b49916e09f4a8c5cab0d7d49486cb971
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73145651"
---
# <a name="sysdm_pdw_nodes_exec_query_profiles-transact-sql"></a>sys. dm _pdw_nodes_exec_query_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Monitora o andamento da consulta data warehouse em tempo real enquanto a consulta está em execução.   
  
## <a name="table-returned"></a>Tabela retornada  
Os contadores retornados são por operador por thread. Os resultados são dinâmicos e não correspondem aos resultados das opções existentes, como `SET STATISTICS XML ON` que só criam a saída quando a consulta é concluída.  
  
|Nome da coluna|Tipo de Dados|Description|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**Int**|ID numérica exclusiva associada ao nó.|
|session_id|**smallint**|Identifica a sessão na qual esta consulta é executada. Referencia dm_exec_sessions.session_id.|  
|request_id|**Int**|Identifica a solicitação de destino. Referencia dm_exec_sessions.request_id.|  
|sql_handle|**varbinary(64)**|É um token que identifica exclusivamente o lote ou o procedimento armazenado do qual a consulta faz parte. Referencia dm_exec_query_stats.sql_handle.|  
|plan_handle|**varbinary(64)**|É um token que identifica exclusivamente um plano de execução de consulta para um lote que foi executado e seu plano reside no cache de planos ou está em execução no momento. Faz referência a dm_exec_query_stats. plan_handle.|  
|physical_operator_name|**nvarchar(256)**|Nome do operador físico.|  
|node_id|**Int**|Identifica um nó do operador na árvore de consulta.|  
|thread_id|**Int**|Distingue os threads (para uma consulta paralela) que pertencem ao mesmo nó do operador de consulta.|  
|task_address|**varbinary (8)**|Identifica a tarefa do sistema operacional SQL que esse thread está usando. Referencia dm_os_tasks.task_address.|  
|row_count|**bigint**|Número de linhas retornadas pelo operador até o momento.|  
|rewind_count|**bigint**|Número de retrocessos até o momento.|  
|rebind_count|**bigint**|Número de reassociações até o momento.|  
|end_of_scan_count|**bigint**|Número de término de exames até o momento.|  
|estimate_row_count|**bigint**|Número estimado de linhas. Pode ser útil comparar estimated_row_count com o row_count real.|  
|first_active_time|**bigint**|A hora, em milissegundos, em que operador foi chamado primeiro.|  
|last_active_time|**bigint**|A hora, em milissegundos, em que operador foi chamado por último.|  
|open_time|**bigint**|Carimbo de data/hora quando aberto (em milissegundos).|  
|first_row_time|**bigint**|Carimbo de data/hora quando a primeira linha foi aberta (em milissegundos).|  
|last_row_time|**bigint**|Carimbo de data/hora quando a última linha foi aberta (em milissegundos).|  
|close_time|**bigint**|Carimbo de data/hora quando fechado (em milissegundos).|  
|elapsed_time_ms|**bigint**|Tempo total decorrido (em milissegundos) usado pelas operações do nó de destino até o momento.|  
|cpu_time_ms|**bigint**|Tempo total de CPU (em milissegundos) usado pelas operações do nó de destino até o momento.|  
|database_id|**smallint**|ID do banco de dados que contém o objeto no qual as leituras e gravações estão sendo realizadas.|  
|object_id|**Int**|O identificador do objeto no qual as leituras e gravações estão sendo realizadas. Referências sys.objects.object_id.|  
|index_id|**Int**|O índice (se houver) no qual o conjunto de linhas é aberto.|  
|scan_count|**bigint**|Número de verificações de tabela/índice até o momento.|  
|logical_read_count|**bigint**|Número de leituras lógicas até o momento.|  
|physical_read_count|**bigint**|Número de leituras físicas até o momento.|  
|read_ahead_count|**bigint**|Número de read-aheads até o momento.|  
|write_page_count|**bigint**|Número de gravações de página até o momento devido ao derramamento.|  
|lob_logical_read_count|**bigint**|Número de leituras lógicas LOB até o momento.|  
|lob_physical_read_count|**bigint**|Número de leituras físicas LOB até o momento.|  
|lob_read_ahead_count|**bigint**|Número de read-aheads LOB até o momento.|  
|segment_read_count|**Int**|Número de read-aheads de segmento até o momento.|  
|segment_skip_count|**Int**|Número de segmentos ignorados até o momento.| 
|actual_read_row_count|**bigint**|Número de linhas lidas por um operador antes da aplicação do predicado residuais.| 
|estimated_read_row_count|**bigint**|**Aplica-se a:** A partir do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1. <br/>Número estimado de linhas a serem lidas por um operador antes da aplicação do predicado residuais.|  
  
## <a name="remarks"></a>Remarks  
Os mesmos comentários em [Sys. dm _exec_query_profiles](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql?view=sql-server-ver15) se aplicam.  

## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW SERVER STATE` no servidor.  

## <a name="see-also"></a>Confira também  
 [Exibições &#40;de gerenciamento dinâmico SQL data warehouse e Parallel Data Warehouse TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
   

 ## <a name="next-steps"></a>Próximas etapas
 Para obter mais dicas de desenvolvimento, consulte [visão geral do desenvolvimento de SQL data warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop).
