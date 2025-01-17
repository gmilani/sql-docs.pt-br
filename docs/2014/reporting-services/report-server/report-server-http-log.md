---
title: Log HTTP do Servidor de Relatório | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- HTTP [Reporting Services]
ms.assetid: 6cc433b7-165c-4b16-9034-79256dd6735f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ca3437315803ff8435640bf58219fe93f96e242a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103394"
---
# <a name="report-server-http-log"></a>Log HTTP do Servidor de Relatório
  O log HTTP do servidor de relatório [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] mantém um registro de cada solicitação HTTP e resposta manipuladas pelo servidor de relatório. Como os erros de estouro e tempo limite de solicitação não atingem o servidor de relatório, eles não são registrados no arquivo de log.  
  
 O log HTTP não está habilitado por padrão. Para habilitar o log HTTP, modifique o arquivo de configuração **ReportingServicesService.exe.config** para usar esse recurso em sua instalação.  
  
## <a name="viewing-log-information"></a>Exibindo as informações do log  
 O log é um arquivo de texto ASCII. Você pode usar qualquer editor de texto para exibir o arquivo. O log HTTP do servidor de relatório é equivalente ao arquivo de log estendido W3C em IIS e usa campos similares para que você possa usar os visualizadores do arquivo de log IIS existente para ler o arquivo de log HTTP do servidor de relatório. A tabela a seguir fornece informações adicionais sobre o arquivo de log HTTP:  
  
|||  
|-|-|  
|**Nome do arquivo**|Por padrão, os nomes do arquivo de log são<br /><br /> `ReportServerService_HTTP_<timestamp>.log.`<br /><br /> Você pode personalizar o prefixo do nome do arquivo modificando o atributo HttpTraceFileName no arquivo ReportingServicesService.exe.config. O carimbo de data e hora é baseado em UTC (Tempo Universal Coordenado).|  
|**Local do arquivo**|Os arquivos são copiados no seguinte local:<br /><br /> `\Microsoft SQL Server\<SQL Server Instance>\Reporting Services\LogFiles`|  
|**Formato do arquivo**|O arquivo está em formato pt-BR. É um arquivo de texto ASCII.|  
|**Criação de arquivo e retenção**|O log HTTP é criado quando você o habilita no arquivo de configuração, reinicia o serviço e o servidor de relatório manipula uma solicitação HTTP. Se você definir as configurações, mas o arquivo de log não aparecer, abra um relatório ou inicie um aplicativo do servidor de relatório (como o Gerenciador de Relatórios) para gerar uma solicitação HTTP e criar o arquivo.<br /><br /> Uma nova instância do arquivo de log será criada após cada reinicialização do serviço e o envio subsequente da solicitação HTTP para o servidor de relatório.<br /><br /> Por padrão, os logs de rastreamento são limitados a 32 megabytes e excluídos depois de 14 dias.|  
  
## <a name="configuration-settings-for-report-server-http-log"></a>Configurações do log HTTP do servidor de relatório  
 Para configurar o log HTTP do servidor de relatório, use o bloco de notas para modificar o arquivo **ReportingServicesService.exe.config** . O arquivo de configuração está localizado na pasta \Arquivos de Programas\Microsoft SQL Server\MSSQL.n\Reporting Services\ReportServer\Bin.  
  
 Para habilitar o servidor HTTP, adicione `http:4` à seção RStrace do arquivo ReportingServicesService.exe.config. Todas as outras entradas do arquivo de log HTTP são opcionais. O exemplo a seguir inclui todas as configurações de modo que você pode colar a seção inteira na seção RStrace e, em seguida, excluir as configurações que não são necessárias.  
  
```  
   <RStrace>  
         <add name="FileName" value="ReportServerService_" />  
         <add name="FileSizeLimitMb" value="32" />  
         <add name="KeepFilesForDays" value="14" />  
         <add name="Prefix" value="tid, time" />  
         <add name="TraceListeners" value="debugwindow, file" />  
         <add name="TraceFileMode" value="unique" />  
         <add name="HttpTraceFileName" value="ReportServerService_HTTP_" />  
         <add name="HttpTraceSwitches" value="date,time, clientip,username,serverip,serverport,host,method,uristem,uriquery,protocolstatus,bytesreceived,timetaken,protocolversion,useragent,cookiereceived,cookiesent,referrer" />  
         <add name="Components" value="all:3,http:4" />  
   </RStrace>  
```  
  
## <a name="log-file-fields"></a>Campos do arquivo de log  
 A tabela a seguir descreve os campos disponíveis no log. A lista de campos pode ser configurada; é possível especificar quais campos devem ser incluídos com a configuração `HTTPTraceSwitches`. O **padrão** coluna Especifica se o campo será incluído no arquivo de log automaticamente se você não especificar `HTTPTraceSwitches`.  
  
|Campo|Descrição|Padrão|  
|-----------|-----------------|-------------|  
|HttpTraceFileName|Esse valor é opcional. O valor padrão é ReportServerServiceHTTP_. Você pode especificar um valor diferente se desejar usar uma convenção de nomeação de arquivo diferente (por exemplo, para incluir o nome do servidor se estiver salvando arquivos de log em um local central).|Sim|  
|HTTPTraceSwitches|Esse valor é opcional. Se esse valor for especificado, você poderá configurar os campos usados no arquivo de log em um formato delimitado por vírgula.|Não|  
|Date|A data em que a atividade ocorreu.|Não|  
|Time|A hora em que a atividade ocorreu.|Não|  
|ClientIp|O endereço IP do cliente que acessa o servidor de relatório.|Sim|  
|UserName|O nome do usuário que acessou o servidor de relatório.|Não|  
|ServerPort|O número da porta usada para a conexão.|Não|  
|Host|O conteúdo do cabeçalho do host.|Não|  
|Método|A ação ou método SOAP chamado do cliente.|Sim|  
|UriStem|O recurso acessado.|Sim|  
|UriQuery|A consulta usada para acessar o recurso.|Não|  
|ProtocolStatus|O código de status HTTP.|Sim|  
|BytesReceived|O número de bytes recebidos pelo servidor.|Não|  
|TimeTaken|O tempo (em milissegundos) desde o instante em que HTTP.SYS retorna os dados da solicitação até o servidor concluir o último envio, sem contar o tempo de transmissão de rede.|Não|  
|ProtocolVersion|A versão de protocolo usada pelo cliente.|Não|  
|UserAgent|O tipo de navegador usado pelo cliente.|Não|  
|CookieReceived|O conteúdo do cookie recebido pelo servidor.|Não|  
|CookieSent|O conteúdo do cookie enviado pelo servidor.|Não|  
|Referenciador|O site anterior visitado pelo cliente.|Não|  
  
## <a name="see-also"></a>Consulte também  
 [Log de rastreamento do serviço Servidor de Relatório](report-server-service-trace-log.md)   
 [Fontes e arquivos de log do Reporting Services](../report-server/reporting-services-log-files-and-sources.md)   
 [Referência de erros e eventos &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
