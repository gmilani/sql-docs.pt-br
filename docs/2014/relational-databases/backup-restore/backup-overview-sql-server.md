---
title: Visão geral de backup (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server], backing up data
- backups [SQL Server]
- database backups [SQL Server]
- backup types [SQL Server]
- data backups [SQL Server]
- backing up tables [SQL Server]
- database restores [SQL Server], backups
- backing up [SQL Server], about backing up
- restoring [SQL Server], backup types
- backups [SQL Server], about
- backups [SQL Server], table-level backups unsupported
ms.assetid: 09a6e0c2-d8fd-453f-9aac-4ff24a97dc1f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bf284ffce044e0efa1f855e0e504a1f92dc7e3da
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175988"
---
# <a name="backup-overview-sql-server"></a>Backup Overview (SQL Server)
  Este tópico apresenta o componente de backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O backup do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é essencial para proteger seus dados. Esta discussão abrange tipos de backup e restrições de backup. O tópico também apresenta dispositivos de backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e mídia de backup.  
  
 **Neste tópico:**  
  
-   [Componentes e conceitos](#TermsAndDefinitions)  
  
-   [Compactação de backup](#BackupCompression)  
  
-   [Restrições de operações de backup no SQL Server](#Restrictions)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="TermsAndDefinitions"></a> Componentes e conceitos  
 fazer backup [verbo]  
 Copia os dados ou registros de log de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou de seu log de transações para um dispositivo de backup, como um disco, a fim de criar um backup de dados ou backup de log.  
  
 backup [substantivo]  
 Uma cópia dos dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que pode ser usada para restaurar e recuperar os dados após uma falha. Um backup dos dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é criado no nível de um banco de dados ou de um ou mais de seus arquivos ou grupos de arquivos. Não é possível criar backups no nível da tabela. Além dos backups de dados, o modelo de recuperação completa requer a criação de backups do log de transações.  
  
 [modelo de recuperação](recovery-models-sql-server.md)  
 Uma propriedade de banco de dados que controla a manutenção do log de transações em um banco de dados. Existem três modelos de recuperação: simples, completo e bulk-logged. O modelo de recuperação de banco de dados determina seus requisitos de backup e de restauração.  
  
 [restaurar](restore-and-recovery-overview-sql-server.md)  
 Um processo multifase que copia todos os dados e páginas de log de um backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um banco de dados especificado e, em seguida, efetua roll forward de todas as transações registradas no backup, aplicando as alterações registradas para avançar os dados no tempo.  
  
 **Tipos de backups**  
  
 [backup somente cópia](copy-only-backups-sql-server.md)  
 Um backup de uso especial que é independente da sequência regular dos backups do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 backup de dados  
 Um backup de dados em um banco de dados completo (um backup de banco de dados), um banco de dados parcial (um backup parcial) ou um conjunto de arquivos de dados ou grupos de arquivos (um backup de arquivo).  
  
 [backup de banco de dados](full-database-backups-sql-server.md)  
 Um backup de um banco de dados. Os backups completos de banco de dados representam todo o banco de dados no momento em que o backup é concluído. Os backups de banco de dados diferenciais contêm somente alterações feitas no banco de dados desde seu backup completo de banco de dados mais recente.  
  
 [backup diferencial](full-database-backups-sql-server.md)  
 Um backup de dados que se baseia no backup completo mais recente de um banco de dados completo ou parcial ou um conjunto de arquivos de dados ou grupos de arquivos (a *base diferencial*) que contém somente as extensões de dados alterados desde a base diferencial.  
  
 Um backup diferencial parcial registra apenas as extensões de dados que foram alteradas nos grupos de arquivos desde o backup parcial anterior, conhecido como a base para o diferencial.  
  
 backup completo  
 Um backup de dados que contém todos os dados em um banco de dados ou em um conjunto de grupos de arquivos ou arquivos, além de log suficiente para permitir a recuperação desses dados.  
  
 [backup de log](transaction-log-backups-sql-server.md)  
 Um backup de logs de transações que inclui todos os registros de log dos quais não foi feito backup em um backup de log anterior. (modelo de recuperação completa)  
  
 [backup de arquivo](full-file-backups-sql-server.md)  
 Um backup de um ou mais arquivos ou grupos de arquivos de banco de dados.  
  
 [backup parcial](partial-backups-sql-server.md)  
 Contém dados apenas de alguns grupos de arquivos em um banco de dados, incluindo os dados no grupo de arquivos primário, em cada grupo de arquivos de leitura/gravação e em qualquer arquivo somente leitura especificado opcionalmente.  
  
 **Termos e definições de mídia de backup**  
  
 [dispositivo de backup](backup-devices-sql-server.md)  
 Um disco ou dispositivo de fita no qual são gravados backups do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e nos quais eles podem ser restaurados. SQL Server backups também podem ser gravados em um serviço de armazenamento de BLOBs do Azure, e o formato de **URL** é usado para especificar o destino e o nome do arquivo de backup.. Para obter mais informações, consulte [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Azure](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 [mídia de backup](media-sets-media-families-and-backup-sets-sql-server.md)  
 Uma ou mais fitas ou arquivos de disco nos quais um ou mais backups foram gravados.  
  
 [conjunto de backup](media-sets-media-families-and-backup-sets-sql-server.md)  
 O conteúdo de backup adicionado a um conjunto de mídias por uma operação de backup bem-sucedida.  
  
 [família de mídia](media-sets-media-families-and-backup-sets-sql-server.md)  
 Os backups criados em um único dispositivo não espelhado ou um conjunto de dispositivos espelhados em um conjunto de mídias  
  
 [conjunto de mídias](media-sets-media-families-and-backup-sets-sql-server.md)  
 Uma coleção ordenada de mídias de backup, fitas ou arquivos de disco, em que uma ou mais operações de backup foram gravadas, usando um número e um tipo fixo de dispositivos de backup.  
  
 [conjunto de mídias espelhado](mirrored-backup-media-sets-sql-server.md)  
 Várias cópias (espelhos) de um conjunto de mídias.  
  
##  <a name="BackupCompression"></a>Compactação de backup  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e versões posteriores dão suporte à compactação de backups, e o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores podem restaurar um backup compactado. Para obter mais informações, veja [Compactação de backup &#40;SQL Server&#41;](backup-compression-sql-server.md).  
  
##  <a name="Restrictions"></a>Restrições de operações de backup no SQL Server  
 O backup pode ser realizado com o banco de dados online e em uso. No entanto, existem as seguintes restrições.  
  
### <a name="offline-data-cannot-be-backed-up"></a>Não é possível fazer backup de dados offline  
 Operações de backup que implícita ou explicitamente fizerem referência a dados offline falharão. Alguns exemplos comuns incluem:  
  
-   Você solicita um backup de banco de dados completo, mas um grupo de arquivos do banco de dados está offline. Como todos os grupos de arquivos são implicitamente incluídos em um backup de banco de dados completo, a operação falhará.  
  
     Para fazer backup desse banco de dados, você pode usar um backup de arquivo e especificar apenas os grupos de arquivos que estão online.  
  
-   Você solicita um backup parcial, mas um grupo de arquivos de leitura/gravação está offline. Como todos os grupos de arquivos de leitura/gravação são requeridos para um backup parcial, a operação falhará.  
  
-   Você solicita um backup de arquivo de arquivos específicos, mas um dos arquivos não está online. A operação falhará. Para fazer backup dos arquivos online, você pode omitir o arquivo offline da lista de arquivos e repetir a operação.  
  
 Normalmente, um backup de log será realizado com êxito mesmo se um ou mais arquivos de dados estiverem indisponíveis. Entretanto, se algum arquivo contiver alterações bulk-logged feitas sob o modelo de recuperação bulk-logged, todos os arquivos devem estar online para a realização do backup.  
  
### <a name="concurrency-restrictions-during-backup"></a>Restrições de simultaneidade durante o backup  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um processo de backup online para permitir que um backup de banco de dados seja feito com o banco de dados em uso. Durante um backup, a maior parte das operações é possível. Por exemplo, instruções INSERT, UPDATE ou DELETE são permitidas durante uma operação de backup Contudo, se você tentar iniciar uma operação de backup enquanto um arquivo do banco de dados estiver sendo criado ou excluído, a operação de backup aguardará até a conclusão dessa operação ou até o tempo limite do backup.  
  
 Operações que não podem ser executadas durante um backup de banco de dados ou de log de transações incluem:  
  
-   Operações de gerenciamento de arquivos, como a instrução ALTER DATABASE com as opções ADD FILE ou REMOVE FILE.  
  
-   Operações de redução do banco de dados ou de arquivos. Isso inclui operações de redução automática.  
  
-   Se você tentar criar ou excluir um arquivo de banco de dados enquanto houver uma operação de backup em andamento, a operação de criação ou exclusão falhará.  
  
 Se uma operação de backup for sobreposta por uma operação de gerenciamento de arquivos ou de redução, ocorrerá um conflito. Independentemente de qual operação conflitante começou primeiro, a segunda operação aguardará até que o bloqueio definido para a primeira operação seja esgotado. (O tempo limite é controlado por uma configuração de tempo limite da sessão.) Se o bloqueio for liberado durante o período de tempo limite, a segunda operação continuará. Se o tempo limite do bloqueio for esgotado, a segunda operação falhará.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para trabalhar com dispositivos de backup e mídia de backup**  
  
-   [Definir um dispositivo de backup lógico para um arquivo de disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definir um dispositivo de backup lógico para uma unidade de fita &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Especificar um disco ou fita como destino de backup &#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Excluir um dispositivo de backup &#40;SQL Server&#41;](delete-a-backup-device-sql-server.md)  
  
-   [Definir a data de validade em um backup &#40;SQL Server&#41;](set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Exibir o conteúdo de um arquivo ou fita de backup &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Exibir os dados e arquivos de log em um conjunto de backup &#40;SQL Server&#41;](view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Exibir as propriedades e o conteúdo de um dispositivo de backup lógico &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Restaurar um backup de um dispositivo &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)  
  
-   [Tutorial: SQL Server Backup e restauração para o serviço de armazenamento de BLOBs do Azure](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
 **Para criar um backup**  
  
> [!NOTE]  
>  Para backups parciais ou somente cópia, use a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](/sql/t-sql/statements/backup-transact-sql) com a opção PARTIAL ou COPY_ONLY, respectivamente.  
  
-   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [Fazer backup de arquivos e de grupos de arquivos &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)  
  
-   [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [Fazer backup do log de transações quando o banco de dados está danificado &#40;SQL Server&#41;](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [Habilitar ou desabilitar as somas de verificação de backup durante backup ou restauração &#40;SQL Server&#41;](enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [Especificar se uma operação de backup ou restauração continua ou é interrompida após um erro &#40;SQL Server&#41;](specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
-   [Usar o Resource Governor para limitar o uso de CPU por meio de compactação de backup &#40;Transact-SQL&#41;](use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [Tutorial: SQL Server Backup e restauração para o serviço de armazenamento de BLOBs do Azure](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="see-also"></a>Consulte também  
 [Fazer backup e restaurar bancos de dados do SQL Server](back-up-and-restore-of-sql-server-databases.md)   
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [Planos de manutenção](../maintenance-plans/maintenance-plans.md)   
 [O log de transações &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [Modelos de recuperação &#40;SQL Server&#41;](recovery-models-sql-server.md)  
  
  
