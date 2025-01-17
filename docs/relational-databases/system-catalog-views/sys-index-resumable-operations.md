---
title: sys. index_resumable_operations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.index_resumable_operations_TSQL
- sys.indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes
- sys.index_resumable_operations
ms.assetid: ''
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d33b78710605841e4559f9c402a18210e25b2daa
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73980300"
---
# <a name="sysindex_resumable_operations-transact-sql"></a>sys. index_resumable_operations (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]
**Sys. index_resumable_operations** é uma exibição do sistema que monitora e verifica o status de execução atual para recompilação ou criação de índice retomável.  
**Aplica-se a**: SQL Server (2017 e mais recente) e banco de dados SQL do Azure
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto ao qual este índice pertence (não permite valor nulo).|  
|**index_id**|**int**|ID do índice (não permite valor nulo). **index_id** é exclusivo somente dentro do objeto.|
|**name**|**sysname**|Nome do índice. o **nome** é exclusivo somente dentro do objeto.|  
|**sql_text**|**nvarchar(max)**|Texto da instrução T-SQL DDL|
|**last_max_dop**|**smallint**|Última MAX_DOP usado (padrão = 0)|
|**partition_number**|**int**|Número da partição dentro do índice ou heap de propriedade. Para tabelas e índices não particionados ou, caso todas as partições estejam sendo recriadas, o valor dessa coluna é NULL.|
|**state**|**tinyint**|Estado operacional do índice retomável:<br /><br />0 = em execução<br /><br />1 = pausar|
|**state_desc**|**nvarchar(60)**|Descrição do estado operacional do índice retomável (em execução ou em pausa)|  
|**start_time**|**datetime**|Hora de início da operação de índice (não permite valor nulo)|
|**last_pause_time**|**DataTime**| Tempo da última pausa da operação de índice (anulável). NULL se a operação estiver em execução e nunca for pausada.|
|**total_execution_time**|**int**|Tempo de execução total de tempo de início em minutos (não permite valor nulo)|
|**percent_complete**|**real**|Conclusão do andamento da operação de índice em% (não permite valor nulo).|
|**page_count**|**bigint**|Número total de páginas de índice alocadas pela operação de compilação de índice para os índices novos e de mapeamento (não permite valor nulo).

## <a name="permissions"></a>Permissões

[!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  

## <a name="example"></a>Exemplo

 Liste todas as operações de criação ou recriação de índice retomáveis que estão no estado de pausa.

```sql
SELECT * FROM  sys.index_resumable_operations WHERE STATE = 1;  
```

## <a name="see-also"></a>Consulte também

- [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)
- [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)
- [Exibições do catálogo](catalog-views-transact-sql.md)
- [Exibições do catálogo de objetos](object-catalog-views-transact-sql.md)
- [sys.indexes](sys-xml-indexes-transact-sql.md)
- [sys.index_columns](sys-index-columns-transact-sql.md)
- [sys.xml_indexes](sys-xml-indexes-transact-sql.md)
- [sys.objects](sys-index-columns-transact-sql.md)
- [sys.key_constraints](sys-key-constraints-transact-sql.md)
- [sys.filegroups](sys-filegroups-transact-sql.md)
- [sys.partition_schemes](sys-partition-schemes-transact-sql.md)
- [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](querying-the-sql-server-system-catalog-faq.md)
