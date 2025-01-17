---
title: Criar um novo guia de plano | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.designer.newplanguide.f1
helpviewer_keywords:
- creating plan guides
- plan guides [SQL Server]. creating
ms.assetid: e1ad78bb-4857-40ea-a0c6-dcf5c28aef2f
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 5f37f0189df126054626fdd4820368911b1fa5cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946964"
---
# <a name="create-a-new-plan-guide"></a>Criar um novo guia de plano
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Guias de plano influenciam a otimização de consulta, anexando a elas dicas de consulta ou um plano de consulta fixo. No guia de plano, você especifica a instrução que deseja otimizar e uma cláusula OPTION que contém as dicas de consulta que deseja usar. ou um plano de consulta específico que você deseja usar para otimizar a consulta. Quando a consulta é executada, o otimizador de consultas faz a correspondência da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] com o guia de plano, anexando a cláusula OPTION à consulta em tempo de execução ou usando o plano de consulta especificado.  

Um Guia de Plano aplica-se a um plano de consulta fixa, e/ou dicas de consulta, para uma consulta.
  
##  <a name="Restrictions"></a> Limitações e restrições  
-   Os argumentos para sp_create_plan_guide devem ser fornecidos na ordem em que aparecem. Quando você fornece valores para os parâmetros de **sp_create_plan_guide**, todos os nomes de parâmetros devem ser especificados explicitamente ou nenhum deles deve ser especificado. Por exemplo, se **@name =** for especificado, então **@stmt =** , **@type =** e assim por diante, também deverá ser especificado. Da mesma forma, se **@name =** for omitido e apenas o valor do parâmetro for fornecido, os nomes de parâmetro restantes também deverão ser omitidos e apenas seus valores deverão ser fornecidos. Os nomes de argumento são usados apenas para fins descritivos, para ajudar compreender a sintaxe. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não verifica se o nome de parâmetro especificado corresponde ao nome do parâmetro na posição em que o nome é usado.  
  
-   Você pode criar mais de um guia de plano OBJECT ou SQL para a mesma consulta e lote ou módulo. Porém, só um guia de plano pode ser ativado em um determinado momento.  
  
-   Os guias de plano OBJECT não podem ser criados para um valor @module_or_batch que referencie um procedimento armazenado, uma função ou um gatilho DML que especifique a cláusula WITH ENCRYPTION ou que seja temporário.  
  
-   A tentativa de cancelar ou modificar uma função, procedimento armazenado ou gatilho DML referenciado por um guia de plano, habilitado ou desabilitado, provoca um erro. A tentativa de descartar uma tabela com um gatilho definido nela que é mencionado por um guia de plano também causa um erro.  

##  <a name="Permissions"></a> Permissões  
 Para criar um guia de plano do tipo OBJECT, você precisa da permissão ALTER no objeto referenciado. Para criar um guia de plano do tipo SQL ou TEMPLATE, você precisa de permissão ALTER no banco de dados atual.  
  
##  <a name="SSMSProcedure"></a> Para criar um guia de plano, usando o SSMS  
1.  Clique no sinal de adição para expandir o banco de dados no qual você deseja criar um guia de plano e clique no sinal de adição para expandir a pasta **Programação** .  
  
2.  Clique com o botão direito do mouse na pasta **Guias de Plano** e selecione **Novo Guia de Plano…** . ![select_plan_guide](../../relational-databases/performance/media/select-plan-guide.png)
  
3.  Na caixa de diálogo **Novo Guia de Plano** , na caixa **Nome** , digite o nome do guia de plano.  
  
4.  Na caixa **Instrução** , insira a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] à qual o guia de plano deve ser aplicado.  
  
5.  Na lista **Tipo de escopo** , selecione o tipo de entidade na qual a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] aparece. Isso especifica o contexto para se fazer a correspondência da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] ao guia de plano. Os valores possíveis são **OBJECT**, **SQL**e **TEMPLATE**.  
  
6.  Na caixa **Lote de escopo** , digite o texto de lote no qual a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] aparece. O texto de lote não pode incluir uma instrução `USE`*database*. A caixa **Lote de escopo** está disponível apenas quando **SQL** é selecionado como um tipo de escopo. Se nada for inserido na caixa de lote de escopo quando o SQL for o tipo de escopo, o valor do texto de lote será definido com o mesmo valor que a caixa **Instrução** .  
  
7.  Na lista **Nome do esquema de escopo** , digite o nome do esquema no qual o objeto está contido. A caixa **Nome do esquema de escopo** está disponível apenas quando **Objeto** é selecionado como um tipo de escopo.  
  
8.  Na caixa **Nome do objeto de escopo** , digite o nome do [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimento armazenado, função escalar definida pelo usuário, função com valor de tabela de várias instruções ou gatilho DML no qual a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] aparece. A caixa **Nome do objeto de escopo** está disponível apenas quando **Objeto** é selecionado como um tipo de escopo.  
  
9. Na caixa **Parâmetros** , digite o nome do parâmetro e os tipos de dados de todos os parâmetros inseridos na instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
   Parâmetros são aplicados somente quando uma das seguintes condições for verdadeira:  
  
   -   O tipo de escopo é **SQL** ou **TEMPLATE**. No caso de **TEMPLATE**, parâmetros não devem ser NULL.  
  
   -   A instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] é enviada usando-se sp_executesql e um valor para o parâmetro é especificado ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envia internamente uma instrução depois de parametrizá-la.  
  
10. Na caixa **Dicas** , digite as dicas de consulta ou o plano de consulta a ser aplicado à instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] . Para especificar uma ou mais dicas de consulta, digite uma cláusula OPTION válida.  
  
11. Clique em **OK**.  

![plan_guide](../../relational-databases/performance/media/plan-guide.png)  

##  <a name="TsqlProcedure"></a> Criar um guia de plano usando T-SQL  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql  
    -- creates a plan guide named Guide1 based on a SQL statement  
    EXEC sp_create_plan_guide   
        @name = N'Guide1',   
        @stmt = N'SELECT TOP 1 *   
                  FROM Sales.SalesOrderHeader   
                  ORDER BY OrderDate DESC',   
        @type = N'SQL',  
        @module_or_batch = NULL,   
        @params = NULL,   
        @hints = N'OPTION (MAXDOP 1)';  
  
    ```  

Para obter mais informações, consulte [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md).  

  
