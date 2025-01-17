---
title: sp_lock (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_lock_TSQL
- sp_lock
dev_langs:
- TSQL
helpviewer_keywords:
- sp_lock
ms.assetid: 9eaa0ec2-2ad9-457c-ae48-8da92a03dcb0
author: stevestein
ms.author: sstein
ms.openlocfilehash: c31148d09621caf9fd2ebc83a9b629f320418995
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305130"
---
# <a name="sp_lock-transact-sql"></a>sp_lock (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Reporta informações sobre bloqueios.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] para obter informações sobre bloqueios no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], use a exibição de gerenciamento dinâmico [Sys. dm _tran_locks](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_lock [ [ @spid1 = ] 'session ID1' ] [ , [@spid2 = ] 'session ID2' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @spid1 = ] 'session ID1'` é um número de ID de sessão [!INCLUDE[ssDE](../../includes/ssde-md.md)] de **Sys. dm _exec_sessions** para o qual o usuário deseja informações de bloqueio. a *sessão ID1* é **int** com um valor padrão de NULL. Execute **sp_who** para obter informações de processo sobre a sessão. Se a *sessão ID1* não for especificada, serão exibidas informações sobre todos os bloqueios.  
  
`[ @spid2 = ] 'session ID2'` é outro número de ID de sessão [!INCLUDE[ssDE](../../includes/ssde-md.md)] de **Sys. dm _exec_sessions** que pode ter um bloqueio ao mesmo tempo que a *sessão ID1* e sobre a qual o usuário também deseja informações. a *sessão ID2* é **int** com um valor padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 O conjunto de resultados **sp_lock** contém uma linha para cada bloqueio mantido pelas sessões especificadas nos parâmetros **\@spid1** e **\@spid2** . Se nem **\@spid1** nem **\@spid2** for especificado, o conjunto de resultados relatará os bloqueios para todas as sessões atualmente ativas na instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**spid**|**smallint**|A identificação da sessão [!INCLUDE[ssDE](../../includes/ssde-md.md)] para o processo solicitando o bloqueio.|  
|**dbid**|**smallint**|O número de identificação do banco de dados no qual o bloqueio é mantido. Você pode usar a função DB_NAME() para identificar o banco de dados.|  
|**ObjId**|**int**|O número de identificação do objeto no qual o bloqueio é mantido. Você pode usar a função OBJECT_NAME() no banco de dados relacionado para identificar o objeto. Um valor de 99 é um caso especial que indica um bloqueio em uma das páginas do sistema usada para registrar a alocação de páginas em um banco de dados.|  
|**IndId**|**smallint**|O número de identificação do índice no qual o bloqueio é mantido.|  
|**Tipo**|**nchar(4)**|O tipo de bloqueio:<br /><br /> RID = Bloqueio em uma única linha na tabela identificada por um identificador de linha (RID).<br /><br /> KEY = Bloqueio dentro de um índice que protege um intervalo de chaves em transações serializáveis.<br /><br /> PAG = Bloqueio em uma página de dados ou de índice.<br /><br /> EXT = Bloqueio em uma extensão.<br /><br /> TAB = Bloqueio em uma tabela inteira, inclusive todos os dados e índices.<br /><br /> DB = Bloqueio em um banco de dados.<br /><br /> FIL = Bloqueio em um arquivo de banco de dados.<br /><br /> APP = Bloqueio em um recurso de aplicativo especificado.<br /><br /> MD = Bloqueio em metadados ou informações do catálogo.<br /><br /> HBT = Lock em um heap ou árvore B (HoBT). Essas informações estão incompletas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> AU = Bloqueio em uma unidade de alocação. Essas informações estão incompletas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Kit**|**nchar(32)**|O valor que identifica o recurso bloqueado. O formato do valor depende do tipo de recurso identificado na coluna **tipo** :<br /><br /> **Tipo** de Valor **Recurso** do Valor<br /><br /> ELIMINÁ Um identificador no formato FileID: PageNumber: RID, em que FileID identifica o arquivo que contém a página, PageNumber identifica a página que contém a linha e rid identifica a linha específica na página. FileID corresponde à coluna **file_id** na exibição do catálogo **Sys. database_files** .<br /><br /> CHAVES Um número hexadecimal usado internamente pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)].<br /><br /> PAG Um número no formato FileID: PageNumber, em que FileID identifica o arquivo que contém a página e PageNumber identifica a página.<br /><br /> EXTERNA Um número que identifica a primeira página na extensão. O número está no formato idarquivo:númeropágina.<br /><br /> ABAS Nenhuma informação fornecida porque a tabela já está identificada na coluna **objID** .<br /><br /> ÚNICAS Nenhuma informação fornecida porque o banco de dados já está identificado na coluna **DBID** .<br /><br /> FIL O identificador do arquivo, que corresponde à coluna **file_id** na exibição do catálogo **Sys. database_files** .<br /><br /> APLICAÇÃO Um identificador exclusivo para o recurso de aplicativo que está sendo bloqueado. No formato DbPrincipleId: \<first de dois a 16 caracteres da cadeia de caracteres de recurso > valor \<hashed >.<br /><br /> MD: varia por tipo de recurso. Para obter mais informações, consulte a descrição da coluna **resource_description** em [Sys. dm _TRAN_LOCKS &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).<br /><br /> HBT: Nenhuma informação fornecida. Use a exibição de gerenciamento dinâmico **Sys. dm _tran_locks** em vez disso.<br /><br /> AU: Nenhuma informação fornecida. Use a exibição de gerenciamento dinâmico **Sys. dm _tran_locks** em vez disso.|  
|**Modo**|**nvarchar(8)**|O modo de bloqueio solicitado. Pode ser:<br /><br /> NULL = Nenhum acesso concedido ao recurso. Funciona como espaço reservado.<br /><br /> Sch-S = Estabilidade do esquema. Assegura que um elemento de esquema, como uma tabela ou índice, não seja cancelado enquanto qualquer sessão mantém o bloqueio de estabilidade do esquema no elemento do esquema.<br /><br /> Sch-M = Modificação do esquema. Deve ser mantido por qualquer sessão que desejar alterar o esquema do recurso especificado. Assegura que nenhuma outra sessão esteja fazendo referência ao objeto indicado.<br /><br /> S = Compartilhado. A sessão mantenedora possui acesso compartilhado ao recurso.<br /><br /> U = Atualizar. Indica um bloqueio de atualização adquirido em recursos que podem ser atualizados eventualmente. É usado para evitar uma forma comum de deadlock que ocorre quando várias sessões bloqueiam recursos para uma atualização potencial em um momento posterior.<br /><br /> X = Exclusivo. A sessão mantenedora possui acesso exclusivo ao recurso.<br /><br /> IS = Tentativa compartilhada. Indica a intenção de colocar bloqueios S em algum recurso subordinado na hierarquia de bloqueio.<br /><br /> IU = Atualização da tentativa. Indica a intenção de colocar bloqueios U em algum recurso subordinado na hierarquia de bloqueio.<br /><br /> IX = Exclusivo da tentativa. Indica a intenção de colocar bloqueios X em algum recurso subordinado na hierarquia de bloqueio.<br /><br /> SIU = Atualização da tentativa compartilhada. Indica o acesso compartilhado a um recurso com a intenção de adquirir bloqueios de atualização em recursos subordinados na hierarquia de bloqueio.<br /><br /> SIX = Exclusivo da tentativa compartilhada. Indica o acesso compartilhado a um recurso com a intenção de adquirir bloqueios exclusivos em recursos subordinados na hierarquia de bloqueio.<br /><br /> UIX = Atualizar exclusivo da tentativa. Indica a manutenção de um bloqueio de atualização de um recurso com a intenção de adquirir bloqueios exclusivos em recursos subordinados na hierarquia de bloqueio.<br /><br /> BU = Atualização em massa. Usado por operações em massa.<br /><br /> RangeS_S = Intervalo de chave compartilhada e bloqueio de recurso compartilhado. Indica varredura de intervalo serializável.<br /><br /> RangeS_U = Intervalo de chave compartilhada e bloqueio de recurso de atualização. Indica verificação de atualização serializável.<br /><br /> RangeI_N = Intervalo de chave de inserção e bloqueio de recurso nulo. Usado para testar intervalos antes de inserir uma nova chave em um índice.<br /><br /> RangeI_S = Bloqueio de conversão do intervalo de chave. Criado por uma sobreposição dos bloqueios RangeI_N e S.<br /><br /> RangeI_U = Bloqueio de conversão de intervalo de chave criado por uma sobreposição dos bloqueios RangeI_N e U.<br /><br /> RangeI_X = Bloqueio de conversão de intervalo de chave criado por uma sobreposição dos bloqueios RangeI_N e X.<br /><br /> RangeX_S = Bloqueio de conversão de intervalo de chaves criado por uma sobreposição de bloqueios RangeI_N e RangeS-S.<br /><br /> RangeIX_U = Bloqueio de conversão de intervalo de chave criado por uma sobreposição dos bloqueios RangeI_N e RangeS-U.<br /><br /> RangeX_X = Bloqueio de intervalo de chave exclusivo e de recurso exclusivo. Este é um bloqueio de conversão usado na atualização de uma chave em um intervalo.|  
|**Status**|**nvarchar(5)**|O estado de solicitação do bloqueio:<br /><br /> CNVRT: O bloqueio está sendo convertido de outro modo, mas a conversão está bloqueada por outro processo que mantém um bloqueio com um modo conflitante.<br /><br /> CONCEDER O bloqueio foi obtido.<br /><br /> ESPERADO O bloqueio está bloqueado por outro processo que mantém um bloqueio com um modo conflitante.|  
  
