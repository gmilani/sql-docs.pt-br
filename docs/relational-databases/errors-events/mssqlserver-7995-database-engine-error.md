---
title: MSSQLSERVER_7995 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7995 (Database Engine error)
ms.assetid: af6d6322-3cba-43d8-be97-e6ef15f8c933
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 16f2bebd761898fad44cd19c78c02470420b6d18
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72906557"
---
# <a name="mssqlserver_7995"></a>MSSQLSERVER_7995
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|7995|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC2_SYSTEM_CATALOGS_CORRUPT|  
|Texto da mensagem|Banco de dados 'DBNAME': erros de consistência em catálogos do sistema impedem processamento adicional de DBCC CHECKNAME.|  
  
## <a name="explanation"></a>Explicação  
O processo DBCC CHECKDB consiste nestas três fases:  
  
1.  Verificações de alocação. É equivalente a executar DBCC CHECKALLOC.  
  
2.  Verificações de consistência de tabelas do sistema. É equivalente a executar DBCC CHECKTABLE em uma pequena lista de tabelas base do sistema necessárias.  
  
3.  Verificações de consistência no banco de dados completo.  

MSSQLEngine_7995 é gerado na fase 2 para indicar que DBCC CHECKDB encontrou erros que não podem ser corrigidos pelo comando ou que REPAIR não foi especificado. DBCC CHECKDB não pode prosseguir para a fase 3, pois as tabelas base do sistema em questão armazenam os metadados de todos os objetos do banco de dados ou porque as tabelas base do sistema estão corrompidas.  
  
## <a name="user-action"></a>Ação do usuário  
  
### <a name="look-for-hardware-failure"></a>Procurar falhas de hardware  
Execute o diagnóstico de hardware e corrija quaisquer problemas. Examine também os logs do aplicativo e do sistema [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para verificar se o erro ocorreu devido a uma falha de hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.  
  
Se você tiver problemas contínuos de danos aos dados, tente alternar diferentes componentes de hardware para isolar o problema. Verifique se o sistema não está com a gravação em cache habilitada no controlador de disco. Se você suspeitar que a gravação de caching seja o problema, contate o fornecedor do hardware.  
  
Finalmente, pode ser útil mudar para um sistema de hardware novo. Essa mudança pode incluir a reformatação de unidades de disco e a reinstalação do sistema operacional.  
  
### <a name="restore-from-backup"></a>Restaurar a partir de backup  
Se o problema não estiver relacionado ao hardware e se houver um backup limpo conhecido, restaure o banco de dados do backup.  
  
### <a name="run-dbcc-checkdb"></a>Executar DBCC CHECKDB  
Se não houver um backup limpo, execute DBCC CHECKDB sem uma cláusula REPAIR para determinar a extensão do dano. DBCC CHECKDB recomendará uma cláusula REPAIR para ser usada. Execute DBCC CHECKDB com a cláusula REPAIR apropriada para reparar o dano.  
  
> [!CAUTION]  
> Se você não tiver certeza do efeito de DBCC CHECKDB com uma cláusula REPAIR sobre seus dados, contate o provedor de suporte antes de executar essa instrução.  
  
Se a execução de DBCC CHECKDB com uma das cláusulas REPAIR não corrigir o problema, contate seu provedor de suporte.  
  
### <a name="results-of-running-repair-options"></a>Resultados da execução de opções REPAIR  
Examine a lista de erros para saber o que a cláusula REPAIR fará em relação a cada erro.  
  
