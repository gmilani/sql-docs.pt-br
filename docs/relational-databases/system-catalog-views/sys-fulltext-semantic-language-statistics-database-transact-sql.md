---
title: sys. fulltext_semantic_language_statistics_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_semantic_language_statistics_database_TSQL
- fulltext_semantic_language_statistics_database_TSQL
- fulltext_semantic_language_statistics_database
- sys.fulltext_semantic_language_statistics_database
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_semantic_language_statistics_database catalog view
ms.assetid: 32e95614-ed88-4068-8c37-1e21544717bc
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: e1d2e60ce41cd3c57af209123471696cf02a03ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133786"
---
# <a name="sysfulltextsemanticlanguagestatisticsdatabase-transact-sql"></a>sys.fulltext_semantic_language_statistics_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha sobre o banco de dados de estatísticas semânticas de idioma instalado na instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 É possível consultar essa exibição para descobrir o componente de estatísticas de idioma semântico para processamento semântico.  
   
  
||||  
|-|-|-|  
|**Nome da coluna**|**Tipo**|**Descrição**|  
|**database_id**|**int**|ID do banco de dados, exclusivo em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**register_date**|**datetime**|Data do registro do banco de dados para processamento semântico.|  
|**registered_by**|**int**|ID da entidade de segurança de servidor que registrou o banco de dados para processamento semântico.|  
|**version**|**nvarchar(128)**|As informações de versão mais recentes específicas ao banco de dados de estatísticas de idioma semântico.|  
  
## <a name="general-remarks"></a>Comentários gerais  
 Para obter mais informações, veja [Instalar e configurar a pesquisa semântica](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
## <a name="metadata"></a>Metadados  
 Para obter informações sobre os idiomas que têm suporte para indexação semântica, consulte a exibição do catálogo [sys. fulltext_semantic_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 A visibilidade dos metadados em exibições do catálogo está limitada aos protegíveis que pertencem a um usuário ou para os quais o usuário recebeu permissão.  
  
## <a name="examples"></a>Exemplos  
 A exemplo a seguir mostra como consultar **sys. fulltext_semantic_language_statistics_database** para obter informações sobre o banco de dados de estatísticas semânticas de idioma registrado na instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Instalar e configurar a pesquisa semântica](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
