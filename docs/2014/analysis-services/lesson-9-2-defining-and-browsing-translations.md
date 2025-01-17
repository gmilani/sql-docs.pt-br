---
title: Definindo e pesquisando traduções | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0e60be99-3768-499c-a22c-a4ec37e61887
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9a254f685f83e97b14c78c7d6c4c21e2737b636
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "69493785"
---
# <a name="defining-and-browsing-translations"></a>Definindo e pesquisando traduções
  Uma tradução é uma representação dos nomes de objetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em uma linguagem específica. Os objetos incluem grupos de medidas, medidas, dimensões, atributos, hierarquias, KPIs, ações e membros calculados. As traduções fornecem suporte ao servidor para aplicativos cliente que podem dar suporte a vários idiomas. Como cliente, basta passar o identificador de localidade (LCID) para a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], que usa o LCID para determinar qual conjunto de traduções deverá ser usado quando ele fornecer metadados para os objetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Se um objeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não tiver uma tradução para o idioma ou para um objeto específico, o idioma padrão será usado para retornar o metadados do objeto ao cliente. Por exemplo, se um usuário comercial na França acessar um cubo de uma estação de trabalho que tenha uma configuração de localidade francesa, o usuário comercial verá as legendas dos membros e os valores de Propriedade do membro em francês, se existir uma tradução em francês. No entanto, se um usuário comercial na Alemanha acessar o mesmo cubo de uma estação de trabalho que tenha uma configuração de localidade alemã, o usuário comercial verá os nomes de legendas e os valores de propriedade de membro em alemão. Para obter mais informações, consulte traduções de [dimensões](multidimensional-models-olap-logical-dimension-objects/dimension-translations.md), conversões de [cubo](multidimensional-models-olap-logical-cube-objects/cube-translations.md), [traduções &#40;Analysis Services&#41;](translations-analysis-services.md).  
  
 Nas tarefas deste tópico, você define as traduções de metadados para um conjunto limitado de objetos de dimensões na dimensão Data e objetos de cubo no cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Em seguida, você procurará esses objetos de dimensão e cubo para examinar as traduções de metadados.  
  
## <a name="specifying-translations-for-the-date-dimension-metadata"></a>Especificando traduções para os metadados de dimensão de data  
  
1.  Abra o Designer de Dimensão na dimensão **Data** e clique na guia **Traduções**.  
  
     Os metadados no idioma padrão para cada objeto de dimensão são exibidos. O idioma padrão no cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] é o inglês.  
  
2.  Na barra de ferramentas da guia **Traduções**, clique no botão **Nova Tradução**.  
  
     Uma lista de idiomas é exibida na caixa de diálogo **Selecionar Idioma**.  
  
3.  Clique em **Espanhol (Espanha)** e em **OK**.  
  
     Uma nova coluna é exibida, na qual você definirá as traduções do espanhol para os objetos de metadados que deseja traduzir. Neste tutorial, só converteremos alguns objetos para ilustrar o processo.  
  
4.  Na barra de ferramentas da guia **Traduções**, clique no botão **Nova Tradução**, clique em **Francês (França)** na caixa de diálogo **Selecionar Idioma** e clique em **OK**.  
  
     Outra coluna de idioma é exibida na qual você definirá traduções francesas.  
  
5.  Na linha do objeto de **legenda** da dimensão **data** , digite `Fecha` na coluna de tradução para **espanhol (Espanha)** e `Temps` na coluna de tradução **francês (França)** .  
  
6.  Na linha do objeto de **legenda** do atributo **nome do mês** , digite `Mes del Año` na coluna de tradução do **espanhol (Espanha)** e `Mois d'Année` na coluna de tradução **francês (França)** .  
  
     Observe que quando você insere essas traduções, uma reticências ( **...** ) é exibida. Clicar nesta elipse permitirá que você especifique uma coluna na tabela subjacente que fornece traduções para cada membro da hierarquia de atributo.  
  
7.  Clique nas reticências ( **...** ) para a tradução **espanhola (Espanha)** do atributo **nome do mês** .  
  
     A caixa de diálogo **Tradução de Dados de Atributo** é exibida.  
  
8.  Na lista **Colunas de tradução**, selecione **SpanishMonthName**, conforme mostrado na imagem a seguir.  
  
     ![Caixa de diálogo conversão de dados de atributo](../../2014/tutorials/media/l9-translations-4.gif "Caixa de diálogo conversão de dados de atributo")  
  
9. Clique em **OK**e, em seguida, clique nas reticências ( **...** ) da tradução **francês (França)** do atributo **nome do mês** .  
  
10. Na lista **Colunas de tradução**, selecione **FrenchMonthName** e clique em **OK**.  
  
     As etapas neste procedimento ilustram o processo de definição de conversões de metadados para objetos de dimensão e membros.  
  
