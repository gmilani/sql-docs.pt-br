---
title: Fazer backup e restaurar um banco de dados usando o Studio de dados do Azure | Microsoft Docs
description: Saiba como fazer backup e restaurar um banco de dados usando o Studio de dados do Azure
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b687c05e591e78b836a18c192828cca4fe7f97fa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "48037683"
---
# <a name="backup-and-restore-using-includename-sosincludesname-sos-shortmd"></a>Backup e restauração usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Neste tutorial, você aprenderá a usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para:
> [!div class="checklist"]
> * Fazer backup de um banco de dados 
> * Exibir o status do backup
> * Gerar o script usado para realizar o backup
> * Restaurar um banco de dados
> * Exibir o status da tarefa de restauração

## <a name="prerequisites"></a>Prerequisites

Este tutorial requer o SQL Server *TutorialDB*. Para criar o *TutorialDB* banco de dados, conclua um dos seguintes inícios rápidos:

- [Conectar e consultar usando SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)


## <a name="backup-a-database"></a>Fazer backup de um banco de dados

1. Abra o painel de banco de dados TutorialDB (Abra o **servidores** barra lateral (**CTRL + G**), expanda **bancos de dados**, clique com botão direito **TutorialDB**, e selecione **gerenciar**). 

2. Abra o **banco de dados de Backup** caixa de diálogo (clique em **Backup** no **tarefas** widget).

   ![Widget de tarefas](./media/tutorial-backup-restore-sql-server/tasks.png)

3. Este tutorial usa as opções de backup padrão, clique em **Backup**.
   ![caixa de diálogo backup](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

Depois de clicar em **Backup**, o **banco de dados de Backup** caixa de diálogo desaparece e começa o processo de backup.

## <a name="view-the-backup-status-and-view-the-backup-script"></a>Exibir o status do backup e exibir o script de backup

1. Abra o **histórico de tarefa** barra lateral, clicando no ícone de relógio na *barra de ação* ou pressione **CTRL + T**.

   ![Histórico de tarefas](./media/tutorial-backup-restore-sql-server/task-history.png)

2. Para exibir o script de backup no editor, clique com botão direito **banco de dados de Backup foi bem-sucedido** e selecione **Script**.

   ![script de backup](./media/tutorial-backup-restore-sql-server/task-script.png) 

## <a name="restore-a-database-from-a-backup-file"></a>Restaurar um banco de dados de um arquivo de backup


1. Abra o **servidores** barra lateral (**CTRL + G**), seu servidor com o botão direito e selecione **gerenciar**. 

2. Abra o **restaurar banco de dados** caixa de diálogo (clique em **restaurar** no **tarefas** widget).

2. Selecione **arquivo de Backup** na **restaurar a partir de** campo. 

3. Clique nas reticências (...) na **caminho do arquivo de Backup** campo e, em seguida, selecione o arquivo de backup mais recente para *TutorialDB*.

3. Tipo de **TutorialDB_Restored** na **banco de dados de destino** campo o **destino** seção para restaurar o arquivo de backup para um novo banco de dados.

   ![restaurar](./media/tutorial-backup-restore-sql-server/restore.png)

4. Clique em **restaurar**

5. Para exibir o status da operação de restauração, pressione **CTRL + T** para abrir o **histórico de tarefa** barra lateral.

   ![restaurar](./media/tutorial-backup-restore-sql-server/task-history-restore.png)


Neste tutorial, você aprendeu como:
> [!div class="checklist"]
> * Fazer backup de um banco de dados 
> * Exibir o status do backup
> * Gerar o script usado para realizar o backup
> * Restaurar um banco de dados
> * Exibir o status da tarefa de restauração
