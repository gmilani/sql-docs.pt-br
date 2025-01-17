---
title: Gerenciar com o Resource Governor
description: Saiba como usar o Resource Governor para gerenciar a alocação de CPU, E/S física e recursos de memória para cargas de trabalho de Python e R nos Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/02/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: bbd55f7796f61bfb2ac85cdfc061f5e754ca70b2
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727721"
---
# <a name="manage-python-and-r-workloads-with-resource-governor-in-sql-server-machine-learning-services"></a>Gerenciar cargas de trabalho do Python e do R com o Resource Governor nos Serviços de Machine Learning do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Saiba como usar o [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) para gerenciar a alocação de CPU, E/S física e recursos de memória para cargas de trabalho de Python e R nos Serviços de Machine Learning do SQL Server.

Normalmente, os algoritmos de aprendizado de máquina em Python e R têm uso intensivo de computação. Dependendo de suas prioridades de carga de trabalho, talvez seja necessário aumentar ou diminuir os recursos disponíveis para os Serviços de Machine Learning.

Para ver informações mais gerais, confira [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).

> [!NOTE] 
> O Resource Governor é um recurso da Edição Enterprise.

## <a name="default-allocations"></a>Alocações padrão

Por padrão, os runtimes de script externo para aprendizado de máquina são limitados a não mais do que 20% da memória total do computador. Isso depende do seu sistema, mas, em geral, você pode achar esse limite inadequado para tarefas de aprendizado de máquina sérias, como treinar um modelo ou prever muitas linhas de dados. 

## <a name="manage-resources-with-resource-governor"></a>Gerenciar recursos com o Resource Governor
 
Por padrão, os processos externos usam até 20% da memória total do host no servidor local. É possível modificar o pool de recursos padrão para fazer alterações em todo o servidor com processos de R e Python e utilizando qualquer capacidade que você disponibilizar para processos externos.

Como alternativa, você pode criar **pools de recursos externos** personalizados, com grupos de carga de trabalho e classificadores associados para determinar a alocação de recurso para solicitações provenientes de programas, hosts ou outros critérios específicos que você definir. Um pool de recursos externos é um tipo de pool de recursos introduzido no [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] para ajudar a gerenciar os processos de R e Python externos ao mecanismo de banco de dados.

1. [Habilite a governança de recursos](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor) (ela está desativada por padrão).

2. Execute [CREATE EXTERNAL RESOURCE POOL](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql) para criar e configurar o pool de recursos, seguido por [ALTER RESOURCE GOVERNOR](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql) para implementá-lo.

3. Crie um grupo de carga de trabalho para alocações granulares, por exemplo, entre treinamento e pontuação.

4. Crie um classificador para interceptar chamadas para processamento externo.

5. Execute consultas e procedimentos usando os objetos que você criou.

Para ver um passo a passo, confira [Como criar um pool de recursos para scripts externos de R e Python](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md).

Para ver uma introdução à terminologia e conceitos gerais, confira [Pool de recursos do Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md).

## <a name="processes-under-resource-governance"></a>Processos sob governança de recursos
  
 Você pode usar um *pool de recursos externos* para gerenciar os recursos usados pelos seguintes executáveis em uma instância do mecanismo de banco de dados:

+ Rterm.exe quando chamado localmente do SQL Server ou chamado remotamente com o SQL Server como o contexto de computação remota
+ Python.exe quando chamado localmente do SQL Server ou chamado remotamente com o SQL Server como o contexto de computação remota
+ BxlServer.exe e processos satélite
+ Processos de satélite iniciados pelo Launchpad, como PythonLauncher.dll
  
> [!NOTE]
> Não há suporte para o gerenciamento direto do serviço Launchpad por meio do Resource Governor. O Launchpad é um serviço confiável que só pode hospedar iniciadores desenvolvidos pela Microsoft. Inicializadores confiáveis também são configurados explicitamente para evitar o consumo excessivo de recursos.
  
## <a name="next-steps"></a>Próximas etapas

+ [Criar um pool de recursos para o aprendizado de máquina](create-external-resource-pool.md)
+ [Pools de recursos do Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
