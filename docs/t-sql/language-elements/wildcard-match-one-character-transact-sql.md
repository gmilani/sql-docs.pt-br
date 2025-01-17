---
title: _ (curinga – corresponder a um caractere) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Match
- wildcard
- _TSQL
- Match One
- _
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- _ (wildcard - match one character)
ms.assetid: 11a2ed36-9e21-4bdf-ae20-a31db1434b97
author: rothja
ms.author: jroth
ms.openlocfilehash: 6f6876003c64889d32e31266ebe74b6532c1a8f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000304"
---
# <a name="-wildcard---match-one-character-transact-sql"></a>_ (Curinga – corresponde a um caractere) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Use o caractere sublinhado _ para corresponder a qualquer caractere único em uma operação de comparação de cadeia de caracteres que envolva correspondência de padrões, como `LIKE` e `PATINDEX`.  
  
## <a name="examples"></a>Exemplos  

## <a name="a-simple-example"></a>A: Exemplo simples   

O exemplo a seguir retorna todos os nomes de banco de dados que começam com a letra `m` e têm a letra `d` como a terceira letra. O caractere sublinhado especifica que o segundo caractere do nome pode ser qualquer letra. Os bancos de dados `model` e `msdb` atendem a esse critério. O banco de dados `master` não atende.

```sql
SELECT name FROM sys.databases
WHERE name LIKE 'm_d%';
```   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-----
model
msdb
```   
Pode haver bancos de dados adicionais que atendem a esses critérios.

Você pode usar vários sublinhados para representar vários caracteres. Alterar o critério `LIKE` para incluir dois sublinhados `'m__%`, inclui o banco de dados mestre no resultado.

### <a name="b-more-complex-example"></a>B: exemplo mais complexo
 O exemplo a seguir usa o operador _ para localizar todas as pessoas na tabela `Person` que têm um nome de três letras que termina com `an`.  
  
```sql  
-- USE AdventureWorks2012
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE '_an'  
ORDER BY FirstName;  
```  
## <a name="c-escaping-the-underscore-character"></a>C: Como fazer escape do caractere sublinhado   
O exemplo a seguir retorna os nomes das funções de banco de dados fixas como `db_owner` e `db_ddladmin`, mas também retorna o usuário `dbo`. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db_%';
```

O sublinhado na posição do terceiro caractere é interpretado como um caractere curinga e não está filtrando somente entidades de segurança que começam com as letras `db_`. Para usar um escape no caractere sublinhado coloque-o entre colchetes `[_]`. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db[_]%';
```   
Agora o usuário `dbo` foi excluído.   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-------------
db_owner
db_accessadmin
db_securityadmin
...
```

  
## <a name="see-also"></a>Consulte Também  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% (curinga – caracteres a serem correspondidos)](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; (curinga – caracteres a serem correspondidos)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#91;^&#93; (Curinga – caracteres para não correspondência)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
  
