---
title: Suporte a FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], SQL Server Native Client
- SQL Server Native Client [FILESTREAM support]
ms.assetid: 1ad3400d-7fcd-40c9-87ae-f5afc61e0374
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4a60cb23aa48b071aa4f1db492cbd1629f38ab22
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761474"
---
# <a name="filestream-support"></a>Suporte a FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  FILESTREAM é uma forma de armazenar e acessar valores altos de binário, por meio do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou por acesso direto ao sistema de arquivos do Windows. Um valor binário grande é um valor superior a 2 gigabytes (GB). Para obter mais informações sobre o suporte a FILESTREAM avançado, consulte [filestream &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md).  
  
 Quando uma conexão de banco de dados for aberta, **@@TEXTSIZE** será definido, por padrão, como -1 ("ilimitado").  
  
 Também é possível acessar e atualizar colunas FILESTREAM usando as APIs do sistema de arquivos do Windows.  
  
 Para obter mais informações, consulte os seguintes tópicos:  
  
-   [OLE DB de &#40;suporte a FileStream&#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [Suporte &#40;a FileStream ODBC&#41;](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [Acessar dados do FILESTREAM com OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>Consultando colunas FILESTREAM  
 Conjuntos de linhas de esquema no OLE DB não relatarão se uma coluna é uma coluna FILESTREAM. ITableDefinition no OLE DB não pode ser usado para criar uma coluna FILESTREAM.  
  
 As funções de catálogo, como SQLColumns no ODBC, não relatarão se uma coluna é uma coluna FILESTREAM.  
  
 Para criar colunas FILESTREAM ou detectar quais colunas existentes são colunas FILESTREAM, use a coluna **is_filestream** da exibição de catálogo [sys.columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).  
  
 A seguir, é mostrado um exemplo:  
  
```  
-- Create a table with a FILESTREAM column.  
CREATE TABLE Bob_01 (GuidCol1 uniqueidentifier ROWGUIDCOL NOT NULL UNIQUE DEFAULT NEWID(), IntCol2 int, varbinaryCol3 varbinary(max) FILESTREAM);  
  
-- Find FILESTREAM columns.  
SELECT name FROM sys.columns WHERE is_filestream=1;  
  
-- Determine whether a column is a FILESTREAM column.  
SELECT is_filestream FROM sys.columns WHERE name = 'varbinaryCol3' AND object_id IN (SELECT object_id FROM sys.tables WHERE name='Bob_01');  
```  
  
## <a name="down-level-compatibility"></a>Compatibilidade com níveis inferiores  
 Se o cliente foi compilado usando a versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que foi incluída com o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]e o aplicativo se conecta ao comportamento de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], **varbinary (max)** será compatível com [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Ou seja, o tamanho máximo de dados retornados será limitado a 2 GB. Para valores de resultado superiores a 2 GB, ocorrerá truncamento e será retornado um aviso de "truncamento à direita de dados de cadeia de caracteres".  
  
 Quando a compatibilidade de tipo de dados estiver definida como 80, o comportamento do cliente será consistente com o comportamento de clientes de nível inferior.  
  
 Para clientes que usam SQLOLEDB ou outros provedores que foram liberados antes da versão [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, **varbinary (max)** serão mapeados para a imagem.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
