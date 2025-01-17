---
title: Carregando e executando um pacote local de forma programática | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Integration Services packages, running
- events [Integration Services], capturing
- packages [Integration Services], running
- loading packages programmatically
- Visual Basic [Integration Services]
- running packages [Integration Services]
- programmatically load and run packages [SSIS]
ms.assetid: 2f9fc1a8-a001-4c54-8c64-63b443725422
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d8f9264a456464b40cfce4382cb7d70cbb7ce4cf
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295760"
---
# <a name="loading-and-running-a-local-package-programmatically"></a>Carregando e executando um pacote local programaticamente

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  É possível executar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] conforme necessário ou em horários predeterminados por meio dos métodos descritos em [Executando pacotes](../packages/run-integration-services-ssis-packages.md). Entretanto, bastam algumas linhas de código para executar um pacote de um aplicativo personalizado, como, por exemplo, um aplicativo Windows Forms, um aplicativo do console, um formulário/serviço da Web ASP.NET ou um serviço do Windows.  
  
 Esse tópico discute:  
  
-   Carregando um pacote programaticamente  
  
-   Executando um pacote programaticamente  
  
 Todos os métodos usados nesse tópico para carregar e executar pacotes exigem uma referência ao assembly **Microsoft.SqlServer.ManagedDTS**. Após adicionar a referência em um novo projeto, importe o namespace <xref:Microsoft.SqlServer.Dts.Runtime> com uma instrução **using** ou **Imports**.  
  
## <a name="loading-a-package-programmatically"></a>Carregando um pacote programaticamente  
 Para carregar um pacote programaticamente no computador local, se o pacote for armazenado local ou remotamente, chame um destes métodos:  
  
|Local de armazenamento|Método de chamada|  
|----------------------|--------------------|  
|Arquivo|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadPackage%2A>|  
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromSqlServer%2A>|  
  
> [!IMPORTANT]  
>  Os métodos da classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> para trabalhar com o Repositório de Pacotes SSIS só dão suporte a ".", localhost ou ao nome do servidor local. Você não pode usar "(local)".  
  
## <a name="running-a-package-programmatically"></a>Executando um pacote programaticamente  
 O desenvolvimento de um aplicativo personalizado em código gerenciado que executa um pacote no computador local requer a abordagem a seguir. As etapas resumidas aqui são demonstradas no exemplo de aplicativo de console a seguir.  
  
#### <a name="to-run-a-package-on-the-local-computer-programmatically"></a>Para executar um pacote programaticamente no computador local  
  
1.  Inicie o ambiente de desenvolvimento do Visual Studio e crie um aplicativo novo no idioma de desenvolvimento de sua preferência. Esse exemplo usa um aplicativo de console; contudo, você também pode executar um pacote de um aplicativo Windows Forms, de um formulário/serviço da Web ASP.NET ou de um serviço do Windows.  
  
2.  No menu **Projeto**, clique em **Adicionar Referência** e adicione uma referência a **Microsoft.SqlServer.ManagedDTS.dll**. Clique em **OK**.  
  
3.  Usar a instrução **Imports** do Visual Basic ou a instrução **using** do C# para importar o namespace **Microsoft.SqlServer.Dts.Runtime**.  
  
4.  Adicione o código a seguir na rotina principal. O aplicativo de console completo deve ter a aparência do exemplo a seguir.  
  
    > [!NOTE]  
    >  O código de exemplo demonstra o carregamento do pacote do sistema de arquivos através do método <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadPackage%2A>. Mas você também pode carregar o pacote a partir do banco de dados MSDB, chamando o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromSqlServer%2A>, ou a partir do repositório do pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], chamando o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A>.  
  
5.  Execute o projeto. O código de exemplo executa o pacote de exemplo CalculatedColumns que é instalado com os exemplos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O resultado da execução do pacote é exibido na janela de console.  
  
