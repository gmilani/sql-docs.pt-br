---
title: sys. resource_governor_resource_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_resource_pools
- resource_governor_resource_pools
- sys.resource_governor_resource_pools_TSQL
- resource_governor_resource_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor_resource_pools catalog view
ms.assetid: 56793e9c-aa90-452e-88c6-d9b799239888
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0446943767217050753c233b03b5b8031dddd1f7
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982640"
---
# <a name="sysresource_governor_resource_pools-transact-sql"></a>sys.resource_governor_resource_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna a configuração armazenada do pool de recursos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada linha da exibição determina a configuração de um pool.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|pool_id|**int**|ID exclusivo do pool de recursos. Não permite valor nulo.|  
|name|**sysname**|Nome do pool de recursos. Não permite valor nulo.|  
|min_cpu_percent|**int**|Média de largura de banda de CPU garantida para todas as solicitações no pool de recursos quando houver contenção de CPU. Não permite valor nulo.|  
|max_cpu_percent|**int**|Largura de banda de CPU máxima permitida para todas as solicitações no pool de recursos quando houver contenção de CPU. Não permite valor nulo.|  
|min_memory_percent|**int**|Quantidade garantida de memória para todas as solicitações no pool de recursos. Não é compartilhada com outros pools de recursos. Não permite valor nulo.|  
|max_memory_percent|**int**|Porcentagem de memória total de servidor que pode ser usada por solicitações nesse pool de recursos. Não permite valor nulo. O efetivo máximo depende dos mínimos de pools. Por exemplo, max_memory_percent pode ser definido como 100, mas o máximo efetivo é inferior.|  
|cap_cpu_percent|**int**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Extremidade rígida na largura de banda de CPU que todas as solicitações no pool de recursos receberão. Limita a largura de banda de CPU máxima ao nível especificado. O intervalo permitido para o valor é de 1 a 100.|  
|min_iops_per_volume|**int**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> A configuração das operações de E/S por segundo (IOPS) mínimas por volume deste pool. 0 = sem reserva. Não pode ser nulo.|  
|max_iops_per_volume|**int**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> A configuração das operações de E/S por segundo (IOPS) máximas por volume deste pool. 0 = ilimitado. Não pode ser nulo.|  
  
## <a name="remarks"></a>Remarks  
 A exibição do catálogo exibe os metadados armazenados. Para ver a configuração na memória, use a exibição de gerenciamento dinâmico correspondente, [Sys. dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW ANY DEFINITION para exibir conteúdo e a permissão CONTROL SERVER para alterar conteúdo.  
  
## <a name="see-also"></a>Consulte também  
   [de exibições &#40;do catálogo&#41; resource governor Transact-SQL](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)  
 [sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)   
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)  
  
  
