---
title: Editor de destino SAP BW (página Mapeamentos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: dfa1f1d6-6b64-4331-bdc5-eaa8b7aa41a1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0af079eaa96fd7925ef361b398cd628641c55a3c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770866"
---
# <a name="sap-bw-destination-editor-mappings-page"></a>Editor de Destino de SAP BW (página Mapeamentos)
  Use a página **Mapeamentos** do **Editor de Destino SAP BW** para mapear colunas de entrada para colunas de destino.  
  
 Para saber mais sobre o destino SAP BW do Connector 1.1 do [!INCLUDE[msCoName](../../includes/msconame-md.md)] para SAP BW, consulte [Destino SAP BW](sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir a página Mapeamentos**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o destino SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino SAP BW.  
  
3.  No **Editor de Destino SAP BW**, clique em **Mapeamentos** para abrir a página **Mapeamentos** do editor.  
  
## <a name="options"></a>Opções  
  
> [!NOTE]  
>  Se você não souber todos os valores necessários para configurar o destino, talvez precise perguntar ao administrador do SAP.  
  
 A página **Mapeamentos** do **Editor de destino SAP BW consiste** em duas seções:  
  
-   A seção superior mostra as colunas de entrada e destino disponíveis e permite criar mapeamentos entre esses dois tipos de colunas.  
  
-   A seção inferior é uma tabela que listas quais colunas de entrada foram mapeadas para quais colunas de saída.  
  
### <a name="upper-section-options"></a>Opções da seção superior  
 A seção superior tem as seguintes opções:  
  
 **Colunas de Entrada Disponíveis**  
 Exiba a lista das colunas de entrada disponíveis.  
  
 Para mapear uma coluna de entrada para uma coluna de destino, arraste uma coluna da lista **Colunas de Entrada Disponíveis** e solte essa coluna em uma coluna na lista **Colunas de Destino Disponíveis** .  
  
 **Colunas de Destino Disponíveis**  
 Exiba a lista de colunas de destino disponíveis.  
  
 Para mapear uma coluna de entrada para uma coluna de destino, arraste uma coluna da lista **Colunas de Entrada Disponíveis** e solte essa coluna em uma coluna na lista **Colunas de Destino Disponíveis** .  
  
 A seção superior também tem um menu de contexto que você pode abrir clicando com o botão direito do mouse no plano de fundo. Esse menu de contexto contém as seguintes opções:  
  
-   **Selecionar Todos os Mapeamentos**  
  
-   **Excluir Mapeamentos Selecionados**  
  
-   **Mapear Itens Correspondendo Nomes**  
  
### <a name="lower-section-columns"></a>Colunas da seção inferior  
 A seção inferior é uma tabela de mapeamentos, e tem as seguintes colunas:  
  
 **Coluna de Entrada**  
 Visualize as colunas de entrada que você selecionou.  
  
 Para mapear uma coluna de entrada diferente para a mesma coluna de destino, selecione uma coluna diferente de entrada na lista. Para remover um mapeamento, selecione **\<ignorar>** para excluir a coluna de entrada da saída.  
  
 **Coluna de Destino**  
 Visualize cada coluna de destino disponível, esteja essa coluna mapeada ou não.  
  
## <a name="see-also"></a>Consulte também  
 [Editor de Destino SAP BW &#40;Página Gerenciador de Conexões&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [Editor de Destino SAP BW &#40;Página Saída de Erro&#41;](sap-bw-destination-editor-error-output-page.md)   
 [Editor de Destino SAP BW &#40;Página Avançado&#41;](sap-bw-destination-editor-advanced-page.md)   
 [Ajuda F1 do Microsoft Connector 1.1 para SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
