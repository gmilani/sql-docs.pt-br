---
title: Elemento Issue (ssbdiagnose) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- issue element
- XML output file format [ssbdiagnose], issue element
- ssbdiagnose
ms.assetid: 2246a886-686b-44ca-9771-b155cedad8be
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3e4fff2c62073094805c075479724d3fc934ffca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986170"
---
# <a name="issue-element-ssbdiagnose"></a>Elemento Issue (ssbdiagnose)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Reporta um problema que foi encontrado pelo utilitário **ssbdiagnose** . O arquivo de saída XML de **ssbdiagnose** tem um elemento Issue por problema reportado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Issue  
    type="..."   
    code="..."   
    server="..."   
    database="..."   
    object="...">   
    ...   
</Issue>  
```  
  
## <a name="element-attributes"></a>Atributos do elemento  
  
|attribute|Descrição|  
|---------------|-----------------|  
|**type**|Identifica qual categoria de problema o elemento Issue está reportando:<br /><br /> **"Diagnóstico"** reporta um problema de configuração encontrado durante a análise da configuração de um [!INCLUDE[ssSB](../../includes/sssb-md.md)] .<br /><br /> **"Problema"** reporta um problema que impediu o **ssbdiagnose** de concluir sua análise. Corrija o problema e execute o **ssbdiagnose**novamente.<br /><br /> **"Evento"** reporta um evento [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] encontrado quando você executa uma verificação de **-RUNTIME** . Os eventos só serão reportados se **-SHOWEVENTS** for especificado.|  
|**código**|Identifica o número de erro da mensagem.|  
|**servidor**|Identifica a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] na qual o problema foi encontrado. Se o problema estava em uma instância padrão, o atributo de servidor só terá o nome do computador. Se o problema estava em uma instância nomeada, o atributo de servidor estará no formato NomedoComputador\NomedaInstância.|  
|**banco de dados**|Identifica o nome do banco de dados no qual o problema foi encontrado.|  
|**objeto**|Identifica o nome do objeto no qual o problema foi encontrado. Se o problema ocorreu em um nível de instância ou banco de dados, o atributo de objeto repetirá o nome da instância ou do banco de dados.|  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, tamanho é ilimitado.|  
|**Value**|Retorna o texto da mensagem de erro.|  
|**Ocorrência**|Uma vez por erro reportado.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento DiagnosticInformation &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**Elementos filho**|None|  
  
## <a name="example"></a>Exemplo  
 Este elemento reporta um erro 1102 para um banco de dados que não tenha uma chave mestra e o erro foi encontrado durante a análise de uma configuração do [!INCLUDE[ssSB](../../includes/sssb-md.md)] .  
  
```  
<Issue type="Diagnosis" code="1102" server="TestComputer" database="TargetDB" object="TargetDB">The master key was not found</diagnostic>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário ssbdiagnose &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
