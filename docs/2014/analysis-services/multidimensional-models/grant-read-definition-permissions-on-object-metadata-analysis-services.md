---
title: Conceder permissões Ler definição em metadados de objeto (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- metadata [Analysis Services]
- permissions [Analysis Services], read metadata
- read metadata permissions
ms.assetid: c857e48e-64b0-4ffe-900d-a0a3ddafcefb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e03e55451c2340b5f0773e2873127c3551a82aab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074903"
---
# <a name="grant-read-definition-permissions-on-object-metadata-analysis-services"></a>Conceder permissões para ler definição em metadados de objetos (Analysis Services)
  A permissão para ler uma definição de objeto, ou metadados, em objetos selecionados permite que o administrador conceda permissão para exibir informações de objeto, sem conceder permissão para modificar a definição ou a estrutura do objeto ou para exibir os dados reais do objeto. `Read Definition` permissões podem ser concedidas no banco de dados, fonte de dados, dimensões, estrutura de mineração e nos níveis do modelo de mineração. Se você precisar `Read Definition` permissões para um cubo, você deve habilitar `Read Definition` para o banco de dados. Lembre-se de que as permissões são aditivas. Por exemplo, uma função concede permissão para ler os metadados de um cubo, enquanto uma segunda função fornece ao mesmo usuário permissão para ler os metadados de uma dimensão. As permissões das duas funções diferentes são combinadas para fornecer ao usuário permissão para ler os metadados do cubo e os metadados da dimensão dentro desse banco de dados.  
  
> [!NOTE]  
>  A permissão para ler os metadados de um banco de dados é a permissão mínima necessária para conectar-se a um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Um usuário que tem permissão para ler os metadados também pode usar o conjunto de linhas de esquema DISCOVER_XML_METADATA para consultar o objeto e exibir os metadados. Para obter mais informações, consulte [Conjunto de linhas DISCOVER_XML_METADATA](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-xml-metadata-rowset).  
  
## <a name="set-read-definition-permissions-on-a-database"></a>Definir permissões Ler Definição em um banco de dados  
 Conceder permissão para ler os metadados de banco de dados também concede permissão para ler os metadados de todos os objetos do banco de dados.  
  
 Sugerimos que você inclua o `Read Definition` permissão no nível do banco de dados sempre que você estiver configurando funções para processamento dedicado. Tendo `Read Definition` permite que usuários não administradores exibam a hierarquia de objeto de um modelo em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e naveguem até objetos individuais para processamento posterior.  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], expanda **Funções** para o banco de dados adequado no Pesquisador de Objetos e clique em uma função de banco de dados (ou crie uma nova função de banco de dados).  
  
2.  Sobre o **gerais** guia, selecione o `Read Definition` opção.  
  
3.  No painel **Associação** , insira as contas de usuário e de grupo do Windows que se conectam ao Analysis Services usando essa função.  
  
4.  Clique em **OK** para concluir a criação da função.  
  
## <a name="set-read-definition-permissions-on-individual-objects"></a>Definir permissões Ler Definição em objetos individuais  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], abra a pasta **Banco de Dados** , selecione um banco de dados, expanda **Funções** para o banco de dados apropriado no Pesquisador de Objetos e clique em uma função de banco de dados (ou crie uma nova função de banco de dados).  
  
2.  No **gerais** painel, desmarque a permissão de banco de dados para `Read Definition`. Essa etapa remove a herança de permissão para que você possa definir permissões em objetos individuais.  
  
3.  Selecione o objeto para o qual você está especificando `Read Definition` propriedades:  
  
    -   No **fontes de dados** painel, clique no `Read Definition` caixa de seleção para essa fonte de dados. Os membros da função podem ver a cadeia de conexão até a fonte de dados, incluindo o nome do servidor e, possivelmente, o nome de usuário. A permissão está disponível caso você queria fornecer informações da cadeia de conexão, sem conceder também a permissão para modificar a sequência de conexão ou exibir as definições de algum outro objeto.  
  
    -   No **dimensões** painel, clique no `Read Definition` caixa de seleção daquela dimensão. Analistas e desenvolvedores experientes talvez precisem exibir a definição sem permissão para modificar ou exibir as definições de outros objetos (como outras dimensões, objetos de cubo ou estruturas e modelos de mineração).  
  
    -   No painel de estruturas de mineração, clique o `Read Definition` caixa de seleção de modelos ou estruturas de mineração de dados. `Read Definition` é necessário para navegar no modelo de dados. Consulte [Conceder permissões em estruturas e modelos de mineração de dados &#40;Analysis Services&#41;](grant-permissions-on-data-mining-structures-and-models-analysis-services.md) para obter mais detalhes.  
  
4.  No painel **Associação**, insira as contas de usuário e de grupo do Windows que se conectam ao Analysis Services usando essa função.  
  
5.  Clique em **OK** para concluir a criação da função.  
  
## <a name="see-also"></a>Consulte também  
 [Conceder permissões de banco de dados &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md)   
 [Conceder permissões de processo &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)  
  
  
