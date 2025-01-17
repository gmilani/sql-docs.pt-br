---
title: sys.dm_os_memory_cache_entries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_cache_entries
- sys.dm_os_memory_cache_entries
- dm_os_memory_cache_entries_TSQL
- sys.dm_os_memory_cache_entries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_entries dynamic management view
ms.assetid: dd32be6b-10d1-4059-b4fd-0bf817f40d54
author: stevestein
ms.author: sstein
ms.openlocfilehash: 737de971ca39cdf8c164787ff7703b87c38e92e2
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983118"
---
# <a name="sysdm_os_memory_cache_entries-transact-sql"></a>sys.dm_os_memory_cache_entries (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre todas as entradas em caches no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use esta exibição para rastrear entradas de cache para os objetos associados. Você também pode usar esta exibição para obter estatísticas sobre entradas de cache.  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **Sys. dm_pdw_nodes_os_memory_cache_entries**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|Endereço do cache. Não permite valor nulo.|  
|**name**|**nvarchar(256)**|Nome do cache. Não permite valor nulo.|  
|**tipo**|**varchar(60)**|Tipo de cache. Não permite valor nulo.|  
|**entry_address**|**varbinary(8)**|Endereço do descritor da entrada de cache. Não permite valor nulo.|  
|**entry_data_address**|**varbinary(8)**|Endereço dos dados de usuário na entrada de cache.<br /><br /> 0x00000000 = Endereço de dados de entrada não está disponível.<br /><br /> Não permite valor nulo.|  
|**in_use_count**|**int**|Número de usuários simultâneos desta entrada de cache. Não permite valor nulo.|  
|**is_dirty**|**bit**|Indica se a entrada de cache está marcada para remoção. 1 = marcada para remoção. Não permite valor nulo.|  
|**disk_ios_count**|**int**|Número de E/S incorrido durante a criação dessa entrada. Não permite valor nulo.|  
|**context_switches_count**|**int**|Número de alternâncias de contexto incorrido durante a criação dessa entrada. Não permite valor nulo.|  
|**original_cost**|**int**|Custo original da entrada. Esse valor é uma aproximação do número de E/S incorrido, do custo de instrução de CPU e da quantidade de memória consumida pela entrada. Quanto maior o custo, menor a chance de o item ser removido do cache. Não permite valor nulo.|  
|**current_cost**|**int**|Custo atual da entrada de cache. Este valor é atualizado durante o processo de limpeza de entrada. O custo atual é redefinido com seu valor original na reutilização da entrada. Não permite valor nulo.|  
|**memory_object_address**|**varbinary(8)**|Endereço do objeto de memória associado. Permite valor nulo.|  
|**pages_allocated_count**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Número de páginas de 8 KB para armazenar esta entrada de cache. Não permite valor nulo.|  
|**pages_kb**|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Quantidade de memória em quilobytes (KB) usada por essa entrada de cache.  Não permite valor nulo.|  
|**entry_data**|**nvarchar(2048)**|Representação serializada da entrada de cache. Essa informação é dependente do repositório de cache. Permite valor nulo.|  
|**pool_id**|**int**|**Aplica-se a**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] e posterior.<br /><br /> ID do pool de recursos associado à entrada. Permite valor nulo.<br /><br /> não katmai|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões 

No [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer a permissão `VIEW SERVER STATE`.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a permissão `VIEW DATABASE STATE` no banco de dados. Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   

## <a name="see-also"></a>Consulte também  
 
  [SQL Server exibições &#40;de gerenciamento dinâmico relacionadas ao sistema operacional&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


