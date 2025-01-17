---
title: Visualizar tabela selecionada (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.previewselecttable.f1
ms.assetid: b6b34b5a-43b3-4a75-9f3b-b2ad1084b1b6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a0f168dabd237fe685eb90d2caeeba0db4eed97
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070715"
---
# <a name="preview-selected-table-ssas"></a>Visualizar Tabela Selecionada (SSAS)
  Esta página do **Assistente de Importação de Tabela** o habilita a visualizar os dados na tabela selecionada, para selecionar as colunas a serem incluídas na importação de dados e para filtrar os dados nas colunas selecionadas. Para acessar o assistente do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Modelo** , clique em **Importar de Fonte de Dados**.  
  
 Nem todas as linhas na tabela são exibidas. No entanto, os filtros definidos serão aplicados a todos os dados na tabela durante a importação.  
  
 Para fontes de dados que usam a autenticação do Windows, as credenciais do usuário atual são usadas para buscar os dados exibidos na caixa de diálogo Visualizar e Filtrar. Para outras fontes de dados, as credenciais fornecidas na cadeia de conexão são usadas para buscar os dados.  
  
 A aparência de dados nesta página não garante que a importação terá êxito. Se o nome do usuário especificado na página Informações sobre Representação não tiver privilégios suficientes para ler do banco de dados selecionado, a importação falhará.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Caixa de seleção no cabeçalho da coluna**  
 Marque a caixa de seleção para incluir a coluna na importação de dados. Desmarque a caixa de seleção para remover a coluna da importação de dados.  
  
 **Botão de seta para baixo no cabeçalho da coluna**  
 Filtre dados na coluna.  
  
 **Limpar filtros de linha**  
 Remova todos os filtros aplicados aos dados nas colunas.  
  
  
