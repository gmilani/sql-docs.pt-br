---
title: Criar relações entre tabelas em um diagrama (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- diagrams [SQL Server], designing
ms.assetid: 28e9630c-dff4-46cc-bb0e-fe77998b6ac2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab36ebfefbfd3d8cee8e6da7caadf86eb4a10032
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63184272"
---
# <a name="create-relationships-between-tables-on-a-diagram-visual-database-tools"></a>Criar relações entre tabelas em um diagrama (Visual Database Tools)
  Você pode criar relações entre colunas em tabelas diferentes no Designer de Diagrama arrastando colunas entre tabelas.  
  
### <a name="to-create-a-relationship-graphically"></a>Para criar uma relação graficamente  
  
1.  No Designer de Banco de Dados, clique no seletor de linha de uma ou mais colunas do banco de dados que você quer relacionar a uma coluna em outra tabela.  
  
2.  Arraste as colunas selecionadas para a tabela relacionada.  
  
3.  Duas caixas de diálogo são exibidas: **Relação de Chaves Estrangeiras** e **Tabelas e Colunas**, com a última aparecendo no primeiro plano.  
  
4.  **Nome da relação** tem um nome fornecido pelo sistema no formato FK_*localtable*_*foreigntable*. Você pode alterar esse valor.  
  
5.  Verifique se a **Tabela de chaves primárias** especifica a tabela correta.  
  
6.  A grade lista as colunas locais e as suas colunas estrangeiras correspondentes. Você pode adicionar ou remover colunas de tabela ou alterar mapeamentos.  
  
7.  Escolha **OK**.  
  
     A caixa de diálogo **Relação de Chaves Estrangeiras** é exibida. **Relação Selecionada** mostra a relação que você criou.  
  
8.  Altere as propriedades da relação na grade.  
  
9. Escolha **OK** para criar a relação.  
  
     O Designer de Banco de Dados mostra uma relação entre as colunas que você escolheu.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo de colunas e tabelas &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [As restrições UNIQUE e restrições de verificação](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [Trabalhar com tabelas no diagrama de banco de dados &#40;Visual Database Tools&#41;](work-with-tables-in-database-diagram-visual-database-tools.md)  
  
  
