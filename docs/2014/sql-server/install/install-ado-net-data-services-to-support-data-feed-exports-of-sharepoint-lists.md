---
title: Instalar o ADO.NET Data Services para dar suporte a exportações de feed de dados de listas do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: f32527ae-f623-4e08-adfb-6d3262f5c2ac
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b9b3ec2d8b7459f9d66313c6a40b1cbc26450e0d
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952161"
---
# <a name="install-adonet-data-services-to-support-data-feed-exports-of-sharepoint-lists"></a>Instalar o ADO.NET Data Services para dar suporte a exportações do feed de dados das listas do SharePoint
  O ADO.NET Data Services é obrigatório para uma exportação do feed de dados das listas do SharePoint. Como o SharePoint 2010 não inclui esse componente no programa SharePoint Prerequisite Installer, você deve instalá-lo manualmente.  
  
 Sem esse pré-requisito, você receberá o seguinte erro ao tentar usar uma lista do SharePoint que foi exportada como um feed de dados: "Por motivos de segurança, o DTD é proibido neste documento XML. Para habilitar o processamento do DTD, defina a propriedade ProhibitDtd em XmlReaderSettings como falsa e passe as configurações para o método XmlReader.Create."  
  
 Use as instruções a seguir para instalar o ADO.NET Data Services em cada SharePoint Server para o qual você deseja permitir a exportação de listas como feeds de dados.  
  
### <a name="download-and-install-adonet-data-services"></a>Baixar e instalar o ADO.NET Data Services  
  
1.  Acesse a documentação de requisitos de hardware e software para o SharePoint 2010, [requisitos de hardware e software (SharePoint 2010)](https://go.microsoft.com/fwlink/?LinkId=169734)  
  
2.  Em **acesso ao software aplicável**, encontre o link para o ADO.NET Data Services 3,5 que corresponde ao sistema operacional que você está usando (windows Server 2008 SP2 ou windows Server 2008 R2).  
  
3.  Clique no link e execute o programa de instalação que instala o serviço.  
  
## <a name="see-also"></a>Consulte também  
 [Instalação do PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
