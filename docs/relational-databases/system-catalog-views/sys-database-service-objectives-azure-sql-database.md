---
title: sys.database_service_objectives
titleSuffix: Azure SQL Database
ms.custom: seo-dt-2019
ms.date: 03/21/2018
ms.service: sql-database
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.topic: conceptual
keywords:
- pool elástico
- pool elástico, gerenciamento
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 465416e87966ba3a80c8e98394c0b1f2009f591b
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844458"
---
# <a name="sysdatabase_service_objectives-azure-sql-database"></a>sys. database_service_objectives (banco de dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Retorna a edição (camada de serviço), o objetivo de serviço (tipo de preço) e o nome do pool elástico, se houver, para um banco de dados SQL do Azure ou um SQL Data Warehouse do Azure. Se estiver conectado ao banco de dados mestre em um servidor de banco de dados SQL do Azure, retorna informações sobre todos os bancos de dados. Para o Azure SQL Data Warehouse, você deve estar conectado ao banco de dados mestre.  
  
  
 Para obter informações sobre preços, consulte [Opções e desempenho do banco de dados SQL: preços do banco de dados SQL](https://azure.microsoft.com/pricing/details/sql-database/) e [preços de SQL data warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).  
  
 Para alterar as configurações de serviço, consulte [ALTER DATABASE (banco de dados SQL do Azure)](../../t-sql/statements/alter-database-azure-sql-database.md) e [alter database (Azure SQL data warehouse)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest).  
  
 A exibição sys. database_service_objectives contém as colunas a seguir.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id|int|A ID do banco de dados, exclusiva dentro de uma instância do servidor de banco de dados SQL do Azure. Ingresse com o [ &#40;Transact-SQL&#41;sys. databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|edição|sysname|A camada de serviço para o banco de dados ou data warehouse: **Basic**, **Standard**, **Premium** ou **data warehouse**.|  
|service_objective|sysname|O tipo de preço do banco de dados. Se o banco de dados estiver em um pool elástico, retornará **ElasticPool**.<br /><br /> Na camada **básica** , retorna **Basic**.<br /><br /> O **banco de dados individual em uma camada de serviço Standard** retorna um dos seguintes: S0, S1, S2, S3, S4, S6, S7, S9 ou S12.<br /><br /> **Um banco de dados individual em uma camada Premium** retorna do seguinte: P1, P2, P4, P6, P11 ou P15.<br /><br /> **SQL data warehouse** retorna DW100 por meio de DW30000c.<br /><br /> Para obter detalhes, consulte bancos de dados [individuais](/azure/sql-database/sql-database-dtu-resource-limits-single-databases/), [pools elásticos](/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools/)e [data warehouses](/azure/sql-data-warehouse/what-is-a-data-warehouse-unit-dwu-cdwu/)|  
|elastic_pool_name|sysname|O nome do [pool elástico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/) ao qual o banco de dados pertence. Retornará **NULL** se o banco de dados for um banco de dado único ou um data warehoue.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **dbManager** no banco de dados mestre.  No nível do banco de dados, o usuário deve ser o criador ou proprietário.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo pode ser executado no banco de dados mestre ou em bancos de dados de usuário do banco de dados SQL do Azure. A consulta retorna o nome, o serviço e as informações do nível de desempenho dos bancos de dados.  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
