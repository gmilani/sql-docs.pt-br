---
title: Criando previsões em uma sequência de agrupamento de modelo (Tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 94a8d4f9-a76a-49c5-9785-917010359511
caps.latest.revision: 20
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2334975b13b3d503a2208f5a73997549befae219
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312984"
---
# <a name="creating-predictions-on-a-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Criando previsões em um modelo de cluster de sequências (Tutorial de mineração de dados intermediário)
  Depois de entender o melhor o modelo msc ao navegar por ele no visualizador, você pode criar consultas de previsão usando o construtor de consultas de previsão no **previsão do modelo de mineração** guia no Designer de mineração de dados. Para criar uma previsão, primeiro selecione o modelo de clustering de sequências e selecione os dados de entrada. Para entradas, use uma fonte de dados externa ou crie uma consulta singleton e forneça valores em uma caixa de diálogo.  
  
 Esta lição supõe que você já saiba usar o construtor de consultas de previsão e que deseja aprender a criar consultas específicas de um modelo de clustering de sequências. Para obter informações gerais sobre como usar o construtor de consultas de previsão, consulte [Interfaces de consulta de mineração de dados](../../2014/analysis-services/data-mining/data-mining-query-tools.md) ou na seção do tutorial de mineração de dados básico, [criar previsões &#40;Basic Data Mining Tutorial&#41;](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md).  
  
## <a name="creating-predictions-on-the-regional-model"></a>Criando previsões em um modelo regional  
 Para este cenário, primeiro você criará algumas consultas de previsão singleton, para ter uma ideia de como as previsões podem variar por região.  
  
#### <a name="to-create-a-singleton-query-on-a-sequence-clustering-model"></a>Para criar uma consulta de previsão singleton em um modelo de clustering de sequências  
  
1.  Clique o **previsão do modelo de mineração** guia do Designer de mineração de dados.  
  
2.  No **modelo de mineração** menu da coluna, selecione **consulta Singleton**.  
  
     O **modelo de mineração** painel e **entrada de consulta Singleton** painel exibido.  
  
3.  No **modelo de mineração** painel, clique em **Selecionar modelo**. (se o modo de clustering de sequências já tiver sido selecionado, você poderá ignorar esta etapa).  
  
     O **Selecionar modelo de mineração** caixa de diálogo é aberta.  
  
4.  Expanda o nó que representa a estrutura de mineração **Clustering de sequências com região**e selecione o modelo **Clustering de sequências com região**. Clique em **OK**. Por ora, ignore o painel de entrada; você especificará as entradas depois de configurar as funções de previsão.  
  
5.  Na grade, clique na célula vazia em **fonte** e selecione **função de previsão.** Na célula sob **campo**, selecione **PredictSequence**.  
  
    > [!NOTE]  
    >  Você também pode usar o **prever** função. Se você, escolha a versão do **prever** função que tenha uma coluna de tabela como argumento.  
  
6.  No **modelo de mineração** painel, selecione a tabela aninhada `v Assoc Seq Line Items`e arraste-a para a grade, até o **critérios/argumento** caixa para o **PredictSequence** função.  
  
     Arrastando e soltando os nomes de tabela e coluna permite que você crie instruções complexas sem erros de sintaxe. No entanto, ele substitui o conteúdo atual da célula, o que inclui outros argumentos opcionais para o **PredictSequence** função. Para exibir os outros argumentos, você pode adicionar temporariamente uma segunda instância da função à grade para referência.  
  
7.  Clique o **resultados** botão no canto superior do construtor de consultas de previsão.  
  
 Os resultados esperados contêm uma única coluna com o título **expressão**. O **expressão** coluna contém uma tabela aninhada com três colunas da seguinte maneira:  
  
|$SEQUENCE|Número da Linha|Modelo|  
|---------------|-----------------|-----------|  
|1||Mountain-200|  
  
 O que significam esses resultados? Lembre-se de que você não especificou entradas. Dessa forma, a previsão é feita em relação à toda a população de casos, e o Analysis Services retorna a previsão geral mais provável.  
  
### <a name="adding-inputs-to-a-singleton-prediction-query"></a>Adicionando entradas a uma consulta de previsão singleton  
 Até agora, você não especificou entradas. A próxima tarefa, você usará o **entrada de consulta Singleton** painel para especificar algumas entradas à consulta. Primeiro, use [Região] como uma entrada do modelo de clustering de sequências regional para determinar se as sequências previstas são iguais para todas as regiões. Assim, você aprenderá a modificar a consulta para adicionar a probabilidade de cada previsão e mesclar os resultados para facilitar sua exibição.  
  
##### <a name="to-generate-predictions-for-a-specific-customer-group"></a>Para gerar previsões para um grupo de clientes específico  
  
1.  Clique o **Design** botão no canto superior esquerdo do construtor de consultas de previsão para voltar à grade de criação de consultas.  
  
2.  No **entrada de consulta Singleton** caixa de diálogo, clique o **valor** caixa `Region`e selecione **Europa**.  
  
3.  Clique o **resultados** botão para exibir as previsões para clientes na Europa.  
  
4.  Clique o **Design** botão no canto superior esquerdo do construtor de consultas de previsão para voltar à grade de criação de consultas.  
  
5.  No **entrada de consulta Singleton** caixa de diálogo, clique o **valor** caixa `Region`e selecione **América do Norte**.  
  
6.  Clique o **resultados** botão para exibir as previsões para clientes na América do Norte.  
  
### <a name="adding-probabilities-by-using-a-custom-expression"></a>Adicionando probabilidades usando uma expressão personalizada  
 Gerar a probabilidade de cada previsão é ligeiramente mais complicado, já que a probabilidade é um atributo da previsão e é gerada como uma tabela aninhada. Se você já conhece DMX (Data Mining Extensions), poderá alterar com facilidade a consulta e adicionar uma instrução de subseleção na tabela aninhada. No entanto, você também poderá criar uma instrução de subseleção no Construtor de Consultas de Previsão ao adicionar uma expressão personalizada.  
  
##### <a name="to-output-probabilities-for-a-predicted-sequence-by-using-a-custom-expression"></a>Para gerar probabilidades para uma sequência prevista usando uma expressão personalizada  
  
1.  Clique o **Design** botão no canto superior esquerdo do construtor de consultas de previsão para voltar à grade de criação de consultas.  
  
2.  Na grade, em **fonte**, clique em uma nova linha e selecione **expressão personalizada**.  
  
3.  Deixe a caixa em **campo** em branco.  
  
4.  Para **Alias**, tipo `t`.  
  
5.  No **critérios/argumento** , digite a instrução de Subseleção completa, conforme mostrado no exemplo de código a seguir. Não se esqueça de incluir os parênteses inicial e final.  
  
    ```  
    (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))  
    ```  
  
6.  Clique o **resultados** botão para exibir as previsões para clientes na Europa.  
  
 Agora, os resultados contêm duas tabelas aninhadas, uma com a previsão e outra com a probabilidade da previsão. Se a consulta não funcionar, você poderá alternar para o modo de design e examinar a instrução completa da consulta, que deve ser assim:  
  
```  
SELECT  
  PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]),  
  ( (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))) as [t]  
FROM  
  [Sequence Clustering with Region]  
NATURAL PREDICTION JOIN  
(SELECT 'Europe' AS [Region]) AS t  
```  
  
### <a name="working-with-results"></a>Trabalhando com resultados  
 Quando houver muitas tabelas aninhadas nos resultados, talvez seja melhor mesclá-los para obter uma exibição melhor. Para isso, modifique a consulta manualmente e adicione a palavra-chave `FLATTENED`.  
  
##### <a name="to-flatten-nested-rowsets-in-a-prediction-query"></a>Para mesclar conjuntos de linhas aninhadas em uma consulta de previsão  
  
1.  Clique o **consulta** botão no canto do construtor de consultas de previsão.  
  
     A grade se transformará em um painel aberto, onde você poderá exibir e modificar a instrução DMX criada pelo Construtor de Consultas de Previsão.  
  
2.  Após a palavra-chave `SELECT`, digite `FLATTENED`.  
  
     O texto completo da consulta deve ser similar ao seguinte:  
  
    ```  
    SELECT FLATTENED  
      PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]),  
      ( (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))) as [t]  
    FROM  
      [Sequence Clustering with Region]  
    NATURAL PREDICTION JOIN  
    (SELECT 'Europe' AS [Region]) AS t  
    ```  
  
3.  Clique o **resultados** botão no canto superior do construtor de consultas de previsão.  
  
 Depois de editar manualmente uma consulta, você não conseguirá voltar ao modo Design sem perder as alterações. No entanto, é possível salvar a instrução DMX criada manualmente em um arquivo de texto e então voltar para o modo Design. Quando você fizer isso, a consulta será revertida para a última versão válida do modo Design.  
  
## <a name="creating-predictions-on-the-related-model"></a>Criando previsões em um modelo relacionado  
 Os exemplos anteriores usaram uma coluna da tabela de casos, Região, como a entrada da consulta de previsão singleton, porque você estava interessado em saber se o modelo encontrou diferenças entre regiões. No entanto, depois de explorar o modelo, você decidiu que as diferenças não são significativas o suficiente para justificar recomendações de personalização de produtos por região. O que realmente interessa a você na previsão são os itens selecionados pelos clientes. Dessa forma, nas consultas a seguir, você usará o modelo de clustering de sequências que não inclui Região para gerar recomendações para todos os clientes.  
  
### <a name="using-nested-table-columns-as-input"></a>Usando colunas da tabela aninhada como entrada  
 Primeiro, você criará uma consulta de previsão singleton que obtém um único item como entrada e retorna o próximo item mais provável. Para obter uma previsão desse tipo, use uma coluna de tabela aninhada como o valor de entrada. Isso acontece porque o atributo que está sendo previsto, Modelo, faz parte de uma tabela aninhada. O Analysis Services fornece a **entrada de tabela aninhada** caixa de diálogo para ajudá-lo a facilmente criar consultas de previsão aninhada atributos de tabela, usando o construtor de consultas de previsão.  
  
##### <a name="to-use-a-nested-table-as-input-to-a-prediction"></a>Para usar uma tabela aninhada como entrada para uma previsão  
  
1.  Clique o **Design** botão no canto superior esquerdo do construtor de consultas de previsão para voltar à grade de criação de consultas.  
  
2.  No **entrada de consulta Singleton** caixa de diálogo, clique o **valor** caixa `Region`e selecione a linha vazia para limpar a entrada para esse campo.  
  
3.  No **entrada de consulta Singleton** caixa de diálogo, clique o **valor** caixa `vAssocSeqLineItems`e, em seguida, clique no botão (…).  
  
4.  No **entrada de tabela aninhada** caixa de diálogo, clique em **adicionar**.  
  
5.  Na nova linha, clique na caixa sob `Model`e selecione pneu de passeio na lista. Clique em **OK**.  
  
6.  Clique o **resultados** botão para exibir as previsões.  
  
 O modelo recomenda os itens a seguir para todos os clientes que escolherem Pneu de Passeio como o primeiro item. Você já sabe, pela exploração do modelo, que os clientes frequentemente compram os produtos Pneu de Passeio e Tubo de Pneu para Passeio juntos e, portanto, essas recomendações parecem boas.  
  
|$SEQUENCE|Número da Linha|Modelo|  
|---------------|-----------------|-----------|  
|1||Tubo de pneu para passeio|  
|2||Sport-100|  
|3||Jersey Logo de manga longa|  
  
### <a name="creating-a-bulk-prediction-query-using-nested-table-inputs"></a>Criando uma consulta de previsão em massa usando entradas de tabela aninhada  
 Agora que você já está satisfeito com o modelo que cria o tipo de previsões que poderão ser usadas em recomendações, crie uma consulta de previsão mapeada para uma fonte de dados externa. Essa fonte de dados fornecerá valores que representam produtos atuais. Como você está interessado na criação de uma consulta de previsão que ofereça ID do Cliente e uma lista de produtos como entrada, adicione a tabela de clientes como uma tabela de caso e a tabela de compras como a tabela aninhada. Em seguida, adicione funções de previsão, como feito anteriormente, para criar recomendações.  
  
 Esse procedimento é igual ao usado na criação de previsões para o cenário de cesta de compras da Lição 3; no entanto, em um modelo de clustering de sequências, as previsões também precisam do pedido como entrada.  
  
##### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>Para criar uma consulta de previsão usando entradas de tabela aninhada  
  
1.  No **modelo de mineração** painel, selecione o modelo Clustering de sequências, se não ainda estiver selecionada.  
  
2.  No **Selecionar tabela (s) de entrada** caixa de diálogo, clique em **Selecionar tabela de casos**.  
  
3.  No **Selecionar tabela** caixa de diálogo de fonte de dados, selecione pedidos. No **nome de tabela/exibição** lista, selecione vAssocSeqOrders e, em seguida, clique em **Okey**.  
  
4.  No **Selecionar tabela (s) de entrada** caixa de diálogo, clique em **Selecionar tabela aninhada**.  
  
5.  No **Selecionar tabela** caixa de diálogo para **fonte de dados**, selecione pedidos. No **nome de tabela/exibição** lista, selecione vAssocSeqLineItems e, em seguida, clique em **Okey**.  
  
     O Analysis Services tentará detectar relacionamentos e os criará automaticamente, caso os tipos de dados forem iguais e se os nomes de colunas forem similares. Se os relacionamentos criados estiverem incorretos, você pode com o botão direito na linha de junção e selecione **modificar conexões** para editar a coluna de mapeamento, ou com o botão direito na linha de junção e selecione **excluir** para Remova completamente o relacionamento. Nesse caso, como as tabelas já foram unidas na exibição da fonte de dados, esses relacionamentos serão automaticamente adicionados ao painel de design.  
  
6.  Adicione uma nova linha à grade. Para **fonte**, selecione vAssocSeqOrders e **campo**, selecione CustomerKey.  
  
7.  Adicione uma nova linha à grade. Para **fonte**, selecione **função de previsão**e para **campo**, selecione **PredictSequence**.  
  
8.  Arraste vAssocSeqLineItems até o **critérios/argumento** caixa. Clique no final do **critérios/argumento** caixa e, em seguida, digite os seguintes argumentos: `2`.  
  
     O texto completo no **critérios/argumento** caixa deve ser: `[Sequence Clustering].[v Assoc Seq Line Items],2`  
  
9. Clique o **resultados** botão para exibir as previsões para cada cliente.  
  
 Você concluiu o tutorial sobre modelos de clustering de sequências.  
  
## <a name="next-steps"></a>Próximas etapas  
 Se você concluiu todas as seções de [Tutorial de mineração de dados intermediário &#40;Analysis Services - mineração de dados&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md), a próxima etapa será aprender usar instruções de extensões DMX (Data Mining) para criar modelos e Gere previsões. Para obter mais informações, consulte [criando e consultando modelos de mineração de dados com DMX: tutoriais &#40;Analysis Services - mineração de dados&#41;](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md).  
  
 Se você já conhece conceitos de programação, também poderá usar Objetos de Gerenciamento de Análise (AMO) para começar a trabalhar com objetos de mineração de dados programaticamente. Para obter mais informações, consulte [Classes de mineração de dados AMO](../analysis-services/multidimensional-models/analysis-management-objects/amo-data-mining-classes.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos de consulta de modelo de Clustering de sequência](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [Conteúdo do modelo para modelos de Clustering de sequência de mineração &#40;Analysis Services – mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  