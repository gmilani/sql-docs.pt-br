---
title: Principais considerações de segurança do SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- security [SQLXML], about security
ms.assetid: 330cd2ff-d5d5-4c8e-8f93-0869c977be94
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d739eb3d4a9a1466a9eef441d683aa0acd81d0a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026927"
---
# <a name="core-sqlxml-security-considerations"></a>Principais considerações de segurança do SQLXML
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A seguir, encontram-se diretrizes de segurança para o uso do SQLXML para acessar dados.  
  
-   O provedor SQLXMLOLEDB expõe um **StreamFlags** propriedade que permite que você defina sinalizadores para indicar qual funcionalidade do SQLXML deve ser habilitada ou desabilitada para cada instância específica. Você pode usar essa propriedade para personalizar o uso do SQLXML e ter certeza de que apenas os que você deseja estão habilitados. Para obter mais informações, consulte [provedor SQLXMLOLEDB &#40;SQLXML 4.0&#41;](https://msdn.microsoft.com/library/fc489682-690a-4bb0-b5ac-237d376dc110).  
  
-   Quando erros de SQLXML ocorrem e são retornados, eles podem conter informações sobre o esquema de banco de dados, como nomes de tabela, nomes de colunas ou informações sobre tipo. Você deve ter cuidado ao tratar esses erros, para que as informações sobre a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não sejam facilmente descobertas por usuários não autorizados.  
  
-   Quando usado para consultar ou enviar atualizações para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o SQLXML não define limites para a quantidade de dados que podem ser trocados e não faz nenhuma verificação em relação ao tamanho dos dados em uma carga do SQLXML antes de tentar processá-los. Quando você desenvolve seu aplicativo usando SQLXML, é sua responsabilidade assegurar que haja memória suficiente no sistema para processar os dados. Por exemplo, ao consultar dados do servidor, você deve verificar se há espaço suficiente na memória do cliente para armazená-los. Da mesma forma, se você está carregando dados para o servidor, deve verificar se há memória disponível para processá-los e se há espaço disponível em disco no servidor para armazenar os dados.  
  
-   O SQLXML gera dinamicamente consultas de [!INCLUDE[tsql](../../../includes/tsql-md.md)] e atualiza comandos e os envia ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para execução. Esse é o único modo no qual o SQLXML consulta e atualiza o servidor. Os resultados serão recebidos como um fluxo (de XML) ou como um conjunto de linhas.  
  
-   Ao receber resultados de consulta, o SQLXML não executa nenhuma ação com base no conteúdo dos dados que recebe. Nenhum processamento adicional é feito baseado no tipo ou no conteúdo dos dados. Os dados nunca são tratados como código com o qual as ações serão executadas.  
  
-   Ao executar modelos XML, o SQLXML converte as consultas XPath e DBObject contidas no modelo enviado em comandos de [!INCLUDE[tsql](../../../includes/tsql-md.md)] que são, por sua vez, executados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esses comandos só afetam os dados existentes. Os comandos gerados pelo SQLXML nunca alterarão a estrutura do banco de dados. Os usuários devem executar comandos explícitos para alterar a estrutura do banco de dados. Por exemplo, ao incluí-los em um **sql:query** bloco de um modelo.  
  
-   Ao executar consultas DBObject e instruções XPath em arquivos de mapeamento, o SQLXML não alterará os dados no banco de dados.  
  
-   O SQLXML pode fazer alterações de formatação nos dados especificados com base nas diferenças entre os XML e os modelos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por exemplo, o formato para especificar hora é diferente. O SQLXML tentará resolver essas diferenças. Como resultado, algumas informações de precisão podem ser perdidas.  
  
-   O SQLXML não define limites para o tempo que leva para processar os dados. O processamento continuará até que um erro ocorra ou o processamento seja concluído.  
  
-   O SQLXML não grava no sistema de arquivos. Se os usuários quiserem salvar os dados que recuperam do banco de dados, deverão usar seus códigos.  
  
-   O SQLXML permite que os usuários executem qualquer consulta SQL que queiram no banco de dados. Essa funcionalidade nunca deve ser exposta para uma fonte não segura ou não controlada, já que ela está abrindo o banco de dados SQL para qualquer usuário.  
  
-   Ao executar diagramas de atualização, o SQLXML converte o **updg:sync** blocos de comandos INSERT, UPDATE e DELETE em relação a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância. Esses comandos só afetam os dados existentes. Os comandos gerados pelo SQLXML nunca alterarão o banco de dados. Os usuários devem executar comandos explícitos para alterar a estrutura do banco de dados. Por exemplo, ao incluí-los em um **sql:query** bloco de um modelo.  
  
-   Ao executar diagramas de atualização, o SQLXML converte o diagrama em comandos DELETE, UPDATE e INSERT na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esses comandos só afetam os dados existentes. Os comandos gerados pelo SQLXML nunca alterarão o banco de dados. Os usuários devem executar comandos explícitos para alterar a estrutura do banco de dados. Por exemplo, ao incluí-los em um **sql:query** bloco de um modelo.  
  
## <a name="see-also"></a>Consulte também  
 [Considerações de segurança do SQLXML 4.0](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/sqlxml-4-0-security-considerations.md)  
  
  
