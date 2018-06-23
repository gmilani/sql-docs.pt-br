---
title: Propriedades do servidor (página Processadores) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.serverproperties.processor.f1
ms.assetid: cc1581a2-492b-41f0-bda5-17909b65c4f7
caps.latest.revision: 24
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0c857a8095f304bb1c97a31c1e0b5cfbc8c265fd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120648"
---
# <a name="server-properties-processors-page"></a>Propriedades do Servidor (página Processadores)
  Use esta página para exibir ou modificar suas opções de processador. As configurações de afinidade do processador só são habilitadas quando há mais de um processador instalado.  
  
## <a name="options"></a>Opções  
 **Afinidade do Processador**  
 Atribui processadores a threads específicos para eliminar recargas do processador e reduzir a migração de thread pelos processadores. Para obter mais informações, veja [Opção affinity mask de configuração de servidor](affinity-mask-server-configuration-option.md).  
  
 **Afinidade de E/S**  
 Associa as E/Ss de disco do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a um subconjunto especificado de CPUs. Para obter mais informações, veja [Opção affinity Input-Output mask de configuração de servidor](affinity-input-output-mask-server-configuration-option.md).  
  
 **Definir automaticamente a máscara de afinidade de todos os processadores**  
 Permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] defina a afinidade do processador.  
  
 **Definir automaticamente a máscara de afinidade de E/S de todos os processadores**  
 Permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] defina a afinidade de E/S.  
  
 **Máximo de threads de trabalho**  
 0 permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] defina dinamicamente o número de threads de trabalho. Essa configuração é melhor para a maioria dos sistemas. Porém, dependendo de sua configuração de sistema, definir essa opção com um valor específico às vezes melhora o desempenho. Para obter mais informações, consulte [Configure the max worker threads Server Configuration Option](configure-the-max-worker-threads-server-configuration-option.md).  
  
 **Aumentar a prioridade do SQL Server**  
 Especifica se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser executado em uma prioridade de agendamento do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows mais alta que outros processos no mesmo computador. Para obter mais informações, consulte [Configure the priority boost Server Configuration Option](configure-the-priority-boost-server-configuration-option.md).  
  
 **Usar fibras do Windows (lightweight pooling)**  
 Use fibras do Windows em vez de threads no serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Observe que isso só está disponível no Windows 2003 Server Edition. Para saber mais, veja [lightweight pooling Server Configuration Option](lightweight-pooling-server-configuration-option.md).  
  
 **Valores Configurados**  
 Exibe os valores configurados para as opções nesse painel. Se você alterar esses valores, clique em **Executando Valores** para verificar se as alterações entraram em vigor. Se não houver nenhum, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser reiniciada.  
  
 **Executando Valores**  
 Exiba os valores que estão sendo executados para as opções neste painel. Esses valores são somente leitura.  
  
## <a name="see-also"></a>Consulte também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  