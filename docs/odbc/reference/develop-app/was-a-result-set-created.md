---
title: Um conjunto de resultados foi criado? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], determining if created
ms.assetid: 4a83b8cb-2d57-4e64-b497-80bd587ee1f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f748e75f4e1579446b72b519356f2f649889fe0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078971"
---
# <a name="was-a-result-set-created"></a>Um conjunto de resultados foi criado?
Na maioria das situações, os programadores de aplicativos saber se as instruções de que seu aplicativo executa criará um conjunto de resultados. Esse é o caso se o aplicativo usa instruções SQL embutido em código escritas pelo programador. Normalmente é o caso quando o aplicativo constrói instruções SQL em tempo de execução: O programador pode incluir facilmente o código que sinaliza se um **selecionar** instrução ou um **inserir** instrução está sendo construída. Em algumas situações, o programador não é possível saber se uma instrução criará um conjunto de resultados. Isso é verdadeiro se o aplicativo fornece uma maneira para o usuário inserir e executar uma instrução SQL. Ele também é verdadeiro quando o aplicativo constrói uma instrução em tempo de execução para executar um procedimento.  
  
 Nesses casos, o aplicativo chama **SQLNumResultCols** para determinar o número de colunas no conjunto de resultados. Se isso for 0, a instrução não tiver criado um conjunto de resultados; Se for qualquer outro número, a instrução tiver criado um conjunto de resultados.  
  
 O aplicativo pode chamar **SQLNumResultCols** a qualquer momento após a instrução estiver preparada ou executada. No entanto, porque algumas fontes de dados não podem facilmente descrevem os conjuntos de resultados que serão criados por instruções preparadas, desempenho sofrerá se **SQLNumResultCols** é chamado depois que uma instrução é preparada, mas antes de ser executado.  
  
 Algumas fontes de dados também dão suporte a determinação do número de linhas que uma instrução SQL retorna em um conjunto de resultados. Para fazer isso, o aplicativo chama **SQLRowCount**. Exatamente o que a contagem de linhas representa é indicado pela configuração da opção SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 ou SQL_STATIC_CURSOR_ATTRIBUTES2 (dependendo do tipo de cursor) retornado por uma chamada para **SQLGetInfo**. Esse bitmask indica para cada tipo de cursor se a contagem de linhas retornada é exato, aproximado, ou não está disponível em todos os. Se contagens de linhas para estática ou cursores controlados por conjunto de chaves são afetados pelas alterações feitas por meio **SQLBulkOperations** ou **SQLSetPos**, ou por atualização posicionada ou instruções delete, depende de outros bits retornado dos mesmos argumentos de opção listados anteriormente. Para obter mais informações, consulte o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.
