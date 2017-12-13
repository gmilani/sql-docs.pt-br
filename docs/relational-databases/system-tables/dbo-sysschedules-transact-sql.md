---
title: dbo. sysschedules (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysschedules_TSQL
- sysschedules
- sysschedules_TSQL
- dbo.sysschedules
dev_langs: TSQL
helpviewer_keywords: sysschedules system table
ms.assetid: 4cac9237-7a69-4035-bb3e-928b76aad698
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6d97d48155a5f9ff41ee8255e9a28a8c1c82443d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysschedules-transact-sql"></a>dbo.sysschedules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações sobre agendas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Essa tabela é armazenada no **msdb** banco de dados.  
  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|ID da agenda de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|**schedule_uid**|**uniqueidentifier**|Identificador exclusivo da agenda do trabalho. Este valor é usado para identificar uma agenda para trabalhos distribuídos.|  
|**originating_server_id**|**int**|ID do servidor mestre do qual a agenda de trabalho foi originada.|  
|**name**|**sysname (nvarchar(128))**|Nome definido pelo usuário para a agenda de trabalho. Este nome deve ser exclusivo em um trabalho.|  
|**owner_sid**|**varbinary(85)**|Microsoft Windows *security_identifier* do usuário ou grupo que possui a agenda de trabalho.|  
|**habilitado**|**int**|O status da agenda de trabalho:<br /><br /> **0** = não habilitado.<br /><br /> **1** = habilitado.<br /><br /> Se o agendamento não estiver habilitado, nenhum trabalho será executado nele.|  
|**freq_type**|**int**|A frequência com que um trabalho é executado para esta agenda.<br /><br /> **1** = apenas uma vez<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensalmente<br /><br /> **32** = mensalmente, relativo a **freq_interval**<br /><br /> **64** = executado quando o serviço SQL Server Agent é iniciado<br /><br /> **128** = executado quando o computador estiver ocioso|  
|**freq_interval**|**int**|Dias em que o trabalho é executado. Depende do valor de **freq_type**. O valor padrão é **0**, que indica que **freq_interval** é usado. Consulte a tabela abaixo para os valores possíveis e seus efeitos.|  
|**freq_subday_type**|**int**|Unidades para o **freq_subday_interval**. Estes são os valores possíveis e suas descrições.<br /><br /> <br /><br /> **1** : no momento especificado<br /><br /> **2** : segundos<br /><br /> **4** : minutos<br /><br /> **8** : horas|  
|**freq_subday_interval**|**int**|Número de **freq_subday_type** períodos devem ocorrer entre cada execução do trabalho.|  
|**freq_relative_interval**|**int**|Quando **freq_interval** ocorre em cada mês, se **freq_interval** é **32** (mensal relativo). Pode ser um dos seguintes valores:<br /><br /> **0** = **freq_relative_interval** é usado<br /><br /> **1** = primeiro<br /><br /> **2** = segundo<br /><br /> **4** = terceiro<br /><br /> **8** = quarto<br /><br /> **16** = último|  
|**freq_recurrence_**<br /><br /> **fator**|**int**|Número de semanas ou meses entre execuções agendadas de um trabalho. **freq_recurrence_factor** é usado somente se **freq_type** é **8**, **16**, ou **32**. Se esta coluna contém **0**, **freq_recurrence_factor** é usado.|  
|**active_start_date**|**int**|Data na qual a execução de um trabalho pode começar. A data é formatada como DDMMAAAA. NULL indica a data de hoje.|  
|**active_end_date**|**int**|Data na qual a execução de um trabalho pode parar. A data é formatada como AAAAMMDD.|  
|**active_start_time**|**int**|Hora em qualquer dia entre **active_start_date** e **active_end_date** esse trabalho começa a executar. A hora é formatada como HHMMSS, usando um relógio de 24 horas.|  
|**active_end_time**|**int**|Hora em qualquer dia entre **active_start_date** e **active_end_date** que o trabalho interrompe a execução. A hora é formatada como HHMMSS, usando um relógio de 24 horas.|  
|**Date_Created**|**datetime**|Data e hora em que a agenda foi criada.|  
|**date_modified**|**datetime**|Data e hora em que a agenda foi modificada pela última vez.|  
|**número_da_versão**|**int**|Número da versão atual da agenda. Por exemplo, se uma agenda foi modificada 10 vezes, o **número_da_versão** é 10.|  
  
|Valor de freq_type|Efeito em freq_interval|  
|-------------------------|------------------------------|  
|**1** (uma vez)|**freq_interval** é usado (**0**)|  
|**4** (diariamente)|Cada **freq_interval** dias|  
|**8** (semanal)|**freq_interval** é um ou mais dos seguintes:<br /><br /> **1** = domingo<br /><br /> **2** = segunda-feira<br /><br /> **4** = terça-feira<br /><br /> **8** = quarta-feira<br /><br /> **16** = quinta-feira<br /><br /> **32** = sexta-feira<br /><br /> **64** = sábado|  
|**16** (mensalmente)|Sobre o **freq_interval** dia do mês|  
|**32** (mensalmente, relativo)|**freq_interval** é um dos seguintes:<br /><br /> **1** = domingo<br /><br /> **2** = segunda-feira<br /><br /> **3** = terça-feira<br /><br /> **4** = quarta-feira<br /><br /> **5** = quinta-feira<br /><br /> **6** = sexta-feira<br /><br /> **7** = sábado<br /><br /> **8** = dia<br /><br /> **9** = dia da semana<br /><br /> **10** = dia de fim de semana|  
|**64** (inicia quando o serviço do SQL Server Agent é iniciado)|**freq_interval** é usado (**0**)|  
|**128** (executado quando o computador estiver ocioso)|**freq_interval** é usado (**0**)|  
  
## <a name="see-also"></a>Consulte também  
 [dbo. sysjobschedules &#40; Transact-SQL &#41;](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
  
  