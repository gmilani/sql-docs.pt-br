---
title: CREATE WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD GROUP
- WORKLOAD_GROUP_TSQL
- CREATE WORKLOAD GROUP
- CREATE_WORKLOAD_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD GROUP statement
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: 50c5edee93747c98060d664f1edd2d42036aa9b2
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982659"
---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP (Transact-SQL)

## <a name="click-a-product"></a>Clique em um produto!

Na linha a seguir, clique em qualquer nome de produto de seu interesse. O clique exibe conteúdo diferente aqui nesta página da Web, apropriado para qualquer produto no qual você clicar.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||||
> |---|---|---|---|
> |**\* _SQL Server \*_** &nbsp;|[Instância gerenciada<br />do Banco de Dados SQL](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](create-workload-group-transact-sql.md?view=azure-sqldw-latest)|

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>Instância gerenciada do SQL Server e do Banco de Dados SQL

Cria um grupo de carga de trabalho do Administrador de recursos e o associa a um pool de recursos do Administrador de recursos. O Resource Governor não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintaxe

```
CREATE WORKLOAD GROUP group_name
[ WITH
    ( [ IMPORTANCE = { LOW | MEDIUM | HIGH } ]
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]
      [ [ , ] MAX_DOP = value ]
      [ [ , ] GROUP_MAX_REQUESTS = value ] )
 ]
[ USING {
    [ pool_name | "default" ]
    [ [ , ] EXTERNAL external_pool_name | "default" ] ]
    } ]
[ ; ]
```

## <a name="arguments"></a>Argumentos

*group_name*     
É o nome definido pelo usuário do grupo de carga de trabalho. *group_name* é alfanumérico, pode ter até 128 caracteres, precisa ser exclusivo em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e precisa estar em conformidade com as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).

IMPORTANCE = { LOW | **MEDIUM** | HIGH }     
Especifica a importância relativa de uma solicitação no grupo de carga de trabalho. A importância é uma das seguintes, com MEDIUM sendo o padrão:

- LOW
- MEDIUM (padrão)
- HIGH

> [!NOTE]
> Internamente, cada configuração de importância é armazenada como um número usado para cálculos.

IMPORTANCE é local para o pool de recursos; grupos de cargas de trabalho de importâncias diferentes no mesmo pool de recursos afetam uns aos outros, mas não afetam grupos de cargas de trabalho em outro pool de recursos.

REQUEST_MAX_MEMORY_GRANT_PERCENT = *value*     
Especifica o máximo de memória que uma única solicitação pode usar do pool. *valor* é um percentual relativo ao tamanho do pool de recursos especificado por MAX_MEMORY_PERCENT. 

