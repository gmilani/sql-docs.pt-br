---
title: sp_enclave_send_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_enclave_send_keys
- sp_enclave_send_keys_TSQL
- sys.sp_enclave_send_keys
- sys.sp_enclave_send_keys_TSQL
helpviewer_keywords:
- sp_enclave_send_keys
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: ca6e7485e85665f06c2410438b902fa0647418ae
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593759"
---
# <a name="sp_enclave_send_keys-transact-sql"></a>sp_enclave_send_keys (Transact-SQL)
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

Envia as chaves de criptografia de colunas, definidas no banco de dados, para o enclave seguro do lado do servidor usado com o [Always Encrypted com Secure enclaves](../security/encryption/always-encrypted-enclaves.md).

`sp_enclave_send_keys` só envia as chaves que são habilitadas para enclave e criptografar colunas que usam criptografia aleatória e têm índices. Para uma consulta de usuário comum, um driver de cliente fornece o enclave com as chaves necessárias para cálculos na consulta. `sp_enclave_send_keys` envia todas as chaves de criptografia de coluna definidas no banco de dados e usadas para índices com colunas criptografadas. 

`sp_enclave_send_keys` fornece uma maneira fácil de enviar chaves para o enclave e popular o cache de chave de criptografia de coluna para operações de indexação subsequentes. Use `sp_enclave_send_keys` para habilitar:
- Um DBA para recriar ou alterar índices ou estatísticas em colunas de banco de dados criptografadas, se o DBA não tiver acesso às chaves mestras de coluna. Consulte [invocar operações de indexação usando chaves de criptografia de coluna em cache](../security/encryption/always-encrypted-enclaves-create-use-indexes.md#invoke-indexing-operations-using-cached-column-encryption-keys).
- [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)] para concluir a recuperação de índices em colunas criptografadas. Consulte [recuperação de banco de dados](../security/encryption/always-encrypted-enclaves.md#database-recovery).
- Um aplicativo que usa .NET Framework Provedor de Dados para SQL Server carregar dados em massa em colunas criptografadas.

Para invocar `sp_enclave_send_keys`com êxito, você precisa se conectar ao banco de dados com os cálculos de Always Encrypted e enclave habilitados para a conexão de banco de dados. Você também precisa ter acesso às chaves mestras de coluna, proteger as chaves de criptografia de coluna, você vai enviar e precisar de permissões para acessar os metadados de chave Always Encrypted no banco de dados. 

## <a name="syntax"></a>Sintaxe  
  
```
sp_enclave_send_keys
[ ;]  
```

## <a name="arguments"></a>Argumentos

Este procedimento armazenado não tem argumentos.

## <a name="return-value"></a>Valor de retorno

Este procedimento armazenado não tem nenhum valor de retorno.
  
## <a name="result-sets"></a>Conjuntos de resultados

Este procedimento armazenado não tem conjuntos de resultados.
  
## <a name="permissions"></a>Permissões

 Exigir as permissões de `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` e `VIEW ANY COLUMN MASTER KEY DEFINITION` no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>Consulte também
- [Always Encrypted com enclaves seguros](../security/encryption/always-encrypted-enclaves.md) 
 
- [Criar e usar índices em colunas usando Always Encrypted com Secure enclaves](../security/encryption/always-encrypted-enclaves-create-use-indexes.md)

- [Tutorial: criar e usar índices em colunas habilitadas para enclave usando criptografia aleatória](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)
