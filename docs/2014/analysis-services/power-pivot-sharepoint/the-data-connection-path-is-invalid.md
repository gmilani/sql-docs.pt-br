---
title: 'O caminho de conexão de dados na pasta de trabalho aponta para um arquivo na unidade local ou é um URI inválido. As conexões a seguir não foram atualizadas: Dados do PowerPivot | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: bd22e41a-0931-4d32-888a-633a3046fc5e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0cc18a2c7111c71b62f77f5f52727a4a50a661ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071041"
---
# <a name="the-data-connection-path-in-the-workbook-points-to-a-file-on-the-local-drive-or-is-an-invalid-uri-the-following-connections-failed-to-refresh-powerpivot-data"></a>O caminho de conexão de dados na pasta de trabalho aponta para um arquivo na unidade local ou é um URI inválido. As conexões a seguir não foram atualizadas: Dados PowerPivot
  Para pastas de trabalho do Excel que contenham dados PowerPivot, os Serviços do Excel retornarão este erro se não for possível conectar a fontes de dados inseridas.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a|PowerPivot para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Os Serviços do Excel são configurados para permitir somente conexões de dados de arquivos .odc arquivos que estejam em uma biblioteca de conexões de dados confiável.|  
|Texto da mensagem|O caminho de conexão de dados na pasta de trabalho aponta para um arquivo na unidade local ou é um URI inválido. As conexões a seguir não foram atualizadas: Dados PowerPivot|  
  
## <a name="explanation"></a>Explicação  
 As pastas de trabalho PowerPivot contêm conexões de dados inseridas. Para dar suporte à interação de pastas de trabalho por slicers e filtros, os Serviços do Excel devem ser configurados para permitir acesso a dados externos por informações de conexão inseridas. O acesso a dados externos é necessário para recuperar dados PowerPivot carregados em servidores PowerPivot no farm.  
  
## <a name="user-action"></a>Ação do usuário  
 Altere as definições de configuração para permitir conexões de fontes de dados inseridas.  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Clique em **Aplicativo dos Serviços do Excel**.  
  
3.  Clique em **Local de Arquivo Confiável**.  
  
4.  Clique em **http://** ou no local que você deseja configurar.  
  
5.  Em Dados Externos, em Permitir Dados Externos, clique em **Bibliotecas de conexões de dados confiáveis e incorporadas**.  
  
6.  Clique em **OK**.  
  
 Também é possível criar um novo local confiável para sites que contenham pastas de trabalho PowerPivot e, em seguida, modificar os parâmetros de configuração apenas para esse site. Para obter mais informações, consulte [criar um local confiável para sites do PowerPivot na Administração Central](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
  
