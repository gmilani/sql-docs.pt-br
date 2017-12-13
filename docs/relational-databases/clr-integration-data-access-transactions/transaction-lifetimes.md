---
title: "Vidas úteis de transação | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- lifetimes [SQL Server]
- Transact-SQL vs. managed code
ms.assetid: cb076fda-6488-4959-a6a4-7adaccf3f25c
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 445984322c81766be4919cfda8b211a21e2519a0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="transaction-lifetimes"></a>Vidas úteis de transação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Há uma diferença importante entre transações iniciadas nos [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados e aquelas iniciadas no código gerenciado: código common language runtime (CLR) não pode desequilibrar o estado da transação na entrada ou saída de uma invocação CLR. Esteja ciente das seguintes implicações dessa diferença:  
  
-   Uma transação iniciada em um quadro CLR precisa ser confirmada ou revertida ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará um erro quando o quadro for fechado.  
  
-   Uma transação externa não pode ser confirmada ou revertida no código CLR.  
  
-   Uma tentativa de confirmar uma transação não iniciada no mesmo procedimento causa um erro em tempo de execução.  
  
-   Uma tentativa de reverter uma transação não iniciada no mesmo procedimento causa a paralisação da transação (impedindo a ocorrência de qualquer outra operação como efeito colateral). A transação é descontinuada até que o código CLR saia do escopo. Observe que isso pode ser útil quando você detecta um erro em seu procedimento e deseja verificar se a transação inteira é finalizada.  
  
## <a name="see-also"></a>Consulte também  
 [Integração CLR e transações](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  