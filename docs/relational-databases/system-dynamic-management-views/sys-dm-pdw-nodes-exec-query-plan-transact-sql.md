---
title: sys. dm _pdw_nodes_exec_query_plan (Transact-SQL) | Microsoft Docs
description: Exibição de gerenciamento dinâmico que retorna o Showplan em formato XML para o lote especificado pelo identificador de plano. O plano especificado pelo identificador do plano pode estar em cache ou estar sendo executado.
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
ms.openlocfilehash: 96b499ea5bc38d2a4cf9c380116108009ea46086
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73145631"
---
# <a name="syspdw_nodes_dm_exec_query_plan-transact-sql"></a>sys. PDW _nodes_dm_exec_query_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Retorna o plano de execução em formato XML para o lote especificado pelo identificador de plano. O plano especificado pelo identificador do plano pode estar em cache ou estar sendo executado.  

## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de Dados|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**Int**|ID numérica exclusiva associada ao nó.| 
|**dbid**|**smallint**|A ID do banco de dados de contexto em vigor quando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondente a esse plano foi compilada. Para instruções SQL não planejadas e preparadas, a ID do banco de dados em que as instruções foram compiladas.<br /><br /> A coluna é anulável.|  
|**objectid**|**Int**|A identificação do objeto (por exemplo, procedimento armazenado ou função definida pelo usuário) para este plano de consulta. Para lotes ad hoc e preparados, essa coluna é **nula**.<br /><br /> A coluna é anulável.|  
|**number**|**smallint**|Inteiro de procedimento armazenado numerado. Para lotes ad hoc e preparados, essa coluna é **nula**.<br /><br /> A coluna é anulável.| 
|**criptografados**|**bit**|Indica se o procedimento armazenado correspondente está criptografado.<br /><br /> 0 = não criptografado<br /><br /> 1 = criptografado<br /><br /> A coluna não é anulável.|  
|**query_plan**|**xml**|Contém a representação de SHOWPLAN de tempo de compilação do plano de execução de consulta especificado com *plan_handle*. O Showplan está em formato XML. Um plano é gerado para cada lote que contém, por exemplo, instruções ad hoc [!INCLUDE[tsql](../../includes/tsql-md.md)], chamadas de procedimento armazenado e chamadas de função definidas pelo usuário.<br /><br /> A coluna é anulável.|  
  
## <a name="remarks"></a>Remarks  
Os mesmos comentários em [Sys. dm _exec_query_plan](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql?view=sql-server-ver15) se aplicam.  
  
## <a name="permissions"></a>Permissões  
 Requer a função de servidor **sysadmin** ou a permissão `VIEW SERVER STATE` no servidor.  
  
## <a name="see-also"></a>Confira também  
 [Exibições &#40;de gerenciamento dinâmico SQL data warehouse e Parallel Data Warehouse TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

 ## <a name="next-steps"></a>Próximas etapas
 Para obter mais dicas de desenvolvimento, consulte [visão geral do desenvolvimento de SQL data warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop).