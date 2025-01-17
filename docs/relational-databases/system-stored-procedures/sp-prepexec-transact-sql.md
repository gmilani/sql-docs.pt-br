---
title: sp_prepexec (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexec
- sp_cursor_prepexec_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexec
ms.assetid: f9141850-a62b-43bf-8e46-b2f92b75ca56
author: stevestein
ms.author: sstein
ms.openlocfilehash: 670b64cb107610fe8b5506654b9e655b0da5fb16
ms.sourcegitcommit: bcc3b2c7474297aba17b7a63b17c103febdd0af9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794719"
---
# <a name="sp_prepexec-transact-sql"></a>sp_prepexec (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Prepara e executa uma [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução parametrizada. sp_prepexec combina as funções de sp_prepare e sp_execute. Essa ação é invocada pela ID = 13 em um pacote TDS (tabela de dados tabulares).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_prepexec handle OUTPUT, params , stmt  
    [ , bound param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *processamento*  
 É o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]identificador de identificador gerado. o *identificador* é um parâmetro necessário com um valor de retorno **int** .  
  
 *params*  
 Identifica instruções parametrizadas. A definição params das variáveis é substituída por marcadores de parâmetro na instrução. *params* é um parâmetro necessário que chama um valor de entrada **ntext**, **nchar**ou **nvarchar** . Insira um valor NULL se a instrução não for parametrizada.  
  
 *stmt*  
 Define o conjunto de resultados do cursor. O parâmetro *stmt* é necessário e chama um valor de entrada **ntext**, **nchar**ou **nvarchar** .  
  
 *bound_param*  
 Significa o uso opcional de parâmetros adicionais. *bound_param* chama um valor de entrada de qualquer tipo de dados para designar os parâmetros adicionais em uso.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir prepara e executa uma instrução simples:  
  
```  
Declare @Out int;  
EXEC sp_prepexec @Out output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name  
      FROM sys.databases  
      WHERE name=@P1 AND state_desc = @P2',   
          @P1 = 'tempdb', @P2 = 'ONLINE';   
EXEC sp_unprepare @Out;  
```  
  
## <a name="see-also"></a>Confira também  
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [Transact &#40;-SQL sp_execute&#41;](../../relational-databases/system-stored-procedures/sp-execute-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
