---
title: Salvar resultados de rastreamento em um arquivo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 74f80667-62f3-4e14-bb1a-f0c2b6ef3402
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1506c13655187ad29d27f96f5fa1b73d01f67620
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846822"
---
# <a name="save-trace-results-to-a-file"></a>Salvar resultados de rastreamento em um arquivo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você pode salvar os resultados de rastreamentos em um arquivo. Um arquivo de rastreamento é um arquivo no qual são gravados os resultados de um rastreamento. Um arquivo de rastreamento pode estar localizado em um diretório local (como C:\\*foldername*\\*filename.trc*) ou em um diretório de rede (como \\\computername\sharename\filename.trc).  
  
 É possível usar os arquivos de rastreamento para o seguinte:  
  
-   Repetir rastreamentos  
  
-   Auditar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Conduzir análises de desempenho  
  
-   Correlacionar eventos de rastreamento com contadores de desempenho para aperfeiçoar a detecção de problemas  
  
-   Executar análises do Orientador de Otimização do Mecanismo de Banco de Dados  
  
-   Efetuar otimização de consultas  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] salva os resultados de rastreamento em um arquivo quando são especificados um caminho e um nome de arquivo para o argumento **\@tracefile** do procedimento armazenado **sp_trace_create**.  
  
> [!NOTE]  
>  Se for especificado um caminho para que o procedimento armazenado **sp_trace_create** para salvar o arquivo de rastreamento, o diretório deverá estar acessível ao servidor. Esteja ciente, ainda, de que, se for especificado um diretório local para **sp_trace_create**, terá de ser um diretório local no computador do servidor.  
  
 Se o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] for usado, ele permitirá salvar os resultados do rastreamento em um arquivo ou em uma tabela. Salvar resultados de rastreamento em uma tabela permite o mesmo acesso que salvá-los em um arquivo, com o adicional de que a tabela poderá ser consultada quanto a eventos específicos.  
  
 Para obter mais informações sobre como salvar os resultados do rastreamento, veja [Salvar resultados de rastreamento em uma tabela &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md) e [Salvar resultados de rastreamento em um arquivo &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md).  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [Criar um rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [Criar um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  
