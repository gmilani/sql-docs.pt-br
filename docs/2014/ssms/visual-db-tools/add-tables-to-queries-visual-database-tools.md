---
title: Adicionar tabelas a consultas (Ferramentas de Banco de Dados Visual) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting tables
- adding tables
- queries [SQL Server], tables
ms.assetid: 6551aa7e-31a1-4636-852a-819bc53d658b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ba3957eb5b0c88396376d615033107b13d0621ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63297863"
---
# <a name="add-tables-to-queries-visual-database-tools"></a>Adicionar tabelas a consultas (Visual Database Tools)
  Quando você cria uma consulta, está recuperando dados de uma tabela ou outros objetos estruturados como tabelas – exibições e determinadas funções definidas pelo usuário. Para trabalhar com qualquer um desses objetos em sua consulta, adicione-os ao **Painel Diagrama**.  
  
### <a name="to-add-a-table-or-table-valued-object-to-a-query"></a>Para adicionar uma tabela ou objeto com valor de tabela a uma consulta  
  
1.  No **painel Diagrama** do Designer de Consulta e Exibição, clique com o botão direito do mouse na tela de fundo e escolha **Adicionar Tabela** no menu de atalho.  
  
2.  Na caixa de diálogo **Adicionar Tabela** , selecione a guia do tipo de objeto que deseja adicionar à consulta.  
  
3.  Na lista de itens, clique duas vezes em cada item que deseja adicionar.  
  
4.  Quando terminar de adicionar os itens, clique em **Fechar**.  
  
     O Designer de Consulta e Exibição atualiza adequadamente o **Painel Diagrama**, o **Painel Critérios**e o **Painel SQL** .  
  
 As tabelas e as exibições são adicionadas automaticamente à consulta quando você as referencia na instrução do painel SQL.  
  
 O Designer de Consulta e Exibição não exibirá as colunas de dados de uma tabela ou objeto com estrutura de tabela se você não tiver direitos de acesso suficientes ou se o provedor não puder retornar informações sobre as mesmas. Nesses casos, serão exibidas apenas a barra de título e a caixa de seleção * (Todas as Colunas) para a tabela ou objeto com valor de tabela.  
  
### <a name="to-add-an-existing-query-to-a-new-query"></a>Para adicionar uma consulta existente a uma nova consulta  
  
1.  Verifique se o **Painel SQL** é exibido na nova consulta que está sendo criada.  
  
2.  No **Painel SQL**, digite um parêntese direito e esquerdo () depois da palavra FROM.  
  
3.  Abra o Designer de Consulta para a consulta existente. (Agora você tem dois Designers de Consulta abertos.)  
  
4.  Exiba o **Painel SQL** para a consulta interna – a consulta existente que você está incluindo na nova consulta externa.  
  
5.  Selecione todo o texto no **Painel SQL**e copie para a Área de Transferência.  
  
6.  Clique no **Painel SQL** da consulta nova, posicione o cursor entre os parênteses que você adicionou e cole o conteúdo da Área de Transferência.  
  
7.  Ainda no **Painel SQL**, adicione um alias depois do parêntese direito.  
  
## <a name="see-also"></a>Consulte também  
 [Criar Aliases de tabela &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Remover tabelas de consultas &#40;Visual Database Tools&#41;](remove-tables-from-queries-visual-database-tools.md)   
 [Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)   
 [Resumir resultados da consulta &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [Executar operações básicas com consultas &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
