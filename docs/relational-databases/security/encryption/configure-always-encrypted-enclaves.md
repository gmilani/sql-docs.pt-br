---
title: Configurar e usar o Always Encrypted com enclaves seguros | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: bda4d41d4f2a9c92dca2d41b959ad4c4b32a1c79
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594472"
---
# <a name="configure-and-use-always-encrypted-with-secure-enclaves"></a>Configurar e usar o Always Encrypted com enclaves seguros 

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md) estende o recurso [Always Encrypted](always-encrypted-database-engine.md) existente para habilitar funcionalidades mais avançadas em dados confidenciais mantendo a confidencialidade desses dados. Este artigo lista tarefas comuns para configurar e usar o recurso.

Para ver um tutorial que mostra como começar rapidamente a usar o Always Encrypted com enclaves seguros, confira [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).

## <a name="set-up-your-environment-to-support-enclaves-and-attestation"></a>Configurar seu ambiente para dar suporte a enclaves e atestado
Para obter detalhes, confira os seguintes artigos:
- [Configuração do Serviço Guardião de Host para Always Encrypted no SQL Server](https://docs.microsoft.com/windows-server/security/set-up-hgs-for-always-encrypted-in-sql-server).

## <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>Gerenciar chaves para Always Encrypted com enclaves seguros
Confira os seguintes artigos para obter detalhes:
- [Gerenciar chaves para Always Encrypted com enclaves seguros – visão geral](always-encrypted-enclaves-manage-keys.md)
- [Provisionar chaves habilitadas para enclave](always-encrypted-enclaves-provision-keys.md)
- [Girar chaves habilitadas para enclave](always-encrypted-enclaves-rotate-keys.md)

## <a name="configure-columns-with-always-encrypted-with-secure-enclaves"></a>Configurar colunas com o Always Encrypted com enclaves seguros
Confira os seguintes artigos para obter detalhes:
- [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros – visão geral](always-encrypted-enclaves-configure-encryption.md)
- [Configurar criptografia de coluna in-loco com Transact-SQL](always-encrypted-enclaves-configure-encryption-tsql.md)
- [Habilitar o Always Encrypted com enclaves seguros para as colunas criptografadas existentes](always-encrypted-enclaves-enable-for-encrypted-columns.md)

> [!NOTE]
> Para obter um tutorial passo a passo sobre como configurar um ambiente de teste e experimentar a funcionalidade do Always Encrypted com enclaves seguras no SSMS, confira [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).

## <a name="query-columns-using-always-encrypted-with-secure-enclaves"></a>Consultar colunas usando o Always Encrypted com enclaves seguros
Confira os seguintes artigos para obter detalhes:
- [Consultar colunas usando o Always Encrypted com enclaves seguros – visão geral](always-encrypted-enclaves-query-columns.md)
- [Consultar colunas usando o Always Encrypted com enclaves seguros com o SSMS](always-encrypted-enclaves-query-columns-ssms.md)

## <a name="create-and-use-indexes-on-enclave-enabled-columns"></a>Criar e usar índices em colunas habilitadas para enclave
Confira os seguintes artigos para obter detalhes:
- [Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-create-use-indexes.md)

## <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>Desenvolver aplicativos usando o Always Encrypted com enclaves seguros
Confira os seguintes artigos para obter detalhes:
- [Desenvolver aplicativos usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-client-development.md)
