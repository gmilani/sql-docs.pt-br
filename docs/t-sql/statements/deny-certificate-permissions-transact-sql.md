---
title: Permissões DENY de certificado (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], permissions
- permissions [SQL Server], certificates
- DENY statement, certificates
- denying permissions [SQL Server], certificates
ms.assetid: 5971ff9e-d6a4-414b-ae1f-819bc2e348f5
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2b9314935f347fb4c8768cfaa192c5df0c18d1ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114928"
---
# <a name="deny-certificate-permissions-transact-sql"></a>Permissões de certificado DENY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Nega permissões em um certificado.  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DENY permission  [ ,...n ]   
    ON CERTIFICATE :: certificate_name   
    TO principal [ ,...n ]  
    [ CASCADE ]  
    [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *permission*  
 Especifica uma permissão que pode ser negada em um certificado. Listada abaixo.  
  
 ON CERTIFICATE **::** _certificate_name_  
 Especifica o certificado no qual a permissão está sendo negada. O qualificador de escopo "::" é obrigatório.  
  
 *database_principal*  
 Especifica a entidade à qual a permissão está sendo negada. Um dos seguintes:  
  
-   usuário de banco de dados  
  
-   função de banco de dados  
  
-   função de aplicativo  
  
-   usuário de banco de dados mapeado para um logon do Windows  
  
-   usuário de banco de dados mapeado para um grupo do Windows  
  
-   usuário de banco de dados mapeado para um certificado  
  
-   usuário de banco de dados mapeado para uma chave assimétrica  
  
-   usuário de banco de dados não mapeado para uma entidade do servidor.  
  
 CASCADE  
 Indica que a permissão que está sendo negada também é negada a outros principais aos quais ela foi concedida por esse principal.  
  
 *denying_principal*  
 Especifica uma entidade de segurança da qual a entidade de segurança que executa essa consulta deriva seu direito de negar a permissão. Um dos seguintes:  
  
-   usuário de banco de dados  
  
-   função de banco de dados  
  
-   função de aplicativo  
  
-   usuário de banco de dados mapeado para um logon do Windows  
  
-   usuário de banco de dados mapeado para um grupo do Windows  
  
-   usuário de banco de dados mapeado para um certificado  
  
-   usuário de banco de dados mapeado para uma chave assimétrica  
  
-   usuário de banco de dados não mapeado para uma entidade do servidor.  
  
## <a name="remarks"></a>Remarks  
 Um certificado é um protegível em nível de banco de dados contido no banco de dados pai da hierarquia de permissões. As permissões mais específicas e limitadas que podem ser negadas em um certificado estão listadas abaixo, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão de certificado|Indicado pela permissão de certificado|Implícito na permissão de banco de dados|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CERTIFICATE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no certificado. Se a cláusula AS for usada, a entidade especificada deverá ser proprietária do certificado.  
  
## <a name="see-also"></a>Consulte Também  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
