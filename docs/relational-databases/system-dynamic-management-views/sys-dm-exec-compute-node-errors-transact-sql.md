---
title: sys. dm _exec_compute_node_errors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
- DM_EXEC_COMPUTE_NODE_ERRORS
- DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase
- PolyBase, views
- dm_exec_compute_node_errors
- sys.dm_exec_compute_node_errors management view
ms.assetid: 9a03c039-70e4-4974-95d8-d3fa45984ffb
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b074da717a2c5deac9d576da938d1229dafeac77
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532785"
---
# <a name="sysdm_exec_compute_node_errors-transact-sql"></a>sys. dm _exec_compute_node_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Retorna os erros que ocorrem em nós de computação do polybase.  
  
|Nome da coluna|Tipo de dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|error_id|`nvarchar(36)`|ID numérica exclusiva associada ao erro.|Exclusivo em todos os erros de consulta no sistema|  
|origem|`nvarchar(255)`|Descrição do thread ou processo de origem||  
|tipo|`nvarchar(255)`|Tipo de erro.||  
|create_time|`datetime`|A hora da ocorrência de erro||  
|compute_node_id|`int`|Identificador do nó de computação específico|Confira compute_node_id de [Sys. dm &#40;_EXEC_COMPUTE_NODES Transact-&#41; SQL](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|  
|rexecution_id|`nvarchar(36)`|Identificador da consulta do polybase, se houver.||  
|spid|`int`|Identificador da sessão de SQL Server||  
|thread_id|`int`|Identificador numérico do thread no qual o erro ocorreu.||  
|detalhes|nvarchar(4000)|Descrição completa dos detalhes do erro.||
|compute_pool_id|`int`|Identificador exclusivo do pool.|

  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas do polybase com exibições de gerenciamento dinâmico](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições &#40;de gerenciamento dinâmico relacionadas ao banco de dados TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
