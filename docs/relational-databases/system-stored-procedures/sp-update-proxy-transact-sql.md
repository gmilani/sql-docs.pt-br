---
title: sp_update_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_proxy
- sp_update_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PROXY statement
- sp_update_proxy
ms.assetid: 864fd0e6-9d61-4f07-92ef-145318d2f881
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ec6c40abd080c86722565762fab3b4f9d30bd0c0
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305311"
---
# <a name="sp_update_proxy-transact-sql"></a>sp_update_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de um proxy existente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_update_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @new_name = ] 'new_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @proxy_id = ] id` o número de identificação de proxy do proxy a ser alterado. O *proxy_id* é **int**, com um padrão de NULL.  
  
`[ @proxy_name = ] 'proxy_name'` o nome do proxy a ser alterado. O *proxy_name* é **sysname**, com um padrão de NULL.  
  
`[ @credential_name = ] 'credential_name'` o nome da nova credencial para o proxy. O *credential_name* é **sysname**, com um padrão de NULL. O *credential_name* ou o *credential_id* podem ser especificados.  
  
`[ @credential_id = ] credential_id` o número de identificação da nova credencial para o proxy. O *credential_id* é **int**, com um padrão de NULL. O *credential_name* ou o *credential_id* podem ser especificados.  
  
`[ @new_name = ] 'new_name'` o novo nome do proxy. O *new_name* é **sysname**, com um padrão de NULL. Quando fornecido, o procedimento altera o nome do proxy para *new_name*. Quando esse argumento for NULL, o nome do proxy permanecerá inalterado.  
  
`[ @enabled = ] is_enabled` é se o proxy está habilitado. O sinalizador *is_enabled* é **tinyint**, com um padrão de NULL. Quando *is_enabled* é **0**, o proxy não é habilitado e não pode ser usado por uma etapa de trabalho. Quando esse argumento for NULL, o status do proxy permanecerá inalterado.  
  
`[ @description = ] 'description'` a nova descrição do proxy. A *Descrição* é **nvarchar (512)** , com um padrão de NULL. Quando esse argumento for NULL, a descrição do proxy permanecerá inalterada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 É necessário especificar **\@proxy_name** ou **\@proxy_id** . Se os dois argumentos forem especificados, eles deverão se referir ao mesmo proxy, caso contrário o procedimento armazenado falhará.  
  
 É necessário especificar **\@credential_name** ou **\@credential_id** para alterar a credencial do proxy. Se os dois argumentos forem especificados, eles deverão se referir à mesma credencial, caso contrário o procedimento armazenado falhará.  
  
 Esse procedimento altera o proxy, mas não altera o acesso a ele. Para alterar o acesso a um proxy, use **sp_grant_login_to_proxy** e **sp_revoke_login_from_proxy**.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de segurança fixa **sysadmin** podem executar este procedimento.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir define o valor habilitado para o proxy `Catalog application proxy` como `0`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 0;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Agent procedimentos &#40;armazenados Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Implementar SQL Server Agent segurança](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
