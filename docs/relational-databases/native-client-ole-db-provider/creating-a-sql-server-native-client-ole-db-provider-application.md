---
title: Criando um aplicativo de provedor de OLE DB de SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, application creation
- applications [SQL Server Native Client]
- OLE DB, creating applications
ms.assetid: f3ae6815-f32d-4913-a1a2-2ba2f20cfd88
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f4b872d8b12ed73079f28a0b0daff15afcc642eb
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73789243"
---
# <a name="creating-a-sql-server-native-client-ole-db-provider-application"></a>Criando um aplicativo provedor OLE DB do SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A criação de um aplicativo de provedor de OLE DB de cliente nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envolve estas etapas:  
  
1.  Estabelecimento de uma conexão a uma fonte de dados.  
  
2.  Execução de um comando.  
  
3.  Processamento dos resultados.  

> [!NOTE]  
>  Quando possível, use a Autenticação do Windows. Se a Autenticação do Windows não estiver disponível, solicite aos usuários que digitem suas credenciais em tempo de execução. Evite armazenar as credenciais em um arquivo. Se for necessário persistir as credenciais, criptografe-as com a [Win32 cryptoAPI](https://go.microsoft.com/fwlink/?LinkId=9504).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Estabelecendo uma conexão com uma fonte de dados](../../relational-databases/native-client-ole-db-provider/establishing-a-connection-to-a-data-source.md)  
  
-   [Executando um comando](../../relational-databases/native-client-ole-db-provider/executing-a-command.md)  
  
-   [Processando resultados](../../relational-databases/native-client-ole-db-provider/processing-results.md)  
  
-   [Sobre propriedades OLE DB](../../relational-databases/native-client-ole-db-provider/about-ole-db-properties.md)  
  
-   [Usando a cláusula OUTPUT com OLE DB no SQL Server Native Client](../../relational-databases/native-client-ole-db-provider/using-the-output-clause-with-ole-db-in-sql-server-native-client.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
