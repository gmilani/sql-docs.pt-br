---
title: Executar Assistente de Migração de Dados da linha de comando
description: Saiba como executar Assistente de Migração de Dados da linha de comando para avaliar SQL Server bancos de dados para migração
ms.custom: seo-lt-2019
ms.date: 05/06/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Command Line
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: 3fbf2429a384ad64b1b416e3920a193d92a6c387
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056622"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>Executar Assistente de Migração de Dados da linha de comando

Com a versão 2,1 e superior, quando você instala o Assistente de Migração de Dados, ele também instalará o dmacmd. exe em *% ProgramFiles%\\Assistente de Migração de Dados da Microsoft\\* . Use dmacmd. exe para avaliar seus bancos de dados em um modo autônomo e gerar o resultado para o arquivo JSON ou CSV. Esse método é especialmente útil ao avaliar vários bancos de dados ou bancos de dados enormes. 

> [!NOTE]
> O Dmacmd. exe dá suporte apenas a avaliações de execução. No momento, não há suporte para migrações.

## <a name="assessments-using-the-command-line-interface-cli"></a>Avaliações usando a CLI (interface de linha de comando)

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentSourcePlatform="SourcePlatform"]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```

|Argumento  |Descrição  | Necessário (s/N)
|---------|---------|---------------|
| `/help or /?`     | Como usar o texto de ajuda do dmacmd. exe        | N
|`/AssessmentName`     |   Nome do projeto de avaliação   | S
|`/AssessmentDatabases`     | Lista delimitada por espaço de cadeias de conexão. O nome do banco de dados (catálogo inicial) diferencia maiúsculas de minúsculas. | S
|`/AssessmentSourcePlatform`     | Plataforma de origem para a avaliação: <br>Valores com suporte para avaliação: SqlOnPrem, RdsSqlServer (padrão) <br>Valores com suporte para avaliação de prontidão de destino: SqlOnPrem, RdsSqlServer (padrão), Cassandra (versão prévia)   | N
|`/AssessmentTargetPlatform`     | Plataforma de destino para a avaliação:  <br> Valores com suporte para avaliação: AzureSqlDatabase, ManagedSqlServer, SqlServer2012, SqlServer2014, SqlServer2016, SqlServerLinux2017 e SqlServerWindows2017 (padrão)  <br> Valores com suporte para avaliação de prontidão de destino: ManagedSqlServer (padrão), CosmosDB (versão prévia)   | N
|`/AssessmentEvaluateFeatureParity`  | Execute regras de paridade de recurso. Se a plataforma de origem for RdsSqlServer, a avaliação de paridade de recurso não terá suporte para a plataforma de destino AzureSqlDatabase  | N
|`/AssessmentEvaluateCompatibilityIssues`     | Executar regras de compatibilidade  | S <br> (É necessário o AssessmentEvaluateCompatibilityIssues ou o AssessmentEvaluateRecommendations.)
|`/AssessmentEvaluateRecommendations`     | Executar recomendações de recursos        | S <br> (É necessário o AssessmentEvaluateCompatibilityIssues ou o AssessmentEvaluateRecommendations)
|`/AssessmentOverwriteResult`     | Substituir o arquivo de resultado    | N
|`/AssessmentResultJson`     | Caminho completo para o arquivo de resultado JSON     | S <br> (É necessário o AssessmentResultJson ou o AssessmentResultCsv)
|`/AssessmentResultCsv`    | Caminho completo para o arquivo de resultado CSV   | S <br> (É necessário o AssessmentResultJson ou o AssessmentResultCsv)
|`/Action`    | Use SkuRecommendation para obter recomendações de SKU, use AssessTargetReadiness para executar a avaliação de prontidão de destino.   | N
|`/SourceConnections`    | Lista delimitada por espaço de cadeias de conexão. O nome do banco de dados (catálogo inicial) é opcional. Se nenhum nome de banco de dados for fornecido, todos os bancos de dados na origem serão avaliados.   | S <br> (Obrigatório se action for ' AssessTargetReadiness ')
|`/TargetReadinessConfiguration`    | Caminho completo para o arquivo XML que descreve os valores para o nome, as conexões de origem e o arquivo de resultado.   | S <br> (É necessário o TargetReadinessConfiguration ou o SourceConnections)
|`/FeatureDiscoveryReportJson`    | Caminho para o relatório JSON do recurso de descoberta. Se esse arquivo for gerado, ele poderá ser usado para executar a avaliação de prontidão de destino novamente sem se conectar à origem. | N
|`/ImportFeatureDiscoveryReportJson`    | Caminho para o relatório JSON do recurso de descoberta criado anteriormente. Em vez de conexões de origem, esse arquivo será usado.   | N

## <a name="examples-of-assessments-using-the-cli"></a>Exemplos de avaliações usando a CLI

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Avaliação de banco de dados único usando autenticação do Windows e regras de compatibilidade em execução**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```

