---
title: sys.dm_exec_session_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_session_wait_stats
- sys.dm_exec_session_wait_stats_tsql
- dm_exec_session_wait_stats
- dm_exec_session_wait_stats_tsql
helpviewer_keywords:
- sys.dm_exec_session_wait_stats
ms.assetid: df84842a-71eb-4fda-b448-5953cf9985dc
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6fc51bec78cf01522e6731648bdb7870ea7d9fb0
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982607"
---
# <a name="sysdm_exec_session_wait_stats-transact-sql"></a>sys.dm_exec_session_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre todas as esperas encontradas por threads executados para cada sessão. Você pode usar essa exibição para diagnosticar problemas de desempenho com a sessão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e também com consultas e lotes específicos.  Essa exibição retorna a sessão as mesmas informações agregadas para [Sys. dm_os_wait_stats &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) , mas também fornece o número de **session_id** .  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|A ID da sessão.|  
|wait_type|**nvarchar(60)**|Nome do tipo de espera. Para obter mais informações, veja [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|  
|waiting_tasks_count|**bigint**|Número de esperas nesse tipo de espera. O contador é incrementado no início de cada espera.|  
|wait_time_ms|**bigint**|Tempo de espera total para esse tipo de espera em milissegundos. Essa hora é inclusiva de signal_wait_time_ms.|  
|max_wait_time_ms|**bigint**|Tempo de espera máximo neste tipo de espera.|  
|signal_wait_time_ms|**bigint**|Diferença entre a hora em que o thread de espera foi sinalizado e quando ele começou a ser executado.|  
  
## <a name="remarks"></a>Remarks  
 Essa DMV redefine as informações de uma sessão quando a sessão é aberta ou quando a sessão é redefinida (se o pool de conexões),  
  
 Para obter informações sobre os tipos de espera, consulte [Sys &#40;. DM_OS_WAIT_STATS Transact&#41;-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Se o usuário tiver a permissão **View Server State** no servidor, o usuário verá todas as sessões em execução na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; caso contrário, o usuário verá apenas a sessão atual.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server exibições &#40;de&#41; gerenciamento dinâmico relacionadas ao sistema operacional](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
 
