---
title: ALTER EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL DATA SOURCE
- ALTER_EXTERNAL_DATA_SOURCE
dev_langs:
- TSQL
helpviewer_keywords:
- polybase, alter external data source statement
- ALTER EXTERNAL DATA SOURCE statement
ms.assetid: a34b9e90-199d-46d0-817a-a7e69387bf5f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 236749303a05b54f37be5e24f10f56fc6f5bc41d
ms.sourcegitcommit: 853c2c2768caaa368dce72b4a5e6c465cc6346cf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71227153"
---
# <a name="alter-external-data-source-transact-sql"></a>ALTER EXTERNAL DATA SOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Modifica uma fonte de dados externa usada para criar uma tabela externa. A fonte de dados externa pode ser o Hadoop ou o WASBS (Armazenamento de Blobs do Azure) para SQL SERVER e o WASBS (Armazenamento de Blobs do Azure) ou o ABFSS/ADL (Azure Data Lake Storage) para o SQL Data Warehouse do Azure. 

## <a name="syntax"></a>Sintaxe  

```  
-- Modify an external data source
-- Applies to: SQL Server (2016 or later) and APS
ALTER EXTERNAL DATA SOURCE data_source_name SET
    {   
        LOCATION = 'server_name_or_IP' [,] |
        RESOURCE_MANAGER_LOCATION = <'IP address;Port'> [,] |
        CREDENTIAL = credential_name
    }  
    [;]  

-- Modify an external data source pointing to Azure Blob storage
-- Applies to: SQL Server (starting with 2017)
ALTER EXTERNAL DATA SOURCE data_source_name
    SET
        LOCATION = 'https://storage_account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ] 

-- Modify an external data source pointing to Azure Blob storage or Azure Data Lake storage
-- Applies to: Azure SQL Data Warehouse
ALTER EXTERNAL DATA SOURCE data_source_name
    SET
        [LOCATION = '<location prefix>://<location path>']
        [, CREDENTIAL = credential_name ] 
```

## <a name="arguments"></a>Argumentos  
 data_source_name Especifica o nome da fonte de dados definido pelo usuário. O nome deve ser exclusivo.

 LOCATION = 'server_name_or_IP' Fornece o protocolo de conectividade e o caminho para a fonte de dados externa.

 RESOURCE_MANAGER_LOCATION = '\<IP address;Port>' (Não se aplica ao SQL Data Warehouse do Azure) Especifica a localização do Hadoop Resource Manager. Quando especificado, o otimizador de consulta pode escolher pré-processar os dados para uma consulta do PolyBase usando os recursos de computação do Hadoop. Essa é uma decisão baseada em custo. Chamado de pushdown de predicado, isso pode reduzir significativamente o volume de dados transferidos entre o Hadoop e o SQL e, portanto, melhorar o desempenho da consulta.

 CREDENTIAL = Credential_Name Especifica a credencial nomeada. Confira [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

TYPE = [HADOOP | BLOB_STORAGE]   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
Somente para operações em massa, `LOCATION` precisa ser a URL válida para o Armazenamento de Blobs do Azure. Não coloque **/** , nome de arquivo ou parâmetros de Assinatura de Acesso Compartilhado no final da URL de `LOCATION`.
A credencial usada precisa ser criada usando `SHARED ACCESS SIGNATURE` como a identidade. Para mais informações sobre assinaturas de acesso compartilhado, consulte [Usando SAS (Assinatura de Acesso Compartilhado)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

  

## <a name="remarks"></a>Remarks
 Somente uma única fonte pode ser modificada de cada vez. Solicitações simultâneas para modificar a mesma fonte fazem com que uma instrução precise esperar. No entanto, fontes diferentes podem ser modificados ao mesmo tempo. Essa instrução pode ser executada simultaneamente com outras instruções.

## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY EXTERNAL DATA SOURCE.
 > [!IMPORTANT]  
 > A permissão ALTER ANY EXTERNAL DATA SOURCE concede a qualquer entidade de segurança a capacidade de criar e modificar qualquer objeto de fonte de dados externa e, portanto, isso também concede a capacidade de acessar todas as credenciais no escopo do banco de dados no banco de dados. Essa permissão precisa ser considerada como altamente privilegiada e, portanto, ser concedida somente para entidades de segurança confiáveis no sistema.


## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera o local e o local do Gerenciador de Recursos de uma fonte de dados existente.

```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
     LOCATION = 'hdfs://10.10.10.10:8020',
     RESOURCE_MANAGER_LOCATION = '10.10.10.10:8032'
    ;
  
```

 O exemplo a seguir altera a credencial para conectar-se a uma fonte de dados existente.

```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
   CREDENTIAL = new_hadoop_user
    ;
```

 O exemplo a seguir altera a credencial para uma LOCATION nova. Esse exemplo é uma fonte de dados externa criada para o SQL Data Warehouse do Azure. 

```  
ALTER EXTERNAL DATA SOURCE AzureStorage_west SET
   LOCATION = 'wasbs://loadingdemodataset@updatedproductioncontainer.blob.core.windows.net',
   CREDENTIAL = AzureStorageCredential
```
