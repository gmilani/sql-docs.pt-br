---
title: Gerenciador de Conexões da Assinatura do Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpsubscrconn.f1
- sql14.dts.designer.afpsubscrconn.f1
ms.assetid: e1225327-c308-4c50-8f44-c411f52ef378
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 644136f4f7c0c5ea29e9c198dc3aad2bc1c2d733
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298634"
---
# <a name="azure-subscription-connection-manager"></a>Gerenciador de Conexões da Assinatura do Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O **Gerenciador de conexões de Assinatura do Azure** permite que um pacote SSIS se conecte a uma assinatura do Azure usando os valores especificados para as propriedades: ID da assinatura do Azure e Certificado de gerenciamento.  
  
 O **Gerenciador de conexões da Assinatura do Azure** é um componente do Feature Pack do [SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
1.  Na caixa de diálogo **Adicionar Gerenciador de Conexões SSIS** mostrada acima, escolha **Assinatura do Azure**e clique em **Adicionar**.  Você deve ver a caixa de diálogo **Editor do Gerenciador de Conexões da Assinatura do Azure** a seguir.  
  
    ![SSIS-AzureSubscriptionConnectionManager](../../integration-services/connection-manager/media/ssis-azuresubscriptionconnectionmanager.png)
  
2.  Insira sua ID de assinatura do Azure, que identifica exclusivamente uma assinatura do Azure, em **ID da assinatura do Azure**.  O valor pode ser encontrado no [Portal de Gerenciamento do Azure](https://manage.windowsazure.com) na página **Configurações** :  
  
    ![SSIS-AzureSettings-SubscriptionID](../../integration-services/connection-manager/media/ssis-azuresettings-subscriptionid.png "SSIS-AzureSettings-SubscriptionID")  
  
3.  Escolha **Local do repositório de certificados de gerenciamento** e **Nome do repositório de certificados de gerenciamento** nas listas suspensas.  
  
4.  Insira **Impressão digital do certificado de gerenciamento** ou clique em **Procurar...** para escolher um certificado no repositório selecionado. O certificado deve ser carregado como um certificado de gerenciamento para a assinatura. Para fazer isso, clique em **Carregar** na página a seguir do Portal do Azure (confira esta [postagem do MSDN](https://msdn.microsoft.com/library/azure/gg551722.aspx) para obter mais detalhes).  
  
     ![SSIS-AzureSettings-ManagementCertificate](../../integration-services/connection-manager/media/ssis-azuresettings-managementcertificate.png "SSIS-AzureSettings-ManagementCertificate")  
  
5.  Clique em **Testar Conexão** para testar a conexão.  
  
6.  Clique em **OK** para fechar a caixa de diálogo.  
  
  
