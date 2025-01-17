---
title: sp_addtype (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addtype
- sp_addtype_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addtype
ms.assetid: ed72cd8e-5ff7-4084-8458-2d8ed279d817
author: stevestein
ms.author: sstein
ms.openlocfilehash: ab825ce5eb1310f3ff502965e409731b8741932e
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305139"
---
# <a name="sp_addtype-transact-sql"></a>sp_addtype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um tipo de dados de alias.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] use [Create Type](../../t-sql/statements/create-type-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addtype [ @typename = ] type,   
    [ @phystype = ] system_data_type   
    [ , [ @nulltype = ] 'null_type' ] ;  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @typename = ] type` é o nome do tipo de dados do alias. Os nomes de tipo de dados de alias devem seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md) e devem ser exclusivos em cada banco de dado. o *tipo* é **sysname**, sem padrão.  
  
`[ @phystype = ] system_data_type` é o tipo de dados físico ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornecido no qual o tipo de dados do alias se baseia. *system_data_type* é **sysname**, sem padrão, e pode ser um destes valores:  
  
||||  
|-|-|-|  
|**bigint**|**binary(n)**|**bit**|  
|**char(n)**|**datetime**|**decimal**|  
|**float**|**image**|**int**|  
|**money**|**nchar(n)**|**ntext**|  
|**numeric**|**nvarchar(n)**|**real**|  
|**smalldatetime**|**smallint**|**smallmoney**|  
|**sql_variant**|**text**|**tinyint**|  
|**uniqueidentifier**|**varbinary(n)**|**varchar(n)**|  
  
 São necessárias aspas em todos os parâmetros que têm espaços em branco ou marcas de pontuação inseridos. Para obter mais informações sobre os tipos de dados disponíveis, consulte [tipos &#40;de&#41;dados Transact-SQL](../../t-sql/data-types/data-types-transact-sql.md).  
  
 *n*  
 É um inteiro de não negativo que indica o comprimento pelo tipo de dados escolhido.  
  
 *P*  
 É um inteiro não negativo indicando o número total máximo de dígitos decimais que podem ser armazenados à esquerda e à direita do ponto decimal. Para obter mais informações, consulte [decimal e numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 *s*  
 É um inteiro não negativo indicando o número máximo de dígitos decimais que podem ser armazenados à direita do ponto decimal e deve ser menor que ou igual à precisão. Para obter mais informações, consulte [decimal e numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
`[ @nulltype = ] 'null_type'` indica a maneira como o tipo de dados de alias manipula valores nulos. *null_type* é **varchar (** 8 **)** , com um padrão de NULL e deve ser colocado entre aspas simples (' NULL ', ' NOT NULL ' ou ' NONULL '). Se *null_type* não for definido explicitamente por **sp_addtype**, ele será definido como a nulidade padrão atual. Use a função de sistema GETANSINULL para determinar a nulabilidade padrão atual. Isso pode ser ajustado usando a instrução SET ou ALTER DATABASE. A nulabilidade deve ser definida explicitamente. Se **\@phystype** for **bit**e **\@nulltype** não for especificado, o padrão será NOT NULL.  
  
> [!NOTE]  
>  O parâmetro *null_type* define apenas a nulidade padrão para esse tipo de dados. Se a nulabilidade for explicitamente definida quando o tipo de dados de alias for usado durante a criação da tabela, ela terá precedência sobre a nulabilidade padrão. Para obter mais informações, consulte [ALTER &#40;Table Transact-&#41; SQL](../../t-sql/statements/alter-table-transact-sql.md) e [CREATE TABLE &#40;Transact-&#41;SQL](../../t-sql/statements/create-table-transact-sql.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Um nome de tipo de dados de alias deve ser exclusivo no banco de dados, mas os tipos de dados com nomes diferentes podem ter a mesma definição.  
  
 A execução de **sp_addtype** cria um tipo de dados de alias que aparece na exibição do catálogo **Sys. Types** para um banco de dado específico. Se o tipo de dados do alias precisar estar disponível em todos os novos bancos de dado definidos pelo usuário, adicione-o ao **modelo**. Depois da criação de um tipo de dados de alias, você pode usá-lo em CREATE TABEL ou ALTER TABLE, e também vincular padrões e regras a ele. Todos os tipos de dados de alias escalares criados usando **sp_addtype** estão contidos no esquema **dbo** .  
  
 Os tipos de dados de alias herdam a ordenação padrão do banco de dados. Os agrupamentos de colunas e variáveis de tipos de alias são definidos nas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TABLE, ALTER TABLE e DECLARE @*local_variable* . A alteração da ordenação padrão do banco de dados aplica-se apenas a novas colunas e variáveis do tipo; isso não altera a ordenação das existentes.  
  
> [!IMPORTANT]  
>  Para fins de compatibilidade com versões anteriores, a função de banco de dados **pública** recebe automaticamente a permissão REFERENCES em tipos de dado de alias que são criados usando **sp_addtype**. Observação Quando tipos de dados de alias são criados usando a instrução CREATE TYPE em vez de **sp_addtype**, nenhuma concessão automática ocorre.  
  
 Tipos de dados de alias não podem ser definidos usando os tipos de dados **timestamp**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **tabela**, **XML**, **varchar (max)** , **nvarchar (max)** ou **varbinary (max)** .  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa **db_owner** ou **db_ddladmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-an-alias-data-type-that-does-not-allow-for-null-values"></a>A. Criando um tipo de dados de alias que não permite valores nulos  
 O exemplo a seguir cria um tipo de dados de alias chamado `ssn` (número do seguro social) que se baseia no tipo de dados **varchar** fornecido pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O tipo de dados `ssn` é usado para colunas que contém números de previdência social de 11 dígitos (999-99-9999). A coluna não pode ser NULL.  
  
 Observe que `varchar(11)` está entre aspas simples porque contém pontuação (parênteses).  
  
```  
USE master;  
GO  
EXEC sp_addtype ssn, 'varchar(11)', 'NOT NULL';  
GO  
```  
  
### <a name="b-creating-an-alias-data-type-that-allows-for-null-values"></a>B. Criando um tipo de dados de alias que permite valores nulos  
 O exemplo a seguir cria um tipo de dados de alias (baseado em `datetime`) chamado `birthday` que permite valores nulos.  
  
```  
USE master;  
GO  
EXEC sp_addtype birthday, datetime, 'NULL';  
```  
  
### <a name="c-creating-additional-alias-data-types"></a>C. Criando tipos de dados de alias adicionais  
 O exemplo a seguir cria dois tipos de dados de alias adicionais, `telephone` e `fax`, para número de telefone e fax nacionais e internacionais.  
  
```  
USE master;  
GO  
EXEC sp_addtype telephone, 'varchar(24)', 'NOT NULL';  
GO  
EXEC sp_addtype fax, 'varchar(24)', 'NULL';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Mecanismo de banco de dados procedimentos &#40;armazenados Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [sp_bindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_bindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_droptype &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [sp_unbindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
