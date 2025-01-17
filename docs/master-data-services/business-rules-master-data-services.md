---
title: Regras de negócio
ms.custom: ''
ms.date: 03/18/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], about business rules
- business rules [Master Data Services]
ms.assetid: a9f9e41a-2461-4845-b947-58b3a205543f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1c66914b4b661ea3485ae0354c267e7682f5a6a2
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728694"
---
# <a name="business-rules-master-data-services"></a>Regras de negócio (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], uma regra de negócio é uma regra usada para garantir a qualidade e a exatidão de seus dados mestres. Você pode usar uma regra de negócio para atualizar dados automaticamente, enviar email ou iniciar um processo empresarial ou fluxo de trabalho.  
  
 Para exibir exemplos de regras de negócios, consulte [Exemplos de regras de negócios &#40;Master Data Services&#41;](../master-data-services/business-rule-examples-master-data-services.md).  
  
## <a name="create-and-publish-business-rules"></a>Criar e publicar uma regra de negócio  
 Regras de negócio são instruções **If/Then/Else** criadas no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. Se um valor de atributo corresponder a uma condição especificada, uma ação será executada, caso contrário a ação Else é executada. As possíveis ações incluem a definição de um valor padrão ou a alteração de um valor. Estas ações podem ser combinadas com enviar uma notificação de email.  
  
 Regras de negócios podem ser baseadas em valores de atributo específicos (por exemplo, realizar ação se Cor=Azul), ou quando os valores de atributo são alterados (por exemplo, realizar ação se o valor do atributo de cor for alterado). Para obter mais informações sobre acompanhamento de alterações não específicas, consulte [Controle de alterações &#40;Master Data Services&#41;](../master-data-services/change-tracking-master-data-services.md).  
  
 Para usar regras de negócio, você deve primeiramente criar e publicar suas regras e depois aplicar as regras publicadas aos dados. As regras podem ser aplicadas a subconjuntos de dados ou a todos os dados de uma versão por meio da validação da versão. Uma versão não pode ser confirmada até que todos os atributos sejam submetidos com êxito à validação de regras de negócio.  
  
 Se um usuário tentar adicionar um valor de atributo que não é aprovado na validação da regra de negócios, esse valor ainda poderá ser salvo. Você pode revisar e corrigir problemas de validação, que são exibidos no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
 Ao criar um pacote de implantação de modelo, se quiser incluir regras de negócio, você deverá incluir dados da versão no pacote.  
  
 Se criar uma regra de negócio que usa o operador **OR** , você deverá criar uma regra separada para cada instrução condicional que possa ser avaliada independentemente. É possível excluir regras conforme necessário, para garantir mais flexibilidade e uma solução de problemas mais fácil.  
  
## <a name="how-business-rules-are-applied"></a>Como são aplicadas regras de negócio  
 Você pode definir a ordem de prioridade para executar as regras movendo as regras de negócio para cima e para baixo. No entanto, antes de a prioridade ser levada em conta, são aplicadas regras de negócio com base no tipo de ação que a regra adota. A ordem é a seguinte:  
  
1.  **Valor padrão**  
  
2.  **Alterar valor**  
  
3.  **Validação**  
  
4.  **Ação externa**  
  
5.  **Ação de Script Definido pelo Usuário**  
  
 Nesses grupos, as ações são aplicadas na ordem de prioridade, da mais baixa para a mais alta. Assim, por exemplo, quatro regras separadas podem ter ações de **Valor Padrão** . A ação de **Valor Padrão** que ocorre primeiro depende da ordem de prioridade especificada na interface de usuário da Web.  
  
 Outras observações importantes sobre como aplicar regras:  
  
-   Se uma regra de negócio for excluída ou não for publicada com status **Ativo**, ela ainda estará disponível, mas não será incluída quando as regras de negócio forem aplicadas.  
  
-   As regras de negócio se aplicam aos valores de atributos para todos os membros da folha ou todos os membros consolidados, não ambos.  
  
-   As regras de negócio podem ser aplicadas a qualquer versão de um modelo que esteja **Aberto** ou **Bloqueado**.  
  
-   Alterações feitas a dados quando regras de negócio são aplicadas não são registradas em log como transações.  
  
-   Uma regra de negócios não pode conter mais de uma ação **start workflow** .  
  
## <a name="system-settings"></a>Configurações do sistema  
 Há duas configurações no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] que afetam as regras de negócio. Você pode ajustar essas configurações no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] ou diretamente na tabela Configurações do Sistema. Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar e publicar uma nova regra de negócio.|[Criar e publicar uma regra de negócio &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|Adicionar várias condições a uma regra de negócio.|[Adicionar várias condições a uma regra de negócios &#40;Master Data Services&#41;](../master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)|  
|Criar uma regra de negócio para exigir que os atributos tenham valores.|[Exigir valores de atributos &#40;Master Data Services&#41;](../master-data-services/require-attribute-values-master-data-services.md)|  
|Criar uma regra de negócio para tomar uma ação com base nas alterações para atribuir valores.|[Iniciar ações com base em alterações no valor do atributo &#40;Master Data Services&#41;](../master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)|  
|Criar uma regra de negócio para tirar o script definido pelo usuário como uma condição|[Extensão das Regras de Negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-extension-master-data-services.md)|  
|Criar uma regra de negócio para tirar o script definido pelo usuário como uma ação|[Extensão das Regras de Negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-extension-master-data-services.md)|  
|Alterar o nome de uma regra de negócio existente.|[Alterar o nome de uma regra de negócios &#40;Master Data Services&#41;](../master-data-services/change-a-business-rule-name-master-data-services.md)|  
|Configure o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para enviar notificações quando as regras de negócio forem aplicadas.|[Configurar regras de negócio para enviar notificações &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
|Aplicar regras de negócio a membros específicos.|[Validar membros específicos em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)|  
|Excluir uma regra de negócio para que ela não seja usada.|[Excluir uma regra de negócios &#40;Master Data Services&#41;](../master-data-services/exclude-a-business-rule-master-data-services.md)|  
|Excluir uma regra de negócio existente.|[Excluir uma regra de negócios &#40;Master Data Services&#41;](../master-data-services/delete-a-business-rule-master-data-services.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Visão geral do Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
-   [Versões &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)  
  
-   [Validação &#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md)  
  
-   [Controle de alterações &#40;Master Data Services&#41;](../master-data-services/change-tracking-master-data-services.md)  
  
  
