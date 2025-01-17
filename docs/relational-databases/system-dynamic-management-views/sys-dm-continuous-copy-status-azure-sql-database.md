---
title: sys. dm_continuous_copy_status
titleSuffix: Azure SQL Database
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_continuous_copy_status_TSQL
- dm_continuous_copy_status_TSQL
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
dev_langs:
- TSQL
helpviewer_keywords:
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
ms.assetid: 411b2e71-4421-4ef5-900d-5af068750899
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 6d0bda2d1851d7ec7900a23ad6203d4f85beb73f
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844497"
---
# <a name="sysdm_continuous_copy_status-azure-sql-database"></a>sys.dm_continuous_copy_status (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada banco de dados de usuário (v11) que está atualmente envolvido em uma relação de cópia contínua de replicação geográfica. Se mais de uma relação de cópia contínua for iniciada para um banco de dados primário, essa tabela conterá uma linha para cada banco de dados secundário ativo.  
  
Se você estiver usando o banco de dados SQL V12, deverá usar [Sys. dm_geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md) (porque *Sys. dm_continuous_copy_status* só se aplica a v11).

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**copy_guid**|**uniqueidentifier**|ID exclusiva do banco de dados de réplica.|  
|**partner_server**|**sysname**|Nome do servidor do Banco de Dados SQL vinculado.|  
|**partner_database**|**sysname**|Nome do banco de dados vinculado no servidor do Banco de Dados SQL.|  
|**last_replication**|**datetimeoffset**|O carimbo de data/hora da última transação replicada aplicada.|  
|**replication_lag_sec**|**int**|A diferença de tempo, em segundos, entre a hora atual e o carimbo de data/hora da última transação confirmada com êxito no banco de dados primário que não foi reconhecida pelo banco de dados secundário ativo.|  
|**replication_state**|**tinyint**|O estado da replicação de cópia contínua para este banco de dados. A seguir estão os possíveis valores e suas descrições.<br /><br /> 1: propagação. O destino de replicação está sendo propagado e está em um estado transicionalmente inconsistente. Até que a propagação seja concluída, você não pode se conectar ao banco de dados secundário ativo. <br />2: capturando. O banco de dados secundário ativo está realizando a captura do banco de dados primário e está em um estado transacionalmente consistente.<br />3: refazer a propagação. O banco de dados secundário ativo está sendo repropagado automaticamente devido a uma falha de replicação irrecuperável.<br />4: suspenso. Essa não é uma relação de cópia contínua ativa. Esse estado geralmente indica que a largura de banda disponível para o interlink é insuficiente para o nível de atividade da transação no banco de dados primário. No entanto, a relação de cópia contínua ainda permanece intacta.|  
|**replication_state_desc**|**nvarchar(256)**|Descrição do replication_state:<br /><br /> SEEDING<br /><br /> CATCH_UP<br /><br /> RE_SEEDING<br /><br /> SUSPENDED|  
|**is_rpo_limit_reached**|**bit**|Isso sempre será definido como 0|  
|**is_target_role**|**bit**|0 = Origem da relação de cópia<br /><br /> 1 = Destino da relação de cópia|  
|**is_interlink_connected**|**bit**|1 = O interlink está conectado.<br /><br /> 0 = O interlink está desconectado.|  
  
## <a name="permissions"></a>Permissões  
 Para recuperar dados, o requer a associação na função de banco **db_owner** dados. O usuário dbo, os membros da função de banco de dados **DBManager** e o logon SA também podem consultar essa exibição.  
  
## <a name="remarks"></a>Comentários  
 A exibição **Sys. dm_continuous_copy_status** é criada no banco de dados de **recursos** e fica visível em todos os bancos, incluindo o mestre lógico. No entanto, a consulta dessa exibição no mestre lógico retorna um conjunto vazio.  
  
 Se a relação de cópia contínua for encerrada em um banco de dados, a linha desse banco de dados na exibição **Sys. dm_continuous_copy_status** desaparecerá.  
  
 Assim como a exibição **Sys. dm_database_copies** , **Sys. dm_continuous_copy_status** reflete o estado da relação de cópia contínua na qual o banco de dados é um banco de dados primário ou secundário ativo. Ao contrário de **Sys. dm_database_copies**, **Sys. dm_continuous_copy_status** contém várias colunas que fornecem detalhes sobre operações e desempenho. Essas colunas incluem **last_replication**e **replication_lag_sec**..  
  
## <a name="see-also"></a>Consulte também  
 [Sys. dm_database_copies &#40;banco de dados&#41; SQL do Azure](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)   
 [Procedimentos &#40;armazenados de replicação geográfica ativa TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/81658ee4-4422-4d73-bf7a-86a07422cb0d)  
  
  
