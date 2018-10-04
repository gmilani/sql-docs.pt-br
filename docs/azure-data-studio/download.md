---
title: Baixe e instale o estúdio de dados do Azure | Microsoft Docs
description: Download e instalar o Azure Data Studio para Windows, macOS ou Linux
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 88b79feb3b04dcc7f872653b2e24a9f70c370f57
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "48037685"
---
# <a name="download-and-install-azure-data-studio"></a>Baixe e instale o estúdio de dados do Azure

[!INCLUDE[name-sos](../includes/name-sos.md)] é executado no Windows, macOS e Linux.

Baixe e instale a versão mais recente, o *setembro de versão de GA*:

> [!NOTE]
> Se você estiver atualizando do SQL Operations Studio e deseja manter as configurações, os atalhos de teclado ou os trechos de código, consulte [mover as configurações do usuário](#move-user-settings).

|Plataforma|Download|Data de liberação| Versão |
|:---|:---|:---|:---|
|Windows|[Instalador](https://go.microsoft.com/fwlink/?linkid=2024683)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2024680)|24 de setembro de 2018 |1.0|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2024677)|24 de setembro de 2018 |1.0|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2024668)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2024672)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2024675)|24 de setembro de 2018 |1.0|

Para obter detalhes sobre a versão mais recente, consulte o [notas de versão](release-notes.md).

## <a name="get-azure-data-studio-for-windows"></a>Obter dados do Azure Studio para Windows

Esta versão do [!INCLUDE[name-sos](../includes/name-sos-short.md)] inclui uma experiência padrão do Windows installer e. zip: 

**Instalador**

1. Baixe e execute o [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] installer para Windows](https://go.microsoft.com/fwlink/?linkid=2024683).
1. Iniciar o [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] aplicativo.


**arquivo. zip**

1. Baixe [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] . zip para Windows](https://go.microsoft.com/fwlink/?linkid=2024680).
2. Navegue até o arquivo baixado e extraí-lo.
3. Execute `\azuredatastudio-windows\azuredatastudio.exe`


## <a name="get-azure-data-studio-for-macos"></a>Obtenha o Studio de dados do Azure para macOS

1. Baixe [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] para macOS](https://go.microsoft.com/fwlink/?linkid=2024677).
2. Para expandir o conteúdo do zip, clique duas vezes nele.
3. Para tornar [!INCLUDE[name-sos](../includes/name-sos-short.md)] disponíveis na *Launchpad*, arraste */aplicativos de dados do Azure* para o *aplicativos* pasta.


## <a name="get-azure-data-studio-for-linux"></a>Obtenha o Studio de dados do Azure para Linux

1. Baixar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Linux usando um dos instaladores ou gz arquivo morto:
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2024668)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2024672)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2024675)
1. Para extrair o arquivo e inicialização [!INCLUDE[name-sos](../includes/name-sos-short.md)], abra uma nova janela do Terminal e digite os seguintes comandos:

   **Instalação do Debian:**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/azuredatastudio-linux-<version string>.deb

   azuredatastudio
   ```

   **Instalação do RPM:**
   ```bash
   cd ~
   yum install ./Downloads/azuredatastudio-linux-<version string>.rpm

   azuredatastudio
   ```

   **gz instalação:**
   ```bash 
   cd ~ 
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   azuredatastudio 
   ``` 

   > [!NOTE]
   > No Ubuntu, Redhat e Debian, você pode ter dependências ausentes. Use os comandos a seguir para instalar essas dependências, dependendo de sua versão do Linux:
   

   **Debian:** 
   ```bash
   sudo apt-get install libunwind8
   ```

   **Red Hat:** 
   ```bash
   yum install libXScrnSaver
   ```

   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```


## <a name="uninstall-azure-data-studio"></a>Desinstalar o Studio de dados do Azure

Se você instalou o [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] usando o instalador do Windows, desinstale da mesma maneira que você remova qualquer aplicativo do Windows.

Se você instalou o [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] com um. zip ou outro arquivo, em seguida, simplesmente excluir os arquivos.

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

[!INCLUDE[name-sos](../includes/name-sos-short.md)] é executado no Windows, macOS e Linux e é suportado nas seguintes plataformas:

### <a name="windows"></a>Windows
- Windows 10 (64 bits)
- Windows 8.1 (64 bits)
- Windows 8 (64 bits)
- Requer o Windows 7 (SP1) (64 bits) - [KB2533623](https://www.microsoft.com/en-us/download/details.aspx?id=26767)
- Windows Server 2016
- Windows Server 2012 R2 (64 bits)
- Windows Server 2012 (64 bits)
- Windows Server 2008 R2 (64 bits)

### <a name="macos"></a>macOS
- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux"></a>Linux
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="check-for-updates"></a>Verificar atualizações
Para verificar se há atualizações mais recentes, clique no ícone de engrenagem na parte inferior esquerda da janela e clique **verificar se há atualizações**

## <a name="move-user-settings"></a>Mover as configurações do usuário

Se você quiser mover suas configurações personalizadas, os atalhos de teclado ou trechos de código, siga as etapas abaixo. Isso é importante fazer se você estiver atualizando da versão do SQL Operations Studio ao estúdio de dados do Azure.

*Se você já tiver o Azure Data Studio, ou nunca tiver sido instalado ou personalizado do SQL Operations Studio, você pode ignorar esta seção.*


1. Abra configurações clicando a engrenagem no canto inferior esquerdo e clicando em **configurações.**

   ![Abrir configurações](./media/download/open-settings.png)

2. Clique com botão direito do **as configurações de usuário** guia na parte superior e clique em **Revelar no Explorer**

   ![Revelar no explorer](./media/download/reveal-in-explorer.png)

3. Copie todos os arquivos nessa pasta e salvar em uma forma fácil de encontrar o local em sua unidade local, como sua pasta documentos.

   ![configurações de cópia](./media/download/copy-settings.png)

4. Na nova versão do Studio de dados do Azure, siga as etapas 1 e 2, em seguida, para a etapa 3 cole o conteúdo salvo na pasta. Manualmente, você pode copiar sobre as configurações, associações de teclas ou trechos de código em seus respectivos locais.


## <a name="next-steps"></a>Próximas etapas

Consulte um dos seguintes inícios rápidos para começar:
- [Conectar-se e consultar o SQL Server](quickstart-sql-server.md)
- [Conectar-se e consultar o banco de dados SQL do Azure](quickstart-sql-database.md)
- [Conectar-se e consultar o Data Warehouse do Azure](quickstart-sql-dw.md)

Contribuir com [!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio) 

[Declaração de privacidade da Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839) e [coleta de dados de uso](usage-data-collection.md).