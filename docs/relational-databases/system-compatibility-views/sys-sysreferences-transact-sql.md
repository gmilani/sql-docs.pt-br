---
title: sys. sysreferences (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysreferences
- sys.sysreferences_TSQL
- sysreferences
- sysreferences_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysreferences compatibility view
- sysreferences system table
ms.assetid: 81276f13-202e-4e74-962d-46eb98c98d2e
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3edce02f20a16ebd9814f995f00023f8f3b153de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986488"
---
# <a name="syssysreferences-transact-sql"></a>sys.sysreferences (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contém mapeamentos de definições da restrição FOREIGN KEY para as colunas referenciadas no banco de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|ID da restrição FOREIGN KEY.|  
|**fkeyid**|**int**|ID da tabela de referência.|  
|**rkeyid**|**int**|ID da tabela referenciada.|  
|**rkeyindid**|**smallint**|ID do índice exclusivo na tabela referenciada, abrangendo as colunas de chave referenciadas.|  
|**keycnt**|**smallint**|Número de colunas na chave.|  
|**forkeys**|**varbinary(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**refkeys**|**varbinary(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**fkeydbid**|**smallint**|Reservado.|  
|**rkeydbid**|**smallint**|Reservado.|  
|**fkey1**|**smallint**|ID da coluna da coluna de referência.|  
|**fkey2**|**smallint**|ID da coluna da coluna de referência.|  
|**fkey3**|**smallint**|ID da coluna da coluna de referência.|  
|**fkey4**|**smallint**|ID da coluna da coluna de referência.|  
|**fkey5**|**smallint**|ID da coluna da coluna de referência.|  
|**fkey6**|**smallint**|ID da coluna da coluna de referência.|  
|**fkey7**|**smallint**|ID da coluna da coluna de referência.|  
|**fkey8**|**smallint**|ID da coluna da coluna de referência.|  
|**fkey9**|**smallint**|ID da coluna da coluna de referência.|  
|**fkey10**|**smallint**|ID da coluna da coluna de referência.|  
|**fkey11**|**smallint**|ID da coluna da coluna de referência.|  
|**fkey12**|**smallint**|ID da coluna da coluna de referência.|  
|**fkey13**|**smallint**|ID da coluna da coluna de referência.|  
|**fkey14**|**smallint**|ID da coluna da coluna de referência.|  
|**fkey15**|**smallint**|ID da coluna da coluna de referência.|  
|**fkey16**|**smallint**|ID da coluna da coluna de referência.|  
|**rkey1**|**smallint**|ID da coluna da coluna referenciada.|  
|**rkey2**|**smallint**|ID da coluna da coluna referenciada.|  
|**rkey3**|**smallint**|ID da coluna da coluna referenciada.|  
|**rkey4**|**smallint**|ID da coluna da coluna referenciada.|  
|**rkey5**|**smallint**|ID da coluna da coluna referenciada.|  
|**rkey6**|**smallint**|ID da coluna da coluna referenciada.|  
|**rkey7**|**smallint**|ID da coluna da coluna referenciada.|  
|**rkey8**|**smallint**|ID da coluna da coluna referenciada.|  
|**rkey9**|**smallint**|ID da coluna da coluna referenciada.|  
|**rkey10**|**smallint**|ID da coluna da coluna referenciada.|  
|**rkey11**|**smallint**|ID da coluna da coluna referenciada.|  
|**rkey12**|**smallint**|ID da coluna da coluna referenciada.|  
|**rkey13**|**smallint**|ID da coluna da coluna referenciada.|  
|**rkey14**|**smallint**|ID da coluna da coluna referenciada.|  
|**rkey15**|**smallint**|ID da coluna da coluna referenciada.|  
|**rkey16**|**smallint**|ID da coluna da coluna referenciada.|  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
