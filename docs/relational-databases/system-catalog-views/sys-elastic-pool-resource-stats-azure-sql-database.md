---
title: sys.elastic_pool_resource_stats
titleSuffix: Azure SQL Database
ms.date: 01/28/2019
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: reference
f1_keywords:
- sys.elastic_pool_resource_stats catalog view
helpviewer_keywords:
- sys.elastic_pool_resource_stats_TSQL
- sys.elastic_pool_resource_stats
- elastic_pool_resource_stats_TSQL
- elastic_pool_resource_stats
ms.assetid: f242c1bd-3cc8-4c8b-8aaf-c79b6a8a0329
author: stevestein
ms.author: sstein
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 0712785a5af3e8cc3c606a597ba02e0075c88dd9
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843866"
---
# <a name="syselastic_pool_resource_stats-azure-sql-database"></a>sys. elastic_pool_resource_stats (banco de dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna estatísticas de uso de recursos para todos os pools elásticos em um servidor de banco de dados SQL. Para cada pool elástico, há uma linha para cada janela de relatório de 15 segundos (quatro linhas por minuto). Isso inclui CPU, e/s, log, consumo de armazenamento e utilização de solicitação/sessão simultânea por todos os bancos de dados no pool. Esses dados são mantidos por 14 dias. 
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12.|  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|Hora UTC indicando o início do intervalo de relatório de 15 segundos.|  
|**end_time**|**datetime2**|Hora UTC indicando o final do intervalo de relatórios de 15 segundos.|  
|**elastic_pool_name**|**nvarchar(128)**|Nome do pool de banco de dados elástico.|  
|**avg_cpu_percent**|**decimal (5, 2)**|Média de utilização de computação em porcentagem do limite do pool.|  
|**avg_data_io_percent**|**decimal (5, 2)**|Média de utilização de e/s em porcentagem com base no limite do pool.|  
|**avg_log_write_percent**|**decimal (5, 2)**|Média de utilização de recursos de gravação em porcentagem do limite do pool.|  
|**avg_storage_percent**|**decimal (5, 2)**|Utilização média de armazenamento em porcentagem do limite de armazenamento do pool.|  
|**max_worker_percent**|**decimal (5, 2)**|Máximo de trabalhos simultâneos (solicitações) em porcentagem com base no limite do pool.|  
|**max_session_percent**|**decimal (5, 2)**|Máximo de sessões simultâneas em porcentagem com base no limite do pool.|  
|**elastic_pool_dtu_limit**|**int**|Configuração atual máximo de DTU do pool elástico para este pool elástico durante esse intervalo.|  
|**elastic_pool_storage_limit_mb**|**bigint**|Configuração máxima do limite de armazenamento do pool elástico atual para esse pool elástico em megabytes durante esse intervalo.|
|**avg_allocated_storage_percent**|**decimal (5, 2)**|A porcentagem de espaço de dados alocada por todos os bancos de dado no pool elástico.  Esta é a taxa de espaço de dados alocada para o tamanho máximo de dados para o pool elástico.  Para obter mais informações, consulte: [Gerenciamento de espaço de arquivo no banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|  
  
## <a name="remarks"></a>Comentários

 Essa exibição existe no banco de dados mestre do servidor do banco de dados SQL. Você deve estar conectado ao banco de dados mestre para consultar **Sys. elastic_pool_resource_stats**.  
  
## <a name="permissions"></a>Permissões

 Requer associação na função **DBManager** .  
  
## <a name="examples"></a>Exemplos

 O exemplo a seguir retorna os dados de utilização de recursos ordenados pela hora mais recente para todos os pools de banco de dados elástico no servidor do banco de dados SQL atual.  
  
```sql
SELECT * FROM sys.elastic_pool_resource_stats
ORDER BY end_time DESC;  
```

 O exemplo a seguir calcula o consumo percentual médio de DTU para um determinado pool.  

```sql
SELECT start_time, end_time,
  (SELECT Max(v)
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]
FROM sys.elastic_pool_resource_stats
WHERE elastic_pool_name = '<your pool name>'
ORDER BY end_time DESC;  
```

## <a name="see-also"></a>Consulte também

 Controle o [crescimento explosivo com bancos de dados elásticos](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [Criar e gerenciar um pool de banco de dados elástico do banco de dados SQL (visualização)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [Sys. resource_stats &#40;banco de dados&#41; SQL do Azure](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [sys. dm_db_resource_stats &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  
