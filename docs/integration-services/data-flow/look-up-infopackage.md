---
title: Pesquisar InfoPackage | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7c0cb7a4-cd07-44cc-85cb-eb1ad91f85fd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2c5736704fd170c629dacdadb89cb3466a0180db
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298241"
---
# <a name="look-up-infopackage"></a>Pesquisar InfoPackage

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use a caixa de diálogo **Pesquisar InfoPackage** para pesquisar um InfoPackage definido no sistema SAP Netweaver BW. Quando a lista de InfoPackages é exibida, selecione o InfoPackage que você quer e o destino preencherá as opções associadas com os valores necessários.  
  
 O destino SAP BW do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW usa a caixa de diálogo **Pesquisar Cadeia de Processo** . Para obter mais informações sobre o destino SAP BW, confira [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir a caixa de diálogo Pesquisar InfoPackage**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o destino SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino SAP BW.  
  
3.  No **Editor de Destino SAP BW**, clique em **Gerenciador de Conexões** para abrir a página **Gerenciador de Conexões** do editor.  
  
4.  Na página **Gerenciador de Conexões** , na caixa de grupo **InfoPackage/InfoSource** , clique em **Pesquisar** para exibir a caixa de diálogo **Pesquisar InfoPackage** .  
  
## <a name="lookup-options"></a>Opções de pesquisa  
 Nos campos de pesquisa, você pode filtrar os resultados usando o caractere curinga asterisco (*) ou usando uma cadeia de caracteres parcial em combinação com o caractere curinga asterisco. No entanto, se você deixar um campo de pesquisa vazio, a operação de pesquisa corresponderá apenas a cadeias de caracteres vazias nesse campo.  
  
 **InfoPackage**  
 Digite o nome do InfoPackage que você deseja pesquisar ou um nome parcial com o caractere curinga asterisco (*). Ou use o caractere curinga asterisco sozinho para incluir todos os InfoPackages.  
  
 **InfoSource**  
 Digite o nome do InfoSource ou um nome parcial com o caractere curinga asterisco (*). Ou use o caractere curinga asterisco sozinho para incluir todos os InfoPackages independentemente do InfoSource.  
  
 **Sistema de origem**  
 Digite o nome do sistema de origem ou um nome parcial com o caractere curinga asterisco (*). Ou use o caractere curinga asterisco sozinho para incluir todos os InfoPackages independentemente dos sistemas de origem.  
  
 **Pesquisar**  
 Pesquisar InfoPackages compatíveis que sejam definidos no sistema SAP Netweaver BW.  
  
## <a name="lookup-results"></a>Resultados da pesquisa  
 Depois que você clicar no botão Pesquisar, uma lista de InfoPackages no sistema SAP Netweaver BW é exibido em uma tabela com os seguintes cabeçalhos de coluna.  
  
 **InfoPackage**  
 Exibe o nome do InfoPackage que está definido no sistema SAP Netweaver BW.  
  
 **Tipo**  
 Exibe o tipo do InfoPackage. A tabela a seguir lista os valores possíveis do tipo.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Trans.|Dados da transação.|  
|Atr.|Dados de atributo|  
|Textos|Textos.|  
  
 **Descrição**  
 Exibe a descrição do InfoPackage.  
  
 **InfoSource**  
 Exibe o nome do InfoSource, se houver, associado ao InfoPackage.  
  
 **Source System**  
 Exibe o nome do sistema de origem.  
  
 Quando a lista de InfoPackages é exibida, selecione o InfoPackage que você quer e o destino preencherá as opções associadas com os valores necessários.  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de Destino SAP BW &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Ajuda F1 do Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
