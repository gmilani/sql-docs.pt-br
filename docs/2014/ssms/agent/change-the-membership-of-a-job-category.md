---
title: Alterar a associação de uma categoria de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- members [SQL Server], job categories
ms.assetid: 6a18f7f0-eb50-485f-a9c7-df31ae0f994e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f5ed0e086f5743f6759ed8b317750eefcb377180
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782785"
---
# <a name="change-the-membership-of-a-job-category"></a>Change the Membership of a Job Category
  Este tópico descreve como alterar a associação da categoria de trabalho no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o SQL Server Management Objects.  
  
 As categorias de trabalho ajudam a organizar os trabalhos de modo a facilitar sua filtragem e agrupamento. Você pode criar suas próprias categorias de trabalho. Você também pode alterar a associação de trabalhos do Microsoft SQL Server Agent em categorias de trabalho.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para alterar a associação de uma categoria de trabalho usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>Para alterar a associação de uma categoria de trabalho  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja editar uma categoria de trabalho.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse na pasta **Trabalhos** e selecione **Gerenciar Categorias de Trabalho**.  
  
4.  Na caixa de diálogo **Gerenciar Categorias de Trabalho**_server_name_ , selecione a categoria de trabalho que você deseja editar e clique em **Exibir Trabalhos**.  
  
5.  Marque a caixa de seleção **Mostrar todos os trabalhos** .  
  
6.  Para adicionar um trabalho à categoria, na grade principal, marque a caixa de seleção na coluna **Selecionar** correspondente ao trabalho. Para remover um trabalho da categoria, desmarque a caixa. Quando terminar, clique em **OK**.  
  
7.  Feche a caixa de diálogo **Gerenciar Categorias de Trabalho**_server_name_ .  
  
##  <a name="TSQL"></a> Usando Transact-SQL  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>Para alterar a associação de uma categoria de trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql
    -- adding a new job category to the "NightlyBackups" job  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @category_name = N'[Uncategorized (Local)]';  
    GO  
    ```  
  
 Para obter mais informações, [consulte &#40;Transact-SQL&#41;sp_update_job](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql).  
  
##  <a name="SMO"></a>Usando SQL Server Management Objects  
 **Para alterar a associação de uma categoria de trabalho**  
  
 Use a classe `JobCategory` usando uma linguagem de programação da sua escolha, como o Visual Basic, o Visual C# ou o PowerShell.  
