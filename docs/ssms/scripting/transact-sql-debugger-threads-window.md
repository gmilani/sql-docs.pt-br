---
title: Janela Threads
titleSuffix: T-SQL Debugger
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Threads Window [Transact-SQL]
ms.assetid: e153f619-0049-4162-9076-c24a454f3278
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ba4f72bc5848f14e2bfd9821c43f024a129092e1
ms.sourcegitcommit: add39e028e919df7d801e8b6bb4f8ac877e60e17
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2019
ms.locfileid: "74119237"
---
# <a name="transact-sql-debugger---threads-window"></a>Depurador do Transact-SQL – janela Threads

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A janela **Threads** exibe informações sobre o thread do [!INCLUDE[ssDE](../../includes/ssde-md.md)] usado antes da sessão do Editor de Consultas [!INCLUDE[ssDE](../../includes/ssde-md.md)] que está sendo depurada. Você deve estar no modo de depuração para exibir as informações sobre thread.  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>Lista de Tarefas

**Para acessar a janela Threads**
  
-   No menu **Depurar** , clique em **Janelas**e em **Threads**.  
  
## <a name="columns"></a>Colunas  
 **ID**  
 É um número de identificação exclusiva que o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] atribui ao thread. Você pode localizar mais informações sobre o thread selecionando uma linha da exibição de gerenciamento dinâmico sys.dm_os_threads.  
  
 Se você não estiver executando em modo lightweight pooling, selecione a linha na qual o valor em os_thread_id corresponde ao valor da coluna **ID** . Se você estiver executando em modo lightweight pooling, selecione a linha na qual o valor em fiber_context_address corresponde ao valor na coluna **ID** .  
  
 **Nome**  
 Exibe informações sobre a sessão do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no formato **ComputerName/InstanceName [SPID]** .  
  
 **ComputerName**  
 O nome do computador que está executando a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ao qual a sessão do Editor de Consultas está conectada.  
  
 **InstanceName**  
 O nome da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] à qual a sessão do Editor de Consultas está conectada.  
  
 **[SPID]**  
 A sessão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processa a ID que identifica com exclusividade esta sessão. Você pode obter mais informações sobre a sessão selecionando a linha da exibição sys.sysprocesses que tem o mesmo valor na coluna spid.  
  
 **Local**  
 Exibe o nome do arquivo de script usado pela sessão em depuração do Editor de Consultas.  
  
 **Prioridade**  
 O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] não dá suporte a este recurso.  
  
 **Suspend**  
 O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] não dá suporte a este recurso.  
  
## <a name="see-also"></a>Consulte Também  
 [Depurador do Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Informações do depurador Transact-SQL](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [sys.dm_os_threads &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)   
 [sys.sysprocesses &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)  
