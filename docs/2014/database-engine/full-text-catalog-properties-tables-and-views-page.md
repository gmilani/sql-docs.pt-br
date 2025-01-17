---
title: Propriedades do catálogo de texto completo (página tabelas e exibições) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftcatalogproperties.tablesviews.f1
ms.assetid: 2d45fcd2-0f0f-4167-9027-316d6696c106
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 78d7dc111bc0b6eb10e80f32785beeda710e52bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779187"
---
# <a name="full-text-catalog-properties-tables-and-views-page"></a>Propriedades do catálogo de texto completo (página Tabelas e Exibições)
  Usa essa página de caixa de diálogo para exibir ou modificar as tabelas e exibições atribuídas ao catálogo de texto completo.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Todos os objetos de tabela/exibição qualificados neste banco de dados**  
 Lista as tabelas e exibições que possuem um índice exclusivo definido nelas, mas que ainda não fazem parte do catálogo de texto completo. Para selecionar uma tabela ou exibição e atribuí-lo no catálogo, selecione os itens na caixa de listagem e pressione o botão "->".  
  
 **Objetos de tabela/exibição atribuídos ao catálogo**  
 Lista as tabelas e exibições que estão atualmente atribuídas ao catálogo de texto completo.  
  
## <a name="selected-object-properties"></a>Propriedades dos objetos selecionados  
 **Propriedades do objeto selecionado**  
 Exibe as propriedades do objeto selecionado na caixa de listagem de objetos atribuídos ao catálogo.  
  
 **Índice exclusivo**  
 Lista os índices exclusivos disponíveis da tabela ou exibição.  
  
 **Tabela é habilitada para texto completo**  
 Marque essa caixa de seleção para habilitar o índice de texto completo na tabela. Desmarque-a para desabilitar o índice de texto completo.  
  
## <a name="eligible-columns-grid"></a>Grade de colunas qualificadas  
  
|||  
|-|-|  
|**Colunas disponíveis**|Exibe todas as colunas que são indexadas com texto completo. Marque a caixa de seleção para adicionar a coluna ao índice de texto completo.|  
|**Idioma do separador de palavras**|Exibe o idioma do separador de palavras.|  
|**Coluna de tipo de dados**|Lista o nome da coluna na tabela que contém o tipo de documento da coluna listada na **colunas disponíveis** se a coluna for uma `varbinary(max)` ou `image` coluna.|  
|**Semântica Estatística**|Especifique se habilitará a indexação semântica da coluna selecionada. Para obter mais informações, veja [Pesquisa semântica &#40;SQL Server&#41;](../relational-databases/search/semantic-search-sql-server.md).<br /><br /> Se você selecionar um **Idioma** antes de selecionar **Semântica Estatística**, e o idioma selecionado não tiver um Modelo de Idioma Semântico associado, a caixa de seleção **Semântica Estatística** será desabilitada. Se você selecionar **Semântica Estatística** antes de selecionar um **Idioma**, os idiomas disponíveis na caixa de combinação suspensa serão restringidos a esses para os quais o Modelo de Idioma Semântico dá suporte.|  
  
## <a name="track-changes"></a>Controlar Alterações  
  
|||  
|-|-|  
|**Automático**|O índice de texto completo será atualizado automaticamente quando os dados da tabela subjacente forem alterados, adicionados ou excluídos.|  
|**Manual**|Se os dados forem modificados, adicionados ou excluídos dos dados indexados, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] controlará as alterações. Se o controle de alteração **Manual** estiver em vigor, o índice não será atualizado automaticamente com essas alterações. Em vez disso, um administrador pode se aplicam as alterações manualmente usando um [ALTER FULLTEXT INDEX... START UPDATE POPULATION](/sql/t-sql/statements/alter-fulltext-index-transact-sql) instrução.|  
|**Não controlar alterações**|Com essa opção em vigor, as alterações feitas nos dados indexados do catálogo não são registradas. O administrador deve criar o índice usando ALTER FULLTEXT INDEX com FULL POPULATION ou INCREMENTAL POPULATION.|  
  
## <a name="see-also"></a>Consulte também  
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)   
 [Popular índices de texto completo](../relational-databases/indexes/indexes.md)  
  
  
