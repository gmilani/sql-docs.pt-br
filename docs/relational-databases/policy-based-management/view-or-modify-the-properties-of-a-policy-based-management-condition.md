---
title: Exibir ou modificar as propriedades de uma condição de gerenciamento baseado em políticas | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view policy conditions
- Policy-Based Management, modify policy conditions
ms.assetid: 890d7384-8444-4767-bb6f-f5debb155747
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c904edf49ca2f07e2cb715821f9858ea25302311
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909811"
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-condition"></a>Exibir ou modificar as propriedades de uma condição de gerenciamento baseado em políticas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como exibir ou modificar as propriedades de uma condição de gerenciamento baseado em políticas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  

  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  

  
####  <a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-or-modify-a-conditions-properties"></a>Para exibir ou modificar as propriedades de uma condição  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém a condição que você deseja exibir ou modificar.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique no sinal de adição para expandir a pasta **Condições** .  
  
5.  Clique com o botão direito do mouse na condição que você deseja exibir ou editar e selecione **Propriedades**. Para obter mais informações sobre as opções disponíveis na caixa de diálogo **Abrir Condição -** _nome_da_condição_, confira [Caixa de diálogo Criar Condição ou Abrir Condição, página Geral](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-general-page.md), [Caixa de diálogo Abrir Condição, página Políticas Dependentes](../../relational-databases/policy-based-management/open-condition-dialog-box-dependent-policies-page.md), [Caixa de diálogo Criar Condição ou Abrir Condição, página Descrição](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-description-page.md) e [Caixa de diálogo Edição Avançada &#40;Condição&#41;](../../relational-databases/policy-based-management/advanced-edit-condition-dialog-box.md).  
  
6.  Quando terminar, clique em **OK**.  

##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-a-conditions-properties"></a>Para exibir as propriedades de uma condição  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       description,  
       facet,  
       expression,  
       is_name_condition,  
       obj_name  
    FROM syspolicy_conditions;  
    GO  
  
    ```  
  
 Para obter mais informações, veja [syspolicy_conditions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syspolicy-conditions-transact-sql.md).  
  
  
