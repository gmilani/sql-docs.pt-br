---
title: Alterar o tipo de log de transações da entidade.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 75250b32-3384-43c2-9b5c-1607cc3aa7b3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: fde8e314462846088c7c673524d6e6d8d29ee631
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729668"
---
# <a name="change-the-entity-transaction-log-type-master-data-services"></a>Alterar o Tipo de Log de Transações de Entidade (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Você pode alterar o tipo de log de transações de uma entidade para atributo, membro ou nenhum.  
  
|Tipo de Log de transações|Descrição|  
|--------------------------|-----------------|  
|Atributo|Os logs de alteração de entidades são salvos no nível do atributo.<br /><br /> O log de transações é salvo, assim como para o [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].|  
|Membro|Os logs de alteração de entidades são salvos no nível de linha.<br /><br /> Qualquer alteração de atributo dispara uma nova revisão de linha.<br /><br /> Ao usar o tipo de log de transações de linha, a entidade será armazenada como uma dimensão de alteração lenta do Tipo 4. A exibição de assinatura do Tipo 2 e a exibição de assinatura (histórico) do Tipo 4 têm suporte. Para obter mais informações, consulte [Formatos de exibição de assinatura &#40;Master Data Services&#41;](../master-data-services/subscription-view-formats-master-data-services.md)<br /><br /> Oferece um melhor desempenho.|  
|Nenhuma|Nenhum log de alteração é salvo.<br /><br /> Fornece o melhor desempenho.|  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional Administração do Sistema. Para obter mais informações, consulte [Permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   A entidade deve existir. Para obter mais informações, consulte [Criar uma entidade &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
 **Para alterar o tipo de log de transações**  
  
1.  No Master Data Manager, clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciar Modelo** , selecione a linha do modelo da entidade que você deseja editar e clique em **Entidades**.  
  
3.  Na página **Gerenciar Entidade** , selecione a linha da entidade que deseja atualizar e clique em **Editar**.  
  
4.  Escolha o tipo de log de transações na lista suspensa.  
  
5.  Clique em **Salvar**.  
  
  
