---
title: Especificar uma condição de ponto de interrupção | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.breakpt.condition
helpviewer_keywords:
- Transact-SQL debugger, breakpoint conditions
ms.assetid: b43d8a2b-99a3-4fb7-8848-99c042ea7ef7
caps.latest.revision: 6
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c9f8d69cd320009562b81c4b33c0cbd3374f1498
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122586"
---
# <a name="specify-a-breakpoint-condition"></a>Especificar uma condição de ponto de interrupção
  Uma condição de ponto de interrupção é uma expressão [!INCLUDE[tsql](../../includes/tsql-md.md)] que é avaliada pelo depurador ao atingir o ponto de interrupção. Se a condição for atendida e qualquer contagem de ocorrências especificada for atingida, o depurador será interrompido ou executará a ação especificada para o ponto de interrupção.  
  
## <a name="specifying-conditions"></a>Especificando condições  
 A expressão especificada deve ser uma expressão Transact-SQL válida que seja avaliada como um valor Booliano. Para obter mais informações, veja [Expressões &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/expressions-transact-sql).  
  
 Se você especificar uma condição de ponto de interrupção com sintaxe inválida, será exibida uma mensagem de aviso imediatamente. Se você especificar uma condição com sintaxe válida, mas semântica inválidas, será exibida uma mensagem de aviso da primeira vez que o ponto de interrupção for atingido. Em qualquer um dos casos, o depurador interromperá a execução quando o ponto de interrupção inválido for atingido.  
  
#### <a name="to-specify-a-condition"></a>Para especificar uma condição  
  
1.  Na janela do editor, clique com o botão direito do mouse no glifo do ponto de interrupção e clique em **Condição** no menu de atalho.  
  
     -ou-  
  
     Na janela **Pontos de Interrupção** , clique com o botão direito do mouse no glifo do ponto de interrupção e clique em **Condição** no menu de atalho.  
  
2.  Na caixa de diálogo **Condição de Ponto de Interrupção** , insira uma expressão Booliana válida na caixa **Condição** .  
  
3.  Escolha **é verdadeiro** se você deseja interromper quando a expressão é avaliada como `true`, ou escolha **mudou** se você quiser interromper quando o valor da expressão for alterado.  
  
    > [!NOTE]  
    >  O depurador não avalia a expressão Booliana até a primeira vez que o ponto de interrupção é atingido. Se você escolher **Has changed**, o depurador não considerará a primeira avaliação como uma alteração, então o depurador não interromperá na primeira avaliação.  
  
## <a name="see-also"></a>Consulte também  
 [Especificar uma contagem de ocorrências](specify-a-hit-count.md)   
 [Especificar uma ação de ponto de interrupção](specify-a-breakpoint-action.md)  
  
  