---
title: Anexar dicas de consulta a um guia de plano | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 2131f796-6359-4f9e-9047-da0b3d4dedaf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 89af21c2c591db2dff678be7aaf8c064e728b9ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151070"
---
# <a name="attach-query-hints-to-a-plan-guide"></a>Anexar dicas de consulta para um guia de plano
  Pode ser usada qualquer combinação de dicas de consulta válidas em um guia de plano. Quando um guia de plano corresponde a uma consulta, a cláusula OPTION especificada na cláusula de dicas de um guia de plano é adicionada à consulta antes da compilação e otimização. Se uma consulta que está de acordo com um guia de plano já tem uma cláusula de OPTION, as dicas especificadas no guia substituem aquelas na consulta. Porém, para que um guia de plano corresponda a uma consulta que já tenha uma cláusula OPTION, deve-se incluir a cláusula OPTION da consulta ao especificar o texto da consulta, para que corresponda à instrução sp_create_plan_guide. Se você quiser que as dicas especificadas no guia de plano sejam adicionadas às dicas que já existem na consulta, em vez de substituí-las, é necessário especificar tanto as dicas originais como as dicas adicionais na cláusula OPTION do guia de plano.  
  
> [!CAUTION]  
>  Guias de plano que usam dicas de consulta de forma indevida podem causar problemas de compilação, execução ou de desempenho. Guias de plano devem ser usados apenas por desenvolvedores e administradores de banco de dados experientes.  
  
## <a name="common-query-hints-used-in-plan-guides"></a>Consulta de dicas comuns usadas nos guias de plano  
 As consultas que podem ser beneficiadas pelos guias de plano, geralmente, têm base em parâmetros podem ser realizadas de modo mais fraco porque usam planos de consulta em cache, cujos valores de parâmetro não representam um cenário de casos graves ou um mais representativos. As dicas de consulta de OPTIMIZE FOR e RECOMPILE podem ser usadas para tratar deste problema. OPTIMIZE FOR instrui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usar um valor particular para um parâmetro quando a consulta é aperfeiçoada. RECOMPILE instrui o servidor para descartar um plano de consulta após a execução, forçando o otimizador de consulta a recompilar um novo plano da próxima vez que a mesma consulta for executada. Para obter um exemplo, consulte [Guias de plano](plan-guides.md).  
  
 Além disso, é possível especificar as dicas de tabela INDEX, FORCESCAN e FORCESEEK como dicas de consulta. Quando especificadas como dicas de consulta, elas se comportam da mesma forma que uma tabela embutida ou dica de exibição. A dica INDEX força o otimizador de consulta a usar somente os índices especificados para acessar os dados na tabela ou exibição referenciada na consulta. A dica FORCESEEK força o otimizador a usar somente uma operação de busca de índice para acessar os dados na tabela ou exibição referenciada. Essas dicas fornecem funcionalidade de guia de plano adicional e permitem uma maior influência em relação à otimização de consultas que usam o guia de plano.  
  
  
