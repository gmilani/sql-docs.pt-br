---
title: Executar uma instrução diretamente (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statement execution
ms.assetid: b690f9de-66e1-4ee5-ab6a-121346fb5f85
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a5ece0a8b0e0844e8c33779796b0217ebf744050
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73781418"
---
# <a name="execute-a-statement-directly-odbc"></a>Executar diretamente uma instrução (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-execute-a-statement-directly-and-one-time-only"></a>Para executar uma instrução diretamente e apenas uma vez  
  
1.  Se a instrução tiver marcadores de parâmetro, use [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md) para associar cada parâmetro a uma variável de programa. Preencha as variáveis de programa com valores de dados e configure todos os parâmetros de dados em execução.  
  
2.  Chame [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) para executar a instrução.  
  
3.  Se forem usados parâmetros de entrada de dados em execução, [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) retornará SQL_NEED_DATA. Envie os dados em partes usando [SQLParamData](https://go.microsoft.com/fwlink/?LinkId=58405) e [SQLPutData](../../../relational-databases/native-client-odbc-api/sqlputdata.md).  

### <a name="to-execute-a-statement-multiple-times-by-using-column-wise-parameter-binding"></a>Para executar uma instrução várias vezes usando a associação de parâmetros por coluna  
  
1.  Chame [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para definir os seguintes atributos:  
  
     Defina SQL_ATTR_PARAMSET_SIZE como o número de conjuntos (S) de parâmetros.  
  
     Defina SQL_ATTR_PARAM_BIND_TYPE como SQL_PARAMETER_BIND_BY_COLUMN.  
  
     Defina o atributo SQL_ATTR_PARAMS_PROCESSED_PTR de forma que aponte para uma variável SQLUINTEGER que contém o número de parâmetros processados.  
  
     Defina SQL_ATTR_PARAMS_STATUS_PTR de forma que aponte para uma matriz[S] de variáveis SQLUSSMALLINT que contém os indicadores de status de parâmetro.  
  
2.  Para cada marcador de parâmetro:  
  
     Aloque uma matriz de S buffers de parâmetro para armazenar valores de dados.  
  
     Aloque uma matriz de S buffers de parâmetro para armazenar comprimentos de dados.  
  
     Chame [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md) para associar as matrizes de comprimento de dados e de valor de dados de parâmetro ao parâmetro de instrução.  
  
     Configure quaisquer parâmetros de imagem ou texto de dados em execução.  
  
     Coloque os valores de dados S e os comprimentos de dados S nas matrizes de parâmetro associadas.  
  
3.  Chame [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) para executar a instrução. O driver executa a instrução de maneira eficiente S vezes, sendo uma para cada conjunto de parâmetros.  
  
4.  Se forem usados parâmetros de entrada de dados em execução, [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) retornará SQL_NEED_DATA. Envie os dados em partes usando [SQLParamData](https://go.microsoft.com/fwlink/?LinkId=58405) e [SQLPutData](../../../relational-databases/native-client-odbc-api/sqlputdata.md).  
  
### <a name="to-execute-a-statement-multiple-times-by-using-row-wise-parameter-binding"></a>Para executar uma instrução várias vezes usando a associação de parâmetros por linha  
  
1.  Aloque uma matriz[S] de estruturas, onde S é o número de conjuntos de parâmetros. A estrutura tem um elemento para cada parâmetro e cada elemento tem duas partes:  
  
     A primeira parte é uma variável do tipo de dados apropriado que contém os dados de parâmetro.  
  
     A segunda parte é uma variável SQLINTEGER que contém o indicador de status.  
  
2.  Chame [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para definir os seguintes atributos:  
  
     Defina SQL_ATTR_PARAMSET_SIZE como o número de conjuntos (S) de parâmetros.  
  
     Defina SQL_ATTR_PARAM_BIND_TYPE como o tamanho da estrutura alocada na Etapa 1.  
  
     Defina o atributo SQL_ATTR_PARAMS_PROCESSED_PTR de forma que aponte para uma variável SQLUINTEGER que contém o número de parâmetros processados.  
  
     Defina SQL_ATTR_PARAMS_STATUS_PTR de forma que aponte para uma matriz[S] de variáveis SQLUSSMALLINT que contém os indicadores de status de parâmetro.  
  
3.  Para cada marcador de parâmetro, chame [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md) para direcionar o ponteiro de comprimento de dados e de valor de dados do parâmetro para suas variáveis no primeiro elemento da matriz de estruturas alocadas na Etapa 1. Se o parâmetro for um parâmetro de dados em execução, configure-o.  
  
4.  Preencha a matriz de buffers de parâmetros associada com valores de dados.  
  
5.  Chame [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) para executar a instrução. O driver executa a instrução de maneira eficiente S vezes, sendo uma para cada conjunto de parâmetros.  
  
6.  Se forem usados parâmetros de entrada de dados em execução, [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) retornará SQL_NEED_DATA. Envie os dados em partes usando [SQLParamData](https://go.microsoft.com/fwlink/?LinkId=58405) e [SQLPutData](../../../relational-databases/native-client-odbc-api/sqlputdata.md).  
  
 **Observação** As associações por coluna e por linha geralmente são mais usadas em conjunto com [SQLPrepare Function](https://go.microsoft.com/fwlink/?LinkId=59360) e [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400) do que com [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399).  
  
## <a name="see-also"></a>Consulte também  
 [Tópicos &#40;de instruções sobre como executar consultas ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  
