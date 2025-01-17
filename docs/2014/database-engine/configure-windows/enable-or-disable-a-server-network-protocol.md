---
title: Habilitar ou desabilitar um protocolo de rede de servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- network protocols [SQL Server], disabling
- remote connections [SQL Server], enabling using Configuration Manager
- protocols [SQL Server], enabling using Configuration Manager
- protocols [SQL Server], disabling using Configuration Manager
- disabling network protocols, Configuration Manager
- network protocols [SQL Server], enabling
- enabling network protocols, Configuration Manager
- surface area configuration [SQL Server], connection protocols
- connections [SQL Server], enabling remote using Configuration Manager
ms.assetid: ec5ccb69-61c9-4576-8843-014b976fd46e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 917abf00789cfca75ee6edb52ffef07832bfe981
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783035"
---
# <a name="enable-or-disable-a-server-network-protocol"></a>Habilitar ou desabilitar um protocolo de rede de servidor
  Todos os protocolos de rede são instalados pela Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mas podem ou não ser habilitados. Este tópico descreve como habilitar ou desabilitar um protocolo de rede de servidor no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager ou o PowerShell. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve ser interrompido e reiniciado para que a alteração entre em vigor.  
  
> [!IMPORTANT]  
>  Durante instalação do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , é adicionado um logon para o grupo BUILTIN\Users. Assim, todos os usuários autenticados do computador podem acessar a instância do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] como membros da função pública. O logon BUILTIN\Users pode ser removido com segurança para restringir o acesso a [!INCLUDE[ssDE](../../includes/ssde-md.md)] aos usuários do computador que têm logons individuais ou que são membros de outros grupos do Windows com logons.  
  
> [!WARNING]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] support TLS 1.0 e SSL 3.0. Se você impor um protocolo diferente (como TLS 1.1 ou TLS 1.2) fazendo alterações na camada de sistema operacional SChannel, suas conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderão falhar.  
  
 **Neste tópico**  
  
-   **Para habilitar ou desabilitar um protocolo de rede de servidor usando:**  
  
     [SQL Server Configuration Manager](#SSMSProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-enable-a-server-network-protocol"></a>Para habilitar um protocolo de rede de servidor  
  
1.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no painel de console, expanda **Configuração de Rede do SQL Server**.  
  
2.  No painel do console, clique em **Protocolos de** *\<instance name>* .  
  
3.  No painel de detalhes, clique com o botão direito do mouse no protocolo que você quer alterar e clique em **Habilitar** ou **Desabilitar**.  
  
4.  No painel de console, clique em **Serviços do SQL Server**.  
  
5.  No painel de detalhes, clique com o botão direito do mouse em **SQL Server (***\<instance name>***)** e, depois, clique em **Reiniciar** para parar e reiniciar o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="PowerShellProcedure"></a> Usando o SQL Server PowerShell  
  
#### <a name="to-enable-a-server-network-protocol-using-powershell"></a>Para habilitar um protocolo de rede de servidor usando o PowerShell  
  
1.  Usando as permissões de administrador, abra um prompt de comando.  
  
2.  Inicie o Windows PowerShell 2.0 na barra de tarefas ou clique em Iniciar, Todos os Programas, Acessórios, Windows PowerShell e Windows PowerShell.  
  
3.  Importe o módulo **sqlps** inserindo `Import-Module "sqlps"`  
  
4.  Execute as instruções a seguir para habilitar os protocolos TCP e de pipes nomeados. Substitua `<computer_name>` pelo nome do computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se estiver configurando uma instância nomeada, substitua `MSSQLSERVER` pelo nome da instância.  
  
     Para desabilitar protocolos, defina as propriedades `IsEnabled` como `$false`.  
  
    ```powershell
    $smo = 'Microsoft.SqlServer.Management.Smo.'  
    $wmi = new-object ($smo + 'Wmi.ManagedComputer').  
  
    # List the object properties, including the instance names.  
    $Wmi  
  
    # Enable the TCP protocol on the default instance.  
    $uri = "ManagedComputer[@Name='<computer_name>']/ ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
    $Tcp = $wmi.GetSmoObject($uri)  
    $Tcp.IsEnabled = $true  
    $Tcp.Alter()  
    $Tcp  
  
    # Enable the named pipes protocol for the default instance.  
    $uri = "ManagedComputer[@Name='<computer_name>']/ ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Np']"  
    $Np = $wmi.GetSmoObject($uri)  
    $Np.IsEnabled = $true  
    $Np.Alter()  
    $Np  
    ```  
  
#### <a name="to-configure-the-protocols-for-the-local-computer"></a>Para configurar os protocolos para o computador local  
  
-   Quando o script é executado localmente e configura o computador local, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell pode tornar o script mais flexível determinando o nome do computador local dinamicamente. Para recuperar o nome de computador local, substitua a linha que define a variável `$uri` pela linha a seguir.  
  
    ```powershell
    $uri = "ManagedComputer[@Name='" + (Get-Item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
    ```  
  
#### <a name="to-restart-the-database-engine-by-using-sql-server-powershell"></a>Para reiniciar o Mecanismo de Banco de Dados usando o SQL Server PowerShell  
  
-   Depois de habilitar ou desabilitar os protocolos, você deve parar e reiniciar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para que a alteração entre em vigor. Execute as instruções a seguir para parar e iniciar a instância padrão usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. Para parar e iniciar uma instância nomeada, substitua `'MSSQLSERVER'` por `'MSSQL$<instance_name>'`.  
  
    ```powershell
    # Get a reference to the ManagedComputer class.  
    CD SQLSERVER:\SQL\<computer_name>  
    $Wmi = (Get-Item .).ManagedComputer  
    # Get a reference to the default instance of the Database Engine.  
    $DfltInstance = $Wmi.Services['MSSQLSERVER']  
    # Display the state of the service.  
    $DfltInstance  
    # Stop the service.  
    $DfltInstance.Stop();  
    # Wait until the service has time to stop.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    # Start the service again.  
    $DfltInstance.Start();  
    # Wait until the service has time to start.  
    # Refresh the cache and display the state of the service.  
    $DfltInstance.Refresh(); $DfltInstance  
    ```  
