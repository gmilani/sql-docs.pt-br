---
title: Processar inserções, atualizações e exclusões | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],processing data
ms.assetid: 13a84d21-2623-4efe-b442-4125a7a2d690
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 24ab4d509638b3195c7105602c663c04fb47a411
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771122"
---
# <a name="process-inserts-updates-and-deletes"></a>Processar inserções, atualizações e exclusões
  No fluxo de dados de um pacote do Integration Services, que executa uma carga incremental de dados de alteração, a segunda tarefa serve para separar inserções, atualizações e exclusões. Em seguida, você pode usar comandos apropriados para aplicá-los ao destino.  
  
> [!NOTE]  
>  A primeira tarefa na criação do fluxo de dados de um pacote que realize uma carga incremental de dados de alteração é configurar o componente de origem que executa a consulta que recupera os dados de alteração. Para obter mais informações sobre esse componente, consulte [Recuperar e compreender os dados de alteração](retrieve-and-understand-the-change-data.md). Para obter uma descrição do processo geral para criar um pacote que realiza uma carga incremental de dados de alteração, consulte [Change Data Capture &#40;SSIS&#41;](change-data-capture-ssis.md).  
  
## <a name="associating-friendly-values-to-separate-inserts-updates-and-deletes"></a>Associando valores amigáveis para separar inserções, atualizações e exclusões  
 Na consulta de exemplo que recupera dados de alteração, a função **cdc.fn_cdc_get_net_changes_<capture_instance>** retorna somente a coluna de metadados chamada **__$operation**. Esta coluna de metadados contém um valor ordinal que indica qual operação causou a alteração.  
  
> [!NOTE]  
>  Para obter mais informações sobre a consulta que usa chamadas da função **cdc.fn_cdc_get_net_changes_<capture_instance>**, consulte [Criar a função para recuperar os dados de alteração](create-the-function-to-retrieve-the-change-data.md).  
  
 Corresponder um valor ordinal a sua operação correspondente não é tão fácil quanto usar um mnemônico da operação. Por exemplo, 'D' pode representar facilmente uma operação de exclusão e 'I' representar uma operação de inserção. A consulta de exemplo criada no tópico, [Criando a função para recuperar os dados de alteração](create-the-function-to-retrieve-the-change-data.md), faz essa conversão de um valor ordinal para um valor de cadeia de caracteres amigável que retorna uma nova coluna. O seguinte segmento de código mostra esta conversão:  
  
```  
select   
    ...  
    case __$operation  
        when 1 then 'D'  
        when 2 then 'I'  
        when 4 then 'U'  
        else null  
     end as CDC_OPERATION  
```  
  
## <a name="configuring-a-conditional-split-transformation-to-direct-inserts-updates-and-deletes"></a>Configurando uma transformação de divisão condicional para direcionar inserções, atualizações e exclusões  
 Para direcionar linhas de dados de alteração para uma de três saídas, a transformação de Divisão Condicional é ideal. A transformação apenas verifica o valor da coluna **CDC_OPERATION** em cada linha e determina se essa alteração foi uma inserção, atualização ou exclusão.  
  
> [!NOTE]  
>  A coluna de CDC_OPERATION contém um valor da cadeia de caracteres amigável derivado do valor numérico na coluna **__$operation** .  
  
#### <a name="to-split-inserts-updates-and-deletes-for-processing-by-using-a-conditional-split-transformation"></a>Para dividir inserções, atualizações e exclusões por processamento usando uma transformação de Divisão Condicional  
  
1.  Na guia **Fluxo de Dados** , adicione uma transformação de Divisão Condicional.  
  
2.  Conecte a saída da origem OLE DB à transformação de Divisão Condicional.  
  
3.  No **Editor de Transformação de Divisão Condicional**, no painel inferior do editor, digite as três linhas a seguir para designar as três saídas  
  
    1.  Digite uma linha com a condição `CDC_OPERATION == "I"` para direcionar as linhas inseridas para a saída para inserções.  
  
    2.  Digite uma linha com a condição `CDC_OPERATION == "U"` para direcionar as linhas atualizadas para a saída para atualizações.  
  
    3.  Digite uma linha com a condição `CDC_OPERATION == "D"` para direcionar as linhas excluídas para a saída para exclusões.  
  
## <a name="next-step"></a>Próxima etapa  
 Após você dividir as linhas por processamento, a próxima etapa é aplicar as alterações ao destino.  
  
 **Próximo tópico:** [Aplicar as alterações ao destino](apply-the-changes-to-the-destination.md)  
  
## <a name="see-also"></a>Consulte também  
 [Transformação Divisão Condicional](../data-flow/transformations/conditional-split-transformation.md)   
 [Dividir um conjunto de dados por meio da transformação Divisão Condicional](../data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
  
