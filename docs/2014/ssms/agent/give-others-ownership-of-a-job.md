---
title: Conceder a propriedade de um trabalho a outras pessoas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], owners
- owners [SQL Server], jobs
- SQL Server Agent jobs, owners
ms.assetid: 2ded5e9c-4251-4fb1-a047-99f13d150b61
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 20bd8904f8dfabd81f3f16ef7bed4c6bf1084c0d
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798232"
---
# <a name="give-others-ownership-of-a-job"></a>Give Others Ownership of a Job
  Este tópico descreve como reatribuir a propriedade de trabalhos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a outro usuário.  
  
-   **Before you begin:**  [Limitations and Restrictions](#Restrictions), [Security](#Security)  
  
-   **Para conceder a propriedade de um trabalho a outros usando:**  
  
     [SQL Server Management Studio](#SSMSProc2)  
  
     [Transact-SQL](#TsqlProc2)  
  
     [SQL Server Management Objects](#SMOProc2)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e Restrições  
 Para criar um trabalho, o usuário deve ser membro de uma das funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent ou da função de servidor fixa **sysadmin** . Um trabalho só pode ser editado por seu proprietário ou por membros da função **sysadmin** . Para obter mais informações sobre as funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte [Funções de banco de dados fixas do SQL Server Agent](sql-server-agent-fixed-database-roles.md).  
  
 Você precisa ser um administrador do sistema para alterar o proprietário de um trabalho.  
  
 Atribuir um trabalho a outro logon não garante que o novo proprietário tenha permissões adequadas para executar o trabalho com êxito.  
  
###  <a name="Security"></a> Segurança  
 Por questão de segurança, apenas o proprietário do trabalho ou um membro da função **sysadmin** pode alterar a definição do trabalho. Somente os membros da função de servidor fixa **sysadmin** podem atribuir a propriedade do trabalho a outros usuários, bem como executar qualquer trabalho, independentemente de seu proprietário.  
  
> [!NOTE]  
>  Se você transmitir a propriedade a um usuário que não seja membro da função de servidor fixa **sysadmin** e o trabalho estiver executando etapas que exijam contas proxy (por exemplo, execução de pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] ), verifique se o usuário tem acesso à conta proxy necessária, ou o trabalho falhará.  
  
####  <a name="Permissions"></a> Permissões  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="SSMSProc2"></a> Usando o SQL Server Management Studio  
 **Para conceder a propriedade de um trabalho a outros**  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho e então clique em **Propriedades**.  
  
3.  Na lista **Proprietário** , selecione um logon. Você precisa ser um administrador do sistema para alterar o proprietário de um trabalho.  
  
     Atribuir um trabalho a outro logon não garante que o novo proprietário tenha permissões adequadas para executar o trabalho com êxito.  
  
##  <a name="TsqlProc2"></a> Usando Transact-SQL  
 **Para conceder a propriedade de um trabalho a outros**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do Mecanismo de Banco de Dados e expanda-a.  
  
2.  Na barra de ferramentas, clique em **Nova Consulta**.  
  
3.  Na janela de consulta, insira as instruções a seguir que usam o procedimento armazenado do sistema [Transact-SQL &#40;&#41; sp_manage_jobs_by_login](/sql/relational-databases/system-stored-procedures/sp-manage-jobs-by-login-transact-sql) . O exemplo a seguir reatribui todos os trabalhos de `danw` para `fran??oisa`.  
  
    ```sql
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_manage_jobs_by_login  
        @action = N'REASSIGN',  
        @current_owner_login_name = N'danw',  
        @new_owner_login_name = N'fran??oisa' ;  
    GO  
    ```  
  
##  <a name="SMOProc2"></a>Usando SQL Server Management Objects  

### <a name="to-give-others-ownership-of-a-job"></a>Para conceder a propriedade de um trabalho a outros
  
1.  Chame a classe `Job` usando uma linguagem de programação que você escolher, como Visual Basic, Visual C# ou PowerShell. Para obter um código de exemplo, consulte [Agendamento de tarefas administrativas automáticas no SQL Server Agent](sql-server-agent.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Implementar trabalhos](implement-jobs.md)   
 [Criar trabalhos](create-jobs.md)  
