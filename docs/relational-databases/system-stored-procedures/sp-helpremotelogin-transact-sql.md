---
title: sp_helpremotelogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpremotelogin_TSQL
- sp_helpremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpremotelogin
ms.assetid: 93f50869-2627-4642-899f-8f626f8833f4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 11d71139786ac1442588f016bf8c576b92853cf3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997574"
---
# <a name="sphelpremotelogin-transact-sql"></a>sp_helpremotelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Relata informações sobre logons remotos para um determinado servidor remoto, ou para todos os servidores, definido no servidor local.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Use procedimentos armazenados de servidor vinculado e servidores vinculados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpremotelogin [ [ @remoteserver = ] 'remoteserver' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @remoteserver **=** ] **'***remoteserver***'**  
 É o servidor remoto sobre o qual as informações de logon remoto são retornadas. *remoteserver* está **sysname**, com um padrão NULL. Se *remoteserver* não é especificado, serão retornadas informações sobre todos os servidores remotos definidos no servidor local.  
  
 [ @remotename **=** ] **'***remote_name***'**  
 É um logon remoto específico no servidor remoto. *remote_name* está **sysname**, com um padrão NULL. Se *remote_name* não for especificado, informações sobre todos os usuários remotos definidos para *remoteserver* é retornado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|server|**sysname**|Nome de um servidor remoto definido no servidor local.|  
|local_user_name|**sysname**|Logon no servidor local para os quais os logons remotos do servidor são mapeados.|  
|remote_user_name|**sysname**|Faça logon no servidor remoto que mapeia para local_user_name.|  
|opções|**sysname**|Confiável = O logon remoto não precisa fornecer uma senha ao se conectar ao servidor local a partir do servidor remoto.<br /><br /> Não confiável (ou em branco) = O logon remoto é solicitado a fornecer uma senha ao se conectar ao servidor local a partir do servidor remoto.|  
  
## <a name="remarks"></a>Comentários  
 Use sp_helpserver para listar os nomes de servidores remotos definidos no servidor local.  
  
## <a name="permissions"></a>Permissões  
 Nenhuma permissão é verificada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-reporting-help-on-a-single-server"></a>A. Relatando ajuda em um único servidor  
 O exemplo a seguir exibe as informações sobre todos os usuários remotos no servidor remoto `Accounts`.  
  
```  
EXEC sp_helpremotelogin 'Accounts';  
```  
  
### <a name="b-reporting-help-on-all-remote-users"></a>B. Relatando ajuda em todos os usuários remotos  
 O exemplo a seguir exibe as informações sobre todos os usuários remotos em todos os servidores remotos conhecidos pelo servidor local.  
  
```  
EXEC sp_helpremotelogin;  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_dropremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
