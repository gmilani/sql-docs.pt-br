---
title: USER_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- USER_NAME
- USER_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- usernames [SQL Server]
- IDs [SQL Server], databases
- USER_NAME function
- users [SQL Server], database username
- names [SQL Server], database users
- identification numbers [SQL Server], databases
- database usernames [SQL Server]
ms.assetid: ab32d644-4228-449a-9ef0-5a975c305775
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d2f8a3f4dbdbaa9cbd2cf1c99a86ad6f3573ab11
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844344"
---
# <a name="user_name-transact-sql"></a>USER_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna um nome de usuário de banco de dados de um número de identificação especificado.  
  
 ![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do artigo") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
USER_NAME ( [ id ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *id*  
 É o número de identificação associado a um usuário do banco de dados. *id* é **int**. Os parênteses são necessários.  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar(128)**  
  
## <a name="remarks"></a>Remarks  
 Quando *id* é omitido, o usuário atual no contexto atual é assumido. Se o parâmetro contiver a palavra NULL, retornará NULL. Quando USER_NAME é chamado sem especificar uma *id* depois de uma instrução EXECUTE AS, USER_NAME retorna o nome do usuário representado. Se um principal do Windows acessar o banco de dados por meio da associação em um grupo, USER_NAME retornará o principal do Windows em vez do grupo.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-user_name"></a>A. Usando USER_NAME  
 O exemplo a seguir retorna o nome de usuário para o usuário `13`.  
  
```  
SELECT USER_NAME(13);  
GO  
```  
  
### <a name="b-using-user_name-without-an-id"></a>B. Usando USER_NAME sem uma ID  
 O exemplo a seguir localiza o nome do usuário atual sem especificar um ID.  
  
```  
SELECT USER_NAME();  
GO  
```  
  
 Este é o conjunto de resultados para um usuário que é um membro da função de servidor fixa sysadmin.  
  
 ```
------------------------------  
dbo  
  
(1 row(s) affected)
```  
  
### <a name="c-using-user_name-in-the-where-clause"></a>C. Usando USER_NAME na cláusula WHERE  
 O exemplo a seguir localiza a linha em `sysusers` na qual o nome é igual ao resultado da aplicação da função de sistema `USER_NAME` ao número de identificação de usuário `1`.  
  
```  
SELECT name FROM sysusers WHERE name = USER_NAME(1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
name  
------------------------------  
dbo  
  
(1 row(s) affected)
```  
  
### <a name="d-calling-user_name-during-impersonation-with-execute-as"></a>D. Chamando USER_NAME durante a representação com EXECUTE AS  
 O exemplo a seguir mostra como `USER_NAME` se comporta durante representação.  
  
```  
SELECT USER_NAME();  
GO  
EXECUTE AS USER = 'Zelig';  
GO  
SELECT USER_NAME();  
GO  
REVERT;  
GO  
SELECT USER_NAME();  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
DBO  
Zelig  
DBO
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-user_name-without-an-id"></a>E. Usando USER_NAME sem uma ID  
 O exemplo a seguir localiza o nome do usuário atual sem especificar um ID.  
  
```  
SELECT USER_NAME();  
```  
  
 Este é o conjunto de resultados para um usuário conectado no momento.  
  
```  
------------------------------   
User7                              
```  
  
### <a name="f-using-user_name-in-the-where-clause"></a>F. Usando USER_NAME na cláusula WHERE  
 O exemplo a seguir localiza a linha em `sysusers` na qual o nome é igual ao resultado da aplicação da função de sistema `USER_NAME` ao número de identificação de usuário `1`.  
  
```  
SELECT name FROM sysusers WHERE name = USER_NAME(1);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
name                             
------------------------------   
User7                              
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP &#40;Transact-SQL&#41;](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER &#40;Transact-SQL&#41;](../../t-sql/functions/current-user-transact-sql.md)   
 [SESSION_USER &#40;Transact-SQL&#41;](../../t-sql/functions/session-user-transact-sql.md)   
 [Funções de sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [SYSTEM_USER &#40;Transact-SQL&#41;](../../t-sql/functions/system-user-transact-sql.md)  
  
