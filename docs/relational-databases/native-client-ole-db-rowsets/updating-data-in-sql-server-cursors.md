---
title: Atualizando dados em cursores SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
ms.assetid: 732dafee-f2d5-4aef-aad7-3a8bf3b1e876
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: befedbeedfad8fcdb7f542d23a7dd1a3854d700f
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73788796"
---
# <a name="updating-data-in-sql-server-cursors"></a>Atualizando dados em cursores do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Ao buscar e atualizar dados por meio de cursores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um aplicativo consumidor OLE DB provedor de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo é associado pelas mesmas considerações e restrições que se aplicam a qualquer outro aplicativo cliente.  
  
 Apenas as linhas em cursores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] participam do controle de acesso a dados simultâneo. Quando o consumidor solicita um conjunto de linhas modificável, o controle de simultaneidade é controlado por DBPROP_LOCKMODE. Para modificar o nível do controle de acesso simultâneo, o consumidor define a propriedade DBPROP_LOCKMODE antes de abrir o conjunto de linhas.  
  
 Os níveis de isolamento da transação podem gerar defasagens significativas no posicionamento de linhas, se o design do aplicativo cliente permitir que as transações permaneçam abertas por longos períodos. Por padrão, o provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo do cliente usa o nível de isolamento de leitura confirmada especificado por DBPROPVAL_TI_READCOMMITTED. O provedor de OLE DB de cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte ao isolamento de leitura sujo quando a simultaneidade do conjunto de linhas é somente leitura. Assim, o consumidor pode solicitar um nível mais alto de isolamento em um conjunto de linhas modificável, mas não pode solicitar nenhum nível inferior com êxito.  
  
## <a name="immediate-and-delayed-update-modes"></a>Modos de atualização imediatos e atrasados  
 No modo de atualização imediato, cada chamada a **IRowsetChange::SetData** causa uma viagem de ida e volta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o consumidor fizer várias alterações em uma única linha, será mais eficiente enviar todas as alterações com uma única chamada de **SetData**.  
  
 No modo de atualização atrasada, uma viagem de ida e volta é feita ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada linha indicada nos parâmetros *cRows* e *rghRows* de **IRowsetUpdate::Update**.  
  
 Em qualquer modo, uma viagem de ida e volta representará uma transação distinta quando nenhum objeto de transação estiver aberto para o conjunto de linhas.  
  
 Quando você estiver usando **IRowsetUpdate:: Update**, o provedor de OLE DB do cliente nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentará processar cada linha indicada. Um erro ocorrido devido a dados inválidos, comprimento ou valores de status para qualquer linha não interrompe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processamento de provedor de OLE DB de cliente nativo. É possível modificar todas ou nenhuma das outras linhas que participam da atualização. O consumidor deve examinar a matriz *prgRowstatus* retornada para determinar a falha de qualquer linha específica quando o provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo retorna DB_S_ERRORSOCCURRED.  
  
 Um consumidor não deve presumir que as linhas são processadas em qualquer ordem específica. Se um consumidor solicitar o processamento ordenado da modificação de dados em mais de uma única linha, ele deverá estabelecer essa ordem na lógica do aplicativo e abrir uma transação para conter o processo.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizando dados em conjuntos de linhas](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
