---
title: sp_replmonitorhelppublicationthresholds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublicationthresholds
- sp_replmonitorhelppublicationthresholds_TSQL
helpviewer_keywords:
- sp_replmonitorhelppublicationthresholds
ms.assetid: d6b1aa4b-3369-4255-a892-c0e5cc9cb693
author: stevestein
ms.author: sstein
ms.openlocfilehash: ac1efa2e63bb798ce24785e4240bd756e8737e51
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771201"
---
# <a name="sp_replmonitorhelppublicationthresholds-transact-sql"></a>sp_replmonitorhelppublicationthresholds (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna a métrica de limite definida para uma publicação monitorada. Esse procedimento armazenado, usado para monitorar a replicação, é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replmonitorhelppublicationthresholds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`É o nome do Publicador. o Publicador é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados publicado. *publisher_db* é **sysname**, sem padrão.  
  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @publication_type = ] publication_type`Se o tipo de publicação. *publication_type* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Publicação transacional.|  
|**1**|Publicação de instantâneo.|  
|**2**|Publicação de mesclagem.|  
|NULL (padrão)|A replicação tenta determinar o tipo de publicação.|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|ID da métrica de desempenho de replicação, que pode ter um destes valores.<br /><br /> **1expiration** -monitora a expiração iminente de assinaturas para publicações transacionais.<br /><br /> **2latency** -monitora o desempenho de assinaturas para publicações transacionais.<br /><br /> **4mergeexpiration** -monitora a expiração iminente de assinaturas para publicações de mesclagem.<br /><br /> **5mergeslowrunduration** -monitora a duração de sincronizações de mesclagem em conexões de baixa largura de banda (discada).<br /><br /> **6mergefastrunduration** -monitora a duração das sincronizações de mesclagem em conexões de alta largura de banda (LAN).<br /><br /> **7mergefastrunspeed** -monitora a taxa de sincronização de sincronizações de mesclagem em conexões de alta largura de banda (LAN).<br /><br /> **8mergeslowrunspeed** -monitora a taxa de sincronização de sincronizações de mesclagem em conexões de baixa largura de banda (dial-up).|  
|**title**|**sysname**|Nome da métrica de desempenho da replicação.|  
|**value**|**int**|O valor de limite da métrica de desempenho.|  
|**shouldalert**|**bit**|É se um alerta deve ser gerado quando a métrica excede o limite definido para esta publicação; um valor de **1** indica que um alerta deve ser gerado.|  
|**isenabled**|**bit**|É se o monitoramento está habilitado para esta métrica de desempenho de replicação para esta publicação; um valor de **1** indica que o monitoramento está habilitado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_replmonitorhelppublicationthresholds** é usado com todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de banco de dados fixa **db_owner** ou **replmonitor** no banco de dados de distribuição podem executar **sp_replmonitorhelppublicationthresholds**.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar programaticamente a replicação](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
