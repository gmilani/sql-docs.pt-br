---
title: Conectar-se a outro computador (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], other computers
ms.assetid: c4c1e94f-4f5f-431e-8b5b-d5ff97baf723
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f8f73c30ca589037ed17c52a00021599fbf3ca34
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996585"
---
# <a name="scm-services---connect-to-another-computer"></a>Serviços SCM – conectar-se a outro computador
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como conectar-se a outro computador no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Siga o primeiro procedimento para abrir o Windows Computer Management [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (mmc), conecte-se ao computador e expanda a árvore Serviços e Aplicativos. Siga o segundo procedimento para criar um arquivo com um link para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager em um computador remoto.  
  
> [!NOTE]  
>  Algumas ações não podem ser executadas pelo Configuration Manager ao conectar-se remotamente.  
  
 Para iniciar, parar, pausar ou retomar o serviço em outro computador, você também pode conectar-se ao servidor com o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse no servidor ou no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agente e clique na ação desejada.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-connect-to-another-computer-with-windows-computer-management"></a>Para se conectar a outro computador com o Windows Computer Management  
  
1.  No menu **Iniciar** , clique com o botão direito do mouse em **Meu Computador**e clique em **Gerenciar.**  
  
2.  Em **Gerenciamento do Computador**, clique com o botão direito do mouse em **Gerenciamento do Computador (Local)** e clique em **Conectar a outro computador**.  
  
3.  Na caixa de diálogo **Selecionar Computador** , na caixa de texto **Outro computador** , digite o nome do computador que você deseja administrar e clique em **OK**.  
  
     O Computer Management exibe os serviços que estão sendo executados no computador remoto. O nó de nível superior é alterado para **Gerenciamento de Computador** \<*remotecomputer*>.  
  
4.  Na árvore de console, expanda **Serviços e Aplicativos**e expanda o **SQL Server Configuration Manager** para administrar os serviços do computador remoto.  
  
#### <a name="to-save-a-link-to-sql-server-configuration-manager-for-another-computer"></a>Para salvar um link no SQL Server Configuration Manager para outro computador  
  
1.  No menu **Iniciar** , clique em **Executar**.  
  
2.  Na caixa **Abrir** , digite **mmc -a** para abrir o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console no modo de autor.  
  
3.  No menu **Arquivo** , clique em **Adicionar/Remover Snap-in**.  
  
4.  Na janela **Adicionar/Remover Snap-in** , clique em **Adicionar**.  
  
5.  Na janela **Adicionar Snap-in Autônomo** , clique em **Gerenciamento do Computador** e clique em **Adicionar**.  
  
6.  Na janela **Gerenciamento do Computador** , clique em **Outro computador**, digite o nome do computador remoto que deseja gerenciar e depois clique em **Terminar**.  
  
7.  Na janela **Adicionar Snap-in Autônomo** , clique em **Fechar**.  
  
8.  Na janela **Adicionar/Remover Snap-in** , clique em **OK**.  
  
9. Expanda **Gerenciamento de Computador (** _\<computer name>_ **)** e **Serviços e Aplicativos**.  
  
10. Clique com o botão direito do mouse no **SQL Server Configuration Manager**e clique em **Nova Janela daqui**.  
  
11. No menu **Janela**, clique em **Raiz do Console** para retornar à primeira janela e exclui-la.  
  
12. No menu **Arquivo** , clique em **Salvar como**e salve o arquivo na pasta desejada, com um nome apropriado com a extensão de arquivo **.msc** . Feche o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console.  
  
13. Para abrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager no computador de destino, clique duas vezes no arquivo. Se desejar, salve um link no arquivo na área de trabalho ou no menu **Iniciar** .  
  
> [!CAUTION]  
>  Ao usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager em um computador remoto, o nome do computador não é óbvio e é possível parar erroneamente ou configurar o computador errado. Na guia **Serviço** , marque a caixa **Nome do Host** para confirmar o nome do computador antes de modificar um serviço.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar o WMI para mostrar o status do servidor nas ferramentas do SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
