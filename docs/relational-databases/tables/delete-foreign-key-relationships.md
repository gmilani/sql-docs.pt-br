---
title: Excluir relações de chaves estrangeiras | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- foreign keys [SQL Server], deleting
- removing foreign keys
- deleting foreign keys
ms.assetid: 9c9e9ae4-9e03-4137-acb6-b18928a0c4ca
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b35c409389fa657e45ed3fcee57b28c3229dbbd9
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907901"
---
# <a name="delete-foreign-key-relationships"></a>Excluir relações de chaves estrangeiras
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Você pode excluir uma restrição de chave estrangeira no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Excluir uma restrição de chave estrangeira remove o requisito para forçar uma integridade referencial.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para excluir uma restrição de chave estrangeira usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-delete-a-foreign-key-constraint"></a>Para excluir uma restrição de chave estrangeira  
  
1.  No **Pesquisador de Objetos**, expanda a tabela com a restrição e expanda **Chaves**.  
  
2.  Clique com o botão direito do mouse na restrição e clique em **Excluir**.  
  
3.  Na caixa de diálogo **Excluir Objeto** , clique em **OK**.  

##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-delete-a-foreign-key-constraint"></a>Para excluir uma restrição de chave estrangeira  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE dbo.DocExe   
    DROP CONSTRAINT FK_Column_B;   
    GO  
    ```  
  
 Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
  
