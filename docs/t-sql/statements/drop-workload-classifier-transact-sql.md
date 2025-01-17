---
title: Classificador DROP WORKLOAD (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD CLASSIFIER
- WORKLOAD_CLASSIFIER_TSQL
- DROP_WORKLOAD_CLASSIFIER_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD CLASSIFIER statement
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 5db3c50e4b0a21e2e1acf9512995870b62375dd8
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632839"
---
# <a name="drop-workload-classifier-transact-sql"></a>DROP WORKLOAD CLASSIFIER (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Descarta um classificador de gerenciamento de carga de trabalho definido pelo usuário existente.  Se as solicitações estão em execução ou na fila de solicitação em estado suspenso, elas manterão sua classificação e o classificador poderá ser removido imediatamente. Descartar e recriar o classificador com importância diferente não afetará uma solicitação já classificada.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  

```
DROP WORKLOAD CLASSIFIER classifier_name;
```

## <a name="arguments"></a>Argumentos

*classifier_name*  
Especifique o nome pelo qual o classificador de carga de trabalho é identificado.
  
## <a name="permissions"></a>Permissões

Requer a permissão CONTROL DATABASE.  
  
## <a name="examples"></a>Exemplos

O seguinte exemplo descarta o classificador de carga de trabalho denominado `wgcELTROLE`.  

```sql
DROP WORKLOAD CLASSIFIER wgcELTRole;
```

> [!NOTE]
> Uma solicitação enviada sem um classificador correspondente é classificada para o grupo de carga de trabalho padrão.  O grupo de carga de trabalho padrão é a classe de recurso smallrc.
  
## <a name="see-also"></a>Consulte Também

[CREATE WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-classifier-transact-sql.md)</br>
[Classificação de carga de trabalho do SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
