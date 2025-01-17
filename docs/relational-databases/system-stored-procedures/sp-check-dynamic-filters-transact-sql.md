---
title: sp_check_dynamic_filters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- dynamic_filters_TSQL
- sp_check_TSQL
- check
- sp_check_dynamic filter
- check_TSQL
- filters_TSQL
- check_dynamic_filters_TSQL
- dynamic filters
- filters
- check dynamic filters
- sp_check_dynamic filter_TSQL
- sp_check_for_sync_trigger_TSQL
- sp_check
helpviewer_keywords:
- sp_check_dynamic_filters
ms.assetid: dd7760db-a3a5-460f-bd97-b8d436015e19
author: stevestein
ms.author: sstein
ms.openlocfilehash: 82b333095adfaf50220e5d2392114e3ab74bf822
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771294"
---
# <a name="spcheckdynamicfilters-transact-sql"></a>sp_check_dynamic_filters (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Exibe informações sobre propriedades de filtro de linhas com parâmetros para uma publicação, em específico as funções usadas para gerar uma partição de dados filtrados para uma publicação e se a publicação está qualificada para usar partições pré-computadas. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_check_dynamic_filters [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|É se a publicação é qualificada para usar partições preputadas; em que **1** significa que as partições já computadas podem ser usadas, e **0** significa que elas não podem ser usadas.|  
|**has_dynamic_filters**|**bit**|É se pelo menos um filtro de linha com parâmetros tiver sido definido na publicação; em que **1** significa que um ou mais filtros de linha com parâmetros existem e **0** significa que não existem filtros dinâmicos.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|Lista de funções usada para filtrar artigos em uma publicação, onde cada função está separada por um ponto-e-vírgula.|  
|**validate_subscriber_info**|**nvarchar(500)**|Lista de funções usada para filtrar artigos em uma publicação, onde cada função está separada por um sinal de adição (+).|  
|**uses_host_name**|**bit**|Se a função [HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) for usada em filtros de linha com parâmetros, em que **1** significa que essa função é usada para filtragem dinâmica.|  
|**uses_suser_sname**|**bit**|Se a função [SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md) for usada em filtros de linha com parâmetros, em que **1** significa que essa função é usada para filtragem dinâmica.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_check_dynamic_filters** é usado na replicação de mesclagem.  
  
 Se uma publicação tiver sido definida para usar partições preputadas, o **sp_check_dynamic_filters** verificará se há violações das restrições de partições computadas. Se alguma for encontrada, um erro será retornado. Para obter mais informações, consulte [Optimize Parameterized Filter Performance with Precomputed Partitions](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md) (Otimizar o desempenho do filtro parametrizado com partições pré-computadas).  
  
 Se uma publicação foi definida como tendo filtros de linha com parâmetros, mas nenhum filtro de linha com parâmetros for encontrado, será retornado um erro.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **db_owner** podem executar **sp_check_dynamic_filters**.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar partições para uma publicação de mesclagem com filtros com parâmetros](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [sp_check_join_filter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-check-join-filter-transact-sql.md)   
 [sp_check_subset_filter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-check-subset-filter-transact-sql.md)  
  
  