*value* é um inteiro até [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e um flutuante que começa com [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]. O valor padrão é 25. O intervalo permitido para *value* é de 1 a 100.

> [!NOTE]  
> A quantidade especificada se refere apenas à memória de concessão de execução da consulta.  
  
> [!IMPORTANT]
> A configuração de *value* como 0 impede a execução de consultas com as operações SORT e HASH JOIN em grupos de cargas de trabalho definidos pelo usuário.     
>
> Não é recomendável definir *value* com um valor maior que 70, pois o servidor poderá não conseguir separar memória livre suficiente se outras consultas simultâneas estiverem sendo executadas. Isso pode eventualmente levar ao erro 8645, tempo limite da consulta excedido.      
  
> [!NOTE]  
> Se os requisitos de memória de consulta excederem o limite especificado por esse parâmetro, o servidor fará o seguinte:  
>   
> -  Para grupos de cargas de trabalho definidos pelo usuário, o servidor tenta reduzir o grau de paralelismo da consulta, até que o requisito de memória caia abaixo do limite, ou até que o grau de paralelismo seja igual a 1. Se o requisito de memória de consulta ainda for maior que o limite, ocorrerá o erro 8657.  
>   
> -  Para grupos de cargas de trabalho internos e padrão, o servidor permite que a consulta obtenha a memória necessária.  
>   
> Esteja ciente de que ambos os casos estarão sujeitos ao erro de tempo limite 8645 se a memória física do servidor for insuficiente.  

REQUEST_MAX_CPU_TIME_SEC = *value*     
Especifica o tempo máximo de CPU, em segundos, que uma solicitação pode usar. *value* precisa ser 0 ou um inteiro positivo. A configuração padrão de *value* é 0, o que significa ilimitado.

> [!NOTE]
> Por padrão, o Resource Governor não impedirá a continuação de uma solicitação se o tempo máximo for excedido. Porém, um evento será gerado. Para obter mais informações, consulte [Classe de evento CPU Threshold Exceeded](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md).     

> [!IMPORTANT]
> Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 e usando o [sinalizador de rastreamento 2422](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md), o Resource Governor anulará uma solicitação quando o tempo máximo for excedido.

REQUEST_MEMORY_GRANT_TIMEOUT_SEC = *value*     
Especifica o tempo máximo, em segundos, que uma consulta pode esperar pela disponibilização de uma concessão de memória (memória do buffer do trabalho). *value* precisa ser 0 ou um inteiro positivo. A configuração padrão de *value*, 0, usa um cálculo interno baseado no custo da consulta para determinar o tempo máximo.

> [!NOTE]
> Nem sempre uma consulta falha quando o tempo limite de concessão de memória é atingido. A consulta falhará somente se houver muitas consultas simultâneas em execução. Caso contrário, a consulta poderá obter apenas a concessão de memória mínima, resultando em uma queda no desempenho de consulta.

MAX_DOP = *value*     
Especifica o **grau máximo de paralelismo (MAXDOP)** para execução de consulta paralela. *value* precisa ser 0 ou um inteiro positivo. O intervalo permitido para *value* é de 0 a 64. A configuração padrão para *value*, 0, usa a configuração global. MAX_DOP é tratado como segue:

> [!NOTE]
> O grupo de cargas de trabalho do MAX_DOP substitui a [configuração de servidor para o grau máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) e a [configuração no escopo do banco de dados](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) do **MAXDOP**.

> [!TIP]
> Para fazer isso no nível da consulta, use a [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md) do **MAXDOP**. Definir o grau máximo de paralelismo como uma dica de consulta funciona, desde que não exceda o grupo de carga de trabalho do MAX_DOP. Se o valor de dica de consulta do MAXDOP ultrapassar o valor configurado no Resource Governor, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usará o valor `MAX_DOP` do Resource Governor. A [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md) do MAXDOP sempre substitui a [configuração de servidor para o grau máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).      
>   
> Para fazer isso no nível do banco de dados, use a [configuração com escopo no banco de dados](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) do **MAXDOP**.      
>   
> Para fazer isso no nível do servidor, use o **MAXDOP (grau máximo de paralelismo)** na [opção de configuração do servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).     

GROUP_MAX_REQUESTS = *value*     
Especifica o número máximo de solicitações simultâneas permitido para execução no grupo de carga de trabalho. *value* precisa ser 0 ou um inteiro positivo. A configuração padrão de *valor* é 0 e permite solicitações ilimitadas. Quando as solicitações simultâneas máximas são alcançadas, um usuário nesse grupo pode fazer logon, mas é colocado em um estado de espera até que as solicitações simultâneas sejam ignoradas abaixo do valor especificado.

USING { *pool_name* |  **"default"** }     
Associa o grupo de carga de trabalho ao pool de recursos definido pelo usuário, identificado por *pool_name*. Na realidade, isso coloca o grupo de carga de trabalho no pool de recursos. Se *pool_name* não for fornecido ou se o argumento USING não for usado, o grupo de carga de trabalho será colocado no pool padrão predefinido do Resource Governor.

"default" é uma palavra reservada e, quando usada com USING, deve ficar entre aspas ("") ou colchetes ([]).

> [!NOTE]
> Grupos de cargas de trabalho e pools de recursos predefinidos usam nomes em letras minúsculas, como "default". Isso deve ser levado em consideração nos servidores que usam ordenação com diferenciação de maiúsculas e minúsculas. Os servidores com ordenação sem diferenciação de maiúsculas e minúsculas, como SQL_Latin1_General_CP1_CI_AS, tratarão "default" e "Default" da mesma maneira.

EXTERNAL external_pool_name | "padrão"     
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior).

