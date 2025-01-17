---
title: sys. dm _pdw_nodes_exec_query_statistics_xml (Transact-SQL) | Microsoft Docs
description: Exibição de gerenciamento dinâmico que retorna o plano de execução de consulta para solicitações em andamento. Use essa DMV para recuperar o Showplan XML com estatísticas transitórias.
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
ms.openlocfilehash: 2b12e1a1400ec2d9d4bb85466671cda446511f24
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73145641"
---
# <a name="dm_pdw_nodes_exec_query_statistics_xml-transact-sql"></a>dm_pdw_nodes_exec_query_statistics_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Retorna o plano de execução de consulta para solicitações em andamento. Use essa DMV para recuperar o Showplan XML com estatísticas transitórias.

## <a name="table-returned"></a>Tabela retornada

|Column Name|Tipo de dados|Description|  
|-----------------|---------------|-----------------|
|node_id|**Int**|ID numérica exclusiva associada ao nó.|
|session_id|**smallint**|ID da sessão. Não permite valor nulo.|
|request_id|**Int**|ID da solicitação. Não permite valor nulo.|
|sql_handle|**varbinary(64)**|É um token que identifica exclusivamente o lote ou o procedimento armazenado do qual a consulta faz parte. Anulável.|
|plan_handle|**varbinary(64)**|É um token que identifica exclusivamente um plano de execução de consulta para um lote em execução no momento. Anulável.|
|query_plan|**xml**|Contém a representação Showplan do tempo de execução do plano de execução de consulta especificado com *plan_handle* que contém estatísticas parciais. O Showplan está em formato XML. Um plano é gerado para cada lote que contém, por exemplo, instruções ad hoc [!INCLUDE[tsql](../../includes/tsql-md.md)], chamadas de procedimento armazenado e chamadas de função definidas pelo usuário. Anulável.|

## <a name="remarks"></a>Remarks
Os mesmos comentários em [Sys. dm _exec_query_statistics_xml](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql?view=sql-server-ver15) se aplicam.   

## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW SERVER STATE` no servidor.  

## <a name="see-also"></a>Confira também  
 [Exibições &#40;de gerenciamento dinâmico SQL data warehouse e Parallel Data Warehouse TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

 ## <a name="next-steps"></a>Próximas etapas
 Para obter mais dicas de desenvolvimento, consulte [visão geral do desenvolvimento de SQL data warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop).

