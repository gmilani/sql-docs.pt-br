---
title: Procedimentos armazenados do sistema XML | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- system stored procedures [SQL Server], XML
- sp_xml_removedocument
- OPENXML statement, system stored procedures
- sp_xml_preparedocument
- XML [SQL Server], system stored procedures
ms.assetid: e60c7f85-6823-4d28-93d6-b053d08cc830
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b07b7f782c534c7d98e6e20047f58787fe32e8e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902866"
---
# <a name="xml-system-stored-procedures"></a>Procedimentos armazenados do sistema XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  O SQL Server fornece os seguintes procedimentos armazenados do sistema que são usados junto com o OPENXML:  
  
-   [sp_xml_preparedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)  
  
-   [sp_xml_removedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)  
  
 Para escrever consultas usando OPENXML, é necessário primeiro criar uma representação interna do documento XML chamando **sp_xml_preparedocument**. O procedimento armazenado retorna um identificador para a representação interna do documento XML. Em seguida, esse identificador é passado para o OPENXML. O OPENXML fornece exibições de conjuntos de linhas do documento baseado em XPaths. Especificamente, isso é um padrão de linha e um ou mais padrões de coluna.  
  
> [!NOTE]  
>  O identificador do documento retornado por **sp_xml_preparedocument** é válido durante a sessão.  
  
 A representação interna de um documento XML pode ser removida da memória chamando o procedimento armazenado do sistema **sp_xml_removedocument** .  
  
## <a name="see-also"></a>Consulte Também  
 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)   
 [OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
