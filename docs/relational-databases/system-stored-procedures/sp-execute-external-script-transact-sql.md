---
title: sp_execute_external_script (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: ab3bf4f98abaf5f164a3b38f4e09b10acf28b2f4
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532827"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
O procedimento armazenado **sp_execute_external_script** executa um script fornecido como um argumento de entrada para o procedimento e é usado com [serviços de Machine Learning](../../advanced-analytics/index.yml) e [extensões de linguagem](../../language-extensions/language-extensions-overview.md). 

Para Serviços de Machine Learning, [Python](../../advanced-analytics/concepts/extension-python.md) e [R](../../advanced-analytics/concepts/extension-r.md) são idiomas com suporte. Para extensões de linguagem, há suporte para Java, mas deve ser definido com [criar linguagem externa](../../t-sql/statements/create-external-language-transact-sql.md).

Para executar o **sp_execute_external_script**, você deve primeiro instalar as extensões serviços de Machine Learning ou Language. Para obter mais informações, consulte [instalar SQL Server serviços de Machine Learning (Python e R) no Windows](../../advanced-analytics/install/sql-machine-learning-services-windows-install.md) e [Linux](../../linux/sql-server-linux-setup-machine-learning.md), ou [instalar as extensões de linguagem SQL Server no Windows e no](../../language-extensions/install/install-sql-server-language-extensions-on-windows.md) [Linux](../../linux/sql-server-linux-setup-language-extensions.md).
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
O procedimento armazenado **sp_execute_external_script** executa um script fornecido como um argumento de entrada para o procedimento e é usado com [Serviços de Machine Learning](../../advanced-analytics/index.yml) em SQL Server 2017. 

Para Serviços de Machine Learning, [Python](../../advanced-analytics/concepts/extension-python.md) e [R](../../advanced-analytics/concepts/extension-r.md) são idiomas com suporte. 

Para executar o **sp_execute_external_script**, você deve primeiro instalar o serviços de Machine Learning. Para obter mais informações, consulte [instalar SQL Server serviços de Machine Learning (Python e R) no Windows](../../advanced-analytics/install/sql-machine-learning-services-windows-install.md).
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
O procedimento armazenado **sp_execute_external_script** executa um script fornecido como um argumento de entrada para o procedimento e é usado com o [R Services](../../advanced-analytics/r/sql-server-r-services.md) no SQL Server 2016.

Para o R Services, [r](../../advanced-analytics/concepts/extension-r.md) é o idioma com suporte.

Para executar o **sp_execute_external_script**, você deve primeiro instalar o R Services. Para obter mais informações, consulte [instalar SQL Server serviços de Machine Learning (Python e R) no Windows](../../advanced-analytics/install/sql-r-services-windows-install.md).
::: moniker-end

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="syntax"></a>Sintaxe

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]    
    [ , @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
## <a name="syntax-for-2017-and-earlier"></a>Sintaxe para 2017 e anterior

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end

## <a name="arguments"></a>Argumentos
 **idioma\@** = N '*idioma*'  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
 Indica a linguagem de script. o *idioma* é **sysname**. Os valores válidos são **R**, **Python**e qualquer linguagem definida com [criar linguagem externa](../../t-sql/statements/create-external-language-transact-sql.md) (por exemplo, Java).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
 Indica a linguagem de script. o *idioma* é **sysname**. No SQL Server 2017, os valores válidos são **R** e **Python**.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
 Indica a linguagem de script. o *idioma* é **sysname**. No SQL Server 2016, o único valor válido é **R**.
::: moniker-end

 **\@script** = N script de linguagem externa*de script especificado*como uma entrada literal ou variável. o *script* é **nvarchar (max)** .  

`[ @input_data_1 =  N'input_data_1' ]` especifica os dados de entrada usados pelo script externo na forma de uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)]. O tipo de dados de *input_data_1* é **nvarchar (max)** .

