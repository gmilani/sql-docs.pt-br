---
title: sys.dm_user_db_resource_governance (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_governance
- sys.resource_governance_TSQL
- resource_governance
- resource_governance_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governance catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: aa7c7e7a7c510f797377c3cbbceb7c2751418da3
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165923"
---
# <a name="sysdm_user_db_resource_governance-transact-sql"></a>sys.dm_user_db_resource_governance (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Retorna as configurações de capacidade e configuração reais usadas pelos mecanismos de governança de recursos no banco de dados atual ou no pool elástico.
  
|Nome da coluna|Data type|Descrição|  
|-----------------|---------------|-----------------|  
|**database_id**|int|ID do banco de dados, exclusivo em um servidor de banco de dados SQL do Azure.|
|**logical_database_guid**|uniqueidentifier|GUID lógico do banco de dados de usuário que permanece durante a vida útil de um banco de dados de usuário.  Renomear o banco de dados ou alterar seu objetivo de nível de serviço não alterará esse valor.|
|**physical_database_guid**|uniqueidentifier|O GUID físico de um banco de dados de usuário que permanece na vida útil da instância física do banco de dados do usuário. Alterar o objetivo de nível de serviço do banco de dados fará com que esse valor seja alterado.|
|**server_name**|nvarchar|Nome do servidor lógico.|
|**database_name**|nvarchar|Nome do banco de dados lógico.|
|**slo_name**|nvarchar|Objetivo de nível de serviço, incluindo a geração de hardware.|
|**dtu_limit**|int|Limite de DTU do banco de dados (nulo para vCore).|
|**cpu_limit**|int|limite vCore do banco de dados (nulo para bancos de dados de DTU).|
|**min_cpu**|tinyint|O valor MIN_CPU_PERCENT do pool de recursos de carga de trabalho do usuário. Consulte [conceitos do pool de recursos](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor-resource-pool?#resource-pool-concepts).|
|**max_cpu**|tinyint|O valor MAX_CPU_PERCENT do pool de recursos de carga de trabalho do usuário. Consulte [conceitos do pool de recursos](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor-resource-pool?#resource-pool-concepts).|
|**cap_cpu**|tinyint|O valor CAP_CPU_PERCENT do pool de recursos de carga de trabalho do usuário. Consulte [conceitos do pool de recursos](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor-resource-pool?#resource-pool-concepts).|
|**min_cores**|SMALLINT|Somente para uso interno.|
|**max_dop**|SMALLINT|O valor MAX_DOP para o grupo de carga de trabalho do usuário. Consulte [Criar grupo de cargas de trabalho](https://docs.microsoft.com/sql/t-sql/statements/create-workload-group-transact-sql).|
|**min_memory**|int|O valor MIN_MEMORY_PERCENT do pool de recursos de carga de trabalho do usuário. Consulte [conceitos do pool de recursos](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor-resource-pool?#resource-pool-concepts).|
|**max_memory**|int|O valor MAX_MEMORY_PERCENT do pool de recursos de carga de trabalho do usuário. Consulte [conceitos do pool de recursos](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor-resource-pool?#resource-pool-concepts).|
|**max_sessions**|int|O número máximo de sessões permitidas no grupo de carga de trabalho do usuário.|
|**max_memory_grant**|int|O valor REQUEST_MAX_MEMORY_GRANT_PERCENT para o grupo de carga de trabalho do usuário. Consulte [Criar grupo de cargas de trabalho](https://docs.microsoft.com/sql/t-sql/statements/create-workload-group-transact-sql).|
|**max_db_memory**|int|Somente para uso interno.|
|**govern_background_io**|bit|Somente para uso interno.|
|**min_db_max_size_in_mb**|bigint|O valor mínimo de max_size para um arquivo de dados, em MB. Consulte [Sys. database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql).|
|**max_db_max_size_in_mb**|bigint|O valor máximo de max_size para um arquivo de dados, em MB. Consulte [Sys. database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql).|
|**default_db_max_size_in_mb**|bigint|O valor de max_size padrão para um arquivo de dados, em MB. Consulte [Sys. database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql).|
|**db_file_growth_in_mb**|bigint|Incremento de crescimento padrão para um arquivo de dados, em MB. Consulte [Sys. database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql).|
|**initial_db_file_size_in_mb**|bigint|Tamanho padrão para o novo arquivo de dados, em MB. Consulte [Sys. database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql).|
|**log_size_in_mb**|bigint|Tamanho padrão para o novo arquivo de log, em MB. Consulte [Sys. database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql).|
|**instance_cap_cpu**|int|Somente para uso interno.|
|**instance_max_log_rate**|bigint|Limite de taxa de geração de log para a instância de SQL Server, em bytes por segundo. Aplica-se a todos os logs gerados pela instância, incluindo `tempdb` e outros bancos de dados do sistema. Em um pool elástico, aplica-se ao log gerado por todos os bancos de dados no pool.|
|**instance_max_worker_threads**|int|Limite de thread de trabalho para a instância de SQL Server.|
|**replica_type**|int|Tipo de réplica, em que 0 é primário e 1 é secundário.|
|**max_transaction_size**|bigint|Espaço de log máximo usado por qualquer transação, em KB.|
|**checkpoint_rate_mbps**|int|Somente para uso interno.|
|**checkpoint_rate_io**|int|Somente para uso interno.|
|**last_updated_date_utc**|Datetime|Data e hora da última alteração de configuração ou reconfiguração, em UTC.|
|**primary_group_id**|int|ID do grupo de carga de trabalho para a carga de trabalho do usuário na réplica primária e nas réplicas secundárias.|
|**primary_group_max_workers**|int|Limite de thread do usuário para o grupo de carga de trabalho.|
|**primary_min_log_rate**|bigint|Taxa mínima de log em bytes por segundo no nível de grupo de carga de trabalho do usuário. A governança de recursos não tentará reduzir a taxa de logs abaixo desse valor.|
|**primary_max_log_rate**|bigint|Taxa máxima de log em bytes por segundo no nível de grupo de carga de trabalho do usuário. A governança de recursos não permitirá a taxa de log acima desse valor.|
|**primary_group_min_io**|int|IOPS mínimo para o grupo de carga de trabalho do usuário. A governança de recursos não tentará reduzir o IOPS abaixo desse valor.|
|**primary_group_max_io**|int|IOPS máximo para o grupo de carga de trabalho do usuário. A governança de recursos não permitirá IOPS acima desse valor.|
|**primary_group_min_cpu**|Valor Flutuante|Porcentagem mínima de CPU para o nível de grupo de carga de trabalho do usuário. A governança de recursos não tentará reduzir a utilização da CPU abaixo desse valor.|
|**primary_group_max_cpu**|Valor Flutuante|Porcentagem máxima de CPU para o nível de grupo de carga de trabalho do usuário. A governança de recursos não permitirá a utilização da CPU acima desse valor.|
|**primary_log_commit_fee**|int|Taxa de confirmação de governança de taxa de log para o grupo de carga de trabalho do usuário, em bytes. Uma taxa de confirmação aumenta o tamanho de cada e/s de log por um valor fixo apenas para fins de contabilidade de taxa de log. A e/s de log real para armazenamento não é aumentada.|
|**primary_pool_max_workers**|int|Limite de thread do usuário para o pool de recursos de carga de trabalho.|
|**pool_max_io**|int|Limite máximo de IOPS para o pool de recursos de carga de trabalho do usuário.|
|**govern_db_memory_in_resource_pool**|bit|Somente para uso interno.|
|**volume_local_iops**|int|Somente para uso interno.|
|**volume_managed_xstore_iops**|int|Somente para uso interno.|
|**volume_external_xstore_iops**|int|Somente para uso interno.|
|**volume_type_local_iops**|int|Somente para uso interno.|
|**volume_type_managed_xstore_iops**|int|Somente para uso interno.|
|**volume_type_external_xstore_iops**|int|Somente para uso interno.|
|**volume_pfs_iops**|int|Somente para uso interno.|
|**volume_type_pfs_iops**|int|Somente para uso interno.|
|||

## <a name="permissions"></a>Permissões

Essa exibição exige a permissão VIEW DATABASE STATE.

## <a name="remarks"></a>Remarks

Para obter a descrição da governança de recursos no banco de dados SQL do Azure, consulte [limites de recursos do banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server).

> [!IMPORTANT]
> A maioria dos dados retornados por essa DMV destina-se ao consumo interno e está sujeita a alterações a qualquer momento.

## <a name="examples"></a>Exemplos

A consulta a seguir, executada no contexto de um banco de dados de usuário, retorna a taxa de log máxima e o IOPS máximo no nível do grupo de carga de trabalho do usuário e do pool de recursos. Para um banco de dados individual, uma linha é retornada. Para um banco de dados em um pool elástico, uma linha é retornada para cada banco de dados no pool.

```
SELECT database_name,
       primary_group_id,
       primary_max_log_rate,
       primary_group_max_io,
       pool_max_io
FROM sys.dm_user_db_resource_governance
ORDER BY database_name;  
```

## <a name="see-also"></a>Consulte também

- [Administrador de Recursos](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)
- [sys. dm_resource_governor_resource_pools (Transact-SQL)](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql)
- [sys. dm_resource_governor_workload_groups (Transact-SQL)](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql)
- [sys. dm_resource_governor_resource_pools_history_ex (Transact-SQL)](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-history-ex-azure-sql-database)
- [sys. dm_resource_governor_workload_groups_history_ex (banco de dados SQL do Azure)](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-history-ex-azure-sql-database)
- [Governança de taxa de log de transações](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Limites de recursos de DTU de banco de dados individual](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [Limites de recursos vCore de banco de dados individual](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)
