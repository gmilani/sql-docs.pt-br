---
title: MSSQLSERVER_32044 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 32044 (Database Engine error)
ms.assetid: f2d073be-d9a1-4837-8a38-028d3e3403bd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9c6fd8fceb0ad7f9f724ccfecab8da1c0e34a7f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914153"
---
# <a name="mssqlserver32044"></a>MSSQLSERVER_32044
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|32044|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum32044|  
|Texto da mensagem|O alerta de 'sobrecarga de confirmação de espelho' foi ativado. O valor atual '%d' ultrapassa o limite '%d'.|  
  
## <a name="explanation"></a>Explicação  
 Esse evento de espelhamento de banco de dados é emitido na instância do servidor principal para indicar que o tempo de espera de confirmação de agregação foi alcançado ou excedeu um valor de limite especificado pelo usuário devido ao espelhamento de banco de dados. O tempo de espera é o produto do número de transações e do tempo de cada uma delas. Por exemplo, os dois casos a seguir produzem 1.000 milissegundos de tempo de espera: 1000 transações * 1 milissegundo e 1 transação \* 1000 milissegundos. Um tempo de espera de confirmação aumentado pode ser causado por um surto na contagem de transações, atrasos no envio do log ou atrasos na liberação do log na instância do servidor espelho.  
  
 A quantidade de sobrecarga espelhada confirmada é uma métrica de desempenho que pode ajudar a avaliar o impacto do desempenho atual de operação síncrona. Essa métrica só é relevante no modo de segurança alta. Como o modo de segurança alta é síncrono, a instância do servidor principal espera para confirmar a transação, depois de ter enviado um registro de log para a instância do servidor espelho, até receber a confirmação de que a instância do servidor espelho gravou o registro de log no disco. O registro de log permanece no disco na instância do servidor espelho enquanto ele espera para ser restaurado no banco de dados espelho.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique a causa nas cargas das instâncias do servidor principal e espelho, bem como nas respectivas conexões de rede.  
  
## <a name="see-also"></a>Consulte também  
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Usar os limites de aviso e alertas em métricas de desempenho de espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  
