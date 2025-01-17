---
title: Gerenciador de Conexões de SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 06b166a1-a9df-48ea-a0e8-9b8d6979c0a1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b3ee629cd7701d8b06351e8932daac57637b195e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833667"
---
# <a name="sap-bw-connection-manager"></a>Gerenciador de Conexões SAP BW
  O gerenciador de conexões SAP BW é o componente de gerenciador de conexões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW. Portanto, o gerenciador de conexões do SAP BW fornece a conectividade para um sistema SAP Netweaver BW versão 7 que os componentes de origem e destino do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW precisam. (A origem e o destino SAP BW que fazem parte do pacote do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW são os únicos componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que usam o gerenciador de conexões do SAP BW.)  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 Quando você adiciona um gerenciador de conexões do SAP BW a um pacote, a propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `SAPBI`.  
  
## <a name="configuring-the-sap-bw-connection-manager"></a>Configurando o gerenciador de conexões SAP BW  
 Você pode configurar um gerenciador de conexões SAP BW de uma das seguintes formas:  
  
-   Forneça o cliente, o nome de usuário, a senha e o idioma para a conexão.  
  
-   Escolha se deseja se conectar a um único servidor de aplicativos ou um grupo de servidores com balanceamento de carga.  
  
-   Forneça o host e o número do sistema para um único servidor de aplicativos ou forneça o servidor de mensagens, o grupo e o SID para um grupo de servidores com balanceamento de carga.  
  
-   Habilite o log personalizado das chamadas de função de RFC para os componentes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW. (Esse log é separado do log opcional que você pode habilitar em pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].) Para habilitar o log das chamadas de função de RFC, você especifica um diretório no qual armazenar os arquivos de log que são criados antes e depois de cada chamada de função de RFC. (Esse recurso de registro cria muitos arquivos de log em formato XML. Como esses arquivos de log também contêm todas as linhas de dados que são transferidas, esses arquivos de log podem consumir uma grande quantidade de espaço em disco.) Se você não selecionar um diretório de log, o registro em log não será habilitado.  
  
    > [!IMPORTANT]  
    >  Se os dados que são transferidos contêm informações confidenciais, os arquivos de log também conterão essas informações confidenciais.  
  
-   Use os valores que você inseriu para testar a conexão.  
  
 Se você não souber todos os valores necessários para configurar o gerenciador de conexões, talvez precise perguntar ao administrador do SAP.  
  
 Para obter um passo a passo que demonstre como configurar e usar o gerenciador de conexões do SAP BW, a origem e o destino, consulte o white paper [Usando o SQL Server 2008 Integration Services com SAP BI 7.0](https://go.microsoft.com/fwlink/?LinkID=137090). Este white paper também mostra como configurar os objetos necessários no SAP BW.  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>Usando o Designer SSIS para configurar a origem  
 Para obter mais informações sobre as propriedades do gerenciador de conexões do SAP BW que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Editor do Gerenciador de Conexões de SAP BW](../sap-bw-connection-manager-editor.md)  
  
## <a name="see-also"></a>Consulte também  
 [Componentes do Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-components.md)  
  
  
