---
title: 'Etapa 3: Adicionando e configurando um Gerenciador de Conexão do OLE DB | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c22c9ca183a5975b762fd166ee434f305422e6ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62891715"
---
# <a name="step-3-adding-and-configuring-an-ole-db-connection-manager"></a>Etapa 3: Adicionar e configurar um gerenciador de conexões OLE DB
  Depois de ter adicionado um gerenciador de conexões de arquivo simples para conectar-se à origem de dados, a próxima tarefa é adicionar um gerenciador de conexões OLE DB para conectar-se ao destino. Um gerenciador de conexões OLE DB permite que um pacote extraia dados de qualquer fonte de dados compatível com OLE DB ou carregue dados nela. Usando o gerenciador de conexões OLE DB, você pode especificar o servidor, o método de autenticação e o banco de dados padrão para a conexão.  
  
 Nesta lição, você aprenderá a criar um gerenciador de conexões OLE DB que usa a Autenticação do Windows para se conectar à instância local do **AdventureWorksDB2012**. O gerenciador de conexões OLE DB que você criar também será referenciado por outros componentes que você criar posteriormente neste tutorial, como, por exemplo, a transformação Pesquisa e o destino OLE DB.  
  
### <a name="to-add-and-configure-an-ole-db-connection-manager-to-the-ssis-package"></a>Para adicionar e configurar um Gerenciador de conexões OLE DB no pacote SSIS.  
  
1.  Clique com o botão direito do mouse em qualquer lugar da área **Gerenciadores de Conexões** e clique em **Nova Conexão OLE DB**.  
  
2.  Na caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** , clique em **Novo**.  
  
3.  Em **Nome do servidor**, insira **localhost**.  
  
     Quando você especifica localhost como o nome do servidor, o gerenciador de conexões se conecta à instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no computador local. Para usar uma instância remota do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], substitua localhost pelo nome do servidor ao qual você deseja se conectar.  
  
4.  No grupo **Fazer logon no servidor** , verifique se a opção **Usar Autenticação do Windows** está selecionada.  
  
5.  No **conectar-se a um banco de dados** grupo, o **selecione ou insira um nome de banco de dados** caixa, digite ou selecione `AdventureWorksDW2012`.  
  
6.  Clique em **Testar Conexão** para verificar se as configurações de conexão especificadas são válidas.  
  
7.  Clique em **OK**.  
  
8.  Clique em **OK**.  
  
9. No painel **Conexões de Dados** da caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** , verifique se a opção **localhost.AdventureWorksDW2012** está selecionada.  
  
10. Clique em **OK**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 4: Adicionando uma tarefa de fluxo de dados ao pacote](lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de conexões OLE DB](connection-manager/ole-db-connection-manager.md)  
  
  
