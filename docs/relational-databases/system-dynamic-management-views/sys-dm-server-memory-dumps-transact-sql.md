---
title: sys.DM server_memory_dumps (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_server_memory_dumps_TSQL
- dm_server_memory_dumps_TSQL
- dm_server_memory_dumps
- sys.dm_server_memory_dumps
dev_langs: TSQL
helpviewer_keywords: sys.dm_server_memory_dumps dynamic management view
ms.assetid: 41782719-f54d-4e11-941a-c050c7576e23
caps.latest.revision: "6"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cd4af6e42415814c6fc0771346f94a5283a41730
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmservermemorydumps-transact-sql"></a>sys.dm_server_memory_dumps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada arquivo de despejo de memória gerado pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Use essa exibição de gerenciamento dinâmico para solucionar problemas potenciais.  
 
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**nome de arquivo**|**nvarchar(256)**|Caminho e nome do arquivo de despejo de memória. Não pode ser nulo.|  
|**creation_time**|**DateTimeOffset(7)**|Data e hora em que o arquivo foi criado. Não pode ser nulo.|  
|**size_in_bytes**|**bigint**|Tamanho (em bytes) do arquivo. Permite valor nulo.|  
  
## <a name="general-remarks"></a>Comentários gerais  
 O tipo de despejo pode ser um minidespejo, despejo de todos os threads ou um despejo completo. Os arquivos têm uma extensão .mdmp.  
  
## <a name="security"></a>Segurança  
 Os arquivos de despejo podem conter informações confidenciais. Para ajudar a proteger essas informações, você pode usar uma lista de controle de acesso (ACL) para restringir o acesso aos arquivos ou copiar os arquivos para uma pasta que tenha acesso restrito. Por exemplo, antes de enviar que os arquivos de depuração para a Microsoft serviços de suporte, é recomendável que você remova todas as informações confidenciais.  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STAT.  
  
  