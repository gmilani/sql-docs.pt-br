---
title: Criptografia de backup | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 334b95a8-6061-4fe0-9e34-b32c9f1706ce
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 177eef6f6280e236106f9ec67684e4a15ef479a3
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783077"
---
# <a name="backup-encryption"></a>Criptografia de backup
  Este tópico fornece uma visão geral das opções de criptografia para backups do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ele inclui detalhes do uso, benefícios e práticas recomendadas para criptografia durante o backup.  
  
  
##  <a name="Overview"></a> Visão geral  
 A partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], o SQL Server pode criptografar os dados enquanto cria um backup. Especificando o algoritmo de criptografia e o criptografador (um certificado ou uma chave assimétrica) ao criar um backup, você pode criar um arquivo de backup criptografado. Todos os destinos de armazenamento: há suporte para armazenamento local e do Windows Azure. Além disso, as opções de criptografia podem ser configuradas para operações do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] , um novo recurso incorporado no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 Para realizar a criptografia durante o backup, você deve especificar um algoritmo de criptografia, e um criptografador para proteger a chave de criptografia. Estas são as opções de criptografia com suporte:  
  
-   **Algoritmo de criptografia:** os algoritmos de criptografia com suporte são: AES 128, AES 192, AES 256 e DES triplo  
  
-   **Criptografador:** um certificado ou uma chave assimétrica  
  
> [!CAUTION]  
>  É muito importante fazer backup do certificado ou da chave assimétrica e, preferencialmente, em um local diferente do arquivo de backup usado para criptografar. Sem o certificado ou a chave assimétrica, você não pode restaurar o backup, tornando o arquivo de backup inutilizável.  
  
 **Restaurando o backup criptografado:** a restauração do SQL Server não requer nenhum parâmetro de criptografia a ser especificado durante as restaurações. Requer que o certificado ou a chave assimétrica usada para criptografar o arquivo de backup esteja disponível na instância em que você está fazendo a restauração. A conta de usuário que executa a restauração deve ter as permissões `VIEW DEFINITION` no certificado ou na chave. Se você estiver restaurando o backup criptografado para uma instância diferente, verifique se o certificado está disponível nessa instância.  
  
 Se você estiver restaurando um backup de um banco de dados criptografado TDE, o certificado TDE deverá estar disponível na instância para a qual você estiver restaurando.  
  
##  <a name="Benefits"></a> Benefícios  
  
1.  A criptografia dos backups de banco de dados ajuda a proteger os dados: o SQL Server oferece a opção para criptografar os dados do backup ao criar um backup.  
  
2.  A criptografia também pode ser usada para bancos de dados criptografados usando a TDE.  
  
3.  Há suporte para a criptografia nos backups feitos por [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], que fornece segurança adicional para backups fora do local.  
  
4.  Esse recurso oferece suporte a vários algoritmos de criptografia até AES de 256 bits. Isso permite que você selecione um algoritmo que atenda aos seus requisitos.  
  
5.  Você pode integrar chaves de criptografia com provedores EKM (Extended Key Management).  
  
  
##  <a name="Prerequisites"></a> Prerequisites  
 Estes são os pré-requisitos para criptografar um backup:  
  
