---
title: Banco de dados msdb | Microsoft Docs
ms.custom: ''
ms.date: 11/10/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, msdb database
- alerts [SQL Server], msdb database
- jobs [SQL Server], msdb database
- msdb database [SQL Server]
ms.assetid: 5032cb2d-65a0-40dd-b569-4dcecdd58ceb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cee4c5d802447488930ffd04d698edcd2015e86b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871691"
---
# <a name="msdb-database"></a>Banco de dados msdb
  O banco de dados **msdb** é usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para agendar alertas e trabalhos e por outros recursos, como o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[ssSB](../../includes/sssb-md.md)] e o Database Mail.  
  
 Por exemplo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém automaticamente um histórico de backup e restauração online completo nas tabelas no **msdb**. Estas informações incluem o nome da parte que executou o backup, a hora do backup, e os dispositivos ou arquivos onde o backup é armazenado. O[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa essas informações para propor um plano de restauração de um banco de dados e aplicar qualquer backup de log de transações. Os eventos de backup de todos os bancos de dados são registrados, mesmo que tenham sido criados com aplicativos personalizados ou ferramentas de terceiros. Por exemplo, se você usar um aplicativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que chama objetos SMO (SQL Server Management Objects) para executar operações de backup, o evento será registrado nas tabelas do sistema **msdb** , no log de aplicativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para ajudar a proteger as informações armazenadas no **msdb**, recomendamos que você considere a colocação do log de transações **msdb** no repositório tolerante a falhas.  
  
 Por padrão, **msdb** usa o modelo de recuperação simples. Se você usar as tabelas de [histórico de backup e restauração](../backup-restore/backup-history-and-header-information-sql-server.md), será recomendável utilizar o modelo de recuperação completa para **msdb**. Para obter mais informações, veja [Modelos de recuperação &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md). Observe que, quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalado ou atualizado e sempre que Setup.exe é usado para recriar bancos de dados do sistema, o modelo de recuperação do **msdb** será definido automaticamente como simples.  
  
> [!IMPORTANT]  
>  Após qualquer operação que atualize **msdb**, como o backup ou a restauração de um banco de dados, será recomendável fazer backup do **msdb**. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="physical-properties-of-msdb"></a>Propriedades físicas de msdb  
 A tabela a seguir lista os valores iniciais de configuração dos dados do **msdb** e dos arquivos de log. Os tamanhos desses arquivos podem variar um pouco em diferentes edições do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
|Arquivo|Nome lógico|Nome físico|Aumento do arquivo|  
|----------|------------------|-------------------|-----------------|  
|Dados primários|MSDBData|MSDBData.mdf|Aumento automático de 10 por cento até que o disco fique cheio.|  
|Log|MSDBLog|MSDBLog.ldf|Aumento automático de 10 por cento para um máximo de 2 terabytes.|  
  
 Para mover os dados e arquivos de log de **msdb** , veja [Mover bancos de dados do sistema](move-system-databases.md).  
  
### <a name="database-options"></a>Opções de banco de dados  
 A tabela a seguir lista o valor padrão de cada opção de banco de dados no banco de dados **msdb** e se a opção pode ser modificada. Para exibir as configurações atuais dessas opções, use a exibição de catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) .  
  
|Opção de banco de dados|Valor padrão|Pode ser modificado|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|ON|Não|  
|ANSI_NULL_DEFAULT|OFF|Sim|  
|ANSI_NULLS|OFF|Sim|  
|ANSI_PADDING|OFF|Sim|  
|ANSI_WARNINGS|OFF|Sim|  
|ARITHABORT|OFF|Sim|  
|AUTO_CLOSE|OFF|Sim|  
|AUTO_CREATE_STATISTICS|ON|Sim|  
|AUTO_SHRINK|OFF|Sim|  
|AUTO_UPDATE_STATISTICS|ON|Sim|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sim|  
|CHANGE_TRACKING|OFF|Não|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sim|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sim|  
|CURSOR_DEFAULT|GLOBAL|Sim|  
|Opções de disponibilidade de banco de dados|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|Não<br /><br /> Sim<br /><br /> Sim|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sim|  
|DB_CHAINING|ON|Sim|  
|ENCRYPTION|OFF|Não|  
|NUMERIC_ROUNDABORT|OFF|Sim|  
|PAGE_VERIFY|CHECKSUM|Sim|  
|PARAMETERIZATION|SIMPLE|Sim|  
|QUOTED_IDENTIFIER|OFF|Sim|  
|READ_COMMITTED_SNAPSHOT|OFF|Não|  
|RECOVERY|SIMPLE|Sim|  
|RECURSIVE_TRIGGERS|OFF|Sim|  
|Opções do Service Broker|ENABLE_BROKER|Sim|  
|TRUSTWORTHY|ON|Sim|  
  
 Para obter uma descrição dessas opções de banco de dados, veja [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
## <a name="restrictions"></a>Restrictions  
 As operações a seguir não podem ser executadas no banco de dados **msdb** :  
  
-   Alteração de ordenação. A ordenação padrão é a ordenação do servidor.  
  
-   Descartando o banco de dados.  
  
-   Descartando o usuário **convidado** do banco de dados.  
  
-   Habilitação do Change Data Capture.  
  
-   Participação no espelhamento de banco de dados.  
  
-   Remoção do grupo de arquivos primário, arquivo de dados primário ou arquivo de log.  
  
-   Renomeação do banco de dados ou grupo de arquivos primário.  
  
-   Definindo o banco de dados como OFFLINE.  
  
-   Definindo o banco de dados ou grupo de arquivos primário como READ_ONLY.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Bancos de dados do sistema](system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [Mover arquivos de banco de dados](move-database-files.md)  
  
 [Database Mail](../database-mail/database-mail.md)  
  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