`[ @input_data_1_name = N'input_data_1_name' ]` especifica o nome da variável usada para representar a consulta definida por @input_data_1. O tipo de dados da variável no script externo depende do idioma. No caso do R, a variável de entrada é um quadro de dados. No caso do Python, a entrada deve ser tabular. *input_data_1_name* é **sysname**.  O valor padrão é *InputDataSet*.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]` usado para criar modelos por partição. Especifica o nome da coluna usada para ordenar o conjunto de resultados, por exemplo, por nome do produto. O tipo de dados da variável no script externo depende do idioma. No caso do R, a variável de entrada é um quadro de dados. No caso do Python, a entrada deve ser tabular.

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]` usado para criar modelos por partição. Especifica o nome da coluna usada para segmentar dados, como região geográfica ou data. O tipo de dados da variável no script externo depende do idioma. No caso do R, a variável de entrada é um quadro de dados. No caso do Python, a entrada deve ser tabular. 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]` especifica o nome da variável no script externo que contém os dados a serem retornados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] após a conclusão da chamada de procedimento armazenado. O tipo de dados da variável no script externo depende do idioma. Para R, a saída deve ser um quadro de dados. Para Python, a saída deve ser um quadro de dados pandas. *output_data_1_name* é **sysname**.  O valor padrão é *OutputDataSet*.  

`[ @parallel = 0 | 1 ]` habilita a execução paralela de scripts R definindo o parâmetro `@parallel` como 1. O padrão para esse parâmetro é 0 (sem paralelismo). Se `@parallel = 1` e a saída estiver sendo transmitida diretamente para o computador cliente, a cláusula `WITH RESULT SETS` será necessária e um esquema de saída deverá ser especificado.  

 + Para scripts R que não usam funções RevoScaleR, o uso do parâmetro `@parallel` pode ser benéfico para o processamento de conjuntos de grandes volumes, supondo que o script possa ser trivialmente paralelizado. Por exemplo, ao usar a função R `predict` com um modelo para gerar novas previsões, defina `@parallel = 1` como uma dica para o mecanismo de consulta. Se a consulta puder ser paralelizada, as linhas serão distribuídas de acordo com a configuração **MAXDOP** .  
  
 + Para scripts R que usam funções RevoScaleR, o processamento paralelo é manipulado automaticamente e você não deve especificar `@parallel = 1` à chamada **sp_execute_external_script** .  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]` uma lista de declarações de parâmetro de entrada que são usadas no script externo.  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]` uma lista de valores para os parâmetros de entrada usados pelo script externo.  

## <a name="remarks"></a>Comentários

> [!IMPORTANT]
> A árvore de consulta é controlada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os usuários não podem executar operações arbitrárias na consulta. 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Use **sp_execute_external_script** para executar scripts escritos em um idioma com suporte. Os idiomas com suporte são **Python** e **R** usados com serviços de Machine Learning, e qualquer linguagem definida com a [criação de linguagem externa](../../t-sql/statements/create-external-language-transact-sql.md) (por exemplo, Java) usada com extensões de linguagem.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Use **sp_execute_external_script** para executar scripts escritos em um idioma com suporte. Os idiomas com suporte são **Python** e **R** no SQL Server 2017 serviços de Machine Learning.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Use **sp_execute_external_script** para executar scripts escritos em um idioma com suporte. O único idioma com suporte é **R** no SQL Server r Services 2016.
::: moniker-end

Por padrão, os conjuntos de resultados retornados por esse procedimento armazenado são gerados com colunas sem nome. Os nomes de coluna usados em um script são locais para o ambiente de script e não são refletidos no conjunto de resultados de saída. Para nomear colunas do conjunto de resultados, use a cláusula `WITH RESULT SET` de [`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md).

Além de retornar um conjunto de resultados, você pode retornar valores escalares para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando parâmetros de saída. 
  
