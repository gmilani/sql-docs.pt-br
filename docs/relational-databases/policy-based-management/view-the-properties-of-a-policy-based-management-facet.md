---
title: Exibir as propriedades de uma faceta de gerenciamento baseado em políticas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view facet properties
ms.assetid: 022a244c-c2e7-4467-b9a2-c7a27859be22
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 50cdd9031d309a1bbfd6f4229749b5cc5de56125
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72906881"
---
# <a name="view-the-properties-of-a-policy-based-management-facet"></a>Exibir as propriedades de uma faceta de gerenciamento baseado em políticas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como exibir as propriedades de uma faceta do Gerenciamento Baseado em Políticas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir as propriedades de uma faceta, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-a-facet"></a>Para visualizar as propriedades de uma faceta  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém a faceta cujas propriedades você deseja exibir.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique no sinal de adição para expandir a pasta **Facetas** .  
  
5.  Clique com o botão direito do mouse na faceta cujas propriedades você deseja exibir e selecione **Propriedades**. Para obter mais informações sobre as opções disponíveis na caixa de diálogo **Propriedades da faceta -** _nome_da_faceta_, confira [Caixa de diálogo Propriedades de Faceta, página Geral](../../relational-databases/policy-based-management/facet-properties-dialog-box-general-page.md), [Caixa de diálogo Propriedades da Faceta, página Políticas Dependentes](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-policies-page.md) e [Caixa de diálogo Propriedades da Faceta, página Condições Dependentes](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-conditions-page.md).  
  
6.  Quando terminar, clique em **Fechar**.  

