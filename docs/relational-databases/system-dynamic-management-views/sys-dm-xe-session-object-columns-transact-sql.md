---
title: sys.dm_xe_session_object_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xe_session_object_columns_TSQL
- sys.dm_xe_session_object_columns_TSQL
- dm_xe_session_object_columns
- sys.dm_xe_session_object_columns
dev_langs:
- TSQL
helpviewer_keywords:
- xe
- sys.dm_xe_session_object_columns dynamic management view
ms.assetid: e97f3307-2da6-4c54-b818-a474faec752e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 039c3b0be4feab53215bae22836b7fd5be4ecfb5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090229"
---
# <a name="sysdmxesessionobjectcolumns-transact-sql"></a>sys.dm_xe_session_object_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mostra os valores de configuração de objetos associados a uma sessão.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|O endereço da memória da sessão de evento. Tem uma relação muitos para um com sys.dm_xe_sessions.address. Não permite valor nulo.|  
|column_name|**nvarchar(256)**|O nome do valor de configuração. Não permite valor nulo.|  
|column_id|**int**|A ID da coluna. É exclusiva no objeto. Não permite valor nulo.|  
|column_value|**nvarchar(3072)**|O valor configurado da coluna. Permite valor nulo.|  
|object_type|**nvarchar(60)**|O tipo do objeto. Não permite valor nulo. object_type é um de:<br /><br /> event<br /><br /> target|  
|object_name|**nvarchar(256)**|O nome do objeto ao qual a coluna pertence. Não permite valor nulo.|  
|object_package_guid|**uniqueidentifier**|O GUID do pacote que contém o objeto. Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|dm_xe_session_object_columns.object_name,<br /><br /> dm_xe_session_object_columns.object_package_guid|sys.dm_xe_objects.package_guid,<br /><br /> sys.dm_xe_objects.name|Muitos para um|  
|dm_xe_session_object_columns.column_name,<br /><br /> dm_xe_session_object_columns.column_id|sys.dm_xe_object_columns.Name,<br /><br /> sys.dm_xe_object_columns.column_id|Muitos para um|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