**Avaliação de banco de dados único usando a autenticação de SQL Server e a execução de recomendação de recurso**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;User Id=myUsername;Password=myPassword;"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**Avaliação de banco de dados único para plataforma de destino SQL Server 2012, salvar resultados em arquivo. JSON e. csv**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2012"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**Avaliação de banco de dados único para plataforma de destino SQL Azure banco de dados, salvar resultados em arquivos. JSON e. csv**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="AzureSqlDatabaseV12"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"
```

**Avaliação de vários bancos de dados**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName1;Initial
Catalog=DatabaseName1;Integrated Security=true"
"Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated
Security=true" "Server=SQLServerInstanceName2;Initial
Catalog=DatabaseName3;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2016"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
/AssessmentResultJson="C:\\Results\\test2016.json"
```

**Avaliação de prontidão de destino de banco de dados único usando a autenticação do Windows**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;Integrated Security=true" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"
```

**Avaliação de prontidão de destino de banco de dados único usando a autenticação SQL Server**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;User Id=myUsername;Password=myPassword;" /AssessmentEvaluateRecommendations 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json" 

```

**Avaliação de banco de dados único para plataforma de destino SQL Azure banco de dados, salvar resultados em arquivos. JSON e. csv**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentSourcePlatform="SqlOnPrem"
/AssessmentTargetPlatform="AzureSqlDatabase"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"

```

**Avaliação de prontidão de destino de vários bancos de dados**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/AssessmentSourcePlatform=SourcePlatform
/AssessmentTargetPlatform=TargetPlatform
/SourceConnections="Server=SQLServerInstanceName1;Initial Catalog=DatabaseName1;Integrated Security=true" "Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated Security=true" "Server=SQLServerInstanceName2;Initial Catalog=DatabaseName3;Integrated Security=true"
/AssessmentOverwriteResult  
/AssessmentResultJson="C:\Results\test2016.json"

(/AssessmentSourcePlatform and /AssessmentTargetPlatform are optional.)
```

**Avaliação de preparação de destino para todos os bancos de dados em um servidor usando a autenticação do Windows**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/SourceConnections="Server=SQLServerInstanceName;Integrated Security=true"
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**Avaliação de preparação de destino importando relatório de descoberta de recursos criado anteriormente**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/ImportFeatureDiscoveryReportJson="c:\temp\feature_report.json" 
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**Avaliação de preparação de destino ao fornecer o arquivo de configuração**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/TargetReadinessConfiguration=.\Config.xml
```

Conteúdo do arquivo de configuração ao usar conexões de origem:

```
<?xml version="1.0" encoding="utf-8" ?>
<TargetReadinessConfiguration xmlns="https://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <SourcePlatform>Source Platform</SourcePlatform> <!-- Optional. The default is SqlOnPrem -->
  <TargetPlatform>TargetPlatform</TargetPlatform> <!-- Optional. The default is ManagedSqlServer -->
  <SourceConnections>
    <SourceConnection>connection string 1</SourceConnection>
    <SourceConnection>connection string 2</SourceConnection>
    <!-- ... -->
    <SourceConnection>connection string n</SourceConnection>
  </SourceConnections>
  <AssessmentResultJson>path\to\file.json</AssessmentResultJson>
  <FeatureDiscoveryReportJson>path\to\featurediscoveryreport.json</FeatureDiscoveryReportJson>
  <OverwriteResult>true</OverwriteResult> <!-- or false -->
</TargetReadinessConfiguration>
```

Conteúdo do arquivo de configuração ao importar o relatório de descoberta de recursos:

```
<TargetReadinessConfiguration xmlns="https://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <ImportFeatureDiscoveryReportJson>path\to\featurediscoveryfile.json</ImportFeatureDiscoveryReportJson>
  <AssessmentResultJson>path\to\resultfile.json</AssessmentResultJson>
  <OverwriteResult>true</OverwriteResult><!-- or false -->
</TargetReadinessConfiguration>
```

## <a name="azure-sql-databasemanaged-instance-sku-recommendations-using-the-cli"></a>Recomendações de SKU da instância gerenciada/banco de dados SQL do Azure usando a CLI

Esses comandos dão suporte a recomendações para o banco de dados SQL do Azure e opções de implantação de instância gerenciada.

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true 
```

