---
title: Caixa de diálogo Propriedades do Pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.ispackageprop.general.f1
- sql12.ssis.ssms.packageproperties.f1
ms.assetid: a70acbf4-5f5c-4606-8ce4-8eb3684233de
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ab3cdf0079d0c01d95b73339e1fce8960658f93a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62836327"
---
# <a name="package-properties-dialog-box"></a>Caixa de diálogo Propriedades do Pacote
  Use a caixa de diálogo **Propriedades do Pacote** para exibir propriedades de pacotes individuais armazenados no servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Para obter mais informações, consulte [Servidor do Integration Services &#40;SSIS&#41;](integration-services-ssis-server-and-catalog.md).  
  
 **O que você deseja fazer?**  
  
-   [Abrir a caixa de diálogo Propriedades do Pacote](#open_dialog)  
  
-   [Configurar as opções](#options)  
  
##  <a name="open_dialog"></a> Abrir a caixa de diálogo Propriedades do Pacote  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Você está se conectando à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados SSISDB.  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **SSISDB** .  
  
4.  Expanda a pasta que contém o pacote para o qual você deseja exibir propriedades.  
  
5.  Clique com o botão direito do mouse no pacote e selecione **Propriedades**.  
  
##  <a name="options"></a> Configurar as opções  
 Use a página **Geral** para exibir as propriedades do pacote selecionado.  
  
 Todas as propriedades da página **Geral** são somente leitura.  
  
 **Nome**  
 Exibe o nome do pacote.  
  
 **Identificador**  
 Lista a ID do pacote.  
  
 **Entry Point**  
 O valor de `True` indica que o pacote é iniciado diretamente. O valor de `False` indica que o pacote é iniciado por outro pacote usando a tarefa Executar Pacote. O valor padrão é `True`.  
  
 Defina essa propriedade no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para o pacote pai e os pacotes filho clicando com o botão direito do mouse no pacote em Gerenciador de Soluções e clicando em **Pacote de Ponto de Entrada**.  
  
 **Descrição**  
 Exibe a descrição opcional do pacote.  
  
  
