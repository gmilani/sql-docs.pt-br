---
title: sp_delete_log_shipping_primary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_primary_database
- sp_delete_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_primary_database
ms.assetid: cb1d5d00-2805-4d47-bd04-545232067345
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: aff19eabc5738e986fca1bf13f85130daead3217
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909863"
---
# <a name="sp_delete_log_shipping_primary_database-transact-sql"></a>sp_delete_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Este procedimento armazenado remove o envio de logs do banco de dados primário, incluindo tarefas de backup, assim como o histórico local e remoto. Use esse procedimento armazenado somente depois de remover os bancos de dados secundários usando **sp_delete_log_shipping_primary_secondary**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_log_shipping_primary_database  
[ @database = ] 'database'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @database = ] 'database'` é o nome do banco de dados primário de envio de logs. o *banco de dados* é **sysname**, sem padrão, e não pode ser nulo.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma.  
  
## <a name="remarks"></a>Remarks  
 **sp_delete_log_shipping_primary_database** deve ser executado a partir do banco de dados **mestre** no servidor primário. Esse procedimento armazenado faz o seguinte:  
  
1.  Exclui o trabalho de backup do banco de dados primário especificado.  
  
2.  Remove o registro de monitor local em **log_shipping_monitor_primary** no servidor primário.  
  
3.  Remove as entradas correspondentes em **log_shipping_monitor_history_detail** e **log_shipping_monitor_error_detail**.  
  
4.  Se o servidor monitor for diferente do servidor primário, o removerá o registro do monitor em **log_shipping_monitor_primary** no servidor monitor.  
  
5.  Remove as entradas correspondentes em **log_shipping_monitor_history_detail** e **log_shipping_monitor_error_detail** no servidor monitor.  
  
6.  Remove a entrada em **log_shipping_primary_databases** para este banco de dados primário.  
  
7.  Chama **sp_delete_log_shipping_alert_job** no servidor monitor.  

## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo ilustra o uso de **sp_delete_log_shipping_primary_database** para excluir o banco de dados primário **AdventureWorks2012**.  
  
```  
EXEC master.dbo.sp_delete_log_shipping_primary_database @database = N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
