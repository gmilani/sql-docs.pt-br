---
title: sp_helptracertokens (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helptracertokens
- sp_helptracertokens_TSQL
helpviewer_keywords:
- sp_helptracertokens
ms.assetid: 61f27234-531d-4b37-8fa3-fe4c32e6f521
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9b4df50d1cf43ba1b0f4eb8b8f313634b4d11d18
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771539"
---
# <a name="sp_helptracertokens-transact-sql"></a>sp_helptracertokens (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna uma linha para cada token de rastreamento que foi inserido em uma publicação para determinar latência. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação, ou no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helptracertokens [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação na qual os tokens de rastreamento foram inseridos. a *publicação* é **sysname**, sem padrão.  
  
`[ @publisher = ] 'publisher'`O nome do Publicador. o Publicador é **sysname**, com um padrão de NULL.  
  
> [!NOTE]
>  Esse parâmetro só deve ser especificado para não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores.  
  
`[ @publisher_db = ] 'publisher_db'`O nome do banco de dados de publicação. *publisher_db* é **sysname**, com um valor padrão de NULL. Esse parâmetro será ignorado se o procedimento armazenado for executado no Publicador.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**int**|Identifica um registro de token de rastreamento.|  
|**publisher_commit**|**datetime**|A data e hora que o registro do token foi confirmado no Publicador no banco de dados de publicação.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helptracertokens** é usado na replicação transacional.  
  
 **sp_helptracertokens** é usado para obter IDs de token de rastreamento ao executar o [Transact&#41;-SQL sp_helptracertokenhistory &#40;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md).  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokens-tran_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** , a função de banco de dados fixa **db_owner** no banco de dados de publicação ou as funções de banco de dados fixas **db_owner** ou **replmonitor** no banco de dados de distribuição podem executar **sp_ helptracertokenhistory**.  
  
## <a name="see-also"></a>Consulte também  
 [Medir a latência e validar as conexões para a replicação transacional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
