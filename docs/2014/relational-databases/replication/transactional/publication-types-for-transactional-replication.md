---
title: Tipos de publicação para a replicação transacional | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transactional replication, publications
ms.assetid: ad66aa34-3e37-401e-a6a1-fc1514eb6d50
caps.latest.revision: 31
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 11e9e6ffafe62c66684470b4b04e2e0b67cc868b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008137"
---
# <a name="publication-types-for-transactional-replication"></a>Tipos de publicação para Replicação Transacional
  A Replicação Transacional oferece três tipos de publicação:  
  
|Tipo de Publicação|Description|  
|----------------------|-----------------|  
|Publicação Transacional padrão|Apropriada para topologias em que todos os dados do Assinante são do modo somente leitura (a replicação transacional não impõe isto no Assinante).<br /><br /> As publicações transacionais padrão são criadas por padrão ao usar Transact-SQL ou RMO (Replication Management Objects). Ao usar o Assistente para Nova Publicação, elas são criadas selecionando **Publicação Transacional** na página **Tipo de Publicação** .<br /><br /> Para obter mais informações sobre como criar publicações, veja [Publicar dados e objetos de banco de dados](../publish/publish-data-and-database-objects.md).|  
|Publicação Transacional em uma topologia ponto a ponto|As características deste tipo de publicação são:<br /><br /> Cada local tem dados idênticos e atua como um Publicador e Assinante.<br /><br /> A mesma linha pode ser alterada apenas em um local de cada vez.<br /><br /> Esta topologia é melhor adequada para ambientes de servidor que requerem alta disponibilidade e escalabilidade de leitura.<br /><br /> <br /><br /> Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](peer-to-peer-transactional-replication.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação transacional](transactional-replication.md)  
  
  