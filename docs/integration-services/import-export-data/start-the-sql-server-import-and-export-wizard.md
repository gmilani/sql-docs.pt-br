---
title: Iniciar o Assistente de Importação e Exportação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d54a4d4363b2585d951ca0621306427f8f0e8533
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285113"
---
# <a name="start-the-sql-server-import-and-export-wizard"></a>Iniciar o Assistente de Importação e Exportação do SQL Server

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]




Inicie o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma das maneiras descritas neste tópico para importar dados e exportar dados para qualquer fonte de dados compatível.

> [!IMPORTANT]
> Este tópico descreve somente como **iniciar** o assistente. Se você estiver procurando por alguma outra coisa, consulte [Tarefas e conteúdo relacionados](#related).

Você pode iniciar o assistente:
-   Do [menu Iniciar](#startStart).
-   Do [prompt de comando](#startCmd). 
-   Do [SSMS (SQL Server Management Studio)](#startSSMS).
-   Do [Visual Studio com o SSDT (SQL Server Data Tools)](#startVS).

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>Pré-requisito – O assistente está instalado no computador?
Se você deseja executar o assistente, mas não tem o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado no computador, é possível instalar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalando o SSDT (SQL Server Data Tools). Para obter mais informações, consulte [Baixar o SSDT (SQL Server Data Tools)](https://msdn.microsoft.com/library/mt204009.aspx).

> [!NOTE]
> Para usar a versão de 64 bits do Assistente de Importação e Exportação do SQL Server, você precisa instalar o SQL Server. O SSDT (SQL Server Data Tools) e o SSMS (SQL Server Management Studio) são aplicativos de 32 bits e somente instalam arquivos de 32 bits, incluindo a versão de 32 bits do assistente.

## <a name="startStart"></a> menu Iniciar  
### <a name="start-the-sql-server-import-and-export-wizard-from-the-start-menu"></a>Iniciar o Assistente de Importação e Exportação do SQL Server do menu Iniciar
1.  No menu **Iniciar**, localize e expanda **Microsoft SQL Server 2016**.
3.  Clique em uma das opções a seguir.
  
    -   **Importar e Exportar Dados do SQL Server 2016 (64 bits)**
          
    -   **Importar e Exportar Dados do SQL Server 2016 (32 bits)**  
  
    Execute a versão de 64 bits do assistente, a menos que você saiba que a fonte de dados requer um provedor de dados de 32 bits.
 
    ![Iniciar o assistente](../../integration-services/import-export-data/media/start-wizard-start.jpg)
  
## <a name="startCmd"></a> Command prompt
### <a name="start-the-sql-server-import-and-export-wizard-from-the-command-prompt"></a>Iniciar o Assistente de Importação e Exportação do SQL Server do prompt de comando  
Em uma janela de Prompt de comando, execute **DTSWizard.exe** de um dos seguintes locais.  
  
-   **C:\Arquivos de Programas\Microsoft SQL Server\130\DTS\Binn** para a versão de 64 bits.  
  
-   **C:\Arquivos de Programas (x86)\Microsoft SQL Server\130\DTS\Binn** para a versão de 32 bits.  
  
Execute a versão de 64 bits do assistente, a menos que você saiba que a fonte de dados requer um provedor de dados de 32 bits.

![Inicie o Assistente cmd](../../integration-services/import-export-data/media/start-wizard-cmd.jpg)  
  
## <a name="startSSMS"></a> SSMS (SQL Server Management Studio)
### <a name="start-the-sql-server-import-and-export-wizard-from-sql-server-management-studio-ssms"></a>Iniciar o Assistente de Importação e Exportação do SQL Server do SSMS (SQL Server Management Studio)    
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)].
    
2.  Expanda os **Bancos de dados**.
3.  Clique com o botão direito do mouse em um banco de dados.
4.  Aponte para **Tarefas**.
5.  Clique em uma das opções a seguir.
  
    -   **Importar dados**
      
    -   **Exportar dados**  

    ![Inicie o Assistente SSMS](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

Se você não tem o SQL Server instalado, ou se tem o SQL Server, mas não tem o SQL Server Management Studio instalado, consulte [Baixar o SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md).
  
## <a name="startVS"></a> Visual Studio
### <a name="start-the-sql-server-import-and-export-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a>Iniciar o Assistente de Importação e Exportação do SQL Server do Visual Studio com o SSDT (SQL Server Data Tools) 
 No Visual Studio com o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], com um projeto do Integration Services aberto, faça um dos itens a seguir. 
  
-   No menu **Projeto** , clique em **Assistente de Importação e Exportação do SSIS**. 

    ![Inicie o projeto do assistente](../../integration-services/import-export-data/media/start-wizard-project.jpg) 
    
    \- ou –
    
-   No Gerenciador de Soluções, clique com o botão direito do mouse na pasta **Pacotes SSIS** e clique em **Assistente de Importação e Exportação do SSIS**.

    ![Inicie pacotes do assistente](../../integration-services/import-export-data/media/start-wizard-packages.jpg)

Se você não tem o Visual Studio instalado ou se tem o Visual Studio, mas não tem o SQL Server Data Tools instalado, consulte [Baixar o SSDT (SQL Server Data Tools)](../../ssdt/download-sql-server-data-tools-ssdt.md).

## <a name="get-the-wizard"></a>Obter o assistente
Se você deseja executar o assistente, mas não tem o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado no computador, é possível instalar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalando o SSDT (SQL Server Data Tools). Para obter mais informações, consulte [Baixar o SSDT (SQL Server Data Tools)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="get-help-while-the-wizard-is-running"></a>Obter ajuda enquanto o assistente está em execução
> [!TIP]
> Pressione a tecla F1 em qualquer caixa de diálogo ou página do assistente para ver a documentação da página atual.   

 ## <a name="whats-next"></a>O que vem a seguir?  
 Quando você iniciar o assistente, a primeira página será **Bem-vindo ao Assistente de Importação e Exportação do SQL Server**. Você não precisa realizar nenhuma ação nesta página. Para obter mais informações, consulte [Bem-vindo ao Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md).  
  
## <a name="related"></a> Tarefas e conteúdo relacionados  
 Aqui estão algumas outras tarefas básicas.
-   **Veja um exemplo rápido de como o assistente funciona.**

    -   **Se você prefere ver capturas de tela.** Veja este exemplo de ponta a ponta simples em uma única página – [Introdução a este exemplo simples do Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

    -   **Se você prefere assistir a um vídeo.** Assista a este vídeo de quatro minutos no YouTube que demonstra o assistente e explica, com instruções claras e simples, como exportar dados para o Excel – [Usando o Assistente de Importação e Exportação do SQL Server para exportar para o Excel](https://go.microsoft.com/fwlink/?linkid=829049).

-   **Saiba mais sobre como o assistente funciona.**

    -   **Saiba mais sobre o assistente.** Se você estiver procurando uma visão geral sobre o assistente, consulte [Importar e Exportar Dados com o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

    -   **Saiba mais sobre as etapas do assistente.** Para obter informações sobre as etapas do assistente, consulte [Etapas do Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). Há também uma página separada da documentação para cada página do assistente.

    -   **Saiba como se conectar a fontes de dados e destinos.** Se estiver procurando informações sobre como se conectar aos seus dados, selecione a página desejada na lista aqui – [Conectar-se a fontes de dados com o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md). Há uma página separada da documentação para cada uma das várias fontes de dados usadas com frequência.


