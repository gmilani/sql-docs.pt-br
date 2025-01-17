---
title: Implementando pontos de extremidade | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- endpoints [SMO]
ms.assetid: f8674dbb-9bc0-488f-9def-e9e0ce1ddf86
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 042bc1cfe2ccf09580d052b1a4bc045d03fc81ee
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72796842"
---
# <a name="implementing-endpoints"></a>Implementando pontos de extremidade
  Um ponto de extremidade é um serviço que pode escutar nativamente solicitações. O SMO dá suporte a vários tipos de pontos de extremidade usando o objeto <xref:Microsoft.SqlServer.Management.Smo.Endpoint>. Para criar um serviço de ponto de extremidade que manipula um tipo específico de carga, que usa um protocolo específico, crie uma instância de um objeto <xref:Microsoft.SqlServer.Management.Smo.Endpoint> e defina suas propriedades.  
  
 A propriedade <xref:Microsoft.SqlServer.Management.Smo.Endpoint.EndpointType%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Endpoint> pode ser usada para especificar os tipos de carga a seguir:  
  
-   Espelhamento de banco de dados  
  
-   SOAP (o suporte a pontos de extremidade SOAP está presente no [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] e nas versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] )  
  
-   Service Broker  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)]  
  
 Além disso, a propriedade <xref:Microsoft.SqlServer.Management.Smo.Endpoint.ProtocolType%2A> pode ser usada para especificar os dois protocolos com suporte a seguir:  
  
-   Protocolo HTTP  
  
-   Protocolo TCP  
  
 Após a especificação do tipo de carga, a carga real pode ser definida usando a propriedade de objeto <xref:Microsoft.SqlServer.Management.Smo.Endpoint.Payload%2A>. A propriedade de objeto <xref:Microsoft.SqlServer.Management.Smo.Payload> fornece uma referência a um objeto de carga do tipo especificado para o qual as propriedades podem ser modificadas.  
  
 Para o objeto <xref:Microsoft.SqlServer.Management.Smo.DatabaseMirroringPayload>, especifique a função de espelhamento e se a criptografia está habilitada. O objeto <xref:Microsoft.SqlServer.Management.Smo.ServiceBrokerPayload> requer informações sobre o encaminhamento de mensagens, o número máximo de conexões permitidas e o modo de autenticação. O objeto <xref:Microsoft.SqlServer.Management.Smo.SoapPayloadMethod.%23ctor%2A> requer a definição de várias propriedades, incluindo a propriedade de objeto <xref:Microsoft.SqlServer.Management.Smo.SoapPayloadMethodCollection.Add%2A> que especifica os métodos de carga SOAP disponíveis para clientes (procedimentos armazenados e funções definidas pelo usuário).  
  
 Da mesma forma, o protocolo real pode ser definido através da propriedade de objeto <xref:Microsoft.SqlServer.Management.Smo.Endpoint.Protocol%2A> que referencia um objeto de protocolo do tipo especificado pela propriedade <xref:Microsoft.SqlServer.Management.Smo.Endpoint.ProtocolType%2A>. O objeto <xref:Microsoft.SqlServer.Management.Smo.HttpProtocol> requer uma lista de endereços IP restritos e informações sobre porta, site e autenticação. O objeto <xref:Microsoft.SqlServer.Management.Smo.TcpProtocol> também requer uma lista de endereços IP restritos e informações sobre porta.  
  
 Quando o ponto de extremidade estiver sido criado e totalmente definido, usuários do banco de dados, grupos, funções e logons poderão ter o acesso concedido, revogado e negado.  
  
## <a name="example"></a>Exemplo  
 Para o exemplo de código a seguir, selecione o ambiente de programação, o modelo de programação e a linguagem de programação para criar seu aplicativo. Para obter mais informações, consulte [criar um projeto Visual Basic Smo no Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) e [criar um projeto&#35; do Visual C Smo no Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-database-mirroring-endpoint-service-in-visual-basic"></a>Criando um serviço de ponto de extremidade de espelhamento de banco de dados no Visual Basic  
 O exemplo de código demonstra como criar um ponto de extremidade de espelhamento de banco de dados no SMO. Isso é necessário antes da criação de um espelho de banco de dados. Use o <xref:Microsoft.SqlServer.Management.Smo.Database.IsMirroringEnabled%2A> e outras propriedades do objeto <xref:Microsoft.SqlServer.Management.Smo.Database> para criar um espelho de banco de dados.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBEndpoints1](SMO How to#SMO_VBEndpoints1)]  -->  
  
## <a name="creating-a-database-mirroring-endpoint-service-in-visual-c"></a>Criando um serviço de ponto de extremidade de espelhamento de banco de dados no Visual C#  
 O exemplo de código demonstra como criar um ponto de extremidade de espelhamento de banco de dados no SMO. Isso é necessário antes da criação de um espelho de banco de dados. Use o <xref:Microsoft.SqlServer.Management.Smo.Database.IsMirroringEnabled%2A> e outras propriedades do objeto <xref:Microsoft.SqlServer.Management.Smo.Database> para criar um espelho de banco de dados.  
  
```csharp
{  
            //Set up a database mirroring endpoint on the server before   
        //setting up a database mirror.   
        //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Define an Endpoint object variable for database mirroring.   
            Endpoint ep = default(Endpoint);  
            ep = new Endpoint(srv, "Mirroring_Endpoint");  
            ep.ProtocolType = ProtocolType.Tcp;  
            ep.EndpointType = EndpointType.DatabaseMirroring;  
            //Specify the protocol ports.   
            ep.Protocol.Http.SslPort = 5024;  
            ep.Protocol.Tcp.ListenerPort = 6666;  
            //Specify the role of the payload.   
            ep.Payload.DatabaseMirroring.ServerMirroringRole = ServerMirroringRole.All;  
            //Create the endpoint on the instance of SQL Server.   
            ep.Create();  
            //Start the endpoint.   
            ep.Start();  
            Console.WriteLine(ep.EndpointState);  
        }  
```  
  
## <a name="creating-a-database-mirroring-endpoint-service-in-powershell"></a>Criando um serviço de ponto de extremidade de espelhamento de banco de dados no PowerShell  
 O exemplo de código demonstra como criar um ponto de extremidade de espelhamento de banco de dados no SMO. Isso é necessário antes da criação de um espelho de banco de dados. Use o <xref:Microsoft.SqlServer.Management.Smo.Database.IsMirroringEnabled%2A> e outras propriedades do objeto <xref:Microsoft.SqlServer.Management.Smo.Database> para criar um espelho de banco de dados.  
  
```powershell
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = Get-Item default  
  
#Get a new endpoint to congure and add  
$ep = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Endpoint -argumentlist $srv,"Mirroring_Endpoint"  
  
#Set some properties  
$ep.ProtocolType = [Microsoft.SqlServer.Management.SMO.ProtocolType]::Tcp  
$ep.EndpointType = [Microsoft.SqlServer.Management.SMO.EndpointType]::DatabaseMirroring  
$ep.Protocol.Http.SslPort = 5024  
$ep.Protocol.Tcp.ListenerPort = 6666 #inline comment  
$ep.Payload.DatabaseMirroring.ServerMirroringRole = [Microsoft.SqlServer.Management.SMO.ServerMirroringRole]::All  
  
# Create the endpoint on the instance  
$ep.Create()  
  
# Start the endpoint  
$ep.Start()  
  
# Report its state  
$ep.EndpointState;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
