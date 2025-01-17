---
title: Certificados e chaves assimétricas do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server], certificates and asymmetric keys
ms.assetid: 8519aa2f-f09c-4c1c-96b5-abc24811e60c
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 99e5f88f730953929115a5b18c00e5d1bb67562e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126834"
---
# <a name="sql-server-certificates-and-asymmetric-keys"></a>Certificados e chaves assimétricas do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

 A Public Key Cryptography é uma forma de sigilo nas mensagens na qual um usuário cria uma chave *pública* e uma chave *privada*. A chave privada é mantida em segredo, enquanto que a chave pública pode ser distribuída a outros. Embora as chaves estejam matematicamente relacionadas, a chave privada não pode ser obtida facilmente usando a chave pública. A chave pública pode ser usada para criptografar os dados que somente a chave privada correspondente será capaz de descriptografar. Isso pode ser usado para criptografar mensagens para o proprietário da chave privada. Da mesma forma, o proprietário de uma chave privada pode criptografar dados que só podem ser descriptografados com a chave pública. Esse uso constitui a base de certificados digitais em que informações contidas no certificado são criptografadas pelo proprietário de uma chave privada, permitindo que o autor tenha certeza sobre o conteúdo. Devido às chaves de criptografia e de descriptografia serem diferentes, elas são conhecidas como chaves *assimétricas*.
  
 Certificados e chaves assimétricas são duas formas de usar a criptografia assimétrica. Os certificados geralmente são usados como contêineres para chaves assimétricas porque podem conter mais informações, como datas de expiração e emissores. Não há diferenças entre os dois mecanismos para o algoritmo criptográfico, bem como na intensidade dada ao mesmo comprimento de chave. Geralmente você usa um certificado para criptografar outros tipos de chaves de criptografia em um banco de dados ou para assinar módulos de código.  
  
 Os certificados e as chaves assimétricas podem descriptografar dados um do outro. Geralmente você usa a criptografia assimétrica para criptografar uma chave simétrica para armazenamento em um banco de dados.  
  
 Uma chave pública não tem um formato específico como um certificado teria, e você não pode exportá-la para um arquivo.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém recursos que o habilitam a criar e gerenciar certificados e chaves para uso com o servidor e banco de dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ser usado para criar e gerenciar certificados e chaves com outros aplicativos ou no sistema operacional.  
  
## <a name="certificates"></a>Certificados  
 Um certificado é um objeto de segurança assinado digitalmente que contém uma chave pública (e, opcionalmente, uma particular) para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode usar certificados gerados externamente ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode gerá-los.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os certificados estão em conformidade com o padrão de certificado IETF X.509v3.  
  
 Os certificados são úteis devido à opção de exportar e importar chaves para os arquivos do certificado X.509. A sintaxe para criar certificados leva em conta as opções de criação de certificados, como uma data de expiração.  
  
### <a name="using-a-certificate-in-sql-server"></a>Usando um certificado no SQL Server  
 Os certificados podem ser usados para auxiliar nas conexões seguras, no espelhamento de banco de dados, para assinar pacotes e outros objetos ou para criptografar dados ou conexões. A tabela a seguir lista recursos adicionais para certificados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)|Explica o comando para a criação de certificados.|  
|[Identificar a origem dos pacotes com assinaturas digitais](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md)|Mostra informações sobre como usar certificados para assinar pacotes de software.|  
|[Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)|Abrange informações sobre como usar certificados com espelhamento de banco de dados.|  
  
## <a name="asymmetric-keys"></a>Chaves assimétricas  
 As chaves assimétricas são usadas para oferecer segurança às chaves simétricas. Elas também podem ser usadas para a criptografia de dados limitada e para assinar digitalmente objetos de banco de dados. Uma chave assimétrica consiste em uma chave privada e uma chave pública correspondente. Para obter mais informações sobre chaves assimétricas, veja [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md).  
  
 As chaves assimétricas podem ser importadas dos arquivos de chave com nomes seguros, mas não podem ser exportadas. Elas também não têm opções de expiração. As chaves assimétricas não podem criptografar conexões.  
  
### <a name="using-an-asymmetric-key-in-sql-server"></a>Usando uma chave assimétrica no SQL Server  
 As chaves assimétricas podem ser usadas para auxiliar na proteção de dados ou na assinatura de texto não criptografado. A tabela a seguir lista recursos adicionais para chaves assimétricas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)|Explica o comando para a criação de chaves assimétricas.|  
|[SIGNBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)|Exibe as opções de assinatura de objetos.|  
  
## <a name="tools"></a>Ferramentas  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] fornece ferramentas e utilitários que gerarão certificados e arquivos de chave com nomes seguros. Estas ferramentas oferecem maior flexibilidade no processo de geração de chaves do que a sintaxe do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Você pode usá-las para criar chaves RSA com comprimentos de chaves mais complexas e importá-las para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A tabela a seguir mostra onde encontrar essas ferramentas.  
  
|||  
|-|-|  
|Ferramenta|Finalidade|  
|[makecert](/windows/desktop/SecCrypto/makecert)|Cria certificados|  
|[sn](/dotnet/framework/tools/sn-exe-strong-name-tool)|Cria nomes seguros para chaves simétricas.|  
  
## <a name="related-tasks"></a>Related Tasks  
 [Escolher um algoritmo de criptografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)   
 [TDE &#40;Transparent Data Encryption&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
  