O grupo de carga de trabalho pode especificar um pool de recursos externo. Você pode definir um grupo de carga de trabalho e associá-lo a dois pools:

- Um pool de recursos para cargas de trabalho e consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
- Um pool de recursos externo para processos externos. Para obter mais informações, confira [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

## <a name="remarks"></a>Remarks
Quando `REQUEST_MEMORY_GRANT_PERCENT` é usado, a criação de índice tem permissão para usar mais memória do workspace do que a concedida inicialmente, para melhorar o desempenho. Esse tratamento especial tem o suporte do Administrador de Recursos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Porém, a concessão inicial e qualquer concessão de memória adicional estão limitadas pelas configurações de pool de recursos e de grupo de carga de trabalho.

O limite de `MAX_DOP` é definido por [tarefa](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md). Não é um limite por [solicitação](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) ou por consulta. Isso significa que, durante uma execução de consulta paralela, uma solicitação única pode gerar várias tarefas que são atribuídas a um [agendador](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md). Para saber mais, confira o [Guia de arquitetura de threads e tarefas](../../relational-databases/thread-and-task-architecture-guide.md).

Quando `MAX_DOP` for usado e uma consulta for marcada como serial em tempo de compilação, ela não poderá ser revertida a paralela em tempo de execução, independentemente do grupo de carga de trabalho ou da definição de configuração do servidor. Depois de configurar o `MAX_DOP`, ele só poderá ser reduzido devido à pressão de memória. A reconfiguração do grupo de carga de trabalho não é visível durante a espera na fila de concessão de memória.

### <a name="index-creation-on-a-partitioned-table"></a>Criação de índice em uma tabela particionada

A memória consumida pela criação de índice na tabela particionada não alinhada é proporcional ao número de partições envolvidas. Se a memória total necessária exceder o limite por consulta `REQUEST_MAX_MEMORY_GRANT_PERCENT` imposto pela configuração de grupo de cargas de trabalho do Resource Governor, poderá ocorrer uma falha na criação do índice. Como o grupo de carga de trabalho *"padrão"* permite que uma consulta exceda o limite por consulta com o mínimo de memória necessária, o usuário talvez possa executar a mesma criação de índice no grupo de carga de trabalho *"padrão"* caso o pool de recursos *"padrão"* tenha memória total suficiente configurada para executar tal consulta.

## <a name="permissions"></a>Permissões
Requer a permissão `CONTROL SERVER`.

## <a name="example"></a>Exemplo

Crie um grupo de carga de trabalho chamado `newReports`, que usa as configurações padrão do Resource Governor e está no pool padrão desse Resource Governor. O exemplo especifica o pool `default`, mas isso não é necessário.

```sql
CREATE WORKLOAD GROUP newReports
    USING "default" ;
GO
```

## <a name="see-also"></a>Consulte Também

- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)
- [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](create-workload-group-transact-sql.md?view=sql-server-2017)||[Instância gerenciada<br />do Banco de Dados SQL](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)||**_\* SQL Data<br />Warehouse \*_** &nbsp;||||

&nbsp;

## <a name="sql-data-warehouse"></a>SQL Data Warehouse 

CREATE WORKLOAD GROUP (Transact-SQL) (versão prévia) cria um grupo de carga de trabalho.  Grupos de carga de trabalho são contêineres para um conjunto de solicitações e são a base de como o gerenciamento de cargas de trabalho é configurado em um sistema.  Os grupos de cargas de trabalho fornecem a capacidade de reservar recursos para ter isolamento da cargas de trabalho, conter recursos, definir recursos por solicitação e aderir às regras de execução.  Quando a instrução for concluída, as configurações estarão em vigor.

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md). 

