---
title: Modificar chaves primárias | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- modifying primary keys
- primary keys [SQL Server], modifying
ms.assetid: 8e2a15ba-1cd1-4408-b860-16c3ee37d635
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ef278fbdc9fa2599e7612cd9c3b54b909a9bf1f0
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907316"
---
# <a name="modify-primary-keys"></a>Modificar chaves primárias
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Você pode modificar uma chave primária no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Você pode modificar a chave primária de uma tabela alterando a ordem das colunas, o nome do índice, a opção clusterizada ou o fator de preenchimento.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para modificar uma chave primária usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-a-primary-key"></a>Para modificar uma chave primária  
  
1.  Abra o Designer de Tabela da tabela cuja chave primária você quer modificar, clique com o botão direito do mouse no Designer de Tabela e escolha **Índices/Chaves** no menu de atalho.  
  
2.  Na caixa de diálogo **Índices/Chaves** , selecione o índice de chave primária na lista **Índice ou Chave Exclusiva/Primária Selecionada** .  
  
3.  Complete uma ação da seguinte tabela:  
  
    |Para|Siga estas etapas|  
    |--------|------------------------|  
    |Renomeie a chave primária|Digite um novo nome na caixa **Nome** . Verifique se seu novo nome não duplica um nome na lista **Índice ou Chave Exclusiva/Primária Selecionada** .|  
    |Definir a opção clustered|Para criar um índice clusterizado para a chave primária, selecione **Criar como CLUSTERED**e selecione a opção na caixa de listagem suspensa. Só pode existir um índice clusterizado por tabela. Se essa opção não estiver disponível para seu índice, você deve desmarcar essa configuração no primeiro índice clusterizado existente.<br /><br /> Se essa opção não for selecionada, um índice exclusivo não clusterizado será criado.|  
    |Definir um fator de preenchimento|Expanda a categoria **Especificação de Preenchimento** e digite um inteiro de 0 a 100 na caixa **Fator de Preenchimento** . Para obter mais informações sobre fatores de preenchimento e seus usos, veja [Especificar fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).|  
    |Altere a ordem da coluna|Selecione **Colunas** e clique nas reticências **(...)** à direita da propriedade. Na caixa de diálogo  **Colunas de Índices** , remova as colunas da chave primária. Depois, adicione as colunas de novo na ordem desejada. Para remover uma coluna da chave, simplesmente remova o nome de coluna da lista de nomes **Coluna** .|  
  
4.  No menu **Arquivo** , clique em **Salvar**_table name_.  

##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para modificar uma chave primária**  
  
 Para modificar uma restrição PRIMARY KEY usando o Transact-SQL, exclua primeiramente a PRIMARY KEY já existente e, em seguida, recrie essa restrição com a nova definição. Para obter mais informações, consulte [Delete Primary Keys](../../relational-databases/tables/delete-primary-keys.md) e [Create Primary Keys](../../relational-databases/tables/create-primary-keys.md).  
  
###  <a name="TsqlExample"></a>  
