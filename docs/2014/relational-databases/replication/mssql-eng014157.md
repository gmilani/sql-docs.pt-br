---
title: MSSQL_ENG014157 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014157 error
ms.assetid: 1a0890cf-d977-43e0-a2ba-9c5ff1a8f856
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: eccf8c32c5e84bd658ef29fc0176f03fd4e77be4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120330"
---
# <a name="mssqleng014157"></a>MSSQL_ENG014157
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14157|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|A assinatura criada pelo Assinante '%s' para a publicação '%s' expirou e foi descartada.|  
  
## <a name="explanation"></a>Explicação  
 Um Assinante deve fazer a sincronização com o Publicador no momento especificado no período de retenção de publicação. Se um Assinante não fizer a sincronização nesse período, a assinatura será expirada. Para obter mais informações, consulte [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md).  
  
## <a name="user-action"></a>Ação do usuário  
 É necessário recriar e inicializar a assinatura para que o Assinante comece a receber novamente as alterações de dados:  
  
-   Para obter mais informações sobre como criar assinaturas, consulte [Assinar publicações](subscribe-to-publications.md).  
  
-   Para obter informações sobre como inicializar assinaturas, consulte [Inicializar uma assinatura](initialize-a-subscription.md).  
  
 Se o banco de dados de assinatura contiver alterações que não foram sincronizadas com o Publicador, será possível usar o [tablediff Utility](../../tools/tablediff-utility.md) para determinar quais linhas são diferentes nos bancos de dados de publicação e de assinatura.  
  
 É possível aumentar o período de retenção de publicação para que a assinatura não expire. Tome cuidado ao definir um valor alto, já que isso pode resultar no armazenamento de mais dados e metadados, o que afeta o desempenho. Para obter mais informações, consulte [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)  
  
  