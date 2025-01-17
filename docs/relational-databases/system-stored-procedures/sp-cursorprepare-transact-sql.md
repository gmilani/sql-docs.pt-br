---
title: sp_cursorprepare (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_prepare
ms.assetid: 6207e110-f4bf-4139-b3ec-b799c9cb3ad7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2719e330ec2fde61b91ca11ef93784983c6c418c
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165907"
---
# <a name="sp_cursorprepare-transact-sql"></a>sp_cursorprepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Compila a instrução de cursor ou processa em lotes em um plano de execução, mas não cria o cursor. A instrução compilada pode ser usada posteriormente por sp_cursorexecute. Esse procedimento, combinado com sp_cursorexecute, tem a mesma função que sp_cursoropen, mas é dividido em duas fases. sp_cursorprepare é invocado especificando ID = 3 em um pacote TDS (tabela de dados tabulares).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursorprepare prepared_handle OUTPUT, params , stmt , options  
    [ , scrollopt[ , ccopt]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *prepared_handle*  
 Um identificador de *identificador* preparado gerado pelo SQL Server que retorna um valor inteiro.  
  
> [!NOTE]  
>  *prepared_handle* é fornecida posteriormente a um procedimento de sp_cursorexecute para abrir um cursor. Quando um identificador é criado, ele existe até que você faça logoff ou remova-o explicitamente por meio de um procedimento sp_cursorunprepare.  
  
 *params*  
 Identifica instruções parametrizadas. A definição *params* das variáveis é substituída por marcadores de parâmetro na instrução. *params* é um parâmetro necessário que chama um valor de entrada **ntext**, **nchar**ou **nvarchar** . Insira um valor NULL se a instrução não for parametrizada.  
  
> [!NOTE]  
>  Use uma cadeia de caracteres **ntext** como o valor de entrada quando *stmt* estiver parametrizada e o valor de PARAMETERIZED_STMT *scrollopt* for on.  
  
 *stmt*  
 Define o conjunto de resultados do cursor. O parâmetro *stmt* é necessário e chama um valor de entrada **ntext**, **nchar** ou **nvarchar** .  
  
> [!NOTE]  
>  As regras para especificar o valor *stmt* são as mesmas que as para sp_cursoropen, com a exceção de que o tipo de dados da cadeia de caracteres *stmt* deve ser **ntext**.  
  
 *Opções*  
 Um parâmetro opcional que retorna uma descrição das colunas do conjunto de resultados de cursor. *as opções* exigem o seguinte valor de entrada **int** .  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 Opção SCROLL. *scrollopt* é um parâmetro opcional que requer um dos seguintes valores de entrada **int** .  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 Como o valor solicitado pode não ser apropriado para o cursor definido por *stmt*, esse parâmetro serve como entrada e saída. Nesses casos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui um valor apropriado.  
  
 *ccopt*  
 Opção de controle de simultaneidade. *ccopt* é um parâmetro opcional que requer um dos seguintes valores de entrada **int** .  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (anteriormente conhecido como LOCKCC)|  
|0x0004|**Otimista** (anteriormente conhecido como OPTCC)|  
|0x0008|OPTIMISTIC (anteriormente conhecido como OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 Assim como com *scrollpt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode atribuir um valor diferente do solicitado.  
  
## <a name="remarks"></a>Remarks  
 O parâmetro de status RPC é um dos seguintes:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0|Success|  
|0x0001|Failure|  
|1FF6|Não foi possível retornar metadados.<br /><br /> Observação: o motivo para isso é que a instrução não produz um conjunto de resultados; por exemplo, é uma instrução INSERT ou DDL.|  
  
## <a name="examples"></a>Exemplos  
  Veja a seguir um exemplo de como usar sp_cursorprepare e sp_cursorexecute

```sql
declare @handle int , @p5 int, @p6 int
exec sp_cursorprepare @handle OUTPUT, 
    N'@dbid int', 
    N'select * from sys.databases where database_id < @dbid',
    1,
    @p5 output,
    @p6 output


declare @p1 int  
set @P1 = @handle 
declare @p2 int   
declare @p3 int  
declare @p4 int  
set @P6 = 4 
exec sp_cursorexecute @p1, @p2 OUTPUT, @p3 output , @p4 output, @p5 OUTPUT, @p6

exec sp_cursorfetch @P2

exec sp_cursorunprepare @handle
exec sp_cursorclose @p2
```
 
 Quando *stmt* é parametrizado e o valor de PARAMETERIZED_STMT *scrollopt* é on, o formato da cadeia de caracteres é o seguinte:  
  
 { *\<nome da variável local > * *\<tipo de dados >* } [ ,... *n* ]  
  
## <a name="see-also"></a>Consulte também  
 [sp_cursorexecute &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorunprepare &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorunprepare-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
