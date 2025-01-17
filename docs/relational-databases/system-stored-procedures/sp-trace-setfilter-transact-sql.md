---
title: sp_trace_setfilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_setfilter
- sp_trace_setfilter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setfilter
ms.assetid: 11e7c7ac-a581-4a64-bb15-9272d5c1f7ac
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0f48f7e8dd6e7d8fa57868994f9bcabb66777e90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095945"
---
# <a name="sptracesetfilter-transact-sql"></a>sp_trace_setfilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aplica um filtro a um rastreamento. **sp_trace_setfilter** pode ser executado apenas em rastreamentos existentes que são interrompidos (*status* é **0**). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Retorna um erro se esse procedimento armazenado é executado em um rastreamento que não existe ou cujo *status* não está **0**.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use Eventos Estendidos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_trace_setfilter [ @traceid = ] trace_id   
          , [ @columnid = ] column_id  
          , [ @logical_operator = ] logical_operator  
          , [ @comparison_operator = ] comparison_operator  
          , [ @value = ] value  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @traceid = ] trace_id` É a ID do rastreamento para o qual o filtro está definido. *trace_id* está **int**, sem padrão. O usuário emprega este *trace_id* valor para identificar, modificar e controlar o rastreamento.  
  
`[ @columnid = ] column_id` É a ID da coluna na qual o filtro é aplicado. *column_id* está **int**, sem padrão. Se *column_id* for NULL, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] limpa todos os filtros para o rastreamento especificado.  
  
`[ @logical_operator = ] logical_operator` Especifica se o AND (**0**) ou OR (**1**) operador é aplicado. *logical_operator* está **int**, sem padrão.  
  
`[ @comparison_operator = ] comparison_operator` Especifica o tipo de comparação a ser feita. *comparison_operator* está **int**, sem padrão. A tabela contém os operadores de comparação e os valores representativos dos mesmos.  
  
|Valor|Operador de comparação|  
|-----------|-------------------------|  
|**0**|= (Igual)|  
|**1**|<> (Não igual)|  
|**2**|> (Maior que)|  
|**3**|< (Menor que)|  
|**4**|> = (maior que ou igual)|  
|**5**|< = (menor ou igual)|  
|**6**|LIKE|  
|**7**|Não semelhante a|  
  
`[ @value = ] value` Especifica o valor no qual filtrar. O tipo de dados *valor* deve corresponder ao tipo de dados da coluna a ser filtrada. Por exemplo, se o filtro está definido em uma coluna de ID de objeto que é um **int** tipo de dados *valor* deve ser **int**. Se *valor* é **nvarchar** ou **varbinary**, ele pode ter um comprimento máximo de 8000.  
  
 Quando o operador de comparação for LIKE ou NOT LIKE, o operador lógico poderá incluir "%" ou outro filtro apropriado para a operação LIKE.  
  
 Você pode especificar NULL para *valor* para filtrar eventos com valores de coluna NULL. Somente **0** (= igual) e **1** operadores (<> não igual) são válidos com NULL. Neste caso, esses operadores são equivalentes aos operadores [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL e IS NOT NULL.  
  
 Para aplicar o filtro entre um intervalo de valores de coluna **sp_trace_setfilter** deve ser executado duas vezes, uma vez com um maior-que-or-equals ('> =') operador de comparação e outra com um menor-que-or-equals ('< =') operador .  
  
 Para obter mais informações sobre tipos de dados da coluna de dados, consulte o [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 A tabela a seguir descreve os valores de código que os usuários podem obter após a conclusão do procedimento armazenado.  
  
|Código de retorno|Descrição|  
|-----------------|-----------------|  
|0|Nenhum erro.|  
|1|Erro desconhecido.|  
|2|O rastreamento está sendo executado no momento. A alteração do rastreamento neste momento resulta em um erro.|  
|4|A Coluna especificada não é válida.|  
|5|A Coluna especificada não possui permissão para filtro. Esse valor é retornado somente a partir **sp_trace_setfilter**.|  
|6|O Operador de Comparação especificado não é válido.|  
|7|O Operador Lógico especificado não é válido.|  
|9|O Identificador de Rastreamento especificado não é válido.|  
|13|Memória insuficiente. Retornado quando não há memória suficiente para executar a ação especificada.|  
|16|A função não é válida para este rastreamento.|  
  
## <a name="remarks"></a>Comentários  
 **sp_trace_setfilter** é um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedimento armazenado que executa muitas das ações anteriormente executadas por procedimentos armazenados estendidos disponíveis em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use **sp_trace_setfilter** em vez da **xp_trace_set\*filtro** estendido procedimentos armazenados para criar, aplicar, remover ou manipular filtros em rastreamentos. Para obter mais informações, consulte [filtrar um rastreamento](../../relational-databases/sql-trace/filter-a-trace.md).  
  
 Todos os filtros para uma determinada coluna devem ser habilitados juntos em uma execução de **sp_trace_setfilter**. Por exemplo, se um usuário pretende aplicar dois filtros na coluna de nome de aplicativo e um filtro na coluna de nome de usuário, o usuário deve especificar os filtros em nome de aplicativo em sequência. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna um erro se o usuário tentar especificar um filtro em nome de aplicativo em uma chamada de procedimento armazenado, em seguida, por um filtro em nome de usuário, e depois, outro filtro em nome de aplicativo.  
  
 Parâmetros de rastreamento do SQL de todos os procedimentos armazenados (**sp_trace_xx**) são estritamente tipados. Se esses parâmetros não forem chamados pelos tipos de dados com parâmetros de entrada corretos, como especificado na descrição do argumento, o procedimento armazenado retornará um erro.  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter a permissão ALTER TRACE.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir define três filtros em Rastreamento `1`. O filtros `N'SQLT%'` e o `N'MS%'` funcionam em uma coluna (`AppName`, valor `10`) que usa o operador de comparação "`LIKE`". O filtro `N'joe'` funciona em uma coluna diferente (`UserName`, valor `11`) que usa o operador de comparação "`EQUAL`".  
  
```  
sp_trace_setfilter  1, 10, 0, 6, N'SQLT%';  
sp_trace_setfilter  1, 10, 0, 6, N'MS%';  
sp_trace_setfilter  1, 11, 0, 0, N'joe';  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [Rastreamento do SQL](../../relational-databases/sql-trace/sql-trace.md)  
  
  
