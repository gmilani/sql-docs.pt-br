---
title: Exibindo e parando pacotes que são executados sobre a integração do servidor de serviços | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- packages [Integration Services], managing
- managing running packages [Integration Services]
- packages [Integration Services], running
- running package [Integration Services], managing
ms.assetid: 11bf44e6-f6b0-475f-b816-40e914dbac80
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ce4fd750986269c0e92ae2ea764f02e1bd642cb7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117244"
---
# <a name="viewing-and-stopping-packages-running-on-the-integration-services-server"></a>Exibindo e parando pacotes que são executados no servidor do Integration Services
  O `SSISDB` banco de dados armazena o histórico de execução em tabelas internas que não são visíveis aos usuários. Porém, ele expõe as informações necessárias por meio de exibições públicas que você pode consultar. Ele também fornece procedimentos armazenados que você pode chamar para executar tarefas comuns relacionadas a pacotes.  
  
 Normalmente você gerencia objetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no servidor no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. No entanto, você também pode consultar as exibições de banco de dados e chamar os procedimentos armazenados diretamente, ou escrever código personalizado que chame a API gerenciada. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e a API gerenciada consultam as exibições e chamam os procedimentos armazenados para executar muitas de suas tarefas. Por exemplo, você pode exibir a lista de pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que estão em execução atualmente no servidor e solicitar a interrupção de pacotes, se necessário.  
  
## <a name="viewing-the-list-of-running-packages"></a>Exibindo a lista de pacotes em execução  
 É possível exibir a lista de pacotes que estão sendo executados no momento no servidor na caixa de diálogo **Operações Ativas** . Para obter mais informações, consulte [Active Operations Dialog Box](../../2014/integration-services/active-operations-dialog-box.md).  
  
 Para obter informações sobre os outros métodos que podem ser usados para exibir a lista de pacotes em execução, consulte os tópicos a seguir.  
  
 Acesso ao [!INCLUDE[tsql](../includes/tsql-md.md)]  
 Para exibir a lista de pacotes em execução no servidor, consulte a exibição [catalog.executions &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database) para obter pacotes que têm um status 2.  
  
 Acesso programático por meio de API gerenciada  
 Consulte o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> e suas classes.  
  
## <a name="stopping-a-running-package"></a>Interrompendo um pacote em execução  
 Você pode solicitar um pacote em execução a ser interrompido na caixa de diálogo **Operações Ativas** . Para obter mais informações, consulte [Active Operations Dialog Box](../../2014/integration-services/active-operations-dialog-box.md).  
  
 Para obter informações sobre os outros métodos que podem ser usados para interromper um pacote em execução, consulte os tópicos a seguir.  
  
 Acesso ao [!INCLUDE[tsql](../includes/tsql-md.md)]  
 Para interromper um pacote em execução no servidor, chame o procedimento armazenado, [catalog.stop_operation &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database).  
  
 Acesso programático por meio de API gerenciada  
 Consulte o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> e suas classes.  
  
## <a name="viewing-the-history-of-packages-that-have-run"></a>Exibindo o histórico de pacotes executados  
 Para exibir o histórico de pacotes executados no [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], use o relatório **Todas as Execuções** . Para obter mais informações sobre o relatório **Todas as Execuções** e outros relatórios padrão, consulte [Relatórios do servidor do Integration Services](../../2014/integration-services/reports-for-the-integration-services-server.md).  
  
 Para obter informações sobre os outros métodos que podem ser usados para exibir o histórico de pacotes em execução, consulte os tópicos a seguir.  
  
 Acesso ao [!INCLUDE[tsql](../includes/tsql-md.md)]  
 Para exibir informações sobre os pacotes que foram executados, consulte a exibição [catalog.executions &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database).  
  
 Acesso programático por meio de API gerenciada  
 Consulte o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> e suas classes.  
  
## <a name="see-also"></a>Consulte também  
 [Execução de projetos e pacotes](packages/run-integration-services-ssis-packages.md)   
 [Relatórios para solução de problemas de execução de pacote](troubleshooting/troubleshooting-reports-for-package-execution.md)  
  
  