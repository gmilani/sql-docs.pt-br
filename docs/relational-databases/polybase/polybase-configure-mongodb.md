---
title: Configurar o PolyBase para acessar dados externos no MongoDB | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 9b343327b73a8e682a76b94757982f20fde81e7c
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710614"
---
# <a name="configure-polybase-to-access-external-data-in-mongodb"></a>Configurar o PolyBase para acessar dados externos no MongoDB

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O artigo explica como usar o PolyBase em uma instância do SQL Server para consultar dados externos no MongoDB.

## <a name="prerequisites"></a>Prerequisites

Se você ainda não instalou o PolyBase, veja [Instalação do PolyBase](polybase-installation.md).

Antes de criar um banco de dados de credencial no escopo, uma [chave mestra](../../t-sql/statements/create-master-key-transact-sql.md) deve ser criada. 
    

## <a name="configure-a-mongodb-external-data-source"></a>Configurar uma fonte de dados externa do MongoDB

Para consultar os dados de uma fonte de dados do MongoDB, você precisa criar tabelas externas para fazer referência aos dados externos. Esta seção fornece código de exemplo para criar essas tabelas externas.

Os seguintes comandos Transact-SQL são usados nesta seção:

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. Crie uma credencial no escopo do banco de dados para acessar a origem do MongoDB.

    ```sql
    /*  specify credentials to external data source
    *  IDENTITY: user name for external source. 
    *  SECRET: password for external source.
    */
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'password';
    ```
1. Crie uma fonte de dados externa, usando [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

    ```sql
    /*  LOCATION: Location string should be of format '<type>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH (LOCATION = 'mongodb://<server>[:<port>]',
    -- PUSHDOWN = ON | OFF,
    CREDENTIAL = credential_name);
    ```

1. **Opcional:** Crie estatísticas em uma tabela externa.

    É recomendável criar estatísticas em colunas de tabelas externas, especialmente aquelas usadas para junções, filtros e agregações, a fim de ter o desempenho de consulta ideal.

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT] 
>Depois de criar uma fonte de dados externa, você pode usar o comando [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) para criar uma tabela que possa ser consultada por essa fonte. 

## <a name="flattening"></a>Nivelamento
 O nivelamento é habilitado para os dados aninhados e repetidos das coleções de documentos do MongoDB. O usuário precisa habilitar `create an external table` e especificar explicitamente um esquema relacional nas coleções de documentos do MongoDB que possam ter dados repetidos e/ou aninhados. Habilitaremos a detecção de esquema automático em coleções de documentos do mongo em etapas futuras.
Os tipos de dados repetidos/aninhados do JSON serão nivelados da seguinte forma

* Objetos: coleção de chave-valor não ordenada entre chaves (aninhada)

   - Criaremos uma coluna de tabela para cada chave de objeto

     * Nome da coluna: objectname_keyname

* Matriz: valores ordenados, separados por vírgulas, entre colchetes (repetidos)

   - Adicionaremos uma nova linha da tabela para cada item da matriz

   - Criaremos uma coluna por matriz para armazenar o índice do item da matriz

     * Nome da coluna: arrayname_index

     * Tipo de dados: bigint

Há vários possíveis problemas com essa técnica, dois deles sendo:

* um campo repetido vazio mascarará efetivamente os dados contidos nos campos nivelados no mesmo registro

* a presença de vários campos repetidos pode resultar em uma explosão do número de linhas produzidas

Como exemplo, avaliamos a coleção do restaurante do conjunto de dados de amostra do MongoDB armazenada no formato JSON não relacional. Cada restaurante tem um campo de endereço aninhado e uma matriz de classificações atribuídas a ele em dias diferentes. A figura a seguir ilustra um restaurante típico com o endereço aninhado e notas aninhadas repetidas.

![Nivelamento do MongoDB](../../relational-databases/polybase/media/mongo-flattening.png "Nivelamento de restaurante do MongoDB")

O endereço do objeto será nivelado conforme abaixo:

* O campo aninhado restaurant.address.building se torna restaurant.address_building
* O campo aninhado restaurant.address.coord se torna restaurant.address_coord
* O campo aninhado restaurant.address.street se torna restaurant.address_street
* O campo aninhado restaurant.address.zipcode se torna restaurant.address_zipcode

As classificações da matriz serão niveladas conforme abaixo:

| grades_date | grades_grade  | games_score | 
| ------------- | ------------------------- | -------------- |
|1393804800000 |Um |2|
|1378857600000|Um |6|
|135898560000 |Um |10|
|1322006400000|Um |9|
|1299715200000 |B |14|

## <a name="cosmos-db-connection"></a>Conexão do Cosmos DB

Usando a API do mongo do Cosmos DB e o conector do PolyBase do Mongo DB, você pode criar uma tabela externa de uma **instância do Cosmos DB**. Isso pode ser feito seguindo as mesmas etapas listadas acima. Verifique se as credenciais, o endereço do servidor, a porta e a cadeia de caracteres de localização no escopo do banco de dados refletem os do servidor do Cosmos DB. 

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o PolyBase, consulte [Visão geral do PolyBase do SQL Server](polybase-guide.md).
