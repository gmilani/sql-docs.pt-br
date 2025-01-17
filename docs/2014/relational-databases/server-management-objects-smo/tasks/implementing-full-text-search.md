---
title: Implementando a pesquisa de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- full-text search [SMO]
ms.assetid: 9ce9ad9c-f671-4760-90b5-e0c8ca051473
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6ddc3521031f34f179cdfef08abf178f21f5f47e
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72796716"
---
# <a name="implementing-full-text-search"></a>Implementando a pesquisa de texto completo
  A pesquisa de texto completo está disponível por instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e é representada no SMO pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Server.FullTextService%2A>. O objeto <xref:Microsoft.SqlServer.Management.Smo.FullTextService> reside sob o objeto `Server`. Ele é usado para gerenciar as opções de configuração do serviço de Pesquisa de Texto Completo da [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. O objeto <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalogCollection> pertence ao objeto <xref:Microsoft.SqlServer.Management.Smo.Database> e é uma coleção de objetos <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> que representam catálogos de texto completo definidos para o banco de dados. Você só pode ter um índice de texto completo definido para cada tabela, diferente de índices normais. Isso é representado por um objeto <xref:Microsoft.SqlServer.Management.Smo.FullTextIndexColumn> no objeto <xref:Microsoft.SqlServer.Management.Smo.Table>.  
  
 Para criar uma serviço de pesquisa de texto completo, você precisa ter um catálogo de texto completo definido no banco de dados e um índice de pesquisa de texto completo definido em uma das tabelas do banco de dados.  
  
 Primeiro, crie um catálogo de texto completo no banco de dados chamando o construtor <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> e especificando o nome do catálogo. Depois, crie o índice de texto completo chamando o construtor e especificando a tabela na qual ele será criado. Depois, você poderá adicionar colunas de índice ao índice de texto completo, usando o objeto <xref:Microsoft.SqlServer.Management.Smo.FullTextIndexColumn> e fornecendo o nome da coluna dentro da tabela. Em seguida, defina a propriedade <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex.CatalogName%2A> para o catálogo criado. Finalmente, chame o método <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex.Create%2A> e crie o índice de texto completo na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto Visual Basic Smo no Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) ou [criar um projeto&#35; do Visual C Smo no Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-full-text-search-service-in-visual-basic"></a>Criando um serviço de pesquisa de texto completo no Visual Basic  
 Este exemplo de código cria um catálogo de pesquisa de texto completo para a tabela `ProductCategory` no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . Ele cria um índice de pesquisa de texto completo na coluna Nome da tabela `ProductCategory` . O índice de pesquisa de texto completo exige que haja um índice exclusivo já definido na coluna.  
  
```vb
' compile with:   
' /r:Microsoft.SqlServer.SqlEnum.dll   
' /r:Microsoft.SqlServer.Smo.dll   
' /r:Microsoft.SqlServer.ConnectionInfo.dll   
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Sdk.Sfc  
Imports Microsoft.SqlServer.Management.Common  
  
Public Class A  
   Public Shared Sub Main()  
      ' Connect to the local, default instance of SQL Server.  
      Dim srv As Server = Nothing  
      srv = New Server()  
  
      ' Reference the AdventureWorks database.  
      Dim db As Database = Nothing  
      db = srv.Databases("AdventureWorks")  
  
      ' Reference the ProductCategory table.  
      Dim tb As Table = Nothing  
      tb = db.Tables("ProductCategory", "Production")  
  
      ' Define a FullTextCatalog object variable by specifying the parent database and name arguments in the constructor.  
      Dim ftc As FullTextCatalog = Nothing  
      ftc = New FullTextCatalog(db, "Test_Catalog")  
      ftc.IsDefault = True  
  
      ' Create the Full-Text Search catalog on the instance of SQL Server.  
      ftc.Create()  
  
      ' Define a FullTextIndex object varaible by supplying the parent table argument in the constructor.  
      Dim fti As FullTextIndex = Nothing  
      fti = New FullTextIndex(tb)  
  
      ' Define a FullTextIndexColumn object variable by supplying the parent index and column name arguments in the constructor.  
      Dim ftic As FullTextIndexColumn = Nothing  
      ftic = New FullTextIndexColumn(fti, "Name")  
  
      ' Add the indexed column to the index.  
      fti.IndexedColumns.Add(ftic)  
      fti.ChangeTracking = ChangeTracking.Automatic  
  
      ' Specify the unique index on the table that is required by the Full Text Search index.  
      fti.UniqueIndexName = "AK_ProductCategory_Name"  
  
      ' Specify the catalog associated with the index.  
      fti.CatalogName = "Test_Catalog"  
  
      ' Create the Full Text Search index on the instance of SQL Server.  
      fti.Create()  
   End Sub  
End Class  
```  
  
## <a name="creating-a-full-text-search-service-in-visual-c"></a>Criando um serviço de pesquisa de texto completo no Visual C#  
 Este exemplo de código cria um catálogo de pesquisa de texto completo para a tabela `ProductCategory` no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . Ele cria um índice de pesquisa de texto completo na coluna Nome da tabela `ProductCategory` . O índice de pesquisa de texto completo exige que haja um índice exclusivo já definido na coluna.  
  
```csharp
// compile with:   
// /r:Microsoft.SqlServer.SqlEnum.dll   
// /r:Microsoft.SqlServer.Smo.dll   
// /r:Microsoft.SqlServer.ConnectionInfo.dll   
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Sdk.Sfc;  
using Microsoft.SqlServer.Management.Common;  
  
public class A {  
   public static void Main() {  
      // Connect to the local, default instance of SQL Server.  
      Server srv = default(Server);  
      srv = new Server();  
  
      // Reference the AdventureWorks database.  
      Database db = default(Database);  
      db = srv.Databases ["AdventureWorks"];  
  
      // Reference the ProductCategory table.  
      Table tb = default(Table);  
      tb = db.Tables["ProductCategory", "Production"];  
  
      // Define a FullTextCatalog object variable by specifying the parent database and name arguments in the constructor.  
      FullTextCatalog ftc = default(FullTextCatalog);  
      ftc = new FullTextCatalog(db, "Test_Catalog");  
      ftc.IsDefault = true;  
  
      // Create the Full-Text Search catalog on the instance of SQL Server.  
      ftc.Create();  
  
      // Define a FullTextIndex object varaible by supplying the parent table argument in the constructor.  
      FullTextIndex fti = default(FullTextIndex);  
      fti = new FullTextIndex(tb);  
  
      // Define a FullTextIndexColumn object variable by supplying the parent index and column name arguments in the constructor.  
      FullTextIndexColumn ftic = default(FullTextIndexColumn);  
      ftic = new FullTextIndexColumn(fti, "Name");  
  
      // Add the indexed column to the index.  
      fti.IndexedColumns.Add(ftic);  
      fti.ChangeTracking = ChangeTracking.Automatic;  
  
      // Specify the unique index on the table that is required by the Full Text Search index.  
      fti.UniqueIndexName = "AK_ProductCategory_Name";  
  
      // Specify the catalog associated with the index.  
      fti.CatalogName = "Test_Catalog";  
  
      // Create the Full Text Search index on the instance of SQL Server.  
      fti.Create();  
   }  
}  
```  
  
## <a name="creating-a-full-text-search-service-in-powershell"></a>Criando um serviço de pesquisa de texto completo no PowerShell  
 Este exemplo de código cria um catálogo de pesquisa de texto completo para a tabela `ProductCategory` no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . Ele cria um índice de pesquisa de texto completo na coluna Nome da tabela `ProductCategory` . O índice de pesquisa de texto completo exige que haja um índice exclusivo já definido na coluna.  
  
```powershell
# Example of implementing a full text search on the default instance.  
# Set the path context to the local, default instance of SQL Server and database tables  
  
CD \sql\localhost\default\databases  
$db = Get-Item AdventureWorks2012  
  
CD AdventureWorks\tables  
  
#Get a reference to the table  
$tb = Get-Item Production.ProductCategory  
  
# Define a FullTextCatalog object variable by specifying the parent database and name arguments in the constructor.  
  
$ftc = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextCatalog -ArgumentList $db, "Test_Catalog2"  
$ftc.IsDefault = $true  
  
# Create the Full Text Search catalog on the instance of SQL Server.  
$ftc.Create()  
  
# Define a FullTextIndex object variable by supplying the parent table argument in the constructor.  
$fti = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextIndex -ArgumentList $tb  
  
#  Define a FullTextIndexColumn object variable by supplying the parent index
#  and column name arguments in the constructor.  
  
$ftic = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextIndexColumn -ArgumentList $fti, "Name"  
  
# Add the indexed column to the index.  
$fti.IndexedColumns.Add($ftic)  
  
# Set change tracking  
$fti.ChangeTracking = [Microsoft.SqlServer.Management.SMO.ChangeTracking]::Automatic  
  
# Specify the unique index on the table that is required by the Full Text Search index.  
$fti.UniqueIndexName = "AK_ProductCategory_Name"  
  
# Specify the catalog associated with the index.  
$fti.CatalogName = "Test_Catalog2"  
  
# Create the Full Text Search Index  
$fti.Create()  
```  
