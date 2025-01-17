---
title: catalog.get_parameter_values (Banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 5b1aeaf7-c938-4aef-bafc-e4d7a82eb578
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0338675549b49dd5c50eff9a8996f7a3ee6ee329
ms.sourcegitcommit: 4fb6bc7c81a692a2df706df063d36afad42816af
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049947"
---
# <a name="catalogget_parameter_values-ssisdb-database"></a>catalog.get_parameter_values (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Resolve e recupera os valores de parâmetro padrão de um projeto e os pacotes correspondentes no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.get_parameter_values [ @folder_name = ] folder_name  
     , [ @project_name = ] project_name  
     , [ @package_name = ] package_name  
  [  , [ @reference_id = ] reference_id  ]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome da pasta que contém o projeto. O *folder_name* é **nvarchar(128)** .  
  
 [ @project_name = ] *project_name*  
 O nome do projeto em que o parâmetro reside. O *project_name* é **nvarchar(128)** .  
  
 [ @package_name = ] *package_name*  
 O nome do pacote. Especifique o nome do pacote para recuperar todos os parâmetros de projeto e os parâmetros de um pacote específico. O *package_name* é **nvarchar(260)** .  
  
 [ @reference_id = ] *reference_id*  
 O identificador exclusivo de uma referência do ambiente. Esse parâmetro é opcional. O *reference_id* é **bigint**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna uma tabela que tem o seguinte formato:  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|object_type|**smallint**|O tipo do parâmetro. O valor é `20` para um parâmetro de projeto e o valor é `30` para um parâmetro de pacote.|  
|parameter_data_type|**nvarchar(128)**|O tipo de dados do parâmetro.|  
|parameter_name|**sysname**|O nome do parâmetro.|  
|parameter_value|**sql_variant**|O valor do parâmetro.|  
|sensitive|**bit**|Quando o valor é `1`, o valor do parâmetro é confidencial. Quando o valor é `0`, o valor do parâmetro não é confidencial.|  
|required|**bit**|Quando o valor é `1`, o valor do parâmetro é necessário para iniciar a execução. Quando o valor é `0`, o valor de parâmetro não é necessário para iniciar a execução.|  
|value_set|**bit**|Quando o valor é `1`, o valor do parâmetro foi atribuído. Quando o valor é `0`, o valor do parâmetro não foi atribuído.|  
  
> [!NOTE]  
>  Valores literais são exibidos em texto não criptografado. **NULL** é exibido no lugar de valores confidenciais.  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ no projeto e, se aplicável, permissão READ no ambiente referenciado  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   Não é possível encontrar o pacote na pasta ou projeto especificado  
  
-   O usuário não tem as permissões apropriadas  
  
-   A referência de ambiente especificado não existe  
  
  
