---
title: Usar parâmetros com valor de tabela (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table-valued parameters
- table-valued parameters, about table-valued parameters
- parameters [SQL Server], table-valued
- TVP See table-valued parameters
ms.assetid: 5e95a382-1e01-4c74-81f5-055612c2ad99
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c01f99fc2f1964e1a459de12d77f0bfc3ea40ca6
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72796642"
---
# <a name="use-table-valued-parameters-database-engine"></a>Usar parâmetros com valor de tabela (Mecanismo de Banco de Dados)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Os parâmetros com valor de tabela são declarados usando tipos de tabela definidos pelo usuário. Você pode usar parâmetros com valor de tabela para enviar várias linhas de dados para uma rotina ou instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] , como um procedimento armazenado ou função, sem criar uma tabela temporária ou muitos parâmetros.

Os parâmetros com valor de tabela são como matrizes de parâmetro em OLE DB e ODBC, mas oferecem mais flexibilidade e integração mais próxima ao [!INCLUDE[tsql](../../includes/tsql-md.md)]. Eles também têm o benefício de poder participar de operações com base em conjunto.

[!INCLUDE[tsql](../../includes/tsql-md.md)] passa parâmetros com valor de tabela para rotinas por referência, para evitar a criação de uma cópia dos dados de entrada. Você pode criar e executar rotinas [!INCLUDE[tsql](../../includes/tsql-md.md)] com parâmetros com valor de tabela e chamá-las do código [!INCLUDE[tsql](../../includes/tsql-md.md)] , de clientes nativos e gerenciados em qualquer linguagem gerenciada.

 **Neste tópico:**

[Benefícios](#Benefits)

[Restrições](#Restrictions)

[Parâmetros com valor de tabela vs. Operações BULK INSERT](#BulkInsert)

[Exemplo](#Example)

## <a name="Benefits"></a> Benefícios

Um parâmetro com valor de tabela é delimitado ao procedimento armazenado, à função ou ao texto [!INCLUDE[tsql](../../includes/tsql-md.md)] dinâmico, exatamente como outros parâmetros. Do mesmo modo, uma variável de tipo de tabela tem escopo como qualquer outra variável local criada com uma instrução DECLARE. Você pode declarar variáveis com valor de tabela em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] dinâmicas e passar essas variáveis como parâmetros com valor de tabela para funções e procedimentos armazenados.

Os parâmetros com valor de tabela oferecem mais flexibilidade e, em alguns casos, melhor desempenho do que tabelas temporárias ou outras formas de passar uma lista de parâmetros. Eles oferecem os seguintes benefícios:

- Não adquirem bloqueios para a população inicial de dados de um cliente.
- Fornecem um modelo de programação simples.
- Permitem que você inclua lógica de negócios complexa em uma única rotina.
- Reduzem viagens de ida e volta ao servidor.
- Podem ter uma estrutura de tabela de cardinalidade diferente.
- Possuem rigidez de tipo.
- Permitem que o cliente especifique a ordem de classificação e as chaves exclusivas.
- São armazenados em cache como uma tabela temporária quando usado em um procedimento armazenado. A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], os parâmetros com valor de tabela também são armazenados em cache para consultas parametrizadas.

## <a name="Permissions"></a> Permissões
Para criar uma instância de um Tipo de Tabela Definido pelo Usuário ou chamar um procedimento armazenado com um parâmetro com valor de tabela, o usuário deve ter a permissão EXECUTE no tipo, no esquema ou no banco de dados que contém o tipo.

## <a name="Restrictions"></a> Restrições

Os parâmetros com valor de tabela têm as seguintes restrições:

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não mantém estatísticas em colunas de parâmetros com valor de tabela.
- Os parâmetros com valor de tabela devem ser passados como parâmetros de entrada READONLY para rotinas [!INCLUDE[tsql](../../includes/tsql-md.md)] . Não é possível executar operações DML como UPDATE, DELETE ou INSERT em um parâmetro com valor de tabela no corpo de uma rotina.
- Você não pode usar um parâmetro com valor de tabela como destino de uma instrução SELECT INTO ou INSERT EXEC. Um parâmetro com valor de tabela pode estar na cláusula FROM de SELECT INTO ou na cadeia de caracteres ou procedimento armazenado INSERT EXEC.

## <a name="BulkInsert"></a> Parâmetros com valor de tabela vs. Operações BULK INSERT

O uso de parâmetros com valor de tabela é comparável a outros modos de usar variáveis com base em conjunto; no entanto, o uso de parâmetros com valor de tabela normalmente pode ser mais rápido em grandes conjuntos de dados. Comparado a operações em massa que têm um custo maior de inicialização, os parâmetros com valor de tabela têm bom desempenho para inserção de menos de 1000 linhas.

Os parâmetros com valor de tabela que são reutilizados beneficiam-se de cache de tabela temporária. Esse cache de tabela habilita uma escalabilidade melhor do que operações BULK INSERT equivalentes. Ao usar pequenas operações de inserção de linha, pode haver um pequeno ganho de benefício de desempenho se forem usadas listas de parâmetros ou instruções processadas em lotes em vez de operações BULK INSERT ou parâmetros com valor de tabela. Porém, esses métodos são menos convenientes ao programa e o desempenho diminui rapidamente à medida que as linhas aumentam.

Os parâmetros com valor de tabela têm desempenho igualmente bom ou melhor do que uma implementação de matriz de parâmetros equivalente.

## <a name="Example"></a> Exemplo

O exemplo a seguir usa o [!INCLUDE[tsql](../../includes/tsql-md.md)] e mostra como criar um tipo de parâmetro com valor de tabela, declarar uma variável para referenciá-lo, preencher a lista de parâmetros e passar os valores para um procedimento armazenado no banco de dados do AdventureWorks.

```sql
/* Create a table type. */
CREATE TYPE LocationTableType 
   AS TABLE
      ( LocationName VARCHAR(50)
      , CostRate INT );
GO
/* Create a procedure to receive data for the table-valued parameter. */
CREATE PROCEDURE dbo. usp_InsertProductionLocation
   @TVP LocationTableType READONLY
      AS
      SET NOCOUNT ON
      INSERT INTO AdventureWorks2012.Production.Location
         (
            Name
            , CostRate
            , Availability
            , ModifiedDate
         )
      SELECT *, 0, GETDATE()
      FROM @TVP;
GO
/* Declare a variable that references the type. */
DECLARE @LocationTVP AS LocationTableType;
/* Add data to the table variable. */
INSERT INTO @LocationTVP (LocationName, CostRate)
   SELECT Name, 0.00
   FROM AdventureWorks2012.Person.StateProvince;
  
/* Pass the table variable data to a stored procedure. */
EXEC usp_InsertProductionLocation @LocationTVP;
```

## <a name="see-also"></a>Consulte Também

- [CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md)
- [DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
- [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
- [sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)
- [sys.parameter_type_usages](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md)
- [CREATE PROCEDURE](../../t-sql/statements/create-procedure-transact-sql.md)
- [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md)  