## <a name="remarks"></a>Comentários  
 Os usuários podem controlar o bloqueio de operações de leitura:  
  
-   Usando SET TRANSACTION ISOLATION LEVEL para especificar o nível de bloqueio de uma sessão. Para sintaxe e restrições, consulte [definir o nível &#40;de isolamento da transação&#41;Transact-SQL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
-   Usando dicas de tabela de bloqueio para especificar o nível de bloqueio de uma referência individual de uma tabela em uma cláusula FROM. Para sintaxe e restrições, consulte [dicas &#40;de tabela Transact-&#41;SQL](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Todas as transações distribuídas não associadas a uma sessão são transações órfãs. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] atribui a todas as transações distribuídas órfãs o valor SPID de -2, que torna mais fácil para um usuário identificar as transações de bloqueio distribuídas. Para obter mais informações, veja [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STAT.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-all-locks"></a>A. Listando todos os bloqueios  
 O exemplo a seguir exibe informações sobre todos os bloqueios mantidos atualmente em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
```sql  
USE master;  
GO  
EXEC sp_lock;  
GO  
```  
  
### <a name="b-listing-a-lock-from-a-single-server-process"></a>B. Listando um bloqueio de um processo de servidor único  
 O exemplo a seguir exibe informações, inclusive bloqueios, sobre a identificação do processo `53`.  
  
```sql  
USE master;  
GO  
EXEC sp_lock 53;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)   
 [DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md)   
 [OBJECT_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.dm_os_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [sys.dm_os_threads &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)  
  
  
