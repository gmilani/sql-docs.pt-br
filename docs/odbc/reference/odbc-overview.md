---
title: Visão geral do ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 945ebced0703c109ac64c374e31d2e76b556e7ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944832"
---
# <a name="odbc-overview"></a>Visão geral do ODBC
Conectividade de banco de dados aberto (ODBC) é uma interface de programação de aplicativo amplamente aceito (API) para acesso ao banco de dados. Ele se baseia nas especificações do Open Group e ISO/IEC Interface de nível de chamada (CLI) para APIs de banco de dados e usa a linguagem SQL (Structured Query) como sua linguagem de acesso do banco de dados.  
  
 ODBC é projetada para máximo *interoperabilidade* -ou seja, a capacidade de um único aplicativo para acessar sistemas de gerenciamento de outro banco de dados (DBMSs) com o mesmo código-fonte. Aplicativos de banco de dados chamam funções na interface do ODBC, que são implementadas em módulos específicos de banco de dados chamados *drivers*. O uso de drivers isola os aplicativos de chamadas específicas do banco de dados da mesma maneira que drivers de impressora isolar programas de processamento de texto de comandos específicos da impressora. Porque os drivers são carregados em tempo de execução, um usuário só precisa adicionar um novo driver para acessar um DBMS novo; não é necessário recompilar ou vincular novamente o aplicativo.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Por que o ODBC foi criado?](../../odbc/reference/why-was-odbc-created.md)  
  
-   [O que é o ODBC?](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC e a CLI padrão](../../odbc/reference/odbc-and-the-standard-cli.md)
