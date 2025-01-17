---
title: Armazenar dados criptografados do servidor de relatório (Gerenciador de Configurações do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], encryption
- credentials [Reporting Services]
- cryptography [Reporting Services]
- confidential reports [Reporting Services]
- encryption [Reporting Services]
- databases [Reporting Services], encryption
ms.assetid: ac0f4d4d-fc4b-4c62-a693-b86e712e75f2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8156e3d62e8aac027499ad1e267e1f6e14f5ef9a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108686"
---
# <a name="store-encrypted-report-server-data-ssrs-configuration-manager"></a>Armazenar dados criptografados do servidor de relatório (Gerenciador de configurações do SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] armazena valores criptografados no banco de dados do servidor de relatório e em arquivos de configuração. A maioria dos valores criptografados é credencial usada para acessar fontes de dados externas que fornecem dados a relatórios. Este tópico descreve quais valores são criptografados, a funcionalidade de criptografia usada no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], entre outros tipos de dados confidenciais armazenados sobre os quais é útil saber mais a respeito.  
  
## <a name="encrypted-values"></a>Valores criptografados  
 A lista a seguir descreve os valores armazenados em uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   As informações e credenciais de conexão usadas por um servidor de relatório para conexão com um banco de dados de servidor de relatório que armazena dados internos do servidor.  
  
     Esses valores são especificados e criptografados durante a instalação ou configuração do servidor de relatório. É possível atualizar as informações de conexão a qualquer momento usando a ferramenta Configuração do Reporting Services ou o utilitário **rsconfig** . A criptografia das configurações é realizada usando a chave no nível da máquina do computador local disponível para todos os usuários. As informações criptografadas de conexão de servidor de relatório são armazenadas no arquivo rsreportserver.config (nenhum outro arquivo de configuração contém configurações criptografadas). Para obter mais informações, consulte [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
-   Credenciais armazenadas usadas por um servidor de relatório para conexão com fontes de dados externas que fornecem dados a um relatório.  
  
     Esses valores são definidos ao configurar informações de fonte de dados para um relatório e, em seguida, são armazenados como valores criptografados em um banco de dados de servidor de relatório. O servidor de relatório usa uma chave simétrica para criptografar e decifrar esses dados. Para obter mais informações sobre credenciais armazenadas, confira [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../integration-services/connection-manager/data-sources.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Uma conta de usuário autônoma usada pelo servidor de relatório para conexão com outros computadores para recuperar arquivos de imagem externos ou dados externos usados em um relatório.  
  
     Essa conta é usada quando uma conexão com um computador remoto é necessária e não há nenhuma outra credencial disponível para efetuar a conexão. Essa conta é usada principalmente para oferecer suporte ao processamento de relatórios autônomos que não usam credenciais para acessar uma fonte de dados. Se você criar relatórios com base em fontes de dados que não exigem nem usam credenciais para acessar dados, será necessário configurar essa conta para o servidor de relatório a ser usado.  
  
     Essa conta é necessária em determinadas circunstâncias e pode ser criada somente por meio da ferramenta Configuração do Reporting Services ou do **rsconfig**. Esse valor também é armazenado no arquivo rsreportserver.config. É necessário criar essa conta manualmente. Para obter mais informações sobre essa conta e como ela é usada, veja [Configurar a conta de execução autônoma &#40;SSRS Configuration Manager&#41;](configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
-   A chave simétrica usada para criptografia.  
  
     Esse valor é criado durante a instalação ou configuração do servidor e, em seguida, é armazenado como um valor criptografado no banco de dados do servidor de relatório. O serviço Servidor de Relatório do Windows usa essa chave para criptografar e decifrar dados armazenados no banco de dados do servidor de relatório.  
  
## <a name="encryption-functionality-in-reporting-services"></a>Funcionalidade de criptografia no Reporting Services  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa funções criptográficas que fazem parte do sistema operacional Windows. São usadas as criptografias simétrica e assimétrica.  
  
 Dados no banco de dados do servidor de relatório são criptografados por meio de uma chave simétrica. Há uma única chave simétrica para cada banco de dados de servidor de relatório. Essa chave simétrica é criptografada usando a chave pública de um par de chaves assimétricas gerado pelo Windows. A chave privada é mantida pela conta do serviço Servidor de Relatório do Windows.  
  
 Em uma implantação em expansão do servidor de relatório, na qual várias instâncias do servidor de relatório compartilham o mesmo banco de dados de servidor de relatório, uma única chave simétrica é usada por todos os nós do servidor de relatório. É necessário que cada nó tenha uma cópia da chave simétrica compartilhada. Uma cópia da chave simétrica é criada automaticamente para cada nó quando a implantação de extensão é configurada. Cada nó criptografa a sua cópia da chave simétrica usando uma chave pública de um par de chaves específico para a sua conta do serviço do Windows. Para saber mais sobre como a chave simétrica é criada para implantações de expansão e de instância única, veja [Inicializar um servidor de relatório &#40;SSRS Configuration Manager&#41;](ssrs-encryption-keys-initialize-a-report-server.md).  
  
> [!NOTE]  
>  Ao alterar a conta do serviço Servidor de Relatório do Windows, as chaves assimétricas podem se tornar inválidas, o que interromperá operações do servidor. Para evitar esse problema, use sempre a ferramenta Configuração do Reporting Services para modificar configurações da conta do serviço. Ao usar a ferramenta de configuração, as chaves são atualizadas automaticamente. Para obter mais informações, veja [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
## <a name="other-sources-of-confidential-data"></a>Outras fontes de dados confidenciais  
 Um servidor de relatório armazena outros dados que não são criptografados, mas que podem conter informações confidenciais que você quer proteger. Mais especificamente, instantâneos do histórico do relatório e instantâneos de execução do relatório contêm resultados de consultas que podem incluir dados destinados a usuários autorizados. Se você estiver usando a funcionalidade de instantâneo para relatórios que contêm dados confidenciais, saiba que os usuários que podem abrir tabelas em um banco de dados de servidor de relatório talvez possam visualizar partes de um relatório armazenado ao inspecionar o conteúdo da tabela.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não dá suporte ao armazenamento em cache nem histórico de relatórios que usam parâmetros com base na identificação de segurança do usuário.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar e gerenciar chaves de criptografia &#40;SSRS Configuration Manager&#41;](ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
