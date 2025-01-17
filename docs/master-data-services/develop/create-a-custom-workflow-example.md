---
title: Exemplo de fluxo de trabalho personalizado
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: dfd1616c-a75c-4f32-bdb1-7569e367bf41
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c15f708a6deb8da2b0ea32efc70635ef50124621
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729291"
---
# <a name="create-a-custom-workflow---example"></a>Criar um fluxo de trabalho personalizado – Exemplo

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], quando cria uma biblioteca de classes de fluxo de trabalho personalizado, você cria uma classe que implementa a interface Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender interface. Essa interface inclui um método, <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>que é chamado pelo Serviço de Integração de Fluxo de Trabalho MDS do SQL Server quando um fluxo de trabalho é iniciado. O método <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> contém dois parâmetros: *workflowType* contém o texto que você inseriu na caixa de texto **Tipo de Fluxo de trabalho** no [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e *dataElement* contém metadados e dados de item sobre o item que disparou a regra de negócios do fluxo de trabalho.  
  
## <a name="custom-workflow-example"></a>Exemplo de fluxo de trabalho personalizado  
 O exemplo de código a seguir mostra como implementar o método <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> para extrair os atributos Name, Code e LastChgUserName dos dados XML para o elemento que disparou a regra de negócio do fluxo de trabalho e como chamar um procedimento armazenado para inseri-los em outro banco de dados. Para obter um exemplo do XML dos dados de item e uma explicação das marcas que ele contém, consulte [Descrição de XML de fluxo de trabalho personalizado &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-xml-description.md).  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.IO;  
using System.Data.SqlClient;  
using System.Xml;  
  
using Microsoft.MasterDataServices.Core.Workflow;  
  
namespace MDSWorkflowTestLib  
{  
    public class WorkflowTester : IWorkflowTypeExtender  
    {  
        #region IWorkflowTypeExtender Members  
  
        public void StartWorkflow(string workflowType, System.Xml.XmlElement dataElement)  
        {  
            // Extract the attributes we want out of the element data.  
            XmlNode NameNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Name");  
            XmlNode CodeNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Code");  
            XmlNode EnteringUserNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/LastChgUserName");  
  
            // Open a connection on the workflow database.  
            SqlConnection workflowConn = new SqlConnection(@"Data Source=<Server instance>; Initial Catalog=WorkflowTest; Integrated Security=True");  
  
            // Create a command to call the stored procedure that adds a new user to the workflow database.  
            SqlCommand addCustomerCommand = new SqlCommand("AddNewCustomer", workflowConn);  
            addCustomerCommand.CommandType = System.Data.CommandType.StoredProcedure;  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Name", NameNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Code", CodeNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@EnteringUser", EnteringUserNode.InnerText));  
  
            // Execute the command.  
            workflowConn.Open();  
            addCustomerCommand.ExecuteNonQuery();  
            workflowConn.Close();  
        }  
  
        #endregion  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criar um fluxo de trabalho personalizado &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)  
  
  
