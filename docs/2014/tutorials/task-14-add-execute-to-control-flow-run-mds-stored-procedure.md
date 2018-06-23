---
title: 'Tarefa 14: Adicionando tarefa Executar SQL ao fluxo de controle para executar o procedimento armazenado para MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9a5d1b52-d505-4e6f-8a89-569329c094e2
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3d364f3e0a2fbff167336bffa6ea5092d0954d14
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009469"
---
# <a name="task-14-adding-execute-sql-task-to-control-flow-to-run-the-stored-procedure-for-mds"></a>Tarefa 14: Adicionando a tarefa Executar SQL ao fluxo de controle para executar o procedimento armazenado para MDS
  Depois de carregar dados nas tabelas de preparo do MDS, você executará um procedimento armazenado associado a essa tabela para carregar os dados de preparo nas tabelas adequadas no banco de dados MDS. Esse procedimento armazenado tem dois parâmetros necessários que você precisa passar: LogFlag e VersionName. LogFlag especifica se as transações serão registradas em log durante o processo de preparo e VersionName representa a versão do modelo. Consulte [procedimento armazenado preparado](http://msdn.microsoft.com/library/hh231028.aspx) tópico para obter mais detalhes.  
  
 Nesta tarefa, você adicionará a Tarefa Executar SQL ao fluxo de controle para invocar o procedimento armazenado para carregar os dados preparados nas tabelas adequadas do MDS.  
  
1.  Agora, alterne para o **fluxo de controle** guia.  
  
2.  Arraste e solte **tarefa Executar SQL** do **caixa de ferramentas do SSIS** para o **fluxo de controle** guia.  
  
3.  Clique com botão direito **tarefa Executar SQL** no **fluxo de controle** guia e, em seguida, clique em **Renomear**. Tipo **disparar procedimento armazenado para carregar dados no MDS** e pressione **ENTER**.  
  
4.  Conecte-se **receber, limpar, correspondência e corrigir dados do fornecedor** para **disparar procedimento armazenado para carregar dados** usando o conector verde.  
  
     ![Conecte-se para a tarefa Executar SQL](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-01.jpg "conectar-se para a tarefa Executar SQL")  
  
5.  Usando o **variáveis** janela, adicione duas novas variáveis com as seguintes configurações. Se você não vir o **variáveis** janela, clique em **SSIS** na barra de menus, clique em **variáveis**.  
  
    |Nome|Tipo de Dados|Valor|  
    |----------|---------------|-----------|  
    |LogFlag|Int32|1|  
    |VersionName|Cadeia de caracteres|VERSION_1|  
  
     ![Janela de variáveis do SSIS](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-02.jpg "janela variáveis do SSIS")  
  
6.  Clique duas vezes em **disparar procedimento armazenado para carregar dados no MDS**.  
  
7.  No **Editor da tarefa Executar SQL** caixa de diálogo, selecione **(local). MDS** (ou **localhost. MDS**) para **Conexão**.  
  
8.  Tipo **EXEC [stg]. [ udp_Supplier_Leaf]?,?,?** para **instrução SQL**. Você pode verificar o nome usando o SQL Server Management Studio.  
  
     ![Execute a caixa de diálogo Editor de SQL - configurações gerais](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-03.jpg "executar caixa de diálogo Editor de SQL - configurações gerais")  
  
9. Clique em **mapeamento de parâmetro** no menu à esquerda.  
  
10. No **mapeamento de parâmetro** , clique em **adicionar** para adicionar um mapeamento. Maximize a janela e redimensione as colunas para que você possa visualizar os valores nas listas suspensas corretamente.  
  
11. Selecione **User:: VersionName** na lista suspensa para o **nome da variável**.  
  
12. Selecione **NVARCHAR** para **tipo de dados**.  
  
13. Tipo **0** (zero) para **nome do parâmetro**.  
  
14. Repita as quatro etapas anteriores para adicionar mais duas variáveis.  
  
    |Nome da Variável|Tipo de Dados (importante)|Nome do parâmetro|  
    |-------------------|-----------------------------|--------------------|  
    |User::LogFlag|LONG|1|  
    |User::BatchTag|NVARCHAR|2|  
  
     ![Execute o Editor da tarefa SQL - mapeamento de parâmetro](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-04.jpg "executar Editor da tarefa SQL - mapeamento de parâmetro")  
  
15. Clique em **Okey** para fechar o **Editor executar SQL** caixa de diálogo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 15: Criando e executando o projeto SSIS](../../2014/tutorials/task-15-building-and-running-the-ssis-project.md)  
  
  