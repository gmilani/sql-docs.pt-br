---
title: Conformidade de SQL-92 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], SQL-92 compliance
- desktop database drivers [ODBC], SQL-92 compliance
- SQL-92 compliance [ODBC]
- ODBC desktop database drivers [ODBC], SQL-92 compliance
ms.assetid: 50c8c7df-df01-4f4d-ad62-d059cf29d73a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5d8ed2818b466d16591be8b70478221d7ac84df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063375"
---
# <a name="sql-92-compliance"></a>Conformidade com SQL-92
Os Drivers de banco de dados de área de trabalho do ODBC e o mecanismo subjacente do Microsoft Jet não são compatíveis com o SQL-92. Eles oferecem suporte a muitos recursos que foram definidos em SQL-92. Não há suporte para alguns recursos com suporte no driver em SQL-92. Para obter mais informações, consulte o *guia do programador do Microsoft Jet banco de dados Engine*. A seguir está as principais diferenças entre os dois:  
  
-   O SQL usado pelos Drivers de banco de dados da área de trabalho suporta expressões mais complexas que aqueles especificados pelo SQL-92.  
  
-   Aplicam regras diferentes para o predicado BETWEEN.  
  
-   O SQL usado pelos Drivers de banco de dados de área de trabalho e ANSI SQL dá suporte a palavras-chave diferentes.  
  
 Não há suporte para os seguintes recursos do SQL-92 pelo SQL do Microsoft Jet:  
  
-   Instruções de segurança, como GRANT e bloqueio.  
  
-   DISTINCT com referências de função de agregação.  
  
 Os recursos a seguir são aprimoramentos no SQL usado pelos Drivers de banco de dados da área de trabalho que não são especificados pelo SQL-92:  
  
-   A instrução de TRANSFORMAÇÃO fornecendo suporte para consultas de tabela de referência cruzada.  
  
-   Funções de agregação adicionais (**StDev** e **VarP**).  
  
> [!NOTE]  
>  Os Drivers de banco de dados de área de trabalho dão suporte a sintaxe ANSI padrão para % (porcentagem) e _ (sublinhado), não * (asterisco) e? (ponto de interrogação).