Você pode controlar os recursos usados por scripts externos Configurando um pool de recursos externos. Para obter mais informações, veja [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). As informações sobre a carga de trabalho podem ser obtidas nas exibições do catálogo do administrador de recursos, DMV e contadores. Para obter mais informações, consulte [resource governor exibições &#40;do catálogo&#41;Transact-SQL](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), [resource governor exibições &#40;de gerenciamento&#41;dinâmico relacionadas ao Transact-SQL e ao](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md) [SQL Server, objeto scripts externos](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md).  

### <a name="monitor-script-execution"></a>Monitorar a execução do script

Monitore a execução do script usando [Sys. dm _external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) e [Sys. dm _external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>Parâmetros para modelagem de partição

Você pode definir dois parâmetros adicionais que permitem a modelagem em dados particionados, em que as partições se baseiam em uma ou mais colunas que você fornece para segmentar naturalmente um conjunto de dados em partições lógicas criadas e usadas somente durante a execução do script. As colunas que contêm valores repetidos para idade, gênero, região geográfica, data ou hora são alguns exemplos que se prestam a conjuntos de dados particionados.
 
Os dois parâmetros são **input_data_1_partition_by_columns** e **input_data_1_order_by_columns**, em que o segundo parâmetro é usado para ordenar o conjunto de resultados. Os parâmetros são passados como entradas para `sp_execute_external_script` com o script externo executado uma vez para cada partição. Para obter mais informações e exemplos, consulte [tutorial: criar modelos baseados em partição](https://docs.microsoft.com/sql/advanced-analytics/tutorials/r-tutorial-create-models-per-partition).

Você pode executar o script em paralelo especificando `@parallel=1`. Se a consulta de entrada puder ser paralelizada, você deverá definir `@parallel=1` como parte de seus argumentos para `sp_execute_external_script`. Por padrão, o otimizador de consulta opera em `@parallel=1` em tabelas com mais de 256 linhas, mas se você quiser tratar isso explicitamente, esse script incluirá o parâmetro como uma demonstração.

> [!Tip]
> Para treinar o workoads, você pode usar `@parallel` com qualquer script de treinamento arbitrário, mesmo aqueles que usam algoritmos não Microsoft-RX. Normalmente, somente os algoritmos RevoScaleR (com o prefixo RX) oferecem paralelismo em cenários de treinamento no SQL Server. Mas com os novos parâmetros no SQL Server vNext, você pode paralelizar um script que chama funções não especificamente projetadas com esse recurso.
::: moniker-end

### <a name="streaming-execution-for-python-and-r-scripts"></a>Execução de streaming para scripts do Python e do R  

O streaming permite que o script Python ou R funcione com mais dados do que pode caber na memória. Para controlar o número de linhas passadas durante o streaming, especifique um valor inteiro para o parâmetro, `@r_rowsPerRead` na coleção `@params`.  Por exemplo, se você estiver treinando um modelo que usa dados muito largos, poderá ajustar o valor para ler menos linhas, para garantir que todas as linhas possam ser enviadas em uma parte dos dados. Você também pode usar esse parâmetro para gerenciar o número de linhas que estão sendo lidas e processadas ao mesmo tempo, para reduzir os problemas de desempenho do servidor. 
  
O parâmetro `@r_rowsPerRead` para streaming e o argumento `@parallel` devem ser considerados dicas. Para que a dica seja aplicada, deve ser possível gerar um plano de consulta SQL que inclua processamento paralelo. Se isso não for possível, o processamento paralelo não poderá ser habilitado.  
  
> [!NOTE]  
> Somente há suporte para streaming e processamento paralelo no Enterprise Edition. Você pode incluir os parâmetros em suas consultas na Standard Edition sem gerar um erro, mas os parâmetros não têm nenhum efeito e os scripts do R são executados em um único processo.  
  
## <a name="restrictions"></a>Restrições  

### <a name="data-types"></a>Tipos de dados

Os tipos de dados a seguir não têm suporte quando usados na consulta de entrada ou parâmetros do procedimento **sp_execute_external_script** e retornam um erro de tipo sem suporte.  

Como alternativa, **converta** a coluna ou o valor em um tipo com suporte em [!INCLUDE[tsql](../../includes/tsql-md.md)] antes de enviá-lo para o script externo.  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**, **DateTimeOffset**, **hora**  
  
-   **sql_variant**  
  
-   **texto**, **imagem**  
  
-   **xml**  
  
-   **hierarchyid**, **geometria**, **geografia**  
  
-   Tipos definidos pelo usuário de CLR

Em geral, qualquer conjunto de resultados que não pode ser mapeado para um tipo de dados [!INCLUDE[tsql](../../includes/tsql-md.md)] é a saída como NULL.  

### <a name="restrictions-specific-to-r"></a>Restrições específicas ao R

Se a entrada incluir valores de **data e hora** que não se ajustam ao intervalo de valores permitidos em R, os valores serão convertidos em **na**. Isso é necessário porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite um intervalo maior de valores do que o suportado na linguagem R.

Os valores float (por exemplo, `+Inf`, `-Inf`, `NaN`) não têm suporte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mesmo que os dois idiomas usem o IEEE 754. O comportamento atual apenas envia os valores para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diretamente; Como resultado, o cliente do SQL no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] gera um erro. Portanto, esses valores são convertidos em **NULL**.

## <a name="permissions"></a>Permissões

Requer a permissão executar qualquer banco de dados de **script externo** .  

## <a name="examples"></a>Exemplos

Esta seção contém exemplos de como esse procedimento armazenado pode ser usado para executar scripts R ou Python usando [!INCLUDE[tsql](../../includes/tsql-md.md)].

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. Retornar um conjunto de dados do R para SQL Server  

O exemplo a seguir cria um procedimento armazenado que usa **sp_execute_external_script** para retornar o conjunto de conjuntos de o íris incluído com R para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

```sql
DROP PROC IF EXISTS get_iris_dataset;  
go  
CREATE PROC get_iris_dataset
AS  
BEGIN  
 EXEC   sp_execute_external_script  
       @language = N'R'  
     , @script = N'iris_data <- iris;'
     , @input_data_1 = N''  
     , @output_data_1_name = N'iris_data'
     WITH RESULT SETS (("Sepal.Length" float not null,   
           "Sepal.Width" float not null,  
        "Petal.Length" float not null,   
        "Petal.Width" float not null, "Species" varchar(100)));  
END;
GO
```

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. Gerar um modelo de R com base nos dados de SQL Server  

O exemplo a seguir cria um procedimento armazenado que usa **sp_execute_external_script** para gerar um modelo de íris e retornar o modelo para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

> [!NOTE]
>  Este exemplo requer a instalação antecipada do pacote e1071. Para obter mais informações, consulte [instalar pacotes R adicionais em SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md).

```sql
DROP PROC IF EXISTS generate_iris_model;
GO
CREATE PROC generate_iris_model
AS
BEGIN
 EXEC sp_execute_external_script  
      @language = N'R'  
     , @script = N'  
          library(e1071);  
          irismodel <-naiveBayes(iris_data[,1:4], iris_data[,5]);  
          trained_model <- data.frame(payload = as.raw(serialize(irismodel, connection=NULL)));  
'  
     , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from iris_data'  
     , @input_data_1_name = N'iris_data'  
     , @output_data_1_name = N'trained_model'  
    WITH RESULT SETS ((model varbinary(max)));  
END;
GO
```

Para gerar um modelo semelhante usando Python, altere o identificador de idioma de `@language=N'R'` para `@language = N'Python'`e faça as modificações necessárias para o argumento `@script`. Caso contrário, todos os parâmetros funcionam do mesmo modo que para o R.

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>C. Criar um modelo Python e gerar pontuações a partir dele

Este exemplo ilustra como usar sp\_execute\_external\_script para gerar pontuações em um modelo simples de Python. 

```sql
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

-- Input query to generate the customer data
DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders'

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

# Get data from input query
customer_data = my_input_data

# Define the model
n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

Os títulos de coluna usados no código Python não são gerados para SQL Server; Portanto, use a instrução com RESULT para especificar os nomes de coluna e os tipos de dados para o SQL usar.

Para pontuação, você também pode usar a função nativa [PREDICT](../../t-sql/queries/predict-transact-sql.md), que é normalmente mais rápida porque evita que o runtime do Python ou do R seja chamado.

## <a name="see-also"></a>Consulte também

+ [Serviços de aprendizado de máquina do SQL Server](../../advanced-analytics/index.yml)
+ [Extensões de linguagem SQL Server](../../language-extensions/language-extensions-overview.md). 
+ [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
+ [Bibliotecas e tipos de dados do Python](../../advanced-analytics/python/python-libraries-and-data-types.md)  
+ [Bibliotecas de r e tipos de dados do R](../../advanced-analytics/r/r-libraries-and-data-types.md)  
+ [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)   
+ [Problemas conhecidos de SQL Server Serviços de Machine Learning](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)   
+ [CRIAR Transact- &#40;SQL de biblioteca externa&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [Transact &#40;SQL sp_prepare&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
+ [Opção de Configuração do servidor external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
+ [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
+ [SQL Server, objeto External Scripts](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
