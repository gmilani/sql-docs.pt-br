---
title: Criando um projeto de Analysis Services (tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 784c0401-0358-4117-9c85-4e8220ce71d9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a7fcece285a17e158fcdfe77ef00004afe637541
ms.sourcegitcommit: f5807ced6df55dfa78ccf402217551a7a3b44764
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69494030"
---
# <a name="creating-an-analysis-services-project-basic-data-mining-tutorial"></a>Criando um projeto do Analysis Services (Tutorial de mineração de dados básico)
  Cada projeto do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] define os objetos em um único banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] pode conter muitos tipos diferentes de objetos  
  
-   Modelos multidimensionais (cubos)  
  
-   Estruturas de mineração e modelos de mineração  
  
-   Suporte a objetos como fontes de dados, exibições de fonte de dados, e assemblies personalizados  
  
 Observe que você **não** requer um cubo para executar a mineração de dados. Se você precisar executar a mineração de dados em um cubo existente, deverá adicionar os modelos de mineração de dados ao mesmo projeto usado para criar o cubo. No entanto, para a maioria dos propósitos, você poderá criar seus modelos em fontes de dados relacionais, como um data warehouse, e obter o melhor desempenho se um cubo não estiver envolvido.  
  
 Neste tutorial você usará um data warehouse relacional, [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)], como a fonte de dados. Você implantará todos os seus objetos de mineração de dados em um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] chamado `BasicDataMining`, usado apenas para mineração de dados.  
  
 Por padrão, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa a instância **localhost** para novos projetos. Se você estiver usando uma instância nomeada ou um servidor diferente, primeiro crie e abra o projeto e depois altere o nome da instância.  
  
 Para obter mais informações sobre projetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , consulte [Creating an Analysis Services Project](../analysis-services/lesson-1-1-creating-an-analysis-services-project.md).  
  
### <a name="to-create-an-analysis-services-project"></a>Para criar um Projeto de Analysis Services  
  
1.  Abra o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  No menu **Arquivo** , aponte para **Novo**e selecione **Projeto**.  
  
3.  Verifique se **Projetos do Business Intelligence** está selecionado no painel **Tipos de projeto** .  
  
4.  No painel **Modelos** , selecione **Projeto Multidimensional e de Mineração de Dados do Analysis Services**.  
  
5.  Na caixa **nome** , nomeie o novo projeto `BasicDataMining`.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-instance-where-data-mining-objects-are-stored"></a>Para alterar a instância em que os objetos de mineração de dados estão armazenados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], no menu **Projeto** , selecione **Propriedades**.  
  
2.  No lado esquerdo do painel **Páginas de Propriedades** , sob **Propriedades de Configuração**, clique em **Implantação**.  
  
3.  No lado direito do painel **Páginas de Propriedades** , sob **Destino**, verifique se o nome de **Servidor** é **localhost**. Se você estiver usando uma instância diferente, digite o nome dessa instância. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criando um tutorial de &#40;mineração de dados básico de fonte de dados&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Criar projetos do Analysis Services &#40;SSDT&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/build-analysis-services-projects-ssdt)   
 [Criar um projeto do Analysis Services &#40;SSDT&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt)  
  
  
