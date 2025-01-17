---
title: Tradução automática de dados de caractere | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], autotranslating character data
- data types [ODBC], autotranslating character data
- ACPs
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- AutoTranslate feature
- ANSI code pages
- character data autotranslation [ODBC]
- autotranslating character data
- SQL Server Native Client ODBC driver, data types
- ODBC data types, autotranslating character data
ms.assetid: 86a8adda-c5ad-477f-870f-cb370c39ee13
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c08a0987e11f25c3f5b535d8d26526db5bb14a38
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779175"
---
# <a name="autotranslation-of-character-data"></a>Tradução automática de dados de caracteres
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Os dados de caractere, como as variáveis de caractere ANSI declaradas com SQL_C_CHAR ou dados armazenados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando os tipos de dados **Char**, **varchar**ou **Text** , podem representar apenas um número limitado de caracteres. Os dados de caractere armazenados que usam um byte por caractere podem representar apenas 256 caracteres. Os valores armazenados em variáveis SQL_C_CHAR são interpretados usando a ACP (página de código ANSI) do computador cliente. Os valores armazenados usando os tipos de dados **Char**, **varchar**ou **Text** no servidor são avaliados usando o ACP do servidor.  
  
 Se o servidor e o cliente tiverem o mesmo ACP, eles não terão problemas na interpretação dos valores armazenados nos objetos SQL_C_CHAR, **Char**, **varchar**ou **Text** . Se o servidor e o cliente tiverem ACPs diferentes, SQL_C_CHAR dados do cliente poderão ser interpretados como um caractere diferente no servidor se ele for usado nas colunas **Char**, **varchar**ou **Text** , Variables ou Parameters. Por exemplo, um byte de caractere contendo o valor 0xA5 é interpretado como o caractere Ñ em um computador usando a página de código 437 e é interpretado como o sinal de Iene (¥) em um computador que executa a página de código 1252.  
  
 Dados de Unicode são armazenados usando dois bytes por caractere. Todos os caracteres estendidos são abordados pela especificação de Unicode. Dessa forma, todos os caracteres Unicode são interpretados da mesma maneira por todos os computadores.  
  
 O recurso de tradução convertida do driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client tenta minimizar os problemas na movimentação de dados de caractere entre um cliente e um servidor com páginas de código diferentes. A conversão automática pode ser definida na cadeia de conexão de [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md), na cadeia de caracteres de configuração de [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)ou ao configurar fontes de dados para o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client usando o Administrador ODBC.  
  
 Quando AutoTranslate é definido como "no", nenhuma conversão é feita nos dados movidos entre SQL_C_CHAR variáveis nas colunas Client e **Char**, **varchar**ou **Text** , Variables ou Parameters em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os padrões de bit poderão ser interpretados de forma diferente nos computadores cliente e servidor se os dados contiverem caracteres estendidos e os dois computadores tiverem páginas de código diferentes. Os dados serão interpretados da mesma maneira se ambos os computadores tiverem a mesma página de código.  
  
 Quando AutoTranslate é definido como "Yes", o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client usa o Unicode para converter os dados movidos entre SQL_C_CHAR variáveis nas colunas Client e **Char**, **varchar**ou **Text** , Variables ou Parameters em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco  
  
-   Quando os dados são enviados de uma variável SQL_C_CHAR no cliente para uma coluna **Char**, **varchar**ou **Text** , uma variável ou um parâmetro em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o driver ODBC primeiro converte de SQL_C_CHAR para Unicode usando o ACP do cliente e, em seguida, do Unicode de volta ao caractere usando o ACP do servidor.  
  
-   Quando os dados são enviados de uma coluna **Char**, **varchar**ou **Text** , uma variável ou um parâmetro em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma variável SQL_C_CHAR no cliente, o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client primeiro converte de caractere para Unicode usando o ACP do servidor, em seguida, do Unicode de volta para SQL_C_CHAR usando o ACP do cliente.  
  
 Como todas essas conversões são feitas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC de cliente nativo em execução no cliente, o servidor ACP deve ser uma das páginas de código instaladas no computador cliente.  
  
 Fazer as conversões de caractere por Unicode assegura a conversão adequada de todos os caracteres que existem nas duas páginas de código. Se um caractere existir em uma página de código, mas não em outra, entretanto, o caractere não poderá ser representado na página de código de destino. Por exemplo, a página de código 1252 tem o símbolo de marca registrada (®), enquanto a página de código 437 não tem.  
  
 A configuração AutoTranslate não tem nenhum efeito sobre essas conversões:  
  
-   Mover dados entre caracteres SQL_C_CHAR variáveis de cliente e colunas do Unicode **nchar**, **nvarchar**ou **ntext** , variáveis ou parâmetros em bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Mover dados entre Unicode SQL_C_WCHAR variáveis de cliente e caracteres **Char**, **varchar**, ou colunas de **texto** , variáveis ou parâmetros em bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Os dados devem sempre ser convertidos quando movidos de caractere para Unicode.  
  
## <a name="see-also"></a>Consulte também  
   de [processamento&#41; de ODBC de resultados &#40;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
 [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
