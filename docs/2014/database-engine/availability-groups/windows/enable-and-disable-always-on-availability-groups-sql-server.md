---
title: Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], disabling
- Availability Groups [SQL Server], enabling
ms.assetid: 7c326958-5ae9-4761-9c57-905972276a8f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a441595fa07c86ff1cdbeac4e67e3a6ca0361f80
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782982"
---
# <a name="enable-and-disable-alwayson-availability-groups-sql-server"></a>Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn (SQL Server)
  Habilitar o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] é um pré-requisito para uma instância de servidor usar grupos de disponibilidade. Antes de poder criar e configurar qualquer grupo de disponibilidade, o recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] deve ser habilitado em cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedará uma réplica de disponibilidade de um ou mais grupos de disponibilidade.  
  
> [!IMPORTANT]  
>  Se você excluir e recriar um cluster WSFC, deverá desabilitar e reabilitar o recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedava uma réplica de disponibilidade no cluster WSFC original.  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Instruções:**  
  
    -   [Determinar se Grupos de Disponibilidade AlwaysOn está habilitado](#IsEnabled)  
  
    -   [Habilitar Grupos de Disponibilidade AlwaysOn](#EnableAOAG)  
  
    -   [Desabilitar Grupos de Disponibilidade AlwaysOn](#DisableAOAG)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a>Pré-requisitos para habilitar o Grupos de Disponibilidade AlwaysOn  
  
-   A instância de servidor deve residir em um nó WSFC (Windows Server Failover Clustering).  
  
-   A instância de servidor deve estar executando uma edição do SQL Server com suporte para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para obter mais informações, consulte [Features Supported by the Editions of SQL Server 2014](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
-   Habilitar Grupos de Disponibilidade AlwaysOn somente em uma instância de servidor de cada vez. Depois de habilitar os Grupos de Disponibilidade AlwaysOn, aguarde até que o serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tenha reiniciado antes de seguir para a próxima instância de servidor.  
  
 Para obter informações sobre os pré-requisitos adicionais para criar e configurar grupos de disponibilidade, consulte [pré-requisitos, restrições e recomendações &#40;para&#41;grupos de disponibilidade AlwaysOn SQL Server](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Security"></a> Segurança  
 Enquanto os Grupos de Disponibilidade AlwaysOn estiverem habilitados em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a instância de servidor terá total controle no cluster WSFC.  
  
####  <a name="Permissions"></a> Permissões  
 Requer a associação ao grupo **Administrador** no computador local e o controle total no cluster WSFC. Quando for habilitar o AlwaysOn usando o PowerShell, abra a janela Prompt de Comando usando a opção **Executar como administrador** .  
  
 Exige que o Active Directory crie objetos e gerencie permissões de objetos.  
  
##  <a name="IsEnabled"></a>Determinar se Grupos de Disponibilidade AlwaysOn está habilitado  
  
-   [SQL Server Management Studio](#SSMS1Procedure)  
  
-   [Transact-SQL](#Tsql1Procedure)  
  
-   [PowerShell](#PowerShell1Procedure)  
  
###  <a name="SSMS1Procedure"></a> Usando o SQL Server Management Studio  
 **Para determinar se Grupos de Disponibilidade AlwaysOn está habilitado**  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse na instância de servidor e clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Propriedades do Servidor** , clique na página **Geral** . A propriedade **Está habilitado para HADR** exibirá um dos seguintes valores:  
  
    -   **True**, se os Grupos de Disponibilidade AlwaysOn estiverem habilitados  
  
    -   **False**, se os Grupos de Disponibilidade AlwaysOn estiverem desabilitados  
  
###  <a name="Tsql1Procedure"></a> Usando Transact-SQL  
 **Para determinar se Grupos de Disponibilidade AlwaysOn está habilitado**  
  
1.  Use a seguinte instrução [SERVERPROPERTY](/sql/t-sql/functions/serverproperty-transact-sql) :  
  
    ```sql
    SELECT SERVERPROPERTY ('IsHadrEnabled');  
    ```  
  
     A configuração da propriedade de servidor `IsHadrEnabled` indica se uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está habilitada para Grupos de Disponibilidade AlwaysOn da seguinte forma:  
  
    -   Se `IsHadrEnabled` = 1, os Grupos de Disponibilidade AlwaysOn estão habilitados.  
  
    -   Se `IsHadrEnabled` = 0, os Grupos de Disponibilidade AlwaysOn estarão desabilitados.  
  
    > [!NOTE]  
    >  Para obter mais informações sobre a propriedade `IsHadrEnabled` Server, [consulte &#40;Transact-SQL&#41;ServerProperty](/sql/t-sql/functions/serverproperty-transact-sql).  
  
###  <a name="PowerShell1Procedure"></a> Usando o PowerShell  
 **Para determinar se Grupos de Disponibilidade AlwaysOn está habilitado**  
  
1.  Defina o padrão (`cd`) para a instância do servidor (por exemplo, `\SQL\NODE1\DEFAULT`) no qual você deseja determinar se [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] está habilitado.  
  
2.  Digite o seguinte comando `Get-Item` do PowerShell:  
  
    ```powershell
    Get-Item . | Select IsHadrEnabled  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet `Get-Help` no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="EnableAOAG"></a> Habilitar Grupos de Disponibilidade AlwaysOn  
 **Para habilitar o AlwaysOn, usando:**  
  
-   [SQL Server Configuration Manager](#SQLCM2Procedure)  
  
-   [PowerShell](#PScmd2Procedure)  
  
###  <a name="SQLCM2Procedure"></a> Usando o SQL Server Configuration Manager  
 **Para habilitar Grupos de Disponibilidade AlwaysOn**  
  
1.  Conecte-se ao nó do WSFC (Windows Server Failover Clustering) que hospeda a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] onde você deseja habilitar Grupos de Disponibilidade AlwaysOn.  
  
2.  No menu **Iniciar** , aponte para **Todos os Programas**, para [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
3.  Em **SQL Server Configuration Manager**, clique em **serviços SQL Server**, clique com o botão direito do mouse em SQL Server ( **< *`instance name`* >)** , em que **<`instance name`>**  é o nome de uma instância de servidor local para que você deseja habilitar Grupos de Disponibilidade AlwaysOn e clique em **Propriedades.**  
  
4.  Selecione a guia **Alta Disponibilidade AlwaysOn** .  
  
5.  Verifique se o campo **Nome do cluster de failover do Windows** contém o nome do cluster de failover local. Se esse campo estiver em branco, é porque essa instância de servidor não oferece suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]no momento. Pode ser que o computador local não seja um nó de cluster, o cluster WSFC tenha sido desligado ou essa edição do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] não ofereça suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].  
  
6.  Marque a caixa de seleção **Habilitar Grupos de Disponibilidade AlwaysOn** e clique em **OK**.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager salva suas alterações. Em seguida, você deve reiniciar manualmente o serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Isso permite escolher a hora de reinicialização mais adequada de acordo com as necessidades da sua empresa. Quando o serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] for reiniciado, AlwaysOn será habilitado e a propriedade de servidor `IsHadrEnabled` será definida como 1.  
  
###  <a name="PScmd2Procedure"></a> Usando o SQL Server PowerShell  
 **Para habilitar o AlwaysOn**  
  
1.  Altere o diretório (`cd`) para uma instância de servidor que você queira habilitar para Grupos de Disponibilidade AlwaysOn.  
  
2.  Use o cmdlet `Enable-SqlAlwaysOn` para habilitar Grupos de Disponibilidade AlwaysOn.  
  
     Para exibir a sintaxe de um cmdlet, use o cmdlet `Get-Help` no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
    > [!NOTE]  
    >  Para obter informações sobre como controlar se o cmdlet `Enable-SqlAlwaysOn` reinicia o serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [quando um cmdlet reinicia o serviço de SQL Server?](#WhenCmdletRestartsSQL), mais adiante neste tópico.  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
####  <a name="ExmplEnable-SqlHadrServic"></a> Exemplo: Enable-SqlAlwaysOn  
 O comando do PowerShell a seguir habilita o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em uma instância do SQL Server (*Computer*\\*Instance*).  
  
```powershell
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
```  
  
##  <a name="DisableAOAG"></a>Desabilitar Grupos de Disponibilidade AlwaysOn  
  
-   **Antes de desabilitar o AlwaysOn:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para desabilitar o AlwaysOn, usando:**  
  
    -   [SQL Server Configuration Manager](#SQLCM3Procedure)  
  
    -   [PowerShell](#PScmd3Procedure)  
  
-   **Acompanhamento:**  [depois de desabilitar o AlwaysOn](#FollowUp)  
  
> [!IMPORTANT]  
>  Desabilite AlwaysOn em somente uma instância de servidor de cada vez. Depois de desabilitar os Grupos de Disponibilidade AlwaysOn, aguarde até que o serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tenha reiniciado antes de seguir para a próxima instância de servidor.  
  
###  <a name="Recommendations"></a> Recomendações  
 Antes de você desabilitar o AlwaysOn em uma instância de servidor, nós recomendamos que você faça o seguinte:  
  
1.  Se a instância de servidor estiver hospedando a réplica primária de um grupo de disponibilidade que você deseja manter, nós recomendaremos que você realize manualmente o failover do grupo de disponibilidade para uma réplica secundária sincronizada, se possível. Para obter mais informações, veja [Executar um failover manual planejado de um grupo de disponibilidade &#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md).  
  
2.  Remova todas as réplicas secundárias locais. Para obter mais informações, veja [Remover uma réplica secundária de um grupo de disponibilidade &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md).  
  
###  <a name="SQLCM3Procedure"></a> Usando o SQL Server Configuration Manager  
 **Para desabilitar o AlwaysOn**  
  
1.  Conecte-se ao nó do WSFC (Windows Server Failover Clustering) que hospeda a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] onde você deseja desabilitar Grupos de Disponibilidade AlwaysOn.  
  
2.  No menu **Iniciar** , aponte para **Todos os Programas**, para [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
3.  Em **SQL Server Configuration Manager**, clique em **serviços SQL Server**, clique com o botão direito do mouse em SQL Server ( **< *`instance name`* >)** , em que **<`instance name`>**  é o nome de uma instância de servidor local para que você deseja desabilitar Grupos de Disponibilidade AlwaysOn e clique em **Propriedades**.  
  
4.  Na guia**Alta Disponibilidade AlwaysOn**, desmarque a caixa de seleção **Habilitar Grupos de Disponibilidade AlwaysOn** e clique em **OK**.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager salvará as alterações e reiniciará o serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Quando o serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] for reiniciado, AlwaysOn será desabilitado e a propriedade de servidor `IsHadrEnabled` será definida como 0 para indicar que os Grupos de Disponibilidade AlwaysOn estão desabilitados.  
  
5.  Recomendamos que você leia as informações em [Acompanhamento: depois de desabilitar o AlwaysOn](#FollowUp), mais adiante neste tópico.  
  
###  <a name="PScmd3Procedure"></a> Usando o SQL Server PowerShell  
 **Para desabilitar o AlwaysOn**  
  
1.  Altere o diretório (`cd`) para uma instância de servidor habilitada no momento que você deseja desativar para Grupos de Disponibilidade AlwaysOn.  
  
2.  Use o cmdlet `Disable-SqlAlwaysOn` para habilitar Grupos de Disponibilidade AlwaysOn.  
  
     Por exemplo, o comando a seguir desabilita Grupos de Disponibilidade AlwaysOn em uma instância de SQL Server (*computador*\\*instância*).  Este comando requer a reinicialização da instância e você será solicitado a confirmar esta reinicialização.  
  
    ```powershell
    Disable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
    ```  
  
    > [!IMPORTANT]  
    >  Para obter informações sobre como controlar se o cmdlet `Disable-SqlAlwaysOn` reinicia o serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [quando um cmdlet reinicia o serviço de SQL Server?](#WhenCmdletRestartsSQL), mais adiante neste tópico.  
  
     Para exibir a sintaxe de um cmdlet, use o cmdlet `Get-Help` no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
###  <a name="FollowUp"></a>Acompanhamento: depois de desabilitar o AlwaysOn  
 Depois que você desabilitar os grupos de disponibilidade AlwaysOn, a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deverá ser reiniciada. O SQL Server Configuration Manager reinicia a instância de servidor automaticamente. Porém, se você usou o cmdlet `Disable-SqlAlwaysOn`, precisará reiniciar a instância de servidor manualmente. Para obter mais informações, consulte [sqlservr Application](../../../tools/sqlservr-application.md).  
  
 Na instância de servidor reiniciada:  
  
-   Os bancos de dados de disponibilidade não iniciam na inicialização do SQL Server, tornando-os inacessíveis.  
  
-   A única instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] AlwaysOn com suporte é [DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql). CREATE AVAILABILITY GROUP, ALTER AVAILABILITY GROUP e as opções SET HADR de ALTER DATABASE não têm suporte.  
  
-   Os metadados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e os dados de configuração do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no WSFC não são afetados ao desabilitar os Grupos de Disponibilidade AlwaysOn.  
  
 Se você desabilitar os grupos de disponibilidade AlwaysOn permanentemente em todas as instâncias de servidor que hospedam uma réplica de disponibilidade para um ou mais grupos de disponibilidade, nós recomendaremos que você conclua as etapas a seguir:  
  
1.  Se você não removeu as réplicas de disponibilidade locais antes de desabilitar o AlwaysOn, exclua (ignore) cada grupo de disponibilidade para o qual a instância de servidor está hospedando uma réplica de disponibilidade. Para obter informações sobre como excluir um grupo de disponibilidade, veja [Remover um grupo de disponibilidade &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md).  
  
2.  Para remover os metadados deixados para trás, exclua (ignore) cada grupo de disponibilidade afetado em uma instância de servidor que faz parte do cluster do WSFC original.  
  
3.  Qualquer banco de dados primário continuará acessível a todas as conexões, mas a sincronização de dados entre os bancos de dados primário e secundário será interrompida.  
  
4.  Os bancos de dados secundários entram no estado RESTORING. Você pode excluí-los ou restaurá-los usando RESTORE WITH RECOVERY. No entanto, os bancos de dados restaurados não participarão mais da sincronização de dados de grupos de disponibilidade.  
  
##  <a name="WhenCmdletRestartsSQL"></a> Quando um cmdlet reinicia o serviço do SQL Server?  
 Em uma instância de servidor atualmente em execução, usando `Enable-SqlAlwaysOn` ou `Disable-SqlAlwaysOn` para alterar a configuração atual de AlwaysOn pode provocar a reinicialização do serviço do SQL Server. O comportamento de reinicialização depende das seguintes condições:  
  
|Parâmetro -NoServiceRestart especificado|Parâmetro -Force especificado|O serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] foi reiniciado?|  
|--------------------------------------------|---------------------------------|---------------------------------------------------------|  
|não|não|Por padrão. Mas o cmdlet solicita o seguinte:<br /><br /> **Para concluir esta ação, devemos reiniciar o serviço de SQL Server para a instância de servidor ' < instance_name > '. Deseja continuar?**<br /><br /> **[Y] Sim  [N] Não  [S] Suspender  [?] Ajuda (o padrão é “Y”):**<br /><br /> Se você especificar **N** ou **S**, o serviço não será reiniciado.|  
|não|Sim|O serviço será reiniciado.|  
|Sim|não|O serviço não será reiniciado.|  
|Sim|Sim|O serviço não será reiniciado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do &#40;grupos de disponibilidade AlwaysOn&#41; SQL Server](overview-of-always-on-availability-groups-sql-server.md)    
 [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)  
