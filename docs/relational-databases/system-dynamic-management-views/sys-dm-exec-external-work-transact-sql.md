---
title: sys. dm _exec_external_work (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_EXTERNAL_WORK
- DM_EXEC_EXTERNAL_WORK_TSQL
- SYS.DM_EXEC_EXTERNAL_WORK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_external_work management view
- dm_exec_external_work management view
- PolyBase,views
- PolyBase
ms.assetid: 7597d97b-1fde-4135-ac35-4af12968f300
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5afdfd4f9a5f66845ae6d3798910fc2c4bf5ab8a
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532947"
---
# <a name="sysdm_exec_external_work-transact-sql"></a>sys. dm _exec_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Retorna informações sobre a carga de trabalho por trabalhador, em cada nó de computação.  
  
 Consulte sys. dm _exec_external_work para identificar o trabalho girado para se comunicar com a fonte de dados externa (por exemplo, Hadoop ou SQL Server externo).  
  
|Nome da coluna|Tipo de dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|`nvarchar(32)`|Identificador exclusivo para a consulta do polybase associado.|Consulte *request_ID* em [Sys. dm _EXEC_REQUESTS &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|`int`|A solicitação que esse trabalho está executando.|Consulte *step_index* em [Sys. dm _EXEC_REQUESTS &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|dms_step_index|`int`|Etapa no plano DMS que esse trabalho está executando.|Consulte [Sys. dm _exec_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md).|  
|compute_node_id|`int`|O nó no qual o trabalho está sendo executado.|Consulte [Sys. dm _exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|tipo|`nvarchar(60)`|O tipo de trabalho externo.|' Divisão de arquivo '|  
|work_id|`int`|ID da divisão real.|Maior ou igual a 0.|  
|input_name|`nvarchar(4000)`|Nome da entrada a ser lida|Nome do arquivo ao usar o Hadoop.|  
|read_location|`bigint`|Deslocamento ou local de leitura.|Deslocamento do arquivo a ser lido.|  
|bytes_processed|`bigint`|Total de bytes processados por este trabalhador.|Maior ou igual a 0.|  
|comprimento|`bigint`|Comprimento do bloco Split ou HDFS no caso do Hadoop|Definido pelo usuário. O padrão é o 64M|  
|status|`nvarchar(32)`|Status do trabalhador|Pendente, processando, concluído, com falha, anulado|  
|start_time|`datetime`|Início do trabalho||  
|end_time|`datetime`|Fim do trabalho||  
|total_elapsed_time|`int`|Tempo total em milissegundos||
|compute_pool_id|`int`|Identificador exclusivo do pool.|

## <a name="see-also"></a>Consulte também  
 [Solução de problemas do polybase com exibições de gerenciamento dinâmico](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições &#40;de gerenciamento dinâmico relacionadas ao banco de dados TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
