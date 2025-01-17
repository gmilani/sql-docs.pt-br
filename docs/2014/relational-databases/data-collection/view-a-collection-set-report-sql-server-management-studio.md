---
title: Exibir um relatório de conjuntos de coleta (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.dc.reporthistory.calendar.f1
helpviewer_keywords:
- collection sets [SQL Server], viewing reports
- reports [SQL Server], viewing collection set
ms.assetid: c3b1e791-9aa1-4bba-9622-4954568e1820
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 898dd309dae82818b60332b29c14f785c18b173b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62873057"
---
# <a name="view-a-collection-set-report-sql-server-management-studio"></a>Exibir um relatório de conjuntos de coleta (SQL Server Management Studio)
  Depois de configurar o data warehouse de gerenciamento, você pode exibir um relatório do conjunto de coleta no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Os relatórios são fornecidos para os conjuntos de coleta de Dados do Sistema instalados durante a instalação. Os relatórios incluídos são:  
  
-   Resumo de Uso do Disco  
  
-   Histórico de Estatísticas de Consulta  
  
-   Histórico de Atividade do Servidor  
  
 Este procedimento exibe o relatório para o conjunto de coleta **Uso do Disco** . É possível seguir o mesmo procedimento geral para exibir os relatórios para os outros conjuntos de coleta de Dados do Sistema.  
  
### <a name="to-view-a-collection-set-report"></a>Para exibir um relatório de conjunto de coleta  
  
1.  As tabelas de um relatório são criadas apenas na primeira vez em que os dados coletados são carregados. Se você tentar exibir um relatório antes desse primeiro carregamento, ocorrerá um erro e nenhum relatório será exibido. Para carregar os dados do conjunto de coleta Uso do Disco, no Pesquisador de Objetos, expanda a pasta **Gerenciamento** , **Coleta de Dados**e **Conjuntos de Coleta de Dados do Sistema**, clique com o botão direito do mouse no conjunto de coleta **Uso do Disco** e clique em **Coletar e Carregar Agora**.  
  
2.  Para exibir o relatório, no Pesquisador de Objetos, expanda a pasta **Gerenciamento** , clique com o botão direito do mouse em **Coleta de Dados**, aponte para **Relatórios**, aponte para **Data Warehouse de Gerenciamento**e clique em **Resumo de Uso do Disco**.  
  
    > [!NOTE]  
    >  Alguns relatórios podem exibir um botão de calendário sob a linha de tempo de coleta de dados. Clique neste botão para acessar o **Calendário de Relatório de Coleta de Dados**.  
  
#### <a name="data-collection-report-calendar"></a>Calendário de Relatório de Coleta de Dados  
 Use essa caixa de diálogo para especificar a data e a hora de início e a duração dos dados que servirão de base para o relatório. Por exemplo, talvez você queira gerar um relatório sobre a atividade de utilização do disco de um servidor em um período de 12 horas específico da última quarta-feira.  
  
 **Data de início**  
 Digite uma data inicial para obter os dados do relatório ou selecione-a no calendário.  
  
 **Hora de início**  
 Digite uma hora inicial para obter os dados do relatório ou especifique-a clicando nas setas.  
  
 **Duration**  
 Especifique o intervalo de tempo que será incluído no relatório. O valor padrão é 240 minutos. Os valores disponíveis para seleção são 15 minutos, 60 minutos, 240 minutos (4 horas), 720 minutos (12 horas) e 1440 minutos (24 horas).  
  
## <a name="see-also"></a>Consulte também  
 [Coleta de Dados](data-collection.md)   
 [Relatórios personalizados no Management Studio](../../ssms/object/custom-reports-in-management-studio.md)   
 [Configurar o Data Warehouse de Gerenciamento &#40;SQL Server Management Studio&#41;](configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
  
