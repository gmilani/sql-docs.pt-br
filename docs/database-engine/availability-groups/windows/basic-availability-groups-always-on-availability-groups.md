---
title: Grupos de disponibilidade básicos para um banco de dados individual
description: 'Descreve as diferenças entre um Grupo de Disponibilidade AlwaysOn normal e básico, bem como a configuração de um grupo de disponibilidade básico. '
ms.custom: seodec18
ms.date: 02/01/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 285adbc7-ac9b-40f6-b4a9-3f1591d3b632
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 46630e36db03d55c8e90be64570975e42466fbba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67991363"
---
# <a name="basic-always-on-availability-groups-for-a-single-database"></a>Grupos de Disponibilidade AlwaysOn básicos para um banco de dados individual
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Grupos de disponibilidade AlwaysOn da camada BASIC fornecem uma solução de alta disponibilidade para o SQL Server 2016 e o SQL Server 2017 Standard Edition. Um grupo de disponibilidade básica oferece suporte a um ambiente de failover para um único banco de dados. Ele é criado e gerenciado de forma muito semelhante aos [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md) tradicionais (avançados) com Enterprise Edition. As diferenças e limitações dos grupos de disponibilidade básica são resumidas neste documento.  
  
## <a name="features"></a>Recursos  
 Grupos de disponibilidade básicos AlwaysOn substituem o recurso de espelhamento de banco de dados preterido e fornece um nível semelhante de suporte ao recurso. Grupos de disponibilidade básica permitem que um banco de dados primário mantenha uma única réplica. Esta réplica pode usar o modo de confirmação síncrona ou modo de confirmação assíncrona. Para obter mais informações sobre modos de disponibilidade, veja [Modos de disponibilidade &#40;Grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md). A réplica secundária permanece inativa, a menos que haja uma necessidade de failover. Esse failover inverte as atribuições de função primária e secundária, fazendo com que a réplica secundária se torne o banco de dados primário ativo. Para obter mais informações sobre failover, veja [Failover e modos de failover &#40;grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md). Grupos de disponibilidade básica podem operar em um ambiente híbrido que abrange o local e o Microsoft Azure.  
  
## <a name="limitations"></a>Limitações  
 Grupos de disponibilidade básica usam um subconjunto de recursos em comparação com grupos de disponibilidade avançada no SQL Server 2016 Enterprise Edition. Grupos de disponibilidade básica incluem as seguintes limitações:  
  
- Limite de duas réplicas (primárias e secundárias). Os grupos de disponibilidade básicos para o SQL Server 2017 no Linux só são compatíveis com uma réplica de configuração adicional.
  
- Sem acesso de leitura na réplica secundária.  
  
- Sem backups na réplica secundária.  

- Sem verificações de integridade em réplicas secundárias. 

- Não há suporte para réplicas hospedadas em servidores que executam uma versão do SQL Server anterior ao SQL Server 2016 Community Technology Preview 3 (CTP3).  

- Suporte para um banco de dados de disponibilidade.  
  
- Grupos de disponibilidade básica não podem ser atualizados para grupos de disponibilidade avançada. O grupo deve ser removido e adicionado novamente a um grupo que contém servidores que executam somente o SQL Server 2016 Enterprise Edition.  
  
- Grupos de disponibilidade básica só têm suporte para servidores do Standard Edition. 

- Grupos de disponibilidade básicos não podem fazer parte de um grupo de disponibilidade distribuído. 
  
## <a name="configuration"></a>Configuração  
 Um grupo de disponibilidade básico AlwaysOn pode ser criado em quaisquer dois servidores SQL Server 2016 Standard Edition. Quando você cria um grupo de disponibilidade básica, deve especificar ambas as réplicas durante a criação.  
  
 Para criar um grupo de disponibilidade básica, use o comando Transact-SQL **CREATE AVAILABILITY GROUP** e especifique a opção **WITH BASIC** (o padrão é **ADVANCED**). Começando na versão 17.8, você também pode criar o grupo de disponibilidade básico usando a interface do usuário no SQL Server Management Studio. Para obter mais informações, veja [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md). 
  
> [!NOTE]  
>  As limitações dos grupos de disponibilidade básica aplicam-se ao comando **CREATE AVAILABILITY GROUP** quando **WITH BASIC** é especificado. Por exemplo, você obterá um erro se tentar criar um grupo de disponibilidade básica que permite acesso de leitura. Outras limitações aplicam-se da mesma maneira. Consulte a seção Limitações deste tópico para obter detalhes.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
