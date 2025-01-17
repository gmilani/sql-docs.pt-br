---
title: sp_fulltext_table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_table_TSQL
- sp_fulltext_table
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_table
ms.assetid: a765f311-07fc-4af3-b74c-e9a027fbecce
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1db3a16b8072df38937bb482ac85a75dec6e83b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124144"
---
# <a name="spfulltexttable-transact-sql"></a>sp_fulltext_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Marca ou desmarca uma tabela para indexação de texto completo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md), [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)e [DROP FULLTEXT INDEX](../../t-sql/statements/drop-fulltext-index-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_fulltext_table   
   [ @tabname= ] 'qualified_table_name'           
   , [ @action= ] 'action'   
   [   
   , [ @ftcat= ] 'fulltext_catalog_name'           
   , [ @keyname= ] 'unique_index_name'   
   ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @tabname = ] 'qualified_table_name'` É um nome de tabela de uma ou duas partes. A tabela deve existir no banco de dados atual. *qualified_table_name* está **nvarchar(517)** , sem padrão.  
  
`[ @action = ] 'action'` É a ação a ser executada. *ação* está **nvarchar (50)** , sem padrão e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Criar**|Cria os metadados para um índice de texto completo para a tabela referenciada pela *qualified_table_name* e especifica que os dados de índice de texto completo para essa tabela devem residir no *fulltext_catalog_name*. Essa ação também designa o uso de *unique_index_name* como a coluna de chave de texto completo. Este índice exclusivo já deve estar presente e deve ser definido em uma coluna da tabela.<br /><br /> Uma pesquisa de texto completo não pode ser executada nessa tabela até que o catálogo de texto completo seja populado.|  
|**Drop**|Descarta os metadados no índice de texto completo para *qualified_table_name*. Se o índice de texto completo for ativo, será desativado automaticamente antes de ser descartado. Não é necessário remover colunas antes de descartar o índice de texto completo.|  
|**Ativar**|Ativa a capacidade de dados de índice de texto completo serem coletados para *qualified_table_name*, depois que tiver sido desativada. Deve haver pelo menos uma coluna participando do índice de texto completo para que ele seja ativado.<br /><br /> Um índice de texto completo torna-se ativo automaticamente (para população) assim que a primeira coluna é adicionada para indexação. Se a última coluna for descartada do índice, o índice se tornará inativo. Se o controle de alterações estiver ativo, a ativação de um índice inativo inicia um novo população.<br /><br /> Observe que isso não popula realmente o índice de texto completo, mas apenas registra a tabela no catálogo de texto completo no sistema de arquivos para que as linhas de *qualified_table_name* podem ser recuperados durante o próximo índice de texto completo população.|  
|**Desativar**|Desativa o índice de texto completo para *qualified_table_name* para que os dados de índice de texto completo não podem ser coletados para o *qualified_table_name*. Os metadados de índice de texto completo permanecem e a tabela pode ser reativada.<br /><br /> Se o controle de alterações estiver ativo, a desativação de um índice ativo congelará o estado do índice: qualquer população em andamento será interrompido e mais nenhuma alteração será propagada para o índice.|  
|**start_change_tracking**|Inicia uma população incremental do índice de texto completo. Se a tabela não tiver um carimbo de data/hora, inicia uma população completa do índice de texto completo. Inicia o controle de alterações na tabela.<br /><br /> Controle de alterações de texto completo não controla todas as operações WRITETEXT ou UPDATETEXT realizadas em colunas indexadas de texto completo que são do tipo **imagem**, **texto**, ou **ntext**.|  
|**stop_change_tracking**|Interrompe o controle de alterações na tabela.|  
|**update_index**|Propaga o conjunto atual de alterações controladas no índice de texto completo.|  
|**start_background_updateindex**|Inicia a propagação de alterações controladas no índice de texto completo conforme elas ocorrem.|  
|**stop_background_updateindex**|Interrompe a propagação de alterações controladas no índice de texto completo conforme elas ocorrem.|  
|**start_full**|Inicia uma população completa do índice de texto completo na tabela.|  
|**start_incremental**|Inicia uma população incremental do índice de texto completo na tabela.|  
|**Parar**|Interrompe uma população completa ou incremental.|  
  
`[ @ftcat = ] 'fulltext_catalog_name'` É um nome de catálogo de texto completo válido e existente para um **criar** ação. Para todas as outras ações, esse parâmetro deve ser NULL. *fulltext_catalog_name* está **sysname**, com um padrão NULL.  
  
`[ @keyname = ] 'unique_index_name'` É um índice válido única coluna de chave exclusivo não anulável em *qualified_table_name* para um **criar** ação. Para todas as outras ações, esse parâmetro deve ser NULL. *unique_index_name* está **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Depois que um índice de texto completo é desativado para uma tabela específica, o índice de texto completo existente permanece em vigor até a próxima população completa; No entanto, esse índice não é usado porque [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bloqueia consultas em tabelas desativadas.  
  
 Se a tabela é reativada e o índice não é populado novamente, o antigo índice permanece disponível para consultas em qualquer coluna restante habilitada para texto completo que não seja nova. É feita a correspondência de dados de colunas excluídas nas consultas que especificam uma pesquisa de todas as colunas de texto completo.  
  
 Depois que uma tabela tiver sido definida para indexação de texto completo, alternando a texto completo coluna de chave exclusiva de um tipo de dados para outro, seja alterando o tipo de dados dessa coluna ou alterar a chave exclusiva de texto completo de uma coluna para outra, sem uma nova população completa pode causar uma falha ocorrer durante uma consulta subsequente e retornar a mensagem de erro: "Conversão no tipo *data_type* falhou para o valor de chave de pesquisa de texto completo *key_value*." Para evitar isso, descarte a definição de texto completo para essa tabela usando o **drop** ação de **sp_fulltext_table** e redefine-a usando **sp_fulltext_table** e **sp_fulltext_column**.  
  
 A coluna de chave de texto completo deve ser definida para ter 900 bytes ou menos. É recomendável que o tamanho da coluna de chave seja o menor possível por motivos de desempenho.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa **db_owner** e **db_ddladmin** fixa de funções de banco de dados ou um usuário com permissões de referência sobre o catálogo de texto completo pode Execute **sp_fulltext_table**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-enabling-a-table-for-full-text-indexing"></a>A. Habilitando uma tabela para indexação de texto completo  
 O exemplo a seguir cria metadados do índice de texto completo da tabela `Document` do banco de dados `AdventureWorks`. `Cat_Desc` é um catálogo de texto completo. `PK_Document_DocumentID` é um índice exclusivo de uma única coluna em `Document`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'create', 'Cat_Desc', 'PK_Document_DocumentID';  
--Add some columns  
EXEC sp_fulltext_column 'Production.Document','DocumentSummary','add';  
-- Activate the full-text index  
EXEC sp_fulltext_table 'Production.Document','activate';  
GO  
```  
  
### <a name="b-activating-and-propagating-track-changes"></a>B. Ativando e propagando alterações controladas  
 O exemplo a seguir ativa e inicia a propagação alterações controladas no índice de texto completo conforme elas ocorrem.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'Start_change_tracking';  
EXEC sp_fulltext_table 'Production.Document', 'Start_background_updateindex';  
GO  
```  
  
### <a name="c-removing-a-full-text-index"></a>C. Removendo um índice de texto completo  
 Este exemplo remove os metadados de índice de texto completo para a tabela `Document` do banco de dados `AdventureWorks`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'drop';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_help_fulltext_tables &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [sp_helpindex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados de pesquisa de texto completo e pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