```
CREATE WORKLOAD GROUP group_name  
 WITH  
 (        MIN_PERCENTAGE_RESOURCE = value  
      ,   CAP_PERCENTAGE_RESOURCE = value 
      ,   REQUEST_MIN_RESOURCE_GRANT_PERCENT = value   
  [ [ , ] REQUEST_MAX_RESOURCE_GRANT_PERCENT = value ]  
  [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }]
  [ [ , ] QUERY_EXECUTION_TIMEOUT_SEC = value ] )  
  [ ; ]
```

*group_name*</br>
Especifica o nome pelo qual o grupo de carga de trabalho é identificado.  group_name é um sysname.  Ele pode ter até 128 caracteres e deve ser exclusivo dentro da instância.

*MIN_PERCENTAGE_RESOURCE* = value</br>
Especifica uma alocação de recurso mínima garantida para este grupo de carga de trabalho, que não é compartilhada com outros grupos de carga de trabalho.  value é um intervalo de inteiros de 0 a 100.  A soma de min_percentage_resource em todos os grupos de carga de trabalho não pode exceder 100.  O valor de min_percentage_resource não pode ser maior que cap_percentage_resource.  Há valores mínimos efetivos permitidos por nível de serviço.  Confira Valores Efetivos<link> para obter mais detalhes.

*CAP_PERCENTAGE_RESOURCE* = value</br>
Especifica a utilização de recursos máxima para todas as solicitações em um grupo de carga de trabalho.  O intervalo permitido para o valor é de 1 a 100.  O valor de cap_percentage_resource precisa ser maior que min_percentage_resource.  O valor efetivo para cap_percentage_resource pode ser reduzido se min_percentage_resource estiver configurado como maior que zero em outros grupos de carga de trabalho.

*REQUEST_MIN_RESOURCE_GRANT_PERCENT* = value</br>
Define a quantidade mínima de recursos alocados por solicitação.  value é um parâmetro obrigatório com um intervalo decimal entre 0,75 e 100,00.  O valor de request_min_resource_grant_percent deve ser múltiplo de 0,25, deve ser um fator de min_percentage_resource e ser menor que cap_percentage_resource.  Há valores mínimos efetivos permitidos por nível de serviço.  Confira Valores Efetivos<link> para obter mais detalhes.

Por exemplo:

```sql
CREATE WORKLOAD GROUP wgSample WITH  
( MIN_PERCENTAGE_RESOURCE = 26              -- integer value
 ,REQUEST_MIN_RESOURCE_GRANT_PERCENT = 3.25 -- factor of 26 (guaranteed a minimum of 8 concurrency)
 ,CAP_PERCENTAGE_RESOURCE = 100 )
```

considere os valores que são usados para as classes de recurso como uma diretriz para request_min_resource_grant_percent.  A tabela a seguir contém alocações de recursos para Gen2.

|Classe de recurso|Porcentagem de recursos|
|---|---|
|Smallrc|3%|
|Mediumrc|10%|
|Largerc|22%|
|Xlargerc|70%|
|||

*REQUEST_MAX_RESOURCE_GRANT_PERCENT* = value</br>
Define a quantidade máxima de recursos alocados por solicitação.  value é um parâmetro opcional com um valor padrão igual ao request_min_resource_grant_percent.  value deve ser maior ou igual a request_min_resource_grant_percent.  Quando o valor de request_max_resource_grant_percent é maior que request_min_resource_grant_percent e os recursos do sistema estão disponíveis, recursos adicionais são alocados a uma solicitação.

*IMPORTANCE* = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }</br>
Especifica a importância padrão de uma solicitação no grupo de carga de trabalho.  A importância é uma das seguintes, com NORMAL sendo o padrão:
- LOW
- BELOW_NORMAL
- NORMAL (padrão)
- ABOVE_NORMAL
- HIGH  

A importância definida no grupo de carga de trabalho é uma importância padrão para todas as solicitações no grupo de carga de trabalho.  Um usuário também pode definir a importância no nível do classificador, que pode substituir a configuração de importância do grupo de carga de trabalho.  Isso permite diferenciar a importância das solicitações em um grupo de carga de trabalho para ter acesso a recursos não reservados mais rapidamente.  Quando a soma de min_percentage_resource entre grupos de carga de trabalho é menor que 100, há recursos não reservados que são atribuídos em uma base de importância.

