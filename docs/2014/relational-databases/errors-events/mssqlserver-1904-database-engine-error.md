---
title: MSSQLSERVER_1904 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1904 (Database Engine error)
ms.assetid: 2a35d57d-74e2-45a2-8f67-3f2e51d69712
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 119ff7b3bb46e0ea05f1e3cbe87f497132468713
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62869367"
---
# <a name="mssqlserver1904"></a>MSSQLSERVER_1904
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1904|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|KEYCOUNT|  
|Texto da mensagem|O %S_MSG '%.*ls' na tabela '%.\*ls' tem %d nomes de coluna na lista de chaves %S_MSG. O limite máximo para lista de colunas de chaves de índice ou de estatísticas é de %d.|  
  
## <a name="explanation"></a>Explicação  
 A lista de colunas de chaves do índice ou das estatísticas especificadas excede o número máximo de colunas permitidas.  
  
## <a name="user-action"></a>Ação do usuário  
 Modifique a lista de colunas de chaves para incluir não mais do que o número máximo de colunas especificado.  
  
 Para índices não clusterizados, considere a possibilidade de usar a cláusula INCLUDE na instrução CREATE INDEX para adicionar colunas ao índice como colunas não chave. Com esse método, você evita exceder o limite atual de tamanho de índice, que é de até 16 colunas de chave. Para obter mais informações, consulte [Create Indexes with Included Columns](../indexes/create-indexes-with-included-columns.md).  
  
## <a name="see-also"></a>Consulte também  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)  
  
  
