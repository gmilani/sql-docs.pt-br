---
title: Usando a base de dados de conhecimento padrão do DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d0fa10fa26f46857bd4f6848bd98bdcf1d65253a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484070"
---
# <a name="using-the-dqs-default-knowledge-base"></a>Usando a base de dados de conhecimento padrão do DQS
  Este tópico descreve a base de dados de conhecimento padrão, os **Dados do DQS**que são instalados com o [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Esta é uma base de conhecimento padrão pré-criada que contém os seguintes domínios:  
  
-   **País/região**: contêm os nomes convencionais longos (nome oficial conforme designado pelo país/região) e nomes curtos (nome comum usado em listas, mapas, etc.), abreviação de duas letras, abreviação de três letras e código de três dígitos para cada local.  O valor principal é definido como o nome longo do país.  
  
-   **País/região (início com três letras)** : contêm os nomes convencionais longos (nome oficial conforme designado pelo país/região) e nomes curtos (nome comum usado em listas, mapas e assim por diante), abreviação de duas letras, abreviação de três letras e código de três dígitos para cada local.  Os valores principais são definidos como uma abreviação de três letras do Município.  
  
-   **País/região (início com duas letras)** : contêm os nomes convencionais longos (nome oficial conforme designado pelo país/região) e nomes curtos (nome comum usado em listas, mapas, etc.), abreviação de duas letras, abreviação de três letras e código de três dígitos para cada local.  O valor principal é definido como uma abreviação de duas letras do País.  
  
-   **EUA – Municípios**: contém uma lista de municípios dos EUA.  
  
-   **EUA – Sobrenome**: contém uma lista de sobrenomes que ocorreram 100 ou mais vezes no Censo 2000.  
  
-   **EUA – Locais**: contém uma lista de locais para os 50 estados, o Distrito de Colúmbia e Porto Rico extraídos do Censo 2010.  
  
-   **EUA – Estado**: contém o nome convencional longo (oficial) e a abreviação de duas letras para cada estado nos EUA. O valor principal é definido como o nome convencional do estado.  
  
-   **EUA – Estado (título com duas letras)** : contém o nome convencional longo (oficial) e a abreviação de duas letras para cada estado nos EUA. O valor principal é definido como um nome de estado com abreviação de duas letras.  
  
## <a name="using-the-default-knowledge-base"></a>Usando a base de dados de conhecimento padrão  
 Você pode usar a base de dados de conhecimento padrão do DQS, os Dados do DQS, das seguintes formas:  
  
-   Inicie e execute rapidamente um projeto de qualidade de dados de limpeza usando a base de dados de conhecimento padrão sem ter que primeiro criar uma nova base de dados de conhecimento em DQS.  
  
-   Execute o Gerenciamento de Domínio, a Descoberta de Conhecimento ou as atividades de Política de Correspondência na base de dados de conhecimento padrão. Para fazer isso, clique em **Abrir Base de Dados de Conhecimento** na [Data Quality Client Home Screen](../../2014/data-quality-services/data-quality-client-home-screen.md), selecione a base de dados de conhecimento **Dados do DQS** na tela **Abrir Base de Dados de Conhecimento** e, em seguida, selecione a atividade na área **Selecionar Atividade** . Clique em **Avançar** para continuar.  
  
-   Crie uma nova base de dados de conhecimento usando a base de dados de conhecimento padrão. Para criar uma base de dados de conhecimento de uma base de conhecimento existente, consulte [Create a Knowledge Base](../../2014/data-quality-services/create-a-knowledge-base.md).  
  
-   Use-a no [Componente de limpeza DQS no Integration Services](https://go.microsoft.com/fwlink/?LinkId=238830) e [Suplemento do Master Data Services para Excel](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md).  
  
## <a name="see-also"></a>Consulte também  
 [Bases de Dados de Conhecimento DQS e domínios](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