|Argumento  |Descrição  | Necessário (s/N)
|---------|---------|---------------|
|`/Action=SkuRecommendation` | Executar avaliação de SKU usando linha de comando DMA | S
|`/SkuRecommendationInputDataFilePath` | Caminho completo do arquivo do contador de desempenho coletado do computador que hospeda seus bancos de dados | S
|`/SkuRecommendationTsvOutputResultsFilePath` | Caminho completo para o arquivo de resultado TSV | S <br> (Requer o caminho do arquivo TSV ou JSON ou HTML)
|`/SkuRecommendationJsonOutputResultsFilePath` | Caminho completo para o arquivo de resultado JSON | S <br> (Requer o caminho do arquivo TSV ou JSON ou HTML)
|`/SkuRecommendationHtmlResultsFilePath` | Caminho completo para o arquivo de resultado HTML | S <br> (Requer o caminho do arquivo TSV ou JSON ou HTML)
|`/SkuRecommendationPreventPriceRefresh` | Impede que a atualização de preço ocorra. Use se estiver executando no modo offline (por exemplo, true). | S <br> (Selecione este argumento para preços estáticos ou todos os argumentos abaixo precisam ser selecionados para obter os preços mais recentes)
|`/SkuRecommendationCurrencyCode` | A moeda na qual os preços são exibidos (por exemplo, "USD") | S <br> (Para obter os preços mais recentes)
|`/SkuRecommendationOfferName` | O nome da oferta (por exemplo, "MS-AZR-0003P"). Para obter mais informações, consulte a página [detalhes da oferta de Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) . | S <br> (Para obter os preços mais recentes)
|`/SkuRecommendationRegionName` | O nome da região (por exemplo, "Westus") | S <br> (Para obter os preços mais recentes)
|`/SkuRecommendationSubscriptionId` | A ID da assinatura. | S <br> (Para obter os preços mais recentes)
|`/SkuRecommendationDatabasesToRecommend` | Lista de bancos de dados separados por espaços para recomendar (por exemplo, "Database1" "Database2" "Database3"). Os nomes diferenciam maiúsculas de minúsculas e devem estar entre aspas duplas. Se omitido, serão fornecidas recomendações para todos os bancos de dados. | N
|`/AzureAuthenticationTenantId` | O locatário de autenticação. | S <br> (Para obter os preços mais recentes)
|`/AzureAuthenticationClientId` | A ID do cliente do aplicativo AAD usado para autenticação. | S <br> (Para obter os preços mais recentes)
|`/AzureAuthenticationInteractiveAuthentication` | Defina como true para exibir a janela. | S <br> (Para obter os preços mais recentes) <br>(Escolha uma das 3 opções de autenticação-opção 1)
|`/AzureAuthenticationCertificateStoreLocation` | Defina como o local do repositório de certificados (por exemplo, "CurrentUser"). | S <br>(Para obter os preços mais recentes) <br> (Escolha uma das 3 opções de autenticação-opção 2)
|`/AzureAuthenticationCertificateThumbprint` | Defina como a impressão digital do certificado. | S <br> (Para obter os preços mais recentes) <br>(Escolha uma das 3 opções de autenticação-opção 2)
|`/AzureAuthenticationToken` | Defina como o token de certificado. | S <br> (Para obter os preços mais recentes) <br>(Escolha uma das 3 opções de autenticação-opção 3)

## <a name="examples-of-sku-assessments-using-the-cli"></a>Exemplos de avaliações de SKU usando a CLI

**Dmacmd.exe**

`Dmacmd.exe /? or DmaCmd.exe /help`

**Banco de BD SQL do Azure/recomendação de SKU de MI com atualização de preço (obter preços mais recentes)-autenticação interativa** 

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationInteractiveAuthentication=true 
```

**Banco de BD SQL do Azure/recomendação de SKU de MI com atualização de preço (obter preços mais recentes)-autenticação de certificado**

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationCertificateStoreLocation=<Your Certificate Store Location>
/AzureAuthenticationCertificateThumbprint=<Your Certificate Thumbprint>  
```

**Recomendação do BD SQL do Azure/MI com atualização de preço (obter preços mais recentes) – autenticação de token e especificar bancos de dados para recomendar**
  
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationDatabasesToRecommend=“TPCDS1G,EDW_3G,TPCDS10G”
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationToken=<Your Authentication Token> 
```

**Banco de BD SQL do Azure/recomendação de SKU de MI sem atualização de preço (usar preços estáticos)** 
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true  
```

## <a name="see-also"></a>Confira também
- Download de [Assistente de migração de dados](https://aka.ms/get-dma) .
- O artigo [identifica o SKU do banco de dados SQL do Azure correto para seu banco de dados local](https://aka.ms/dma-sku-recommend-sqldb).
