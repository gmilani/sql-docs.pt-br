---
title: dbo.systargetservers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.systargetservers_TSQL
- dbo.systargetservers
- systargetservers_TSQL
- systargetservers
dev_langs:
- TSQL
helpviewer_keywords:
- systargetservers system table
ms.assetid: 479d1314-be37-4d19-ac9c-419fc9110e53
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3c6304b108d75d6fe9ba00ccccdae322bf7cedde
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095837"
---
# <a name="dbosystargetservers-transact-sql"></a>dbo.systargetservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra quais servidores de destino estão inscritos atualmente neste domínio de operação multisservidor.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|ID do servidor.|  
|**server_name**|**sysname**|Nome de servidor.|  
|**Local**|**nvarchar(200)**|Local do servidor de destino especificado.|  
|**time_zone_adjustment**|**int**|Intervalo de ajuste de tempo, em horas, com base na hora de Greenwich (GMT).|  
|**enlist_date**|**datetime**|Data e hora em que o servidor de destino especificado foi inscrito.|  
|**last_poll_date**|**datetime**|Data e hora em que o servidor de destino especificado sondou pela última vez o multiserver **sysdownloadlist** tabela do sistema para a execução de trabalhos.|  
|**status**|**int**|Status do servidor de destino:<br /><br /> **1** = Normal<br /><br /> **2** = ressincronização pendente<br /><br /> **4** = suspeito de estar Offline|  
|**local_time_at_last_poll**|**datetime**|Data e hora que o servidor de destino foi sondado pela última vez por operações de trabalho.|  
|**enlisted_by_nt_user**|**nvarchar(100)**|Nome de usuário da pessoa que executa **sp_msx_enlist** no servidor de destino.|  
|**poll_internal**|**int**|Número de segundos a serem decorridos antes que o servidor de destino sonde o servidor mestre por novas instruções de carregamento.|  
  
  
