---
title: catalog.create_customized_logging_level | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 20b3ba0a-126f-49bf-b70f-61b2a0fcb750
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 87acb8f9b15fa2b22f4a7f1dbe01669eff08b92e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71281014"
---
# <a name="catalogcreate_customized_logging_level"></a>catalog.create_customized_logging_level 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Cria um novo nível de log personalizado. Para obter mais informações sobre níveis de registro em log personalizados, consulte [Registro em Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.create_customized_logging_level [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
    , [ @profile_value = ] profile_value  
    , [ @events_value = ] events_value  
    , [ @level_id = ] level_id OUT   
```  
  
## <a name="arguments"></a>Argumentos  
 [ @level_name = ] *level_name*  
 O nome do novo nível de log personalizado existente.  
  
 O *level_name* é **nvarchar(128)** .  
  
 [ @level_description = ] *level_description*  
 A descrição do novo nível de log personalizado.  
  
 A *level_description* é **nvarchar(max)** .  
  
 [ @profile_value = ] *profile_value*  
 As estatísticas que você deseja que o novo personalizado de nível de log registre em log.  
  
 Os valores válidos para as estatísticas incluem os descritos a seguir. Esses valores correspondem aos valores na guia **Estatísticas** da caixa de diálogo **Gerenciamento de Nível de Log Personalizado**.  
  
-   Execution = 0  
  
-   Volume = 1  
  
-   Performance = 2    
  
 O *profile_value* é um **bigint**.  
  
 [ @events_value = ] *events_value*  
 As estatísticas que você deseja que o novo nível de log personalizado registre em log.  
  
 Os valores válidos para eventos incluem os descritos a seguir. Esses valores correspondem aos valores na guia **Eventos** da caixa de diálogo **Gerenciamento de Nível de Log Personalizado**.  
  
|Eventos sem contexto do evento|Eventos com contexto do evento|  
|----------------------------------|-------------------------------|  
|OnVariableValueChanged = 0<br /><br /> OnExecutionStatusChanged = 1<br /><br /> OnPreExecute = 2<br /><br /> OnPostExecute = 3<br /><br /> OnPreValidate = 4<br /><br /> OnPostValidate = 5<br /><br /> OnWarning = 6<br /><br /> OnInformation = 7<br /><br /> OnError = 8<br /><br /> OnTaskFailed = 9<br /><br /> OnProgress = 10<br /><br /> OnQueryCancel = 11<br /><br /> OnBreakpointHit = 12<br /><br /> OnCustomEvent = 13<br /><br /> Diagnostic = 14<br /><br /> DiagnosticEx = 15<br /><br /> NonDiagnostic = 16|OnVariableValueChanged_IncludeContext = 32<br /><br /> OnExecutionStatusChanged_IncludeContext = 33<br /><br /> OnPreExecute_IncludeContext = 34<br /><br /> OnPostExecute_IncludeContext = 35<br /><br /> OnPreValidate_IncludeContext = 36<br /><br /> OnPostValidate_IncludeContext = 37<br /><br /> OnWarning_IncludeContext = 38<br /><br /> OnInformation_IncludeContext = 39<br /><br /> OnError_IncludeContext = 40<br /><br /> OnTaskFailed_IncludeContext = 41<br /><br /> OnProgress_IncludeContext = 42<br /><br /> OnQueryCancel_IncludeContext= 43<br /><br /> OnBreakpointHit_IncludeContext = 44<br /><br /> OnCustomEvent_IncludeContext = 45<br /><br /> Diagnostic_IncludeContext = 46<br /><br /> DiagnosticEx_IncludeContext = 47<br /><br /> NonDiagnostic_IncludeContext = 48|  
  
 O *events_value* é **bigint**.  
  
 [ @level_id = ] *level_id* OUT  
 A ID do novo nível de log personalizado.  
  
 O *level_id* é um **bigint**.  
  
## <a name="remarks"></a>Remarks  
 Para combinar vários valores em Transact-SQL para o argumento *profile_value* ou *events_value*, siga este exemplo. Para capturar os eventos OnError (8) e DiagnosticEx (15), a fórmula para calcular *events_value* é `2^8 + 2^15 = 33024`.  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (êxito)  
  
 Quando há falha no procedimento armazenado, ele gera um erro.  
  
## <a name="result-set"></a>Conjunto de resultados  
 None  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Associação na função de banco de dados **ssis_admin**  
  
-   Associação na função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve as condições que podem provocar falha no procedimento armazenado.  
  
-   O usuário não tem as permissões necessárias.  
  
  
