---
title: Extensão de SQL Server Agent
titleSuffix: Azure Data Studio
description: Instale e use a extensão de SQL Server Agent (versão prévia) para o Azure Data Studio
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 05356cc815fdba22d55ee339d60994f2c9423373
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959184"
---
# <a name="sql-server-agent-extension-preview"></a>Extensão de SQL Server Agent (versão prévia)

A extensão de SQL Server Agent (versão prévia) é uma extensão para gerenciar e solucionar problemas de trabalhos e configuração do SQL Agent. Esta extensão está em versão prévia.

As principais ações incluem:
- Listar trabalhos do SQL Server Agent configurados em um SQL Server
- Exibir o histórico de trabalhos com os resultados da execução do trabalho
- Controle de trabalho básico para iniciar e parar trabalhos

## <a name="install-the-sql-server-agent-extension"></a>Instalar a extensão de SQL Server Agent

1. Para abrir o gerenciador de extensões e acessar as extensões disponíveis, selecione o ícone de extensões ou selecione **Extensões** no menu **Exibir**.
2. Selecione uma extensão disponível para exibir os detalhes.

   ![Instalar o agente](media/extensions/sql-server-agent-extension/install-sql-agent.png)

1. Selecione a extensão que você deseja e **Instale**-a.
2. Selecione **Recarregar** para habilitar a extensão (necessário apenas na primeira vez que você instala uma extensão).
1. Navegue até o painel de gerenciamento clicando com o botão direito do mouse no servidor ou no banco de dados e selecionando **Gerenciar**.
2. As extensões instaladas aparecem como guias no painel de gerenciamento:

   ![Exibir o agente](media/extensions/sql-server-agent-extension/view-sql-agent.png)

## <a name="view-jobs"></a>Exibir trabalhos

Quando você se conecta à extensão de SQL Server Agent, a primeira coisa que vê é uma lista de todos os seus trabalhos do Agent.

   ![Exibir trabalhos](media/extensions/sql-server-agent-extension/job-view.png)

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o SQL Server Agent, [confira nossa documentação](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent?view=sql-server-2017).


