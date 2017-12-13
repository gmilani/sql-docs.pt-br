---
title: sp_adddistributiondb (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_adddistributiondb_TSQL
- sp_adddistributiondb
helpviewer_keywords: sp_adddistributiondb
ms.assetid: e9bad56c-d2b3-44ba-a4d7-ff2fd842e32d
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6657074bade1db3cb050d6ca0c33e358d05e5f0c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spadddistributiondb-transact-sql"></a>sp_adddistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um novo banco de dados de distribuição e instala o esquema de Distribuição. O banco de dados de distribuição armazena procedimentos, esquema e metadados usados em replicação. Esse procedimento armazenado é executado no Distribuidor, no banco de dados mestre, para criar o banco de dados de distribuição e instalar as tabelas necessárias e os procedimentos armazenados requeridos para habilitar a distribuição da aplicação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_adddistributiondb [ @database= ] 'database'   
    [ , [ @data_folder= ] 'data_folder' ]   
    [ , [ @data_file= ] 'data_file' ]   
    [ , [ @data_file_size= ] data_file_size ]   
    [ , [ @log_folder= ] 'log_folder' ]   
    [ , [ @log_file= ] 'log_file' ]   
    [ , [ @log_file_size= ] log_file_size ]   
    [ , [ @min_distretention= ] min_distretention ]   
    [ , [ @max_distretention= ] max_distretention ]   
    [ , [ @history_retention= ] history_retention ]   
    [ , [ @security_mode= ] security_mode ]   
    [ , [ @login= ] 'login' ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @createmode= ] createmode ]  
    [ , [ @from_scripting = ] from_scripting ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@database=**] *banco de dados '*  
 É o nome do banco de dados de distribuição a ser criado. *banco de dados* é **sysname**, sem padrão. Se o banco de dados especificado já existir e não estiver marcado como banco de dados de distribuição, os objetos necessários para habilitar a distribuição serão instalados e o banco de dados será marcado como banco de dados de distribuição. Se o banco de dados especificado já estiver habilitado como um banco de dados de distribuição, um erro será retornado.  
  
 [  **@data_folder=**] **'***data_folder'*  
 É o nome do diretório usado para armazenar o arquivo de dados do banco de dados de distribuição. *data_folder* é **nvarchar (255)**, com um padrão NULL. Se for NULL, o diretório de dados para aquela instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será usado, por exemplo, `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data`.  
  
 [  **@data_file=**] **'***data_file***'**  
 É o nome do arquivo de banco de dados. *data_file* é **nvarchar (255)**, com um padrão de **banco de dados**. Se for NULL, o procedimento armazenado cria um nome de arquivo usando o nome de banco de dados.  
  
 [  **@data_file_size=**] *data_file_size*  
 É o tamanho de arquivo de dados inicial em megabytes (MB). *data_file_size,*s **int**, com um padrão de 5 MB.  
  
 [  **@log_folder=**] **'***log_folder***'**  
 É o nome do diretório para o arquivo de log de banco de dados. *log_folder* é **nvarchar (255)**, com um padrão NULL. Se for NULL, o diretório de dados para aquela instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será usado (por exemplo, `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data`).  
  
 [  **@log_file=**] **'***Arquivo_de_log***'**  
 É o nome do arquivo de log. *Arquivo_de_log* é **nvarchar (255)**, com um padrão NULL. Se for NULL, o procedimento armazenado cria um nome de arquivo usando o nome de banco de dados.  
  
 [  **@log_file_size=**] *log_file_size*  
 É o tamanho do arquivo de log inicial em megabytes (MB). *log_file_size* é **int**, com um padrão de 0 MB, o que significa que o tamanho do arquivo é criado usando o log de menor arquivo tamanho permitido pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [  **@min_distretention=**] *min_distretention*  
 É o período de retenção mínimo, em horas, antes de as transações serem excluídas do banco de dados de distribuição. *min_distretention* é **int**, com um padrão de 0 horas.  
  
 [  **@max_distretention=**] *max_distretention*  
 É o período máximo de retenção, em horas, antes que as transações sejam excluídas. *max_distretention* é **int**, com um padrão de 72 horas. Assinaturas que não receberam comandos replicados mais antigos do que o período máximo de retenção de distribuição são marcadas como inativas e precisam ser reiniciadas. RAISERROR 21011 é emitido para cada assinatura inativa. Um valor de **0** significa que transações replicadas não é armazenadas no banco de dados de distribuição.  
  
 [  **@history_retention=**] *history_retention*  
 É o número de horas para retenção do histórico. *history_retention* é **int**, com um padrão de 48 horas.  
  
 [  **@security_mode=**] *security_mode*  
 É o modo de segurança a ser usado ao conectar-se a um Distribuidor. *security_mode* é **int**, com um padrão de 1. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação; **1** Especifica autenticação integrada do Windows.  
  
 [  **@login=**] **'***login***'**  
 É o nome de logon usado ao conectar ao Distribuidor para criar o banco de dados de distribuição. Isso é necessário se *security_mode* é definido como **0**. *logon* é **sysname**, com um padrão NULL.  
  
 [  **@password=**] **'***senha***'**  
 É a senha usada ao conectar ao Distribuidor. Isso é necessário se *security_mode* é definido como **0**. *senha* é **sysname**, com um padrão NULL.  
  
 [  **@createmode=**] *createmode*  
 *createmode* é **int**, com um padrão de 1, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**1** (padrão)|Criar banco de dados ou usar existente do banco de dados e, em seguida, aplicar **instdist.sql** para criar objetos de replicação no banco de dados de distribuição.|  
|**2**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 [  **@from_scripting =** ] *from_scripting*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_adddistributiondb** é usado em todos os tipos de replicação. Porém, esse procedimento armazenado só é executado em um distribuidor.  
  
 Você deve configurar o distribuidor executando [sp_adddistributor](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) antes de executar **sp_adddistributiondb**.  
  
 Executar **sp_adddistributor** antes da execução de **sp_adddistributiondb**.  
  
## <a name="example"></a>Exemplo  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Install the Distributor and the distribution database.  
DECLARE @distributor AS sysname;  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @directory AS nvarchar(500);  
DECLARE @publicationDB AS sysname;  
-- Specify the Distributor name.  
SET @distributor = $(DistPubServer);  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
-- Specify the replication working directory.  
SET @directory = N'\\' + $(DistPubServer) + '\repldata';  
-- Specify the publication database.  
SET @publicationDB = N'AdventureWorks2012';   
  
-- Install the server MYDISTPUB as a Distributor using the defaults,  
-- including autogenerating the distributor password.  
USE master  
EXEC sp_adddistributor @distributor = @distributor;  
  
-- Create a new distribution database using the defaults, including  
-- using Windows Authentication.  
USE master  
EXEC sp_adddistributiondb @database = @distributionDB,   
    @security_mode = 1;  
GO  
  
-- Create a Publisher and enable AdventureWorks2012 for replication.  
-- Add MYDISTPUB as a publisher with MYDISTPUB as a local distributor  
-- and use Windows Authentication.  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
  
USE [distribution]  
EXEC sp_adddistpublisher @publisher=@publisher,   
    @distribution_db=@distributionDB,   
    @security_mode = 1;  
GO  
  
```  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_adddistributiondb**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistributiondb &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)  
  
  