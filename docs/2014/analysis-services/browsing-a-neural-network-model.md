---
title: Procurando um modelo de rede Neural | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining models, viewing
- mining model, neural network
- neural networks
- dependency network
ms.assetid: e4224cb7-115b-4889-ac07-03f096fb55fc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e4dcb323a309125695df6d3c483f8996d36fdfd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088448"
---
# <a name="browsing-a-neural-network-model"></a>Procurando um modelo de rede neural
  Quando você abre uma rede neural ou modelo de regressão logística usando **Procurar**, o modelo é exibido em um visualizador interativo, semelhante ao visualizador de modelo da rede neural no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. O visualizador ajuda a explorar correlações e obter informações sobre os padrões no modelo e os dados subjacentes.  
  
##  <a name="BKMK_Tabs"></a> Explorar o modelo  
 Os modelos que são baseados na Rede Neural ou os algoritmos de Regressão Logística da [!INCLUDE[msCoName](../includes/msconame-md.md)] são semelhantes porque analisam dados como um conjunto de conexões entre entradas e saídas conhecidas. O visualizador **Procurar** ajuda a explorar essas conexões, usando os seguintes controles:  
  
-   [Variáveis](#BKMK_Variables)  
  
-   [Entradas](#BKMK_Inputs)  
  
-   [Saídas](#BKMK_Outputs)  
  
 Se quiser fazer experiências com esse visualizador, crie um modelo usando o assistente [Assistente de Classificação &#40;Suplementos de Mineração de Dados para Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md) e use a opção **Avançado** para alterar o algoritmo para Regressão Logística da Microsoft na caixa de diálogo **Parâmetros do Algoritmo**.  
  
###  <a name="BKMK_Variables"></a> Variáveis  
 O painel **Variáveis** exibe uma lista de variáveis de entrada pela ordem de seu efeito no modelo. Você usa os controles de **Entrada** e **Saída** para filtrar o modelo, afetando as variáveis que são exibidas, bem como sua ordem.  
  
 Usando esse visualizador, você poderá explorar os fatores que são muito importantes para determinar se um cliente mais provavelmente pertence à categoria Comprador de bicicleta ou não.  
  
 ![Testando o efeito no resultado de atributos selecionados](media/dm13-neuralnet-agebuyer1.gif "testando o efeito no resultado de atributos selecionados")  
  
##### <a name="explore-variables"></a>Explorar variáveis  
  
1.  Inicialmente, o painel **Variáveis** é classificado na ordem dos atributos mais importantes, considerando os filtros atuais. O comprimento da barra indica a intensidade do fator.  
  
     No exemplo, você pode ver que a renda é o fator mais influente, seguido por região. Por outro lado, os clientes com muitos carros e vários filhos são altamente menos prováveis de comprar uma bicicleta.  
  
2.  No painel **Variáveis**, clique no título de coluna para **Atributo**.  
  
     Ao classificando por atributo, você poderá consultar os compartimentos criados para cada uma das colunas de entrada. As colunas com valores discretos, como ocupação, são *compartimentadas* pelos valores literais.  
  
3.  Observe os intervalos de valores que foram localizados para **Idade** e **Renda**.  
  
     Se alguma de suas colunas de entrada forem números (ou seja, a coluna de dados inteira é um tipo de dados numérico contínuo), os números serão particionados, ou compartimentados, em intervalos discretos.  
  
     Para Renda, a coluna foi subdividida em agrupamentos como 78,4-154,06 (para o intervalo de renda mais alto).  
  
     ![classificação para exibir como as variáveis foram compartimentadas](media/dm13-nn-bucketing-variables.gif "classificação para exibir como as variáveis foram compartimentadas")  
  
     Se você quiser agrupamentos diferentes, deverá usar a ferramenta [Rotular novamente &#40;Suplementos de Mineração de Dados do SQL Server&#41;](relabel-sql-server-data-mining-add-ins.md) ou funções do Excel, para criar novas categorias de renda antes de criar o modelo.  
  
4.  Clique em **Favorece Sim** para restaurar o gráfico para a exibição padrão.  
  
     Por padrão, a exibição será classificada pelo valor de **Favorece** para o valor do primeiro resultado. Você pode alterar quais resultados são atribuídos à primeira coluna e à segunda escolhendo um novo valor para **Valor 1** e **Valor 2** na **Saída**.  
  
5.  Coloque o mouse sobre a barra colorida mais alta no gráfico.  
  
     Uma dica de ferramenta é exibida que inclui uma pontuação de *importância*, um par de pontuações de *probabilidade* e um par de valores de *comparação*.  
  
    -   A **importância** é calculada pelo conjunto de dados inteiro e identifica o atributo que, considerando todas as entradas, está mais correlacionado com o resultado de destino. O visualizador classifica os valores no gráfico pelas pontuações de importância.  
  
    -   A **probabilidade** é calculada para cada conjunto de pares atributo-valor, para os resultados de destino em todo o conjunto de dados.  
  
    -   A **comparação de precisão** informa a utilidade desse par atributo-valor específico para promover um resultado ou outro.  
  
     Observação: A dica de ferramenta contém as mesmas informações independentemente de você posicionar o mouse sobre uma coluna ou a outra.  
  
 [Voltar ao início](#BKMK_Tabs)  
  
###  <a name="BKMK_Inputs"></a> Entradas  
 O painel **Entradas** permite escolher um conjunto de entradas e aplicá-lo como um filtro para o modelo, o que permite ver o efeito dessas opções no resultado, com base nos dados de treinamento  
  
##### <a name="explore-inputs"></a>Explorar entradas  
  
1.  Suponha que você queira definir como destino um grupo específico e ver os fatores que mais influenciam a compra nesse grupo.  
  
     No **entrada** painel, clique no  **\<todos os >** célula sob **atributo**e selecione **idade**.  
  
     Para **Valor**, selecione a categoria de idade mais nova.  
  
2.  Observe que até mesmo quando você filtra em uma faixa etária específica, a região do Pacífico aparece na parte superior da lista. Isso ocorre porque os clientes na região do Pacífico têm muito mais probabilidade de comprar uma bicicleta do que os clientes em outras regiões.  
  
     Como a região não é algo que você possa influenciar, para remover essa variável da consideração e ver outros fatores, você poderá alterar as entradas novamente.  
  
     No painel **Entrada**, clique na célula em branco em **Idade** e selecione **Região**.  
  
     Para **Valor**, selecione **Europa**.  
  
3.  Continue adicionando filtros de entrada para concentrar-se em um grupo de interesse específico.  
  
     Por exemplo, para o atributo de entrada, adicione **Sexo** e selecione **Feminino** como o valor.  
  
     ![Testando o efeito no resultado de atributos selecionados](media/dm13-neuralnet-agebuyer2.gif "testando o efeito no resultado de atributos selecionados")  
  
     Observe como a lista de variáveis muda. Agora **Renda** é a variável que mais importante em prever o resultado do destino.  
  
     A ordem na qual você aplica os filtros de entrada não afeta os resultados.  
  
 [Voltar ao início](#BKMK_Tabs)  
  
###  <a name="BKMK_Outputs"></a> Saídas  
 No painel **Saídas**, você poderá escolher o resultado no qual está interessado. As redes neurais permitem especificar quantas colunas de resultados você desejar, embora adicionar mais saídas adicione também mais complexidade do modelo e pode exigir um tempo maior de processamento.  
  
 Para comparar duas saídas, elas deverão ter sido designadas como colunas **Prever** ou **Prever apenas**.  
  
##### <a name="explore-outputs"></a>Explorar saída  
  
1.  Use a lista **Atributo de saída** para selecionar um atributo.  
  
2.  Selecione dois resultados das listas Valor 1 e Valor 2. Esses dois estados do atributo de saída serão comparados no painel **Variáveis** .  
  
 [Voltar ao início](#BKMK_Tabs)  
  
## <a name="more-about-neural-network-models"></a>Mais sobre modelos de redes neurais  
 As informações no visualizador são recuperadas do servidor usando um procedimento armazenado específico para esse tipo de modelo: System.Microsoft.AnalysisServices.System.DataMining.NeuralNet.GetAttributeScores.  
  
 Se você quiser criar um modelo com vários atributos previsíveis usando os suplementos, use as opções de modelagem **Avançadas**.  
  
 Para obter mais informações, consulte [Criar uma estrutura de mineração &#40;Suplementos de mineração de dados do SQL Server&#41;](create-mining-structure-sql-server-data-mining-add-ins.md) e [Adicionar modelo à estrutura &#40;Suplementos de Mineração de Dados para Excel&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md).  
  
## <a name="see-also"></a>Consulte também  
 [Procurando modelos no Excel &#40;suplementos de mineração de dados do SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
