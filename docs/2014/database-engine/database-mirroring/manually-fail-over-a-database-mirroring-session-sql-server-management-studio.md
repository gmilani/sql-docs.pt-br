---
title: Fazer failover manual de uma sessão de espelhamento de banco de dados (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover [SQL Server], database mirroring
- manual failover [SQL Server]
- database mirroring [SQL Server], failover
ms.assetid: 4ecf9c63-b3a4-4c54-b553-5bc37973232b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b42fdb9d53a4aa0444a98ee311000fb1c2929ff1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62756164"
---
# <a name="manually-fail-over-a-database-mirroring-session-sql-server-management-studio"></a>Realizar failover manualmente de uma sessão de espelhamento de banco de dados (SQL Server Management Studio)
  Quando o banco de dados espelho for sincronizado (ou seja, quando o banco de dados estiver no estado SYNCHRONIZED), o proprietário do banco de dados poderá iniciar failover manual para o servidor espelho.  
  
 Durante um failover manual, as funções do servidor principal e espelho são trocadas para o banco de dados no qual ocorre o failover. O banco de dados espelho torna-se o banco de dados principal, o espelho. Por exemplo, a tabela a seguir mostra como um failover manual troca as funções de dois parceiros de espelhamento: `SQLDBENGINE0_1` e `SQLDBENGINE0_2`.  
  
|Servidor|Antes do failover|Depois do failover|  
|------------|---------------------|--------------------|  
|`SQLDBENGINE0_1`|PRINCIPAL|MIRROR|  
|`SQLDBENGINE0_2`|MIRROR|PRINCIPAL|  
  
 Observe que as funções do servidor para outras sessões de espelhamento de banco de dados não são afetadas. Para obter mais informações, consulte [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md).  
  
### <a name="to-manually-fail-over-database-mirroring"></a>Para realizar failover manualmente de espelhamento de banco de dados  
  
1.  Conecte-se à instância do servidor principal e, no painel **Pesquisador de Objetos** , clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda os **Bancos de Dados**e selecione o banco de dados a receber o failover.  
  
3.  Clique com o botão direito do mouse no banco de dados, selecione **Tarefas**e clique em **Espelhar**. Isso abre a página **Espelhamento** da caixa de diálogo **Propriedades do Banco de Dados** .  
  
4.  Clique em **Failover**.  
  
     Uma caixa de confirmação é exibida.  O servidor principal começa tentando conectar-se ao servidor espelho usando a Autenticação do Windows. Se a Autenticação do Windows não funcionar, o servidor principal exibirá a caixa de diálogo **Conectar-se ao Servidor** . Se o servidor espelho usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selecione **Autenticação do SQL Server** na caixa **Autenticação** . Na caixa de texto **Logon** , especifique a conta de logon com a qual você se conectará no servidor espelho e, na caixa de texto **Senha** , especifique a senha da conta.  
  
     Se o failover for bem-sucedido, a caixa de diálogo **Propriedades do Banco de Dados** será fechada. O banco de dados espelho torna-se o banco de dados principal, o espelho.  
  
     Se o failover falhar, uma mensagem de erro será exibida e a caixa de diálogo permanecerá aberta.  
  
    > [!IMPORTANT]  
    >  Se você modificou qualquer propriedade desde que abriu a página **Espelhamento** , essas alterações não serão salvas.  
  
     A caixa de diálogo é fechada automaticamente.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do banco de dados &#40;página Espelhamento&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Fazer failover manual de uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](manually-fail-over-a-database-mirroring-session-transact-sql.md)   
 [Pausar ou retomar uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](pause-or-resume-a-database-mirroring-session-sql-server.md)   
 [Remover o espelhamento de banco de dados &#40;SQL Server&#41;](remove-database-mirroring-sql-server.md)  
  
  
