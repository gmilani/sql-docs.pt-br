---
title: Propriedades da Conexão Avançadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4edfab68-7e68-45e8-a3f3-a0049ff7eb9e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a7a5744aa2adcaab74ca09bbb962c8c69d985b79
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771512"
---
# <a name="advanced-connection-properties"></a>Propriedades Avançadas de Conexão
  Use a caixa de diálogo **Propriedades Avançadas de Conexão** para adicionar mais parâmetros de conexão à cadeia de conexão.  
  
 Os parâmetros de conexão adicionais podem ser qualquer parâmetro de conexão ODBC que tem suporte pela instância de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você está usando.  
  
 Os parâmetros adicionados através da caixa de diálogo **Propriedades Avançadas de Conexão** são adicionados aos parâmetros selecionados usando as opções da caixa de diálogo **Conecte-se ao SQL Server** .  
  
 A última instância fornecida de cada parâmetro anula qualquer instância anterior do parâmetro. Parâmetros adicionados usando a caixa de diálogo **Parâmetros Avançados de Conexão** seguem e substituem os parâmetros fornecidos na caixa de diálogo **Conexão do SQL Server** . Por exemplo, se a caixa de diálogo **Conexão do SQL Server** especificar SERVER1 como o Nome do servidor e a página **Parâmetros Adicionais de Conexão** tiver ;SERVER=SERVER2, a conexão será feita ao SERVER2.  
  
 Parâmetros adicionados usando a caixa de diálogo **Propriedades Avançadas de Conexão** sempre são passados como texto sem formatação.  
  
> [!IMPORTANT]  
>  Não inclua credenciais de logon na caixa de diálogo **Propriedades Avançadas de Conexão** . Eles não serão criptografados quando forem transmitidos pela rede.  
  
## <a name="see-also"></a>Consulte também  
 [Acessar o CDC Designer Console](access-the-cdc-designer-console.md)   
 [Conexão de SQL Server para a criação de instância](sql-server-connection-for-instance-creation.md)  
  
  
