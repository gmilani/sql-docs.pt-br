---
title: Configurando propriedades para o suplemento Master Data Services para Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cab1c662-5d40-4c16-9f5c-36ff9608810b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a041133bf26865404da6a883992176b19e837c78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479061"
---
# <a name="setting-properties-for-master-data-services-add-in-for-excel"></a>Definindo propriedades para o Suplemento do Master Data Services para Excel
  As configurações do suplemento Master Data Services para Excel determinam como os dados são carregados do MDS para o suplemento do Excel e como os dados são publicados do suplemento do Excel para o MDS.  
  
 Para criar configurações para o suplemento do Excel, abra o **Excel**, clique no menu **Dados Mestres** e clique em **Configurações**. Qualquer um com acesso ao Excel pode alterar essas configurações. As configurações se aplicam ao computador em que o Excel está aberto.  
  
## <a name="excel-add-in-settings"></a>Configurações de suplemento do Excel  
  
||||  
|-|-|-|  
|Guia e seção|Configuração|Descrição|  
|Configurações: Publicando|Mostrar a caixa de diálogo **Publicar e Anotar** ao publicar|Selecione para exibir a caixa de diálogo **Publicar e Anotar** depois de clicar em **Publicar**, permitindo a inserção de uma única anotação para todas as alterações ou a inserção de uma anotação para cada alteração.<br /><br /> Desmarque para especificar que o processo Publicar seja iniciado sem a exibição da caixa de diálogo **Publicar e Anotar** . Você não terá a oportunidade de inserir uma anotação.|  
|Configurações: Versão|Seleção de versão|Selecione a versão dos dados mestres que será carregada no suplemento do Excel. Pode ser:<br /><br /> **Nenhuma** para que a versão não use como padrão nenhuma versão<br /><br /> **Mais antiga** para usar como padrão a versão mais antiga **Mais Nova** para usar como padrão a versão mais recente.|  
|Configurações: Registrando em log|Ativar o log detalhado|Habilite registro em log para o processo de carregar dados mestres do MDS para o Excel Add-in, de modo que o resultado de cada comando no serviço é registrado.|  
|Configurações: Tamanho de lotes|Número de células para carregamento|Selecione um número para indicar quantos milhares de células serão carregados em um lote carregado do servidor MDS para o Excel. O valor padrão é 50.000 células.|  
|Configurações: Tamanho de lotes|Número de células para publicação|Selecione um número para indicar quantos milhares de células serão publicadas em um lote retornado do Excel para o servidor. O valor padrão é 50.000 células.|  
|Configurações: Servidores adicionados à lista segura|Limpar Tudo|Clique para limpar a lista de conexões que foram designadas como seguras quando o arquivo de consulta de atalho associado foi aberto.|  
|Dados: Filtros|Exibir aviso de filtro para conjuntos de dados grandes|Clique para exibir um aviso se o conjunto de dados sendo carregado do MDS para o Excel exceder o número máximo de linhas ou colunas.|  
|Dados: Filtros|Máximo de linhas|Selecione o limite para o número de linhas sendo carregadas, além do qual um aviso de filtro será publicado.|  
|Dados: Filtros|Máximo de colunas|Selecione o limite para o número de colunas sendo carregadas, além do qual um aviso de filtro será publicado.|  
|Dados: Formato da célula|Alterar a cor quando: Alteração de valores de atributo|Clique para especificar que a cor de uma célula será alterada se o valor de atributo nessa célula for alterado quando você atualizar a tabela de suplemento do Excel com novos dados do repositório MDS.|  
|Dados: Formato da célula|Alterar a cor quando: Os membros são adicionados|Clique para especificar que a cor das células de uma linha será alterada se um novo membro for adicionado à linha quando você atualizar a tabela de suplemento do Excel com novos dados do repositório MDS.|  
  
  
