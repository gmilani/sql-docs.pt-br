---
title: Usar uma expressão em um componente de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], data flow
- expressions [Integration Services], data flow components
ms.assetid: 9181b998-d24a-41fb-bb3c-14eee34f910d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bc9f6c28e775cdbd21806172d7074e655fdd1545
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054814"
---
# <a name="use-an-expression-in-a-data-flow-component"></a>Usar uma expressão em um componente de fluxo de dados
  Este procedimento descreve como adicionar uma expressão à transformação Divisão Condicional ou à transformação Coluna derivada. A transformação Divisão Condicional usa expressões para definir as condições que direcionam linhas de dados a uma saída de transformação e a transformação Coluna Derivada usa expressões para definir valores atribuídos a colunas.  
  
 Para implementar uma expressão em uma transformação, o pacote já deve incluir pelo menos uma tarefa Fluxo de Dados e uma fonte. Para obter informações sobre como adicionar itens a pacotes, consulte os seguintes tópicos:  
  
-   [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
    
  
-   [Adicionar ou excluir um componente em um fluxo de dados](data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
-   [Conectar componentes em um fluxo de dados](data-flow/connect-components-in-a-data-flow.md)  
  
### <a name="to-create-an-expression"></a>Para criar uma expressão  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] , clique na guia **Fluxo de Controle** e clique na tarefa Fluxo de Dados que contém o fluxo de dados no qual você deseja implementar uma expressão.  
  
4.  Clique na guia **Fluxo de Dados** e arraste uma transformação Divisão Condicional ou Coluna Derivada da **Caixa de Ferramentas** para a superfície de design.  
  
5.  Arraste o conector verde da fonte ou uma transformação para a transformação Divisão Condicional ou Coluna Derivada.  
  
6.  Clique duas vezes na transformação para abrir sua caixa de diálogo.  
  
7.  No painel à esquerda, expanda **Variáveis** para exibir variáveis definidas pelo sistema e pelo usuário e expanda **Colunas** para exibir as colunas de entrada de transformação.  
  
8.  No painel à direita, expanda **Funções Matemáticas**, **Funções de Cadeia de Caracteres**, **Funções de Data/Hora**, **Funções NULL**, **Conversões de Tipo**e **Operadores** para acessar as funções, as conversões e os operadores fornecidos pela gramática de expressão.  
  
9. Dependendo da transformação, execute uma das seguintes ações para criar uma expressão:  
  
    -   Na caixa de diálogo **Editor de Transformação Divisão Condicional** , arraste variáveis, colunas, funções, operadores e conversões até a coluna **Condição** . Se preferir, digite uma expressão diretamente na coluna **Condição** .  
  
    -   Na caixa de diálogo **Editor de Transformação Coluna Derivada** , arraste variáveis, colunas, funções, operadores e conversões até a coluna **Expressão** . Como alternativa, é possível digitar uma expressão diretamente na coluna **Expressão** .  
  
        > [!NOTE]  
        >  Ao remover o foco da coluna **Condição** ou da coluna **Expressão** , o texto da expressão pode ser realçado para indicar que a sintaxe da expressão está incorreta.  
  
10. Clique em **OK** para fechar a caixa de diálogo.  
  
    > [!NOTE]  
    >  Se a expressão não for válida, um alerta aparecerá descrevendo os erros de sintaxe na expressão.  
  
## <a name="see-also"></a>Consulte também  
 [Expressões do SSIS &#40;Integration Services&#41;](expressions/integration-services-ssis-expressions.md)   
 [Conditional Split Transformation](data-flow/transformations/conditional-split-transformation.md)   
 [Derived Column Transformation](data-flow/transformations/derived-column-transformation.md)   
 [Tarefa de Fluxo de Dados](control-flow/data-flow-task.md)   
 [Fluxo de Dados](data-flow/data-flow.md)  
  
  
