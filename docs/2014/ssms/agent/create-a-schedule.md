---
title: Criar uma agenda | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- scheduling jobs [SQL Server]
- SQL Server Agent jobs, scheduling
- jobs [SQL Server Agent], scheduling
- schedules [SQL Server], jobs
ms.assetid: 8c7ef3b3-c06d-4a27-802d-ed329dc86ef3
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6d7b36afad30e62166851870503a1e43e0e0e812
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007191"
---
# <a name="create-a-schedule"></a>Create a Schedule
  Você pode criar uma agenda para trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)], ou SQL Server Management Objects.  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para criar uma agenda, usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-schedule"></a>Para criar uma agenda  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, clique com o botão direito do mouse em **Trabalhos**e selecione **Gerenciar Agendas**.  
  
3.  Na caixa de diálogo **Gerenciar Agendas** , clique em **Novo**.  
  
4.  Na caixa **Nome** , digite um nome para a nova agenda.  
  
5.  Se você não quiser que a agenda tenha efeito imediatamente após a criação, desmarque a caixa de seleção **Habilitado** .  
  
6.  Para **Tipo de Agenda**, siga um destes procedimentos:  
  
    -   Para iniciar o trabalho quando as CPUs atingem uma condição ociosa, clique em **Iniciar quando as CPUs estiverem ociosas**.  
  
    -   Clique em **Recorrente**se desejar que a agenda seja executada repetidamente. Para definir a agenda recorrente, complete os grupos **Frequência**, **Frequência Diária**e **Duração** na caixa de diálogo.  
  
    -   Para que a agenda seja executada somente uma vez, clique em **Uma vez**. Para definir a agenda **Uma vez** , conclua o grupo **Ocorrência única** na caixa de diálogo.  
  
##  <a name="TSQL"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-schedule"></a>Para criar uma agenda  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- creates a schedule named RunOnce.   
    -- The schedule runs one time, at 23:30 on the day that the schedule is created.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_add_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql).  
  
##  <a name="SMO"></a> Usando o SQL Server Management Objects  
 **Para criar uma agenda**  
  
 Use o `JobSchedule` classe usando uma linguagem de programação que você escolher, como Visual Basic, Visual c# ou PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](http://msdn.microsoft.com/library/ms162169.aspx).  
  
  