---
title: Página Configuração do Banco de Dados
ms.custom: seo-lt-2019
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.dbpg.f1
ms.assetid: dd72220e-a599-465d-8b84-9bb6a7433216
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 82b3762342c30b657f031bd53f89ae7652f5ece8
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729439"
---
# <a name="database-configuration-page-master-data-services-configuration-manager"></a>Página Configuração do Banco de Dados (Gerenciador de Configuração do Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Use a página **Configuração do Banco de Dados** para editar as configurações do sistema de um banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . As configurações do sistema afetam todos os aplicativos Web e serviços Web associados ao banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] selecionado. É necessário selecionar ou criar um banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] antes que os parâmetros do sistema sejam habilitados e estejam disponíveis para configuração.  
  
## <a name="current-database"></a>Banco de dados atual  
 Selecione um banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] existente ou crie um novo banco de dados para o qual as configurações do sistema serão editadas. O novo banco de dados será selecionado após sua criação.  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|**Instância do SQL Server**|Exibe o nome da instância selecionada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Esse será um espaço em branco até você se conectar a uma instância e selecionar ou criar um banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**Banco de dados do Master Data Services**|Exibe o nome do banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] selecionado. Esse será um espaço em branco até você se conectar a uma instância e selecionar ou criar um banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**Versão de banco de dados do Master Data Services**|A versão do esquema de banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**Criar banco de dados**|Abre o assistente para **Criar Banco de Dados** , no qual você se conecta a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e cria um banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para essa instância.|  
|**Selecionar banco de dados**|Abre a caixa de diálogo **Conectar ao Banco de Dados** , na qual você se conecta a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e seleciona um banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**Atualizar Banco de Dados**|Abre um assistente no qual você pode atualizar um banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] especificado. Esse botão é habilitado somente quando o banco de dados especificado requer atualização.|  
|**Reparar Banco de Dados**|Clique neste botão para garantir que o banco de dados MDS seja instalado corretamente. Isso poderá ser útil se você fizer backup e restaurar um banco de dados MDS para uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que nunca hospedou um banco de dados MDS.|  
  
## <a name="system-settings"></a>Configurações do sistema  
 Edite as configurações do sistema de todos os aplicativos Web e serviços Web associados ao banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] selecionado.  
  
 Essas configurações estão disponíveis no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] e são armazenadas no banco de dados na tabela Configurações do Sistema (mdm.tblSystemSetting). Para obter uma lista de todas as configurações, consulte [Configurações do sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
## <a name="see-also"></a>Consulte também  
[Instalação e configuração do Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md)[Requisitos do banco de dados &#40;Master Data Services&#41;](../master-data-services/install-windows/database-requirements-master-data-services.md)  
  
  
