---
title: Classe de evento OLEDB QueryInterface | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- OLEDB QueryInterface event class
ms.assetid: f54c9ef9-3add-497c-a09b-42c4ce3c623d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 39059275021f1196b729af4f30f23a09fd95c197
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050424"
---
# <a name="oledb-queryinterface-event-class"></a>classe de evento OLEDB QueryInterface
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A classe de evento **OLEDB QueryInterface** ocorre quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] emite uma chamada OLE DB **QueryInterface** para consultas distribuídas e procedimentos armazenados remotamente. Inclua essa classe de evento em rastreamentos que estão monitorando problemas associados a consultas distribuídas e procedimentos armazenados remotamente.  
  
 Quando a classe de evento **OLEDB QueryInterface** for incluída, a quantidade de sobrecarga será alta. Se esses eventos ocorrerem com frequência, o rastreamento poderá impedir significativamente o desempenho. Para minimizar a sobrecarga gerada, limite o uso dessa classe de evento a rastreamentos que monitorem problemas específicos em períodos breves de tempo.  
  
## <a name="oledb-queryinterface-event-class-data-columns"></a>Colunas de dados da classe de evento OLEDB QueryInterface  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|ClientProcessID|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|DatabaseID|**int**|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|**nvarchar**|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|Duração|**bigint**|Período de tempo para concluir o evento OLE DB QueryInterface.|13|Não|  
|EndTime|**datetime**|Hora em que o evento terminou.|15|Sim|  
|Erro|**int**|Número de erro de um determinado evento. Geralmente é o número do erro armazenado na exibição de catálogo **sys.messages** .|31|Sim|  
|EventClass|**int**|Tipo de evento = 120.|27|Não|  
|EventSequence|**int**|Sequência da classe de evento OLE DB no lote.|51|Não|  
|EventSubClass|**int**|0 = Iniciando<br /><br /> 1=Concluído|21|Não|  
|GroupID|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IsSystem|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LinkedServerName|**nvarchar**|Nome do servidor vinculado.|45|Sim|  
|LoginName|**nvarchar**|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO/nomedousuário).|11|Sim|  
|LoginSid|**imagem**|SID (identificador de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|MethodName|**nvarchar**|Nome do método de chamada.|47|Não|  
|NTDomainName|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|ProviderName|**nvarchar**|Nome do provedor OLE DB.|46|Sim|  
|RequestID|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|SessionLoginName|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**nvarchar**|Parâmetros enviados e recebidos na chamada OLE DB.|1|Não|  
|TransactionID|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Objetos de automação OLE em Transact-SQL](../../relational-databases/stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