## <a name="specifying-translations-for-the-analysis-services-tutorial-cube-metadata"></a>Especificando traduções para os metadados do cubo de Analysis Services tutorial  
  
1.  Alterne para o Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e mude para a guia **Traduções**.  
  
     Os metadados no idioma padrão para cada objeto de cubo são exibidos, conforme mostrado na imagem a seguir. O idioma padrão no cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] é o inglês.  
  
     ![Idioma padrão na guia Traduções](../../2014/tutorials/media/l9-translations-5.gif "Idioma padrão na guia Traduções")  
  
2.  Na barra de ferramentas da guia **Traduções**, clique no botão **Nova Tradução**.  
  
     Uma lista de idiomas é exibida na caixa de diálogo **Selecionar Idioma**.  
  
3.  Selecione **Espanhol (Espanha)** e clique em **OK**.  
  
     Uma nova coluna é exibida, na qual você definirá as traduções do espanhol para os objetos de metadados que deseja traduzir. Neste tutorial, só converteremos alguns objetos para ilustrar o processo.  
  
4.  Na barra de ferramentas da guia **Traduções**, clique no botão **Nova Tradução**, selecione **Francês (França)** na caixa de diálogo **Selecionar Idioma** e clique em **OK**.  
  
     Outra coluna de idioma é exibida na qual você definirá traduções francesas.  
  
5.  Na linha do objeto de **legenda** da dimensão **data** , digite `Fecha` na coluna de tradução para **espanhol (Espanha)** e `Temps` na coluna de tradução **francês (França)** .  
  
6.  Na linha do objeto de **legenda** do grupo de medidas **vendas pela Internet** , digite `Ventas del lnternet` na coluna de tradução para **espanhol (Espanha)** e `Ventes D'Internet` na coluna de tradução **francês (França)** .  
  
7.  Na linha do objeto de **legenda** da medida Vendas pela Internet – valor das vendas, digite `Cantidad de las Ventas del Internet` na coluna de tradução **espanhol (espanha)** e `Quantité de Ventes d'Internet` na coluna de tradução **francês (França)** .  
  
     As etapas neste procedimento ilustram o processo de definição de conversões de metadados para objetos de cubo.  
  
## <a name="browsing-the-cube-by-using-translations"></a>Navegando no cubo usando traduções  
  
1.  No menu **Compilar** , clique em **implantar Analysis Services tutorial**.  
  
2.  Quando a implantação for concluída com êxito, mude para a guia **Navegador** e clique em **Reconectar**.  
  
3.  Remova todas as hierarquias e medidas do painel **Dados** e selecione Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] na lista **Perspectivas**.  
  
4.  No painel de metadados, expanda **Medidas** e **Vendas pela Internet**.  
  
     Observe que a medida **Vendas pela Internet/Valor das Vendas** é exibida em inglês (Internet Sales-Sales Amount) neste grupo de medidas.  
  
5.  Na barra de ferramentas, selecione **Espanhol (Espanha)** na lista **Idioma**.  
  
     Observe que os itens no painel de metadados são populados novamente. Depois que os itens no painel de metadados forem populados novamente, observe que a medida Vendas pela Internet – valor das vendas não aparece mais na pasta de exibição vendas pela Internet. Em vez disso, ele aparece em espanhol em uma nova pasta de exibição chamada `Ventas del lnternet`, conforme mostrado na imagem a seguir.  
  
     ![Painel de metadados repreenchidos](../../2014/tutorials/media/l9-translations-6.gif "Painel de metadados repreenchidos")  
  
6.  No painel metadados, clique com o botão direito do mouse em `Cantidad de las Ventas del Internet` e selecione **Adicionar à consulta**.  
  
7.  No painel metadados, expanda `Fecha`, expanda **fecha. Calendar data**, clique com o botão direito do mouse em **fecha. Calendar Date**e, em seguida, selecione **Adicionar ao filtro**.  
  
8.  No painel **Filtro**, selecione **CY 2007** como a expressão de filtro.  
  
9. No painel de metadados, clique com o botão direito do mouse em **Mes del Ano** e selecione **Adicionar à Consulta**.  
  
     Observe que os nomes de mês aparecem em espanhol, conforme mostrado na imagem a seguir.  
  
     ![Nomes de mês em espanhol no painel de dados](../../2014/tutorials/media/l9-translations-7.gif "Nomes de mês em espanhol no painel de dados")  
  
10. Na barra de ferramentas, selecione **Francês (França)** na lista **Idioma**.  
  
     Observe que os nomes de mês agora aparecem em francês e que o nome da medida agora também é exibido em francês.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 10: definindo funções administrativas](lesson-10-defining-administrative-roles.md)  
  
## <a name="see-also"></a>Consulte também  
 [Conversões de dimensão](multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)    
 [Conversões de cubo](multidimensional-models-olap-logical-cube-objects/cube-translations.md)    
 [Traduções &#40;Analysis Services&#41;](translations-analysis-services.md)  
  
  
