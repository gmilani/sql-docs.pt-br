---
title: Tipos de Cursor rolável | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 210b66a800670f033508f903b18778f88ddd4c8b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061631"
---
# <a name="scrollable-cursor-types"></a>Tipos de cursor rolável
Os quatro tipos de cursores roláveis são estáticos, dinâmicos, controlados por e misto. Cursores estáticos detectam poucas ou nenhuma alteração, mas são relativamente baratos implementar. Cursores dinâmicos detectam todas as alterações, mas são caros de implementar. Cursores controlados por e mistos se encontra a média, detectando a maioria das alterações, mas, ao menos despesas que cursores dinâmicos.  
  
 Os seguintes termos são usados para definir as características de cada tipo de cursor rolável:  
  
-   **As próprias atualizações, inserções e exclusões.** Atualizações, exclusões e inserções feitas por meio do cursor, seja com uma chamada para **SQLBulkOperations** ou **SQLSetPos** ou com um posicionadas instrução update ou delete.  
  
-   **Outras atualizações, exclusões e inserções.** Atualizações, exclusões e inserções não são feitas pelo cursor, incluindo aquelas feitas por outras operações na mesma transação, aquelas feitas por meio de outras transações e as feitas por outros aplicativos.  
  
-   **Associação.** O conjunto de linhas no conjunto de resultados.  
  
-   **Ordem.** A ordem na qual as linhas são retornadas pelo cursor.  
  
-   **valores.** Os valores em cada linha no conjunto de resultados.  
  
 Para obter informações sobre como atualizar, excluir e inserir dados, consulte [visão geral da atualização de dados](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Cursores estáticos ODBC](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [Cursores dinâmicos ODBC](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [Cursores controlados por conjunto de chaves](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [Cursores mistos](../../../odbc/reference/develop-app/mixed-cursors.md)
