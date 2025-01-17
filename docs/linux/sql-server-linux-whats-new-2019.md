---
title: Novidades do SQL Server 2019 no Linux
description: Este artigo destaca as novidades do SQL Server 2019 no Linux.
author: VanMSFT
ms.author: vanto
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 5183efa51afd89ad82d0cdcb6448996429b81d28
ms.sourcegitcommit: bb56808dd81890df4f45636b600aaf3269c374f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2019
ms.locfileid: "72890555"
---
# <a name="whats-new-for-sql-server-2019-on-linux"></a>Novidades do SQL Server 2019 no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve os principais recursos e serviços disponíveis para o SQL Server 2019 em execução no Linux. Para saber mais sobre os downloads de pacotes e problemas conhecidos, confira as [Notas sobre a versão](sql-server-linux-release-notes-2019.md?view=sql-server-linux-ver15).

## <a name="updates"></a>Updates

As atualizações foram feitas no SQL Server 2019 no Linux:

| Novo recurso ou atualização | Detalhes |
|:-----|:-----|
|Suporte para replicação |[Objetos de replicação do SQL Server em Linux](sql-server-linux-replication.md)
|Suporte para MSDTC (Coordenador de Transações Distribuídas da Microsoft) |[Como configurar o MSDTC no Linux](sql-server-linux-configure-msdtc.md) |
|Suporte para OpenLDAP para provedores de AD de terceiros |[Tutorial: Usar autenticação do Azure Active Directory com o SQL Server em Linux](sql-server-linux-active-directory-authentication.md) |
|Machine Learning no Linux |[Configurar o Machine Learning no Linux](sql-server-linux-setup-machine-learning.md) |
|Aprimoramentos `tempdb` | Por padrão, uma nova instalação do SQL Server em Linux cria vários arquivos de dados `tempdb` com base no número de núcleos lógicos (com até 8 arquivos de dados). Isso não é aplicável a upgrades de versões principais ou secundárias no local. Cada arquivo do `tempdb` tem 8 MB com um aumento automático de 64 MB. Esse comportamento é semelhante à instalação padrão do SQL Server no Windows. |
| PolyBase em Linux | [Instalar o PolyBase](../relational-databases/polybase/polybase-linux-setup.md) no Linux para conectores não Hadoop.<br/><br/>[Mapeamento de tipo do PolyBase](../relational-databases/polybase/polybase-type-mapping.md). |
| Suporte ao CDC (captura de dados de alterações) | O CDC (captura de dados de alterações) agora é compatível no Linux para SQL Server 2019. |
| Registro de Contêiner da Microsoft | O [Registro de Contêiner da Microsoft](https://www.ntweekly.com/2019/09/23/microsoft-container-registry-to-replace-docker-hub-for-new-images/) agora substitui o Docker Hub para novas imagens oficiais de contêiner da Microsoft, incluindo [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. |
| Contêineres não raiz | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduz a capacidade de criar contêineres mais seguros, iniciando o processo [!INCLUDE[sql-server](../includes/ssnoversion-md.md)] como um usuário não raiz por padrão. Confira [criar e executar contêineres do SQL Server como um usuário não raiz](sql-server-linux-configure-docker.md#buildnonrootcontainer) para obter mais detalhes. |

## <a name="next-steps"></a>Próximas etapas

Para instalar o SQL Server em Linux, use um dos seguintes tutoriais:

- [Instalação no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md?view=sql-server-linux-ver15)
- [Instalação no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md?view=sql-server-linux-ver15)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md?view=sql-server-linux-ver15)
- [Executar no Docker](quickstart-install-connect-docker.md?view=sql-server-linux-ver15)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

Para obter respostas a perguntas frequentes, confira as [Perguntas frequentes sobre o SQL Server em Linux](sql-server-linux-faq.md). Para ver outras melhorias introduzidas no SQL Server 2019, confira [Novidades do SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15).

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
