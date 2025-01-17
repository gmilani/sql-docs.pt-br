---
title: Editar uma entidade
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], changing name
ms.assetid: 6a5b9f14-6dfc-49d7-a771-e96461d4feae
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 4329f618b812bb566d974c5434ef0362b1383f2d
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729293"
---
# <a name="edit-an-entity-master-data-services"></a>Editar uma entidade (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode editar uma entidade.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-edit-an-entity"></a>Para editar uma entidade  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciar Modelo** , selecione um modelo na grade e clique em **Entidades**.  
  
3.  Na página **Gerenciar Entidade** , na grade, selecione a linha para a entidade que você deseja editar e clique em **Editar**.  
  
4.  Na caixa **Nome** , digite o nome atualizado da entidade.  
  
5.  No campo **Descrição** , digite a descrição atualizada da entidade.  
  
6.  Na caixa **Nome para tabelas de preparo** , digite um nome atualizado para a tabela de preparo.  
  
7.  No campo **Tipo de Log de Transações**, escolha o tipo de log de transações atualizado na lista suspensa.  
  
     Para obter mais informações, consulte [Alterar o tipo de log de transações da entidade &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
8.  Marque ou desmarque a caixa de seleção **Criar valores de códigos automaticamente** .  
  
     Para obter mais informações, consulte [Criação automática de código &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)  
  
9. Marque ou desmarque a caixa de seleção **Habilitar a compactação de dados** . A compactação de linha é ativada por padrão.  
  
     Para obter mais informações, consulte [Data Compression](../relational-databases/data-compression/data-compression.md).  
  
## <a name="status"></a>Status  
 A coluna de status na grade mostra o status da operação na entidade. Quando você clica em **Salvar entidade**, a imagem a seguir é exibida, indicando que a entidade está atualizando.  
  
 ![Ícone para atualizar o status](../master-data-services/media/mds-statusicon-updating.png "Ícone para atualizar o status")  
  
 Se houver erros ao criar ou editar uma entidade, a imagem a seguir será exibida.  
  
 ![Ícone para status de erro](../master-data-services/media/mds-statusicon-error.png "Ícone para status de erro")  
  
 Quando o status for OK, a imagem a seguir será exibida.  
  
 ![Ícone para status OK](../master-data-services/media/mds-statusicon-ok.png "Ícone para status OK")  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquias explícitas &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [Excluir uma entidade &#40;Master Data Services&#41;](../master-data-services/delete-an-entity-master-data-services.md)   
 [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  
