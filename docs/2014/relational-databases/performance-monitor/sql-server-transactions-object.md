---
title: SQL Server, objeto Transações| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Transactions
- Transactions object
ms.assetid: 85240267-78fd-476a-9ef6-010d6cf32dd8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c7dffaac161a61496c296ec99ec1f9ad2e1951a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63182995"
---
# <a name="sql-server-transactions-object"></a>SQL Server, objeto Transactions
  O objeto **Transactions** no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece contadores para monitorar o número de transações ativas em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], e os efeitos dessas transações em recursos como o repositório de versões de linhas de isolamento de instantâneo em **tempdb**. As transações são unidades de trabalho lógicas; um conjunto de operações que devem ter êxito ou ser apagadas de um banco de dados para manter a integridade lógica dos dados. Todas as modificações de dados nos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são feitas em transações.  
  
 Quando um banco de dados é definido para permitir o nível de isolamento do instantâneo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve manter um registro das modificações feitas para cada linha em um banco de dados. Sempre que uma linha é modificada, uma cópia dela, como estava antes das modificações, é registrada em um repositório de versão de linha em **tempdb**. Muitos dos contadores no objeto **Transactions** podem ser utilizados para monitorar o tamanho e a taxa de crescimento do repositório de versão de linha em **tempdb**.  
  
 Os contadores do objeto **Transactions** reportam todas as transações em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Esta tabela descreve os contadores **SQLServer:Transactions** .  
  
|Contadores de transações do SQL Server|Descrição|  
|--------------------------------------|-----------------|  
|**Espaço livre em tempdb (KB)**|A quantidade de espaço (em quilobytes) disponível em **tempdb**. Deve haver espaço livre suficiente para manter o repositório de versão de nível de isolamento do instantâneo e todos os novos objetos temporários criados nesta instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|**Tempo de execução da transação mais longa**|A quantidade de tempo (em segundos) desde o início da transação que está ativada por mais tempo que qualquer outra transação atual. Este contador somente mostra a atividade quando o banco de dados está no nível de isolamento do instantâneo de leitura confirmada. Ele não registra nenhuma atividade se o banco de dados estiver em qualquer outro nível de isolamento.|  
|**Transações da versão de não instantâneo**|O número de transações atualmente ativas que não estão usando o nível de isolamento do instantâneo e que fizeram modificações de dados que geraram versões de linhas no armazenamento de versão de **tempdb** .|  
|**Transações de instantâneo**|O número de transações atualmente ativas que usam o nível de isolamento do instantâneo.<br /><br /> Observação: O contador do objeto **Transações de Instantâneo** responde quando ocorre o primeiro acesso a dados, não quando a instrução `BEGIN TRANSACTION` é emitida.|  
|**Transactions**|O número de transações atualmente ativas de todos os tipos.|  
|**Taxa de conflito de atualização**|A porcentagem dessas transações que usam o nível de isolamento do instantâneo que encontrou conflitos de atualização no último segundo. Um conflito de atualização ocorre quando uma transação de nível de isolamento do instantâneo tenta modificar uma linha que foi modificada pela última vez por outra transação que não estava confirmada quando a transação de nível de isolamento do instantâneo foi iniciada.|  
|**Transações de instantâneo de atualização**|O número de transações atualmente ativas que usam o nível de isolamento do instantâneo e que modificaram dados.|  
|**Taxa de limpeza de versão (KB/s)**|A taxa (em quilobytes por segundo) na qual as versões de linha são removidas do repositório de versão de isolamento de instantâneo em **tempdb**.|  
|**Taxa de geração de versão (KB/s)**|A taxa (em quilobytes por segundo) na qual novas versões de linha são adicionadas ao repositório de versão de isolamento de instantâneo em **tempdb**.|  
|**Tamanho do repositório de versão (KB)**|A quantidade de espaço (em quilobyte) em **tempdb** usada para armazenar versões de linha de nível de isolamento do instantâneo.|  
|**Contagem de unidade de repositório de versão**|O número de unidades de alocação ativas no repositório de versão de isolamento de instantâneo em **tempdb**.|  
|**Criação de unidade de repositório de versão**|O número de unidades de alocação criadas no repositório de isolamento de instantâneo desde que a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] foi iniciada.|  
|**Truncamento de unidade de repositório de versão**|O número de unidades de alocação removidas do repositório de isolamento de instantâneo desde que a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] foi iniciada.|  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
