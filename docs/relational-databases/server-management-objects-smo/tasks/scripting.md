---
title: Script | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- dependencies [SMO]
- scripts [SMO]
ms.assetid: 13a35511-3987-426b-a3b7-3b2e83900dc7
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 63f6e86f08ea93525704159483b939c79c6575d8
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909036"
---
# <a name="scripting"></a>Script
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  O script no SMO é controlado pelo objeto de <xref:Microsoft.SqlServer.Management.Smo.Scripter> e seus objetos filho, ou pelo método de **script** em objetos individuais. O objeto <xref:Microsoft.SqlServer.Management.Smo.Scripter> controla o mapeamento de relações de dependência para objetos em uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 A geração de scripts avançada usando o objeto <xref:Microsoft.SqlServer.Management.Smo.Scripter> e seus objetos filhos é um processo trifásico:  
  
1.  Descoberta  
  
2.  Geração de lista  
  
3.  Geração de scripts  

 A fase de descoberta usa o objeto <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker>. Dada uma lista de URNs de objetos, o método <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker.DiscoverDependencies%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker> retorna um objeto <xref:Microsoft.SqlServer.Management.Smo.DependencyTree> para os objetos na lista de URNs. O parâmetro booliano *fParents* é usado para selecionar se os pais ou filhos do objeto especificado devem ser descobertos. A árvore de dependência pode ser modificada nesta fase.  
  
 Na fase de geração de lista, a árvore é transmitida e a lista resultante é retornada. Essa lista de objetos está em ordem de scripts e pode ser manipulada.  
  
 As fases da geração de lista usam o método <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker.WalkDependencies%2A> para retornar um <xref:Microsoft.SqlServer.Management.Smo.DependencyTree>. O <xref:Microsoft.SqlServer.Management.Smo.DependencyTree> pode ser modificado nesta fase.  
  
 Na terceira e última fases, um script é gerado com a lista especificada e opções de script. O resultado é retornado como um objeto do sistema <xref:System.Collections.Specialized.StringCollection>. Nesta fase, os nomes de objetos dependentes são extraídos da coleção de itens do objeto <xref:Microsoft.SqlServer.Management.Smo.DependencyTree> e de propriedades tais como <xref:Microsoft.SqlServer.Management.Smo.DependencyTree.NumberOfSiblings%2A> e <xref:Microsoft.SqlServer.Management.Smo.DependencyTree.FirstChild%2A>.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto&#35; do Visual C Smo no Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
 Este exemplo de código requer uma instrução **Imports** para o namespace System. Collections. especializada. Insira isto junto com as outras instruções Imports, antes de qualquer declaração do aplicativo.  
  
```  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
Imports System.Collections.Specialized  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-visual-basic"></a>Gerando scripts das dependências para um banco de dados no Visual Basic  
 Este exemplo de código mostra como descobrir as dependências e iterar pela lista para exibir os resultados.  
  
```  
' compile with:   
' /r:Microsoft.SqlServer.Smo.dll   
' /r:Microsoft.SqlServer.ConnectionInfo.dll   
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Sdk.Sfc  
  
Public Class A  
   Public Shared Sub Main()  
      ' database name  
      Dim dbName As [String] = "AdventureWorksLT2012"   ' database name  
  
      ' Connect to the local, default instance of SQL Server.   
      Dim srv As New Server()  
  
      ' Reference the database.    
      Dim db As Database = srv.Databases(dbName)  
  
      ' Define a Scripter object and set the required scripting options.   
      Dim scrp As New Scripter(srv)  
      scrp.Options.ScriptDrops = False  
      scrp.Options.WithDependencies = True  
      scrp.Options.Indexes = True   ' To include indexes  
      scrp.Options.DriAllConstraints = True   ' to include referential constraints in the script  
  
      ' Iterate through the tables in database and script each one. Display the script.  
      For Each tb As Table In db.Tables  
         ' check if the table is not a system table  
         If tb.IsSystemObject = False Then  
            Console.WriteLine("-- Scripting for table " + tb.Name)  
  
            ' Generating script for table tb  
            Dim sc As System.Collections.Specialized.StringCollection = scrp.Script(New Urn() {tb.Urn})  
            For Each st As String In sc  
               Console.WriteLine(st)  
            Next  
            Console.WriteLine("--")  
         End If  
      Next  
   End Sub  
End Class  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-visual-c"></a>Gerando scripts das dependências para um banco de dados no Visual C#  
 Este exemplo de código mostra como descobrir as dependências e iterar pela lista para exibir os resultados.  
  
```  
// compile with:   
// /r:Microsoft.SqlServer.Smo.dll   
// /r:Microsoft.SqlServer.ConnectionInfo.dll   
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
using System;  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Sdk.Sfc;  
  
public class A {  
   public static void Main() {   
      String dbName = "AdventureWorksLT2012"; // database name  
  
      // Connect to the local, default instance of SQL Server.   
      Server srv = new Server();  
  
      // Reference the database.    
      Database db = srv.Databases[dbName];  
  
      // Define a Scripter object and set the required scripting options.   
      Scripter scrp = new Scripter(srv);  
      scrp.Options.ScriptDrops = false;  
      scrp.Options.WithDependencies = true;  
      scrp.Options.Indexes = true;   // To include indexes  
      scrp.Options.DriAllConstraints = true;   // to include referential constraints in the script  
  
      // Iterate through the tables in database and script each one. Display the script.     
      foreach (Table tb in db.Tables) {   
         // check if the table is not a system table  
         if (tb.IsSystemObject == false) {  
            Console.WriteLine("-- Scripting for table " + tb.Name);  
  
            // Generating script for table tb  
            System.Collections.Specialized.StringCollection sc = scrp.Script(new Urn[]{tb.Urn});  
            foreach (string st in sc) {  
               Console.WriteLine(st);  
            }  
            Console.WriteLine("--");  
         }  
      }   
   }  
}  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-powershell"></a>Gerando scripts das dependências para um banco de dados no PowerShell  
 Este exemplo de código mostra como descobrir as dependências e iterar pela lista para exibir os resultados.  
  
```  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default  
  
# Create a Scripter object and set the required scripting options.  
$scrp = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Scripter -ArgumentList (Get-Item .)  
$scrp.Options.ScriptDrops = $false  
$scrp.Options.WithDependencies = $true  
$scrp.Options.IncludeIfNotExists = $true  
  
# Set the path context to the tables in AdventureWorks2012.  
  
CD Databases\AdventureWorks2012\Tables  
  
foreach ($Item in Get-ChildItem)  
 {    
 $scrp.Script($Item)  
 }  
```  
  
  
