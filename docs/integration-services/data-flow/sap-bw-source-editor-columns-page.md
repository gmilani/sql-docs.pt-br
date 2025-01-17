---
title: Editor de Origem SAP BW (página Colunas) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwsource.columns.f1
ms.assetid: c2ec8bb7-be9b-4783-ad88-32512de784b0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d523437dd2deaddac4462f2e825ff0c197b26bf6
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291845"
---
# <a name="sap-bw-source-editor-columns-page"></a>Editor de Origem de SAP BW (página Colunas)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use a página **Colunas** do **Editor de Origem SAP BW** para mapear uma coluna de saída em cada coluna externa (origem).  
  
 Para saber mais sobre o componente de origem do SAP BW do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW, consulte [Origem SAP BW](../../integration-services/data-flow/sap-bw-source.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
> [!IMPORTANT]  
>  A extração de dados do SAP Netweaver BW exige licenciamento SAP adicional. Verifique esses requisitos com a SAP.  
  
 **Para abrir a página Colunas**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém a origem SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na fonte SAP BW.  
  
3.  No **Editor de Origem SAP BW**, clique em **Colunas** para abrir a página **Colunas** do editor.  
  
## <a name="options"></a>Opções  
  
> [!NOTE]  
>  Se você não souber todos os valores necessários para configurar a origem, talvez precise perguntar ao administrador do SAP.  
  
 **Colunas Externas Disponíveis**  
 Exiba a lista de colunas externas disponíveis na fonte de dados, e selecione as colunas a serem incluídas no fluxo de dados.  
  
 Para incluir uma coluna no fluxo de dados, marque a caixa de seleção que corresponde a essa coluna. A ordem na qual você seleciona as caixas de seleção determina a ordem na qual as colunas serão geradas. Ou seja a primeira caixa de seleção que você selecionar será a primeira coluna gerada, a segunda caixa de seleção será a segunda e assim por diante.  
  
 **Coluna Externa**  
 Visualize as colunas externas (origem) selecionadas. As colunas selecionadas aparecem na ordem na que você verá suas colunas geradas correspondentes ao configurar os componentes downstream que consomem os dados dessa fonte.  
  
 Para alterar a ordem das colunas, na lista **Colunas Externas Disponíveis** , desmarque as caixas de seleção para todas as colunas. Em seguida, selecione as colunas na ordem que você quer que elas apareçam.  
  
 **Coluna de Saída**  
 Forneça um nome exclusivo para cada coluna de saída. O padrão é o nome da coluna externa (origem) selecionada. No entanto, você pode inserir qualquer nome descritivo exclusivo. [!INCLUDE[ssIS](../../includes/ssis-md.md)] exibirá os nomes de **Coluna de Saída** para as colunas ao configurar os componentes downstream que consomem os dados dessa fonte.  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de Origem SAP BW &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Editor de Origem SAP BW &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)   
 [Editor de Origem SAP BW &#40;Página Avançado&#41;](../../integration-services/data-flow/sap-bw-source-editor-advanced-page.md)   
 [Ajuda F1 do Microsoft Connector para SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