*QUERY_EXECUTION_TIMEOUT_SEC* = value</br>
Especifica o tempo máximo, em segundos, que uma consulta pode ser executada antes de ser cancelada.  value precisa ser 0 ou um inteiro positivo.  A configuração padrão de value é 0, o que significa ilimitado.  O tempo gasto aguardando na fila de solicitações não é contado na execução da consulta.

## <a name="remarks"></a>Remarks
Os grupos de carga de trabalho correspondentes às classes de recursos são criados automaticamente para ter compatibilidade com versões anteriores.  Esses grupos de carga de trabalho definidos pelo sistema não podem ser descartados.  Oito grupos de carga de trabalho adicionais definidos pelo usuário podem ser criados.

## <a name="effective-values"></a>Valores efetivos

Os parâmetros min_percentage_resource, cap_percentage_resource, request_min_resource_grant_percent e request_max_resource_grant_percent têm valores efetivos que são ajustados no contexto do nível de serviço atual e da configuração de outros grupos de carga de trabalho.

A simultaneidade com suporte por nível de serviço permanece a mesma de quando as classes de recurso foram usadas para definir as concessões de recursos por consulta, portanto, os valores com suporte para request_min_resource_grant_percent dependem do nível de serviço para o qual a instância está definida.  No nível de serviço mais baixo, DW100c, há suporte para simultaneidade de quatro.  O request_min_resource_grant_percent efetivo de um grupo de carga de trabalho configurado pode ser de 25% ou mais.  Confira a tabela a seguir para obter mais detalhes.

|Nível de serviço|Máximo de consultas simultâneas|Percentual mínimo com suporte para REQUEST_MIN_RESOURCE_GRANT_PERCENT e MIN_PERCENTAGE_RESOURCE|
|---|---|---|
|DW100c|4|25%|
|DW200c|8|12,5%|
|DW300c|12|8%|
|DW400c|16|6,25%|
|DW500c|20|5%|
|DW1000c|32|3%|
|DW1500c|32|3%|
|DW2000c|48|2%|
|DW2500c|48|2%|
|DW3000c|64|1,5%|
|DW5000c|64|1,5%|
|DW6000c|128|0,75%|
|DW7500c|128|0,75%|
|DW10000c|128|0,75%|
|DW15000c|128|0,75%|
|DW30000c|128|0,75%|
||||

De forma semelhante, request_min_resource_grant_percent min_percentage_resource deve ser maior ou igual ao request_min_resource_grant_percent efetivo.  Um grupo de carga de trabalho com um min_percentage_resource configurado que seja menor do que o min_percentage_resource efetivo tem o valor ajustado para zero em tempo de execução.  Quando isso acontece, os recursos configurados para min_percentage_resource podem ser compartilhados entre todos os grupos de carga de trabalho.  Por exemplo, o grupo de carga de trabalho wgAdHoc com um min_percentage_resource de 10% em execução em DW1000c teria um min_percentage_resource efetivo de 10% (3,25% é o valor mínimo com suporte em DW1000c).  wgAdhoc em DW100c teria um min_percentage_resource efetivo de 0%.  Os 10% configurados para wgAdhoc seriam compartilhados entre todos os grupos de carga de trabalho.

Cap_percentage_resource também tem um valor efetivo.  Se um grupo de carga de trabalho wgAdhoc estiver configurado com um cap_percentage_resource de 100% e outro grupo de carga de trabalho wgDashboards for criado com 25% min_percentage_resource, a cap_percentage_resource efetiva para wgAdhoc se tornará 75%.

A maneira mais fácil de entender os valores de tempo de execução para seus grupos de carga de trabalho é consultar o modo de exibição do sistema [sys.dm_workload_management_workload_groups_stats] (../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md?view=azure-sqldw-latest).

## <a name="permissions"></a>Permissões

Requer a permissão CONTROL DATABASE

## <a name="see-also"></a>Confira também
[DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](drop-workload-group-transact-sql.md)

::: moniker-end
