---
title: CLOSE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CLOSE_TSQL
- CLOSE
dev_langs:
- TSQL
helpviewer_keywords:
- closing cursors
- cursors [SQL Server], closing
- CLOSE statement
ms.assetid: 21546874-97e3-4b93-970f-87c27f6b78c7
author: rothja
ms.author: jroth
ms.openlocfilehash: 63234f9f337bd6427c4c5ed33c146e2ed3a714c9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950323"
---
# <a name="close-transact-sql"></a>CLOSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Fecha um cursor aberto liberando o conjunto de resultados atual e qualquer bloqueio de cursor mantido nas linhas onde o cursor é posicionado. `CLOSE` deixa as estruturas de dados disponíveis para reabertura, mas as atualizações buscadas e posicionadas não são permitidas até que o cursor seja reaberto. CLOSE deve ser emitido em um cursor aberto; `CLOSE` não é permitido em cursores que somente foram declarados ou que já estão fechados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CLOSE { { [ GLOBAL ] cursor_name } | cursor_variable_name }  
```  
  
## <a name="arguments"></a>Argumentos  
 GLOBAL  
 Especifica que *cursor_name* se refere a um cursor global.  
  
 *cursor_name*  
 É o nome de um cursor aberto. Se um cursor global e um cursor local existirem com *cursor_name* como seu nome, *cursor_name* se referirá ao cursor global quando GLOBAL for especificado; caso contrário, *cursor_name* se referirá ao cursor local.  
  
 *cursor_variable_name*  
 É o nome de uma variável de cursor associada a um cursor aberto.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra a colocação correta da instrução `CLOSE` em um processo com base em cursor.  
  
```sql  
DECLARE Employee_Cursor CURSOR FOR  
SELECT EmployeeID, Title FROM AdventureWorks2012.HumanResources.Employee;  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      FETCH NEXT FROM Employee_Cursor;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Cursores](../../relational-databases/cursors.md)   
 [Cursores &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
