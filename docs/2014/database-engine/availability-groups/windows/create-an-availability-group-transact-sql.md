---
title: Criar um grupo de disponibilidade (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], creating
ms.assetid: 8b0a6301-8b79-4415-b608-b40876f30066
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 409e2cad9d33c6ac3bc498de6baefa8c252995db
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797681"
---
# <a name="create-an-availability-group-transact-sql"></a>Criar um grupo de disponibilidade (Transact-SQL)
  Este tópico descreve como usar [!INCLUDE[tsql](../../../includes/tsql-md.md)] para criar e configurar um grupo de disponibilidade em instâncias de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] no qual o recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] é habilitado. Um *grupo de disponibilidade* define um conjunto de bancos de dados de usuários que realizará o failover como uma única unidade e um conjunto de parceiros de failover, conhecido como *réplicas de disponibilidade*, que oferece suporte a failover.  
  
> [!NOTE]  
>  Para obter uma introdução aos grupos de disponibilidade, consulte [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  

> [!NOTE]  
>  Como alternativa ao uso do [!INCLUDE[tsql](../../../includes/tsql-md.md)], você pode usar o assistente para Criar Grupo de Disponibilidade ou os cmdlets do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, veja [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md), [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)ou [Criar um grupo de disponibilidade &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 É recomendável que você leia esta seção antes de tentar criar seu primeiro grupo de disponibilidade.  
  
###  <a name="PrerequisitesRestrictions"></a> Pré-requisitos, restrições e recomendações  
  
-   Antes de criar um grupo de disponibilidade, verifique se as instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedam réplicas de disponibilidade residem em um nó diferente do WSFC (Windows Server Failover Clustering), dentro do mesmo cluster de failover do WSFC. Também verifique se cada instância de servidor atende todos os outros pré-requisitos de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para obter mais informações, é altamente recomendável que você leia [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer associação na função de servidor fixa **sysadmin** e a permissão de servidor CREATE AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou CONTROL SERVER.  
  
###  <a name="SummaryTsqlStatements"></a> Resumo de tarefas e instruções Transact-SQL correspondentes  
 A tabela a seguir lista as tarefas básicas envolvidas na criação e configuração de um grupo de disponibilidade e indica quais instruções do [!INCLUDE[tsql](../../../includes/tsql-md.md)] serão usadas nessas tarefas. As tarefas [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] devem ser executadas na sequência em que são apresentadas na tabela.  
  
|Tarefa|Instrução(ões) Transact-SQL|Onde executar a tarefa **<sup>*</sup>**|  
|----------|----------------------------------|-------------------------------------------|  
|Criar ponto de extremidade de espelhamento de banco de dados (uma vez por instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] )|Criar *ponto* de [extremidade EndpointName](/sql/t-sql/statements/create-endpoint-transact-sql) ... PARA DATABASE_MIRRORING|Executar em cada instância de servidor que não tem ponto de extremidade de espelhamento de banco de dados.|  
|Criar grupo de disponibilidade|[CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)|Execute na instância de servidor que deve hospedar a réplica primária inicial.|  
|Unir a réplica secundária ao grupo de disponibilidade|[ALTER AVAILABILITY GROUP](join-a-secondary-replica-to-an-availability-group-sql-server.md) *group_name* JOIN|Execute em cada instância de servidor que hospeda uma réplica secundária.|  
|Preparar os banco de dados secundários|[BACKUP](/sql/t-sql/statements/backup-transact-sql) e [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql).|Crie backups na instância de servidor que hospeda a réplica primária.<br /><br /> Restaure backups em cada instância de servidor que hospeda uma réplica secundária, usando RESTORE WITH NORECOVERY.|  
|Iniciar a sincronização de dados unindo cada banco de dados secundário ao grupo de disponibilidade|[ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-hadr) *database_name* SET HADR AVAILABILITY GROUP = *group_name*|Execute em cada instância de servidor que hospeda uma réplica secundária.|  
  
 **<sup>*</sup>**  Para executar uma determinada tarefa, conecte-se à instância ou instâncias de servidor indicadas.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL para criar e configurar um grupo de disponibilidade  
  
> [!NOTE]  
>  Para obter um procedimento de configuração de exemplo que contém exemplos de código de cada uma dessas instruções do [!INCLUDE[tsql](../../../includes/tsql-md.md)] , veja [Exemplo: configurando um grupo de disponibilidade que usa a Autenticação do Windows](#ExampleConfigAGWinAuth).  
  
1.  Conecte-se à instância de servidor que deve hospedar a réplica primária.  
  
2.  Crie o grupo de disponibilidade usando a instrução [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
3.  Una a nova réplica secundária ao grupo de disponibilidade. Para obter mais informações, consulte [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
4.  Para cada banco de dados do grupo de disponibilidade, crie um banco de dados secundário restaurando backups recentes do banco de dados primário, usando RESTORE WITH NORECOVERY. Para obter mais informações, veja [Exemplo: configurando um grupo de disponibilidade usando a Autenticação do Windows (Transact-SQL)](create-an-availability-group-transact-sql.md), começando pela etapa que restaura o backup do banco de dados.  
  
5.  Una cada novo banco de dados secundário ao grupo de disponibilidade. Para obter mais informações, consulte [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
##  <a name="ExampleConfigAGWinAuth"></a> Exemplo: configurando um grupo de disponibilidade que usa a Autenticação do Windows  
 Esse exemplo cria um procedimento de configuração [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] de exemplo que usa o [!INCLUDE[tsql](../../../includes/tsql-md.md)] para configurar pontos de extremidade de espelhamento de banco de dados que usam a Autenticação do Windows e para criar e configurar um grupo de disponibilidade e seus bancos de dados secundários.  
  
 Esse exemplo contém as seguintes seções:  
  
-   [Pré-requisitos para usar o procedimento de configuração de exemplo](#PrerequisitesForExample)  
  
-   [Procedimento de configuração de exemplo](#SampleProcedure)  
  
-   [Concluir o exemplo de código para procedimento de configuração de exemplo](#CompleteCodeExample)  
  
###  <a name="PrerequisitesForExample"></a> Pré-requisitos para usar o procedimento de configuração de exemplo  
 Este procedimento de exemplo tem os seguintes requisitos:  
  
-   As instâncias de servidor devem oferecer suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para obter mais informações, consulte [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
-   Dois bancos de dados de exemplo, *MyDb1* e *MyDb2*, devem existir na instância de servidor que hospedará a réplica primária. Os exemplos de código a seguir criam e configuram esses dois bancos de dados, e criam um backup completo de cada um deles. Execute esses exemplos de código na instância de servidor na qual você pretende criar o grupo de disponibilidade de exemplo. Essa instância de servidor hospedará a réplica primária inicial do grupo de disponibilidade de exemplo.  
  
    1.  Este exemplo do [!INCLUDE[tsql](../../../includes/tsql-md.md)] cria esses bancos de dados e os alteram para usar o modelo de recuperação completo:  
  
        ```sql
        -- Create sample databases:  
        CREATE DATABASE MyDb1;  
        GO  
        ALTER DATABASE MyDb1 SET RECOVERY FULL;  
        GO  
  
        CREATE DATABASE MyDb2;  
        GO  
        ALTER DATABASE MyDb2 SET RECOVERY FULL;  
        GO  
        ```  
  
    2.  O exemplo de código a seguir cria um backup completo de banco de dados de *MyDb1* e *MyDb2*. Este exemplo de código usa um compartilhamento de backup fictício, \\\\*FILESERVER*\\*SQLbackups*.  
  
        ```sql
        -- Backup sample databases:  
        BACKUP DATABASE MyDb1   
        TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
            WITH FORMAT  
        GO  
  
        BACKUP DATABASE MyDb2   
        TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
            WITH FORMAT  
        GO
        ```  
  
###  <a name="SampleProcedure"></a> Procedimento de configuração de exemplo  
 Nesta configuração de exemplo, a réplica de disponibilidade será criada em duas instâncias de servidor autônomas cujas contas de serviço são executadas em domínios diferentes, porém confiáveis (`DOMAIN1` e `DOMAIN2`).  
  
 A tabela a seguir resume os valores usados nesta configuração de exemplo.  
  
|Função inicial|Sistema|Instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] host|  
|------------------|------------|---------------------------------------------|  
|primary|`COMPUTER01`|`AgHostInstance`|  
|Secundário|`COMPUTER02`|Instância padrão.|  
  
1.  Crie um ponto de extremidade de espelhamento de banco de dados chamado *dbm_endpoint* na instância de servidor em que você pretende criar o grupo de disponibilidade (uma instância denominada `AgHostInstance` em `COMPUTER01`). Esse ponto de extremidade usa a porta 7022. Observe que a instância de servidor na qual você cria o grupo de disponibilidade hospedará a réplica primária.  
  
    ```sql
    -- Create endpoint on server instance that hosts the primary replica:  
    CREATE ENDPOINT dbm_endpoint  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO
    ```  
  
2.  Crie um ponto de extremidade *dbm_endpoint* na instância de servidor que hospedará a réplica secundária (a instância de servidor padrão em `COMPUTER02`). Esse ponto de extremidade usa a porta 5022.  
  
    ```sql
    -- Create endpoint on server instance that hosts the secondary replica:   
    CREATE ENDPOINT dbm_endpoint  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=5022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO
    ```  
  
3.  > [!NOTE]  
    >  Se as contas de serviço das instâncias de servidor que devem hospedar suas réplicas de disponibilidade forem executadas na mesma conta de domínio, esta etapa é desnecessária. Ignore-a e vá diretamente para a próxima etapa.  
  
     Se as contas de serviço das instâncias de servidor forem executadas em usuários de domínio diferentes, em cada instância de servidor, crie um logon para a outra instância de servidor e conceda essa permissão de logon para acessar o ponto de extremidade de espelhamento de banco de dados local.  
  
     O exemplo de código a seguir mostra as instruções do [!INCLUDE[tsql](../../../includes/tsql-md.md)] para criar um logon e conceder a ele a permissão em um ponto de extremidade. A conta de domínio da instância de servidor remoto é representada aqui como *domain_name*\\*user_name*.  
  
    ```sql
    -- If necessary, create a login for the service account, domain_name\user_name  
    -- of the server instance that will host the other replica:  
    USE master;  
    GO  
    CREATE LOGIN [domain_name\user_name] FROM WINDOWS;  
    GO  
    -- And Grant this login connect permissions on the endpoint:  
    GRANT CONNECT ON ENDPOINT::dbm_endpoint   
       TO [domain_name\user_name];  
    GO  
    ```  
  
4.  Na instância de servidor onde os bancos de dados de usuário residem, crie o grupo de disponibilidade.  
  
     O exemplo de código a seguir cria um grupo de disponibilidade chamado *MyAG* na instância de servidor em que os bancos de dados de exemplo, *MyDb1* e *MyDb2*, foram criados. Na `AgHostInstance`COMPUTER01 *, a instância de servidor local* é especificada primeiro. Essa instância hospedará a réplica primária inicial. Uma instância de servidor remota, a instância de servidor padrão em *COMPUTER02*, é especificada para hospedar uma réplica secundária. Ambas as réplicas de disponibilidade são configuradas para usar o modo de confirmação assíncrona com failover manual (para réplicas de confirmação assíncrona, failover manual significa failover forçado com possível perda de dados).  
  
    ```sql
    -- Create the availability group, MyAG:   
    CREATE AVAILABILITY GROUP MyAG   
       FOR   
          DATABASE MyDB1, MyDB2   
       REPLICA ON   
          'COMPUTER01\AgHostInstance' WITH   
             (  
             ENDPOINT_URL = 'TCP://COMPUTER01.Adventure-Works.com:7022',   
             AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
             FAILOVER_MODE = MANUAL  
             ),  
          'COMPUTER02' WITH   
             (  
             ENDPOINT_URL = 'TCP://COMPUTER02.Adventure-Works.com:5022',  
             AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
             FAILOVER_MODE = MANUAL  
             );   
    GO  
    ```  
  
     Para obter mais códigos de exemplo [!INCLUDE[tsql](../../../includes/tsql-md.md)] de criação de um grupo de disponibilidade, veja [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql).  
  
5.  Na instância de servidor que hospeda a réplica secundária, una a réplica secundária ao grupo de disponibilidade.  
  
     O exemplo de código a seguir une a réplica secundária de `COMPUTER02` ao grupo de disponibilidade `MyAG` .  
  
    ```sql
    -- On the server instance that hosts the secondary replica,   
    -- join the secondary replica to the availability group:  
    ALTER AVAILABILITY GROUP MyAG JOIN;  
    GO  
    ```  
  
6.  Na instância de servidor que hospeda a réplica secundária, crie os bancos de dados secundários.  
  
     O exemplo de código a seguir cria os bancos de dados secundários *MyDb1* e *MyDb2* restaurando backups de banco de dados que usam RESTORE WITH NORECOVERY.  
  
    ```sql
    -- On the server instance that hosts the secondary replica,   
    -- Restore database backups using the WITH NORECOVERY option:  
    RESTORE DATABASE MyDb1   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
        WITH NORECOVERY  
    GO  
  
    RESTORE DATABASE MyDb2   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
        WITH NORECOVERY  
    GO
    ```  
  
7.  Na instância de servidor que hospeda a réplica primária, faça backup do log de transações em cada banco de dados primário.  
  
    > [!IMPORTANT]  
    >  Quando você estiver configurando um grupo de disponibilidade real, é recomendável que, antes de fazer esse backup de log, você suspenda as tarefas de backup de log em seus bancos de dados primários até que tenha unido os bancos de dados secundários correspondentes ao grupo de disponibilidade.  
  
     O exemplo de código a seguir cria um backup de log de transações em MyDb1 e MyDb2.  
  
    ```sql
    -- On the server instance that hosts the primary replica,   
    -- Backup the transaction log on each primary database:  
    BACKUP LOG MyDb1   
    TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
        WITH NOFORMAT  
    GO  
  
    BACKUP LOG MyDb2   
    TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
        WITHNOFORMAT  
    GO
    ```  
  
    > [!TIP]  
    >  Normalmente, um backup de log deve ser feito em cada banco de dados primário e restaurado no banco de dados secundário correspondente (usando WITH NORECOVERY). Porém, esse backup de log pode ser desnecessário caso o banco de dados tenha acabado de ser criado e nenhum backup tenha sido feito ou caso o modelo de recuperação tenha sido alterado de SIMPLE para FULL.  
  
8.  Na instância de servidor que hospeda a réplica secundária, aplique backups de log aos bancos de dados secundários.  
  
     O exemplo de código a seguir aplica backups aos bancos de dados secundários *MyDb1* e *MyDb2* restaurando backups de banco de dados que usam RESTORE WITH NORECOVERY.  
  
    > [!IMPORTANT]  
    >  Quando você estiver preparando um banco de dados secundário real, precisará aplicar cada backup de log feito desde o backup de banco de dados do qual criou o banco de dados secundário, começando pelo mais antigo e sempre usando RESTORE WITH NORECOVERY. É claro que, se você restaurar os backups de banco de dados completo e diferencial, precisará apenas aplicar os backups de log feitos após o backup diferencial.  
  
    ```sql
    -- Restore the transaction log on each secondary database,  
    -- using the WITH NORECOVERY option:  
    RESTORE LOG MyDb1   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    RESTORE LOG MyDb2   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    ```  
  
9. Na instância de servidor que hospeda a réplica secundária, una os novos bancos de dados secundários ao grupo de disponibilidade.  
  
     O exemplo de código a seguir une o banco de dados secundário *MyDb1* e, em seguida, os bancos de dados secundários *MyDb2* ao grupo de disponibilidade *MyAG* .  
  
    ```sql
    -- On the server instance that hosts the secondary replica,   
    -- join each secondary database to the availability group:  
    ALTER DATABASE MyDb1 SET HADR AVAILABILITY GROUP = MyAG;  
    GO  
  
    ALTER DATABASE MyDb2 SET HADR AVAILABILITY GROUP = MyAG;  
    GO
    ```  
  
###  <a name="CompleteCodeExample"></a> Concluir o exemplo de código para procedimento de configuração de exemplo  
 O exemplo a seguir mescla os exemplos de código de todas as etapas do procedimento de configuração de exemplo. A tabela a seguir resumiu os valores de espaço reservado usados neste exemplo de código. Para obter mais informações sobre as etapas deste exemplo de código, consulte [Pré-requisitos para usar o procedimento de configuração de exemplo](#PrerequisitesForExample) e [Procedimento de configuração de exemplo](#SampleProcedure), anteriormente neste tópico.  
  
|Espaço reservado|Description|  
|-----------------|-----------------|  
|\\\\*FILESERVER*\\*SQLbackups*|Compartilhamento de backup ficcional.|  
|\\\\*FILESERVER*\\*SQLbackups\MyDb1.bak*|Arquivo de backup de MyDb1.|  
|\\\\*FILESERVER*\\*SQLbackups\MyDb2.bak*|Arquivo de backup de MyDb2.|  
|*7022*|Número de porta atribuído a cada ponto de extremidade de espelhamento de banco de dados.|  
|*COMPUTER01\AgHostInstance*|Instância de servidor que hospeda a réplica primária inicial.|  
|*COMPUTER02*|Instância de servidor que hospeda a réplica secundária inicial. Essa é a instância de servidor padrão em `COMPUTER02`.|  
|*dbm_endpoint*|Nome especificado para cada ponto de extremidade de espelhamento de banco de dados.|  
|*MyAG*|Nome do grupo de disponibilidade de exemplo.|  
|*MyDb1*|Nome do primeiro banco de dados de exemplo.|  
|*MyDb2*|Nome do segundo banco de dados de exemplo.|  
|*DOMAIN1\user1*|Conta de serviço da instância de servidor que deve hospedar a réplica primária inicial.|  
|*DOMAIN2\user2*|Conta de serviço da instância de servidor que deve hospedar a réplica secundária inicial.|  
|TCP://*COMPUTER01.Adventure-Works.com*:*7022*|URL de ponto de extremidade da instância AgHostInstance do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em COMPUTER01.|  
|TCP://*COMPUTER02.Adventure-Works.com*:*5022*|URL de ponto de extremidade da instância padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em COMPUTER02.|  
  
> [!NOTE]  
>  Para obter mais códigos de exemplo [!INCLUDE[tsql](../../../includes/tsql-md.md)] de criação de um grupo de disponibilidade, veja [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql).  
  
```sql
-- on the server instance that will host the primary replica,   
-- create sample databases:  
CREATE DATABASE MyDb1;  
GO  
ALTER DATABASE MyDb1 SET RECOVERY FULL;  
GO  
  
CREATE DATABASE MyDb2;  
GO  
ALTER DATABASE MyDb2 SET RECOVERY FULL;  
GO  
  
-- Backup sample databases:  
BACKUP DATABASE MyDb1   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH FORMAT  
GO  
  
BACKUP DATABASE MyDb2   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITH FORMAT  
GO  
  
-- Create the endpoint on the server instance that will host the primary replica:  
CREATE ENDPOINT dbm_endpoint  
    STATE=STARTED   
    AS TCP (LISTENER_PORT=7022)   
    FOR DATABASE_MIRRORING (ROLE=ALL)  
GO  
  
-- Create the endpoint on the server instance that will host the secondary replica:   
CREATE ENDPOINT dbm_endpoint  
    STATE=STARTED   
    AS TCP (LISTENER_PORT=7022)   
    FOR DATABASE_MIRRORING (ROLE=ALL)  
GO  
  
-- If both service accounts run under the same domain account, skip this step. Otherwise,   
-- On the server instance that will host the primary replica,   
-- create a login for the service account   
-- of the server instance that will host the secondary replica, DOMAIN2\user2,   
-- and grant this login connect permissions on the endpoint:  
USE master;  
GO  
CREATE LOGIN [DOMAIN2\user2] FROM WINDOWS;  
GO  
GRANT CONNECT ON ENDPOINT::dbm_endpoint   
   TO [DOMAIN2\user2];  
GO  
  
-- If both service accounts run under the same domain account, skip this step. Otherwise,   
-- On the server instance that will host the secondary replica,  
-- create a login for the service account   
-- of the server instance that will host the primary replica, DOMAIN1\user1,   
-- and grant this login connect permissions on the endpoint:  
USE master;  
GO  
  
CREATE LOGIN [DOMAIN1\user1] FROM WINDOWS;  
GO  
GRANT CONNECT ON ENDPOINT::dbm_endpoint   
   TO [DOMAIN1\user1];  
GO  
  
-- On the server instance that will host the primary replica,   
-- create the availability group, MyAG:  
CREATE AVAILABILITY GROUP MyAG   
   FOR   
      DATABASE MyDB1, MyDB2   
   REPLICA ON   
      'COMPUTER01\AgHostInstance' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER01.Adventure-Works.com:7022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC  
         ),  
      'COMPUTER02' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER02.Adventure-Works.com:7022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC  
         );   
GO  
  
-- On the server instance that hosts the secondary replica,   
-- join the secondary replica to the availability group:  
ALTER AVAILABILITY GROUP MyAG JOIN;  
GO  
  
-- Restore database backups onto this server instance, using RESTORE WITH NORECOVERY:  
RESTORE DATABASE MyDb1   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH NORECOVERY  
GO  
  
RESTORE DATABASE MyDb2   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITH NORECOVERY  
GO  
  
-- Back up the transaction log on each primary database:  
BACKUP LOG MyDb1   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH NOFORMAT  
GO  
  
BACKUP LOG MyDb2   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITHNOFORMAT  
GO  
  
-- Restore the transaction log on each secondary database,  
-- using the WITH NORECOVERY option:  
RESTORE LOG MyDb1   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH FILE=1, NORECOVERY  
GO  
RESTORE LOG MyDb2   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITH FILE=1, NORECOVERY  
GO  
  
-- On the server instance that hosts the secondary replica,   
-- join each secondary database to the availability group:  
ALTER DATABASE MyDb1 SET HADR AVAILABILITY GROUP = MyAG;  
GO  
  
ALTER DATABASE MyDb2 SET HADR AVAILABILITY GROUP = MyAG;  
GO
```  
  
##  <a name="RelatedTasks"></a> Tarefas Relacionadas  
 **Para configurar um grupo de disponibilidade e propriedades de réplica**  
  
-   [Alterar o modo de disponibilidade de uma réplica de disponibilidade &#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [Alterar o modo de failover de uma réplica de disponibilidade &#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Configurar a política de failover flexível para controlar condições de failover automático (Grupos de Disponibilidade AlwaysOn)](configure-flexible-automatic-failover-policy.md)  
  
-   [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Alterar o período de tempo limite da sessão de uma réplica de disponibilidade &#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **Para concluir a configuração do grupo de disponibilidade**  
  
-   [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **Maneiras alternativas de criar um grupo de disponibilidade**  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Criar um grupo de disponibilidade &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
 **Para habilitar Grupos de Disponibilidade AlwaysOn**  
  
-   [Habilitar e desabilitar grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **Para configurar um ponto de extremidade de espelhamento de banco de dados**  
  
-   [Criar um ponto de extremidade de espelhamento &#40;de banco de dados para grupos de disponibilidade AlwaysOn SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **Para solucionar problemas de configuração Grupos de Disponibilidade AlwaysOn**  
  
-   [Solução de problemas de configuração de Grupos de Disponibilidade AlwaysOn (SQL Server) excluída](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [Solucionar problemas de uma operação &#40;de adição de arquivo com falha grupos de disponibilidade AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Blogs:**  
  
     [Série de aprendizado AlwaysON-HADRON: uso do pool de trabalho para bancos de dados habilitados para HADRON](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [Blogs da equipe do SQL Server AlwaysOn: o blog oficial da equipe do SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **Vídeos:**  
  
     [Microsoft SQL Server o codinome "Denali" da série AlwaysOn, parte 1: apresentando a próxima geração de solução de alta disponibilidade](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server o codinome "Denali" da série AlwaysOn, parte 2: criando uma solução de alta disponibilidade de missão crítica usando o AlwaysOn](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Whitepapers:**  
  
     [Guia de soluções do Microsoft SQL Server AlwaysOn para alta disponibilidade e recuperação de desastres](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [White papers da Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [White papers da equipe de consultoria do cliente do SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Consulte Também  
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Visão geral do &#40;grupos de disponibilidade AlwaysOn&#41; SQL Server](overview-of-always-on-availability-groups-sql-server.md)    
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativos &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
