---
title: Métodos de envio em lote | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- methods [Reporting Services], batches
- BatchHeader SOAP header
- Web service [Reporting Services], methods
- Report Server Web service, batching
- batches [Reporting Services]
- XML Web service [Reporting Services], methods
- locking [Reporting Services]
- multiple Web service methods
ms.assetid: 86435534-c9fe-4b49-b88c-7fb6d21976b0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8b7ec19101b1abcb2e0fb825923cce7a237149dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63020140"
---
# <a name="batching-methods"></a>Métodos de processamento em lote
  O uso de cabeçalhos SOAP no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] permite que você inclua vários métodos de serviço Web em uma única operação. Os métodos são executados dentro do escopo de uma única transação de banco de dados, na ordem que são chamados.  
  
 A reversão é uma vantagem da utilização de operações de lote de vários métodos. Se houver um erro em qualquer uma das chamadas de método durante a execução do lote, o servidor de relatório interromperá a execução do lote e reverterá qualquer operação anterior. Isso é útil quando uma chamada de método depende da conclusão bem-sucedida de outras chamadas de método daquele lote.  
  
 O serviço Web não oferece semântica de bloqueio para operações de lote de vários métodos. As linhas do banco de dados do servidor de relatório não estarão bloqueadas para atualização até que a mensagem seja enviada ao servidor e que o comando Execute seja chamado.  
  
 Também não há nenhum controle de simultaneidade para garantir que o banco de dados não foi alterado desde que os dados foram lidos pela última vez. Se dois clientes modificarem o mesmo item, a última atualização terá êxito se os parâmetros ainda forem válidos (por exemplo, o item ainda não foi renomeado).  
  
 O exemplo a seguir chama o método <xref:ReportService2005.ReportingService2005.CreateFolder%2A> três vezes e executa essas chamadas como um único lote. Se qualquer uma das chamadas para <xref:ReportService2005.ReportingService2005.CreateFolder%2A> falhar, o lote inteiro será cancelado.  
  
```vb  
Imports System  
Imports System.Web.Services.Protocols  
Imports myNamespace.MyReferenceName  
  
Class Sample  
    Sub Main(args() As String)  
        Dim rs As New ReportingService2005()  
        rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
      ' Set the base Web service URL of the source server  
      rs.Url = "http://<Server Name>/reportserver/ReportService2005.asmx"  
  
        Dim bh As New BatchHeader()  
  
        bh.BatchId = service.CreateBatch()  
        rs.BatchHeaderValue = bh  
        rs.CreateFolder("New Folder1", "/", Nothing)  
        rs.CreateFolder("New Folder2", "/", Nothing)  
        rs.CreateFolder("New Folder3", "/", Nothing)  
  
        Console.WriteLine("Creating folders...")  
        rs.BatchHeaderValue = bh  
        rs.ExecuteBatch()  
        Console.WriteLine("Folders created successfully.")  
  
        rs.BatchHeaderValue = Nothing  
    End Sub  
End Class  
```  
  
```csharp  
using System;  
using System.Web.Services.Protocols;   
using myNamespace.MyReferenceName;  
  
class Sample  
{  
    static void Main(string[] args)  
    {  
        ReportingService2005 rs = new ReportingService2005();  
        rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
      // Set the base Web service URL of the source server  
      rs.Url = "http://<Server Name>/reportserver/ReportService2005.asmx"  
  
        BatchHeader bh = new BatchHeader();  
  
        bh1.BatchID = service.CreateBatch();  
        rs.BatchHeaderValue = bh;  
        rs.CreateFolder("New Folder1", "/", null);  
        rs.CreateFolder("New Folder2", "/", null);  
        rs.CreateFolder("New Folder3", "/", null);  
  
        Console.WriteLine("Creating folders...");  
        rs.BatchHeaderValue = bh1;  
        rs.ExecuteBatch();  
        Console.WriteLine("Folders created successfully.");  
  
        rs.BatchHeaderValue = null;  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:ReportService2005.ReportingService2005.CancelBatch%2A>   
 <xref:ReportService2005.ReportingService2005.CreateBatch%2A>   
 [Referência técnica &#40;SSRS&#41;](../technical-reference-ssrs.md)   
 [Usar cabeçalhos SOAP do Reporting Services](using-reporting-services-soap-headers.md)  
  
  
