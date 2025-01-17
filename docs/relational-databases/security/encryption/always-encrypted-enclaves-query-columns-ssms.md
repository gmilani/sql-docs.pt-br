---
title: Consultar colunas usando o Always Encrypted com enclaves seguros com o SSMS | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6bee04f4a794a503b89b73d4ef4a6a1cef897b4b
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595591"
---
# <a name="query-columns-using-always-encrypted-with-secure-enclaves-with-ssms"></a>Consultar colunas usando o Always Encrypted com enclaves seguros com o SSMS
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

Este artigo descreve como usar o SQL Server Management Studio para emitir consultas que usam um enclave seguro no servidor para [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md), incluindo:
- Consultas que disparam operações criptográficas in-loco.
- Consultas que disparam computações avançadas, incluindo comparações de intervalo ou operações de correspondência de padrões em colunas criptografadas com chaves habilitadas para enclave.
- Consultas que criam ou atualizam índices em colunas criptografadas usando criptografia aleatória e chaves habilitadas para enclave.  

Para usar o SSMS para executar consultas em colunas criptografadas usando um enclave seguro, siga as instruções em [Consultar colunas usando Always Encrypted com SQL Server Management Studio](always-encrypted-query-columns-ssms.md). Aqui estão algumas coisas que são específicas para enclaves que você deve estar ciente:

- É necessário o SSMS versão 18.3 ou superior.
- Verifique se você está executando consultas em uma janela de consulta utilizando um enclave seguro de uma conexão que tem cálculos de enclave e Always Encrypted habilitados. Para obter instruções detalhadas, confira [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md) e [Habilitar e desabilitar o Always Encrypted para uma conexão de banco de dados ](always-encrypted-query-columns-ssms.md#en-dis).

## <a name="next-steps"></a>Next Steps
- [Desenvolver aplicativos usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-client-development.md)

## <a name="see-also"></a>Consulte Também  
- [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [Configurar criptografia de coluna in-loco com Transact-SQL](always-encrypted-enclaves-configure-encryption-tsql.md)
- [Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-create-use-indexes.md)