### <a name="sample-code"></a>Código de exemplo  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkgLocation As String  
    Dim pkg As New Package  
    Dim app As New Application  
    Dim pkgResults As DTSExecResult  
  
    pkgLocation = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx"  
    pkg = app.LoadPackage(pkgLocation, Nothing)  
    pkgResults = pkg.Execute()  
  
    Console.WriteLine(pkgResults.ToString())  
    Console.ReadKey()  
  
  End Sub  
  
End Module  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace RunFromClientAppCS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string pkgLocation;  
      Package pkg;  
      Application app;  
      DTSExecResult pkgResults;  
  
      pkgLocation =  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx";  
      app = new Application();  
      pkg = app.LoadPackage(pkgLocation, null);  
      pkgResults = pkg.Execute();  
  
      Console.WriteLine(pkgResults.ToString());  
      Console.ReadKey();  
    }  
  }  
}  
```  
  
## <a name="capturing-events-from-a-running-package"></a>Capturando eventos de um pacote em execução  
 Quando você executar um pacote programaticamente, conforme mostrado no exemplo anterior, talvez também queira capturar erros e outros eventos que ocorram durante a execução do pacote. Para fazer isso, adicione uma classe herdada da classe <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> e passe uma referência para essa classe quando carregar o pacote. Embora o exemplo a seguir capture apenas o evento <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents.OnError%2A>, há vários outros eventos que a classe <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> permite que você capture.  
  
#### <a name="to-run-a-package-on-the-local-computer-programmatically-and-capture-package-events"></a>Para executar um pacote programaticamente no computador local e capturar eventos de pacote  
  
1.  Siga as etapas do exemplo anterior para criar um projeto para esse exemplo.  
  
2.  Adicione o código a seguir na rotina principal. O aplicativo de console completo deve ter a aparência do exemplo a seguir.  
  
3.  Execute o projeto. O código de exemplo executa o pacote de exemplo CalculatedColumns que é instalado com os exemplos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O resultado da execução do pacote é exibido na janela de console, junto com eventuais erros.  
  
### <a name="sample-code"></a>Código de exemplo  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkgLocation As String  
    Dim pkg As New Package  
    Dim app As New Application  
    Dim pkgResults As DTSExecResult  
  
    Dim eventListener As New EventListener()  
  
    pkgLocation = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx"  
    pkg = app.LoadPackage(pkgLocation, eventListener)  
    pkgResults = pkg.Execute(Nothing, Nothing, eventListener, Nothing, Nothing)  
  
    Console.WriteLine(pkgResults.ToString())  
    Console.ReadKey()  
  
  End Sub  
  
End Module  
  
Class EventListener  
  Inherits DefaultEvents  
  
  Public Overrides Function OnError(ByVal source As Microsoft.SqlServer.Dts.Runtime.DtsObject, _  
    ByVal errorCode As Integer, ByVal subComponent As String, ByVal description As String, _  
    ByVal helpFile As String, ByVal helpContext As Integer, _  
    ByVal idofInterfaceWithError As String) As Boolean  
  
    ' Add application-specific diagnostics here.  
    Console.WriteLine("Error in {0}/{1} : {2}", source, subComponent, description)  
    Return False  
  
  End Function  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace RunFromClientAppWithEventsCS  
{  
  class MyEventListener : DefaultEvents  
  {  
    public override bool OnError(DtsObject source, int errorCode, string subComponent,   
      string description, string helpFile, int helpContext, string idofInterfaceWithError)  
    {  
      // Add application-specific diagnostics here.  
      Console.WriteLine("Error in {0}/{1} : {2}", source, subComponent, description);  
      return false;  
    }  
  }  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string pkgLocation;  
      Package pkg;  
      Application app;  
      DTSExecResult pkgResults;  
  
      MyEventListener eventListener = new MyEventListener();  
  
      pkgLocation =  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx";  
      app = new Application();  
      pkg = app.LoadPackage(pkgLocation, eventListener);  
      pkgResults = pkg.Execute(null, null, eventListener, null, null);  
  
      Console.WriteLine(pkgResults.ToString());  
      Console.ReadKey();  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Compreender as diferenças entre execução local e remota](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [Carregar e executar um pacote remoto programaticamente](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [Carregar a saída de um pacote local](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