1.  **Criar uma chave mestra de banco de dados para o banco de dados mestre:** a chave mestra de banco de dados é uma chave simétrica usada para proteger as chaves privadas dos certificados e as chaves assimétricas presentes no banco de dados. Para obter mais informações, consulte [Chaves de criptografia do SQL Server e banco de dados &#40;Mecanismo de Banco de Dados&#41;](../security/encryption/sql-server-and-database-encryption-keys-database-engine.md).  
  
2.  Crie um certificado ou uma chave assimétrica a ser usada na criptografia de backup. Para obter mais informações sobre a criação de um certificado, consulte [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql). Para obter mais informações sobre a criação de uma chave assimétrica, consulte [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql).  
  
    > [!IMPORTANT]  
    >  Há suporte somente para chaves assimétricas que residem em um EKM (Extended Key Management).  
  
##  <a name="Restrictions"></a> Restrições  
 Estas são as restrições que se aplicam às opções de criptografia:  
  
-   Se você estiver usando a chave assimétrica para criptografar os dados de backup, haverá suporte somente para as chaves assimétricas que residem no provedor EKM.  
  
-   O SQL Server Express e o SQL Server Web não oferecem suporte à criptografia durante o backup. No entanto, há suporte para a restauração de um backup criptografado para uma instância do SQL Server Express ou SQL Server Web.  
  
-   As versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem ler backups criptografados.  
  
-   Não há suporte para a anexação a uma opção de conjunto de backup existente em backups criptografados.  
  
  
##  <a name="Permissions"></a> Permissões  
 **Para criptografar um backup ou restaurá-lo de um backup criptografado:**  
  
 Permissão `VIEW DEFINITION` no certificado ou na chave assimétrica usada para criptografar o backup do banco de dados.  
  
> [!NOTE]  
>  Não é necessário ter acesso ao certificado TDE para fazer backup ou restaurar um banco de dados protegido.  
  
##  <a name="Methods"></a> Métodos de criptografia de backup  
 As seções a seguir fornecem uma breve introdução às etapas de criptografia dos dados durante o backup. Para obter um passo a passo completo das diferentes etapas de criptografia de backup usando o Transact-SQL, consulte [Criar um backup criptografado](create-an-encrypted-backup.md).  
  
### <a name="using-sql-server-management-studio"></a>Usando o SQL Server Management Studio  
 Você pode criptografar um backup ao criar o backup de um banco de dados em qualquer uma destas caixas de diálogo:  
  
1.  [Backup de Banco de Dados &#40;página Opções de Backup&#41;](back-up-database-backup-options-page.md) Na página **Opções de Backup**, selecione **Criptografia**; em seguida, especifique o algoritmo de criptografia e o certificado ou a chave assimétrica a serem usados na criptografia.  
  
2.  [Usando o Assistente de Plano de Manutenção](../maintenance-plans/use-the-maintenance-plan-wizard.md#SSMSProcedure) Ao selecionar uma tarefa de backup, na guia **Opções** da página **Define Backup ()Task (Definir ()Tarefa de Backup)** , selecione **Criptografia de Backup**e especifique o algoritmo de criptografia e o certificado ou a chave a serem usados na criptografia.  
  
### <a name="using-transact-sql"></a>Usando Transact-SQL  
 Este é um exemplo de instrução Transact-SQL para criptografar o arquivo de backup:  
  
```sql
BACKUP DATABASE [MYTestDB]  
TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
WITH  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
GO
```  
  
 Para obter a sintaxe completa da instrução Transact-SQL, consulte [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
### <a name="using-powershell"></a>Usando o PowerShell  
 Esse exemplo cria as opções de criptografia e as utiliza como um valor de parâmetro no cmdlet **Backup-SqlDatabase** para criar um backup criptografado.  
  
```powershell
$encryptionOption = New-SqlBackupEncryptionOption -Algorithm Aes256 -EncryptorType ServerCertificate -EncryptorName "BackupCert"  
Backup-SqlDatabase -ServerInstance . -Database "MyTestDB" -BackupFile "MyTestDB.bak" -CompressionOption On -EncryptionOption $encryptionOption  
```  
  
##  <a name="RecommendedPractices"></a> Práticas recomendadas  
 Crie um backup do certificado e das chaves de criptografia em um local que não seja o computador local em que a instância está instalada. Para dar conta de cenários de recuperação de desastre, é recomendável armazenar um backup do certificado ou da chave em um local externo. Você não pode restaurar um backup criptografado sem o certificado usado para criptografar o backup.  
  
 Para restaurar um backup criptografado, o certificado original usado quando o backup foi feito com a impressão digital correspondente deve estar disponível na instância para a qual você está restaurando. Portanto, o certificado não deve ser renovado na expiração nem alterado de forma alguma. A renovação pode resultar na atualização do certificado que está disparando a alteração da impressão digital, tornando o certificado inválido para o arquivo de backup. A conta que executa a restauração deve ter as permissões VIEW DEFINITION no certificado ou na chave assimétrica usada na criptografia durante o backup.  
  
 Os backups de banco de dados do Grupo de Disponibilidade são tipicamente executados na réplica de backup preferencial.  Se estiver restaurando um backup em uma réplica diferente daquela em que foi feito o backup, verifique se o certificado original usado para o backup está disponível na réplica para onde você está restaurando.  
  
 Se o banco de dados for habilitado para TDE, escolha diferentes certificados ou chaves assimétricas na criptografia do banco de dados e do backup para aumentar a segurança.  
  
##  <a name="RelatedTasks"></a> Tarefas Relacionadas  
  
|Tópico/tarefa|Description|  
|-----------------|-----------------|  
|[Criar um Backup Criptografado](create-an-encrypted-backup.md)|Descreve as etapas básicas necessárias para criar um backup criptografado|  
|[SQL Server Backup gerenciado para o Azure – configurações de retenção e armazenamento](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)|Descreve as etapas básicas necessárias para configurar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] com as opções de criptografia especificadas.|  
|[Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;](../security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)|Fornece um exemplo de como criar um backup criptografado protegido por chaves no Azure Key Vault.|  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do backup &#40;SQL Server&#41;](backup-overview-sql-server.md)  
  
  
