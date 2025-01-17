---
title: Como criar e editar um serviço CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1b3d47a5-dc89-482d-bbc7-fff04f194c43
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 525e60450e1cae635cd3a825108dc5a68f80fe42
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771281"
---
# <a name="how-to-create-and-edit-a-cdc-service"></a>Como criar e editar um Serviço CDC
  Estes procedimentos descrevem como criar e editar um novo Serviço Oracle CDC a partir do Console de Configuração do Serviço CDC.  
  
 Este procedimento exige um usuário do Windows com privilégios de administrador no computador onde o serviço Oracle CDC está configurado.  
  
### <a name="to-create-a-new-cdc-service"></a>Para criar um novo serviço CDC  
  
1.  No menu **Iniciar** , selecione **Configuração do Serviço CDC para Oracle**.  
  
2.  No painel esquerdo, clique com o botão direito em Serviços Locais CDC e selecione Novo Serviço  
  
     Você também pode clicar em **Novo Serviço** no painel **Ações** .  
  
3.  Digite ou insira as informações necessárias na caixa de diálogo Novo Serviço Oracle CDC. Consulte [Create and Edit an Oracle CDC Service](create-and-edit-an-oracle-cdc-service.md) para obter informações sobre como inserir informações na caixa de diálogo Novo Serviço Oracle CDC.  
  
     O logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornecido na caixa de diálogo Novo Serviço Oracle CDC é usado pelo Serviço Oracle CDC quando o serviço é executado. Esse logon somente precisa ser um membro da função pública de servidor fixa, nenhum outro privilégio será necessário. Quando novas Instâncias do Oracle CDC são adicionadas, esse logon recebe acesso **db_owner** aos bancos de dados CDC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associados.  
  
4.  Quando você terminar de inserir as informações necessárias, clique em **OK**.  
  
     Para criar a definição de Serviço do Windows do Oracle CDC, o programa precisa de acesso de atualização ao banco de dados MSXDBCDC na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associada. Quando você clica em **OK**, uma caixa de diálogo solicita que o usuário insira um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com um acesso de atualização para o banco de dados MSXDBCDC.  
  
     Para obter informações sobre os dados que você deverá digitar na caixa de diálogo Conecte-se ao SQL Server, consulte [Connection to SQL Server](connection-to-sql-server.md).  
  
5.  Clique em **OK** para fechar a caixa de diálogo Novo Serviço Oracle CDC.  
  
### <a name="to-edit-a-cdc-service"></a>Para editar um serviço CDC  
  
1.  No menu **Iniciar** , selecione **Configuração do Serviço CDC para Oracle**.  
  
2.  No painel esquerdo, selecione **Serviços Locais CDC** e clique com o botão direito do mouse no serviço local que você quer editar e selecione **Propriedades**.  
  
     Você pode selecionar o serviço com o qual você está trabalhando no meio e, no painel **Ações** , clique em **Propriedades**.  
  
3.  Digite ou insira as informações necessárias na caixa de diálogo Propriedades do Serviço CDC. Consulte [Create and Edit an Oracle CDC Service](create-and-edit-an-oracle-cdc-service.md) para obter informações sobre como inserir informações na caixa de diálogo Propriedades do Serviço CDC.  
  
4.  Quando você terminar de inserir as informações necessárias, clique em **OK**e a caixa de diálogo Conecte-se ao SQL Server será aberta.  
  
     Quando um logon sem permissão de gravação para o banco de dados MSXDBDCDC tenta criar uma nova instância Oracle CDC, uma mensagem de erro é exibida. Clique em **OK** nessa caixa de diálogo para exibir a caixa de diálogo Conecte-se ao SQL Server. Nesta caixa de diálogo, você deve inserir as credenciais para um logon que tem permissão de gravação ao banco de dados MSXDBCDC, como a função de banco de dados **db_owner** .  
  
     Para obter informações sobre os dados que você deverá digitar na caixa de diálogo Conecte-se ao SQL Server, consulte [Connection to SQL Server](connection-to-sql-server.md).  
  
5.  Clique em **OK** na caixa de diálogo Conectar ao Oracle. Ambas as caixas de diálogo fecham e o serviço é atualizado e registrado.  
  
## <a name="see-also"></a>Consulte também  
 [Change Data Capture Designer para Oracle da Attunity](change-data-capture-designer-for-oracle-by-attunity.md)   
 [Create and Edit an Oracle CDC Service](create-and-edit-an-oracle-cdc-service.md)  
  
  
