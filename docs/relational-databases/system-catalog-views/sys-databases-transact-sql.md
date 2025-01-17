---
title: sys. databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- databases
- databases_TSQL
- sys.databases
- sys.databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.databases catalog view
ms.assetid: 46c288c1-3410-4d68-a027-3bbf33239289
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a307cf2fb9747e822cc48ca4b0723aed437d4af7
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165952"
---
# <a name="sysdatabases-transact-sql"></a>sys.databases (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Contém uma linha por banco de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Se um banco de dados não estiver `ONLINE`ou `AUTO_CLOSE` estiver definido como `ON` e o banco de dados estiver fechado, os valores de algumas colunas poderão ser `NULL`. Se um banco de dados for `OFFLINE`, a linha correspondente não será visível para usuários com poucos privilégios. Para ver a linha correspondente se o banco de dados for `OFFLINE`, um usuário deverá ter pelo menos a permissão de nível de servidor `ALTER ANY DATABASE` ou a permissão `CREATE DATABASE` no banco de dados `master`.  
  
|Nome da coluna|Data type|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do banco de dados, exclusivo em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou em um servidor do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**database_id**|**int**|ID do banco de dados, exclusivo em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou em um servidor do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**source_database_id**|**int**|Non-NULL = ID do banco de dados de origem deste instantâneo do banco de dados.<br /> NULL = Não é um instantâneo do banco de dados.|  
|**owner_sid**|**varbinary(85)**|SID (Identificador de Segurança) do proprietário externo do banco de dados, como registrado para o servidor. Para obter informações sobre quem pode ter um banco de dados, consulte a seção **ALTER AUTHORIZATION for databases** de [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md).|  
|**create_date**|**datetime**|Data em que o banco de dados foi criado ou renomeado. Para **tempdb**, esse valor é alterado toda vez que o servidor é reiniciado.|  
|**compatibility_level**|**tinyint**|Inteiro que corresponde à versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o qual o comportamento é compatível:<br /> **Valor** &#124; **se aplica a**<br /> 70 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 80 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 90 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]<br /> 100 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 110 &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 120 &#124; [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 130 &#124; [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior<br /> 140 &#124; [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e posterior <br /> 150 &#124; [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]  |  
|**collation_name**|**sysname**|Ordenação do banco de dados. Funciona como a ordenação padrão no banco de dados.<br /> NULL = o banco de dados não está online ou AUTO_CLOSE está definido como ON e o banco de dados está fechado.|  
|**user_access**|**tinyint**|Configuração de acesso do usuário:<br /> 0 = MULTI_USER especificado<br /> 1 = SINGLE_USER especificado<br /> 2 = RESTRICTED_USER especificado|  
|**user_access_desc**|**nvarchar(60)**|Descrição da configuração do acesso do usuário.|  
|**is_read_only**|**bit**|1 = O banco de dados é READ_ONLY<br /> 0 = O banco de dados é READ_WRITE|  
|**is_auto_close_on**|**bit**|1 = AUTO_CLOSE está ON<br /> 0 = AUTO_CLOSE está OFF|  
|**is_auto_shrink_on**|**bit**|1 = AUTO_SHRINK está ON<br /> 0 = AUTO_SHRINK está OFF|  
|**state**|**tinyint**|**Valor &#124; se aplica a**<br /> 0 = ONLINE <br /> 1 = RESTORING <br /> 2 = RECUPERAndo &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior<br /> 3 = RECOVERY_PENDING &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior<br /> 4 = SUSPECT <br /> 5 = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] &#124; de emergência e posterior<br /> 6 = OFFLINE &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior<br /> 7 = COPYING &#124; [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /> 10 = OFFLINE_SECONDARY &#124; [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /><br /> **Observação:** Para bancos de dados Always On, consulte as colunas `database_state` ou `database_state_desc` de [Sys. dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md).|  
|**state_desc**|**nvarchar(60)**|Descrição do estado do banco de dados. Consulte State.|  
|**is_in_standby**|**bit**|O banco de dados é somente leitura para log de restauração.|  
|**is_cleanly_shutdown**|**bit**|1 = Banco de dados desligado corretamente. Nenhuma recuperação é necessária na inicialização<br /> 0 = Banco de dados não desligado corretamente. Recuperação é necessária na inicialização|  
|**is_supplemental_logging_enabled**|**bit**|1 = SUPPLEMENTAL_LOGGING está ON<br /> 0 = SUPPLEMENTAL_LOGGING está OFF|  
|**snapshot_isolation_state**|**tinyint**|Estado de transações de isolamento de instantâneo permitidas, conforme definido pela opção ALLOW_SNAPSHOT_ISOLATION:<br /> 0 = O estado de isolamento de instantâneo está OFF (padrão). O isolamento de instantâneo não é permitido.<br /> 1 = O estado de isolamento de instantâneo está ON. O isolamento de instantâneo é permitido.<br /> 2 = O estado de isolamento de instantâneo está em transição para o estado OFF. Todas as transações têm suas modificações controladas por versão. Não é possível iniciar novas transações usando isolamento de instantâneo. O banco de dados permanece na transição para o estado OFF até que todas as transações que estavam ativas quando ALTER DATABASE foi executado possam ser concluídas.<br /> 3 = O estado de isolamento de instantâneo está em transição para o estado ON. Novas transações têm suas modificações controladas por versão. As transações não podem usar isolamento de instantâneo até que o estado de isolamento de instantâneo se torne 1 (ON). O banco de dados permanece na transição para o estado ON até que todas as transações de atualização que estavam ativas quando ALTER DATABASE foi executado possam ser concluídas.|  
|**snapshot_isolation_state_desc**|**nvarchar(60)**|Descrição do estado de transações de isolamento de instantâneo permitidas, conforme definido pela opção ALLOW_SNAPSHOT_ISOLATION.|  
|**is_read_committed_snapshot_on**|**bit**|1 = A opção READ_COMMITTED_SNAPSHOT está ON. Operações de leitura sob o nível de isolamento confirmado por leitura são baseados em varreduras de instantâneo e não adquirem bloqueios.<br /> 0 = A opção de READ_COMMITTED_SNAPSHOT está OFF (padrão). Operações de leitura sob o nível de isolamento confirmado por leitura usam bloqueios de compartilhamento.|  
|**recovery_model**|**tinyint**|Modelo de recuperação selecionado:<br /> 1 = FULL<br /> 2 = BULK_LOGGED<br /> 3 = SIMPLE|  
|**recovery_model_desc**|**nvarchar(60)**|Descrição de modelo de recuperação selecionado.|  
|**page_verify_option**|**tinyint**|Configuração da opção PAGE_VERIFY:<br /> 0 = NONE<br /> 1 = TORN_PAGE_DETECTION<br /> 2 = CHECKSUM|  
|**page_verify_option_desc**|**nvarchar(60)**|Descrição da configuração da opção PAGE_VERIFY.|  
|**is_auto_create_stats_on**|**bit**|1 = AUTO_CREATE_STATISTICS está ON<br /> 0 = AUTO_CREATE_STATISTICS está OFF|  
|**is_auto_create_stats_incremental_on**|**bit**|Indica a configuração padrão para a opção incremental de estatísticas automáticas.<br /> 0 = as estatísticas criadas automaticamente não são incrementais<br /> 1 = as estatísticas criadas automaticamente são incrementais se possível<br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.|  
|**is_auto_update_stats_on**|**bit**|1 = AUTO_UPDATE_STATISTICS está ON<br /> 0 = AUTO_UPDATE_STATISTICS está OFF|  
|**is_auto_update_stats_async_on**|**bit**|1 = AUTO_UPDATE_STATISTICS_ASYNC está ON<br /> 0 = AUTO_UPDATE_STATISTICS_ASYNC está OFF|  
|**is_ansi_null_default_on**|**bit**|1 = ANSI_NULL_DEFAULT está ON<br /> 0 = ANSI_NULL_DEFAULT está OFF|  
|**is_ansi_nulls_on**|**bit**|1 = ANSI_NULLS está ON<br /> 0 = ANSI_NULLS está OFF|  
|**is_ansi_padding_on**|**bit**|1 = ANSI_PADDING está ON<br /> 0 = ANSI_PADDING está OFF|  
|**is_ansi_warnings_on**|**bit**|1 = ANSI_WARNINGS está ON<br /> 0 = ANSI_WARNINGS está OFF|  
|**is_arithabort_on**|**bit**|1 = ARITHABORT está ON<br /> 0 = ARITHABORT está OFF|  
|**is_concat_null_yields_null_on**|**bit**|1 = CONCAT_NULL_YIELDS_NULL está ON<br /> 0 = CONCAT_NULL_YIELDS_NULL está OFF|  
|**is_numeric_roundabort_on**|**bit**|1 = NUMERIC_ROUNDABORT está ON<br /> 0 = NUMERIC_ROUNDABORT está OFF|  
|**is_quoted_identifier_on**|**bit**|1 = QUOTED_IDENTIFIER está ON<br /> 0 = QUOTED_IDENTIFIER está OFF|  
|**is_recursive_triggers_on**|**bit**|1 = RECURSIVE_TRIGGERS está ON<br /> 0 = RECURSIVE_TRIGGERS está OFF|  
|**is_cursor_close_on_commit_on**|**bit**|1 = CURSOR_CLOSE_ON_COMMIT está ON<br /> 0 = CURSOR_CLOSE_ON_COMMIT está OFF|  
|**is_local_cursor_default**|**bit**|1 = CURSOR_DEFAULT é local<br /> 0 = CURSOR_DEFAULT é global|  
|**is_fulltext_enabled**|**bit**|1 = Texto completo habilitado para o banco de dados<br /> 0 = Texto completo desabilitado para o banco de dados|  
|**is_trustworthy_on**|**bit**|1 = O banco de dados foi marcado como confiável<br /> 0 = O banco de dados não foi marcado como confiável<br /> Por padrão, os bancos de dados restaurados ou anexados têm o confiável não habilitado.|  
|**is_db_chaining_on**|**bit**|1 = O encadeamento de propriedades de bancos de dados está ON<br /> 0 = O encadeamento de propriedades de bancos de dados está OFF|  
|**is_parameterization_forced**|**bit**|1 = A parametrização é FORCED<br /> 0 = A parametrização é SIMPLE|  
|**is_master_key_encrypted_by_server**|**bit**|1 = O banco de dados tem uma chave mestra criptografada<br /> 0 = O banco de dados não tem uma chave mestra criptografada|  
|**is_query_store_on**|**bit**|1 = o repositório de consultas é habilitado para este banco de dados. Marque [Sys. database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) para exibir o status do repositório de consultas.<br /> 0 = o repositório de consultas não está habilitado<br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior).|  
|**is_published**|**bit**|1 = O banco de dados é um banco de dados de publicação em uma topologia de replicação transacional ou de instantâneo<br /> 0 = Não é um banco de dados de publicação|  
|**is_subscribed**|**bit**|Esta coluna não é usada. Sempre retornará 0, independentemente do status de assinante do banco de dados.|  
|**is_merge_published**|**bit**|1 = O banco de dados é um banco de dados de publicação em uma topologia de replicação de mesclagem<br /> 0 = Não é um banco de dados de publicação em uma topologia de replicação de mesclagem|  
|**is_distributor**|**bit**|1 = O banco de dados é o banco de dados de distribuição de uma topologia de replicação<br /> 0 = Não é o banco de dados de distribuição de uma topologia de replicação|  
|**is_sync_with_backup**|**bit**|1 = O banco de dados está marcado para sincronização de replicação com backup<br /> 0 = Não está marcado para sincronização de replicação com backup|  
|**service_broker_guid**|**uniqueidentifier**|Identificador do service broker para este banco de dados. Usado como o **BROKER_INSTANCE** do destino na tabela de roteamento.|  
|**is_broker_enabled**|**bit**|1 = O agente neste banco de dados está enviando e recebendo mensagens atualmente.<br /> 0 = Todas as mensagens enviadas permanecerão na fila de transmissão e as mensagens recebidas não serão colocadas nas filas deste banco de dados.<br /> Por padrão, bancos de dados restaurados ou anexados têm o agente desabilitado. A exceção é espelhamento de banco de dados onde o agente é habilitado após failover.|  
|**log_reuse_wait**|**tinyint**|A reutilização do espaço do log de transações está aguardando um dos itens a seguir no último ponto de verificação. Para obter explicações mais detalhadas sobre esses valores, consulte [o log de transações](../../relational-databases/logs/the-transaction-log-sql-server.md).<br /> **Valor &#124; se aplica a**<br /> 0 = Nada<br />   1 = ponto de verificação (quando um banco de dados usa um modelo de recuperação e tem um grupo de arquivos com otimização de memória, você deve esperar ver a coluna `log_reuse_wait` indicar ponto de verificação ou xtp_checkpoint.) &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior<br />  2 = backup &#124; de log [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior<br />  3 = backup ativo ou restauração &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior<br />  4 = transação &#124; ativa [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior<br />  5 = espelhamento de &#124; banco de dados [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior<br />  6 = replicação &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior<br />  7 = criação &#124; de instantâneo de banco de dados [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior<br />  8 = Verificação de log <br />  9 = uma réplica secundária dos grupos de disponibilidade de Always On está aplicando os registros de log de transações desse banco de dados a um banco de dados secundário correspondente. &#124;[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior<br />  9 = outro (transitório) &#124; até e incluindo [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]<br />  10 = somente &#124; para uso interno [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior<br />  11 = somente &#124; para uso interno [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior<br /> 12 = somente &#124; para uso interno [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior<br />13 = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] de &#124; página mais antiga e posterior<br /> 14 = outros &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posteriores<br />  16 = XTP_CHECKPOINT (quando um banco de dados usa um modelo de recuperação e tem um grupo de arquivos com otimização de memória, você deve esperar ver a coluna log_reuse_wait indicar ponto de verificação ou xtp_checkpoint.) &#124; [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior|  
|**log_reuse_wait_desc**|**nvarchar(60)**|No momento, a descrição da reutilização de espaço do log de transações está aguardando como um dos últimos pontos de verificação.|  
|**is_date_correlation_on**|**bit**|1 = DATE_CORRELATION_OPTIMIZATION está ON<br /> 0 = DATE_CORRELATION_OPTIMIZATION está OFF|  
|**is_cdc_enabled**|**bit**|1 = O banco de dados está habilitado para Change Data Capture. Para obter mais informações, consulte [Sys. &#40;SP_CDC_ENABLE_DB Transact-&#41;SQL](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md).|  
|**is_encrypted**|**bit**|Indica se o banco de dados está criptografado (reflete o estado definido pela última vez usando a cláusula `ALTER DATABASE SET ENCRYPTION`). Pode ser um dos seguintes valores:<br /> 1 = Criptografado<br /> 0 = Não criptografado<br /> Para obter mais informações sobre a criptografia do banco de dados, confira [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).<br /> Se o banco de dados estiver em processo de ser descriptografado, `is_encrypted` mostrará um valor de 0. Você pode ver o estado do processo de criptografia usando a exibição de gerenciamento dinâmico [Sys. dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) .|  
|**is_honor_broker_priority_on**|**bit**|Indica se o banco de dados honra as prioridades de conversa (reflete o estado definido pela última vez usando a cláusula `ALTER DATABASE SET HONOR_BROKER_PRIORITY`). Pode ser um dos seguintes valores:<br /> 1 = HONOR_BROKER_PRIORITY está ON<br /> 0 = HONOR_BROKER_PRIORITY está OFF<br /> Por padrão, os bancos de dados restaurados ou anexados têm a prioridade do agente desativada.|  
|**replica_id**|**uniqueidentifier**|Identificador exclusivo da réplica de disponibilidade local do [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] do grupo de disponibilidade, se houver, no qual o banco de dados está participando.<br /> NULL = o banco de dados não faz parte de uma réplica de disponibilidade em um grupo de disponibilidade.<br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**group_database_id**|**uniqueidentifier**|Identificador exclusivo do banco de dados dentro de um grupo de disponibilidade Always On, se houver, no qual o banco de dados está participando. **group_database_id** é o mesmo para esse banco de dados na réplica primária e em todas as réplicas secundárias nas quais o banco de dados foi ingressado no grupo de disponibilidade.<br /> NULL = o banco de dados não faz parte de uma réplica de disponibilidade em nenhum grupo de disponibilidade.<br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**resource_pool_id**|**int**|A ID do pool de recursos que é mapeado para esse banco de dados. Esse conjunto de recursos controla a memória total disponível para tabelas com otimização de memória nesse banco de dados.<br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior|  
|**default_language_lcid**|**smallint**|Indica a lcid (id local) do idioma padrão de um banco de dados independente.<br /> **Observação:** Funciona como a [opção de configuração de servidor do idioma padrão](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) de `sp_configure`. Esse valor é **nulo** para um banco de dados dependente.<br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_language_name**|**nvarchar(128)**|Indica o idioma padrão de um banco de dados independente.<br /> Esse valor é **nulo** para um banco de dados dependente.<br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_lcid**|**int**|Indica a LCID (identificação de localidade) do idioma de texto completo padrão do banco de dados independente.<br /> **Observação:** Funciona como padrão para [Configurar a opção de configuração de servidor padrão Full-Text Language](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) de `sp_configure`. Esse valor é **nulo** para um banco de dados dependente.<br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_name**|**nvarchar(128)**|Indica o idioma de texto completo padrão do banco de dados independente.<br /> Esse valor é **nulo** para um banco de dados dependente.<br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_nested_triggers_on**|**bit**|Indica se gatilhos aninhados são permitidos no banco de dados independente.<br /> 0 = gatilhos aninhados não são permitidos<br /> 1 = gatilhos aninhados são permitidos<br /> **Observação:** Funciona como a [opção configurar a configuração de servidor de disparadores aninhados](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) de `sp_configure`. Esse valor é **nulo** para um banco de dados dependente. Consulte [Sys. Configurations &#40;Transact&#41; -SQL](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) para obter mais informações.<br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_transform_noise_words_on**|**bit**|Indica se palavras de ruído devem ser transformadas no banco de dados independente.<br /> 0 = palavras de ruído não devem ser transformadas.<br /> 1 = palavras de ruído devem ser transformadas.<br /> **Observação:** Funciona como a [opção de configuração de servidor Transform Noise words](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md) de `sp_configure`. Esse valor é **nulo** para um banco de dados dependente. Consulte [Sys. Configurations &#40;Transact&#41; -SQL](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) para obter mais informações.<br /> **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior|  
|**two_digit_year_cutoff**|**smallint**|Indica um valor de um número entre 1753 e 9999 para representar o ano de corte para interpretar anos com dois dígitos como anos de quatro dígitos.<br /> **Observação:** Funciona como a [opção de configuração de servidor de descorte de ano de dois dígitos](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) de `sp_configure`. Esse valor é **nulo** para um banco de dados dependente. Consulte [Sys. Configurations &#40;Transact&#41; -SQL](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) para obter mais informações.<br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**containment**|**tinyint não nulo**|Indica o status de contenção do banco de dados.<br />  0 = a contenção do banco de dados está desativada. **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 1 = o banco de dados está em contenção parcial **aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior|  
|**containment_desc**|**nvarchar(60) not null**|Indica o status de contenção do banco de dados.<br /> NONE = banco de dados herdado (contenção zero)<br /> PARTIAL = banco de dados parcialmente independente<br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**target_recovery_time_in_seconds**|**int**|A hora estimada para recuperar o banco de dados, em segundos. Anulável.<br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**delayed_durability**|**int**|A configuração de durabilidade atrasada:<br /> 0 = DESABILITADO<br /> 1 = PERMITIDO<br /> 2 = FORÇADO<br /> Para obter mais informações, veja [Controlar a durabilidade da transação](../../relational-databases/logs/control-transaction-durability.md).<br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**delayed_durability_desc**|**nvarchar(60)**|A configuração de durabilidade atrasada:<br /> DISABLED<br /> ALLOWED<br /> FORCED<br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**is_memory_optimized_elevate_to_snapshot_on**|**bit**|As tabelas com otimização de memória são acessadas usando o isolamento SNAPSHOT quando a configuração de sessão TRANSACTION ISOLATION LEVEL é definida como um nível de isolamento inferior, READ COMMITTED ou READ UNCOMMITTED.<br /> 1 = O nível de isolamento mínimo SNAPSHOT.<br /> 0 = O nível de isolamento não é elevado.|  
|**is_federation_member**|**bit**|Indica se o banco de dados é membro de uma federação.<br /> **Aplica-se ao**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_remote_data_archive_enabled**|**bit**|Indica se o banco de dados está ampliado.<br /> 0 = o banco de dados não está habilitado para Stretch.<br /> 1 = o banco de dados está habilitado para Stretch.<br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior<br /> Saiba mais em [Stretch Database](../../sql-server/stretch-database/stretch-database.md).|  
|**is_mixed_page_allocation_on**|**bit**|Indica se as tabelas e os índices no banco de dados podem alocar páginas iniciais de extensões mistas.<br /> 0 = tabelas e índices no banco de dados sempre alocam páginas iniciais de extensões uniformes.<br /> 1 = tabelas e índices no banco de dados podem alocar páginas iniciais de extensões mistas.<br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior<br /> Para obter mais informações, consulte a opção SET MIXED_PAGE_ALLOCATION das [opções &#40;ALTER DATABASE SET Transact-&#41;SQL](../../t-sql/statements/alter-database-transact-sql-set-options.md).|  
|**is_temporal_retention_enabled**|**bit**|Indica se a tarefa de limpeza da política de retenção temporal está habilitada.<br /> **Aplica-se ao**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**catalog_collation_type**|**int**|A configuração de agrupamento do catálogo:<br />0 = DATABASE_DEFAULT<br />2 = SQL_Latin_1_General_CP1_CI_AS<br /> **Aplica-se ao**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**catalog_collation_type_desc**|**nvarchar(60)**|A configuração de agrupamento do catálogo:<br />DATABASE_DEFAULT<br />SQL_Latin_1_General_CP1_CI_AS<br /> **Aplica-se ao**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**is_result_set_caching_on**|**int**|1 = is_result_set_caching_on está on</br>0 = is_result_set_caching_on está desativado</br>**Aplica-se a**: Azure SQL data warehouse Gen2. Embora esses recursos estejam sendo distribuídos para todas as regiões, verifique a versão implantada em sua instância e as notas de versão mais recentes do [Azure SQL DW](/azure/sql-data-warehouse/release-notes-10-0-10106-0) para disponibilidade de recursos.|
  
## <a name="permissions"></a>Permissões

 Se o chamador de `sys.databases` não for o proprietário do banco de dados e o banco de dados não for `master` ou `tempdb`, as permissões mínimas necessárias para ver a linha correspondente serão `ALTER ANY DATABASE` ou a permissão `VIEW ANY DATABASE` no nível do servidor ou a permissão `CREATE DATABASE` no banco de dados `master`. O banco de dados ao qual o chamador está conectado sempre pode ser exibido no `sys.databases`.  
  
> [!IMPORTANT]  
> Por padrão, a função pública tem a permissão `VIEW ANY DATABASE`, permitindo que todos os logons vejam informações do banco de dados. Para bloquear um logon da capacidade de detectar um banco de dados, `REVOKE` a permissão `VIEW ANY DATABASE` de `public`ou `DENY` a permissão `VIEW ANY DATABASE` para logons individuais.  
  
## <a name="azure-sql-database-remarks"></a>Comentários do banco de dados SQL do Azure

No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] essa exibição está disponível no banco de dados de `master` e em bancos de dados de usuário. No banco de dados `master`, essa exibição retorna as informações no banco de dados de `master` e todos os bancos de dados de usuários no servidor. Em um banco de dados de usuário, essa exibição retorna informações apenas sobre o banco de dados atual e o banco de dados mestre.  
  
 Use a exibição de `sys.databases` no banco de dados `master` do servidor de [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] em que o novo banco de dados está sendo criado. Depois que a cópia do banco de dados for iniciada, você poderá consultar o `sys.databases` e as exibições de `sys.dm_database_copies` do banco de dados `master` do servidor de destino para recuperar mais informações sobre o progresso da cópia.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-query-the-sysdatabases-view"></a>A. Consultar a exibição do sys.databases

O exemplo a seguir retorna algumas das colunas disponíveis na exibição `sys.databases`.  
  
```sql  
SELECT name, user_access_desc, is_read_only, state_desc, recovery_model_desc  
FROM sys.databases;  
```  
  
### <a name="b-check-the-copying-status-in-includesssdsincludessssds-mdmd"></a>b. Verificar o status de cópia em [!INCLUDE[ssSDS](../../includes/sssds-md.md)]

O exemplo a seguir consulta as exibições `sys.databases` e `sys.dm_database_copies` para retornar informações sobre uma operação de cópia de banco de dados.  
  
**Aplica-se ao**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
```sql
-- Execute from the master database.  
SELECT a.name, a.state_desc, b.start_date, b.modify_date, b.percentage_complete  
FROM sys.databases AS a  
INNER JOIN sys.dm_database_copies AS b ON a.database_id = b.database_id  
WHERE a.state = 7;  
```

### <a name="c-check-the-temporal-retention-policy-status-in-includesssdsincludessssds-mdmd"></a>C. Verifique o status da política de retenção temporal em [!INCLUDE[ssSDS](../../includes/sssds-md.md)]

O exemplo a seguir consulta o `sys.databases` para retornar informações se a tarefa limpeza de retenção temporal está habilitada. Lembre-se de que, após a operação de restauração, a retenção temporal é desabilitada por padrão. Use `ALTER DATABASE` para habilitá-lo explicitamente.
  
**Aplica-se ao**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
```sql  
-- Execute from the master database.  
SELECT a.name, a.is_temporal_history_retention_enabled 
FROM sys.databases AS a;
```  
  
## <a name="next-steps"></a>Próximas etapas

- [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)
- [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)
- [sys.database_recovery_status &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-recovery-status-transact-sql.md)
- [Exibições &#40;de catálogo de bancos de dados e arquivos TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)
- [sys.dm_database_copies &#40;Banco de Dados SQL do Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)  
