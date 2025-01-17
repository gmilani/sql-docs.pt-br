---
title: sp_helpreplicationdboption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplicationdboption_TSQL
- sp_helpreplicationdboption
helpviewer_keywords:
- sp_helpreplicationdboption
ms.assetid: 143ce689-108b-49d7-9892-fd3a86897f38
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7aa68b2ee2e592f264f5a64c4c675103253da495
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771527"
---
# <a name="sphelpreplicationdboption-transact-sql"></a>sp_helpreplicationdboption (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Mostra se os bancos de dados no Publicador estão habilitados para replicação. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados. *Não há suporte para Publicadores Oracle.*  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpreplicationdboption [ [ @dbname =] 'dbname' ]  
    [ , [ @type = ] 'type' ]  
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'dbname'`É o nome do banco de dados. *dbname* é **sysname**, com um padrão de **%** . Se **%** , em seguida, o conjunto de resultados contiver todos os bancos de dados no Publicador, caso contrário, apenas as informações sobre o banco de dados especificado serão retornadas. Não são retornadas informações para nenhum banco de dados para o qual o usuário não tenha a permissão apropriada, como descrita abaixo.  
  
`[ @type = ] 'type'`Restringe o conjunto de resultados para conter somente os bancos de dados nos quais o valor do *tipo* de opção de replicação especificado foi habilitado. o *tipo* é **sysname**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**publicou**|Replicação transacional permitida.|  
|**publicação de mesclagem**|Replicação de mesclagem permitida.|  
|**replicação permitida** os|Replicação transacional ou replicação de mesclagem permitida.|  
  
`[ @reserved = ] reserved`Especifica se as informações sobre publicações e assinaturas existentes são retornadas. *reservado* é um **bit**, com um valor padrão de 0. Se **1**, o conjunto de resultados incluirá informações sobre se o banco de dados especificado tem alguma publicação ou assinatura existente.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do banco de dados.|  
|**id**|**int**|Identificador de banco de dados.|  
|**transpublicar**|**bit**|Se o banco de dados tiver sido habilitado para publicação de instantâneo ou transacional; em que um valor de **1** significa que a publicação de instantâneo ou transacional está habilitada.|  
|**mergepublish**|**bit**|Se o banco de dados tiver sido habilitado para publicação de mesclagem; em que um valor de **1** significa que a publicação de mesclagem está habilitada.|  
|**dbowner**|**bit**|Se o usuário for um membro da função de banco de dados fixa **db_owner** ; em que um valor de **1** indica que o usuário é um membro dessa função.|  
|**dbreadonly**|**bit**|Se o banco de dados estiver marcado como somente leitura; em que um valor de **1** significa que o banco de dados é somente leitura.|  
|**haspublications**|**bit**|É se o banco de dados tiver qualquer publicação existente; em que um valor de **1** significa que há publicações existentes.|  
|**haspullsubscriptions**|**bit**|É se o banco de dados tiver qualquer assinatura pull existente; em que um valor de **1** significa que há assinaturas pull existentes.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpreplicationdboption** é usado em replicação de instantâneo, transacional e de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Os membros da função de servidor fixa **sysadmin** podem executar **sp_helpreplicationdboption** para qualquer banco de dados. Os membros da função de banco de dados fixa **db_owner** podem executar **sp_helpreplicationdboption** para esse banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
