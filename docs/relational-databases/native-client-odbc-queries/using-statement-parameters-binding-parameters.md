---
title: Parâmetros de associação | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, parameters
- parameters [SQL Server Native Client], ODBC
- statements [ODBC], parameters
- binding parameters [SQL Server Native Client]
- parameter markers [ODBC]
- unbound parameter markers
- SQLBindParameter function
- ODBC applications, parameters
- bound parameter markers [SQL Server Native Client]
ms.assetid: d6c69739-8f89-475f-a60a-b2f6c06576e2
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 340a3a0f44201c81eafe8717962b2894709eb65d
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779528"
---
# <a name="using-statement-parameters---binding-parameters"></a>Usar parâmetros de instrução – Parâmetros de associação
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para que a instrução possa ser executada, cada marcador de parâmetro em uma instrução SQL deve ser associado a uma variável no aplicativo. Isso é feito chamando a função [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) . **SQLBindParameter** descreve a variável do programa (endereço, tipo de dados C e assim por diante) para o driver. Ela também identifica o marcador de parâmetro indicando seu valor ordinal e, em seguida, descreve as características do objeto SQL que representa (tipo de dados SQL, precisão e assim por diante).  
  
 Marcadores de parâmetro podem ser associados ou reassociados a qualquer momento, antes de uma instrução ser executada. Uma associação de parâmetro permanece em vigor até ocorrer um dos seguintes eventos:  
  
-   Uma chamada para [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) com o parâmetro *Option* definido como SQL_RESET_PARAMS libera todos os parâmetros associados ao identificador da instrução.  
  
-   Uma chamada para **SQLBindParameter** com *ParameterNumber* definida como o ordinal de um marcador de parâmetro associado libera automaticamente a Associação anterior.  
  
 Um aplicativo também pode associar parâmetros a matrizes de variáveis de programa para processar uma instrução SQL em lotes. Há dois tipos de associação de matriz:  
  
-   A associação em colunas é feita quando cada um dos parâmetros é associado à sua própria matriz de variáveis.  
  
     A associação de coluna é especificada chamando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) com o *atributo* definido como SQL_ATTR_PARAM_BIND_TYPE e *ValuePtr* definido como SQL_PARAM_BIND_BY_COLUMN.  
  
-   A associação em linhas é feita quando todos os parâmetros na instrução SQL são associados como uma unidade a uma matriz de estruturas que contém cada uma das variáveis para os parâmetros.  
  
     A associação de linha é especificada chamando **SQLSetStmtAttr** com o *atributo* definido como SQL_ATTR_PARAM_BIND_TYPE e *ValuePtr* definido como o tamanho da estrutura que contém as variáveis do programa.  
  
 Quando o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client envia parâmetros de cadeia de caracteres ou de caracteres binários para o servidor, ele preenche os valores para o comprimento especificado no parâmetro **SQLBindParameter** *colunasize* . Se um aplicativo ODBC 2. x especificar 0 para *colunasize*, o driver remeterá o valor do parâmetro para a precisão do tipo de dados. A precisão é 8000 quando houver conexão a servidores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 255 quando houver conexões a versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Colunasize* é em bytes para colunas Variant.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte à definição de nomes para parâmetros de procedimento armazenado. O ODBC 3.5 também introduziu o suporte a parâmetros nomeados usados ao chamar procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse suporte pode ser usado para:  
  
-   Chamar um procedimento armazenado e fornecer valores para um subconjunto dos parâmetros definidos para o procedimento armazenado.  
  
-   Especificar os parâmetros no aplicativo em uma ordem diferente daquela especificada quando o procedimento armazenado foi criado.  
  
 Só há suporte para parâmetros nomeados ao usar a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] **Execute** ou a sequência de escape de chamada ODBC para executar um procedimento armazenado.  
  
 Se **SQL_DESC_NAME** for definido para um parâmetro de procedimento armazenado, todos os parâmetros de procedimento armazenado na consulta também deverão definir **SQL_DESC_NAME**.  Se os literais forem usados em chamadas de procedimento armazenado, em que os parâmetros têm **SQL_DESC_NAME** definido, os literais deverão usar o formato *' nome*=*valor*', em que *nome* é o nome do parâmetro de procedimento armazenado (por exemplo, @p1). Para obter mais informações, consulte [ligando parâmetros por nome (parâmetros nomeados)](https://go.microsoft.com/fwlink/?LinkId=167215).  
  
## <a name="see-also"></a>Consulte também  
 [Usando parâmetros de instrução](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
  
