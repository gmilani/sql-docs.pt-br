---
title: Cache de modelos (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- templates [SQLXML], caching
ms.assetid: 73e151c6-b24e-4422-a116-51e0846bc6f5
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dd36af88aa2cb01c0c2bce05c7c023122eea87cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093265"
---
# <a name="template-caching-sqlxml-40"></a>Cache de modelos (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O armazenamento de modelos em cache aprimora o desempenho significativamente. Se o armazenamento de modelos em cache estiver definido, o modelo permanecerá na memória até sua primeira execução. Isto melhora o desempenho das execuções subsequentes do modelo.  
  
 Você pode definir o tamanho do cache do modelo adicionando a seguinte chave no Registro:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 O tamanho do modelo deve ser definido com base na memória disponível e no número de modelos que estão sendo usados. O padrão de **TemplateCacheSize** tamanho é 31. Você pode aumentar o tamanho do cache se o acesso ao modelo parecer lento ou diminuir o tamanho do cache se houver pouca memória.  
  
 Para obter melhor desempenho, é recomendável que você defina **TemplateCacheSize** maior do que o número de modelos, você geralmente usa. Se **Templatecachesize** é menor que o número de modelos, o desempenho diminuirá conforme o número de aumento de modelos. O **TemplateCacheSize** pode ser definido como um máximo de 128.  
  
 Sempre que um modelo em cache for usado, a hora da modificação do arquivo de modelo será verificada para ver se é necessário atualizá-lo. Isso ocorre porque a cópia em disco é mais recente do que a cópia em cache.  
  
> [!NOTE]  
>  As propriedades de comandos e parâmetros do modelo não são armazenadas em cache.  
  
## <a name="see-also"></a>Consulte também  
 [Cache de esquemas &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)   
 [Cache de XSL &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
  
  
