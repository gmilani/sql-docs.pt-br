---
title: Referência da API de instância do SQL Server Express LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: faec46da-0536-4de3-96f3-83e607c8a8b6
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: adfddc5de02f13b592b1f03107a67c4a3c449d0c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128634"
---
# <a name="sql-server-express-localdb-instance-api-reference"></a>Referência de API da instância LocalDB do SQL Server Express
  No mundo do SQL Server tradicional baseado em serviço, as instâncias individuais do SQL Server instaladas em um único computador são separadas fisicamente; ou seja, cada instância deve ser instalada e removida separadamente, ter um conjunto separado de binários e ser executada em um processo de serviço separado. O nome da instância do SQL Server é usado para especificar a qual instância do SQL Server o usuário deseja se conectar.  
  
 A API da instância do SQL Server Express LocalDB usa um modelo de instância "leve e" simplificado. Embora as instâncias de LocalDB individuais estejam separadas no disco e no Registro, elas usam o mesmo conjunto de binários de LocalDB compartilhados. Além disso, o LocalDB não usa serviços; as instâncias de LocalDB são iniciadas sob demanda através das chamadas de API da instância de LocalDB. No LocalDB, o nome de instância é usado para especificar com qual das instâncias de LocalDB o usuário deseja trabalhar.  
  
 Uma instância de LocalDB sempre pertence a um único usuário e é visível e acessível apenas de contexto do usuário, a menos que o compartilhamento da instância está habilitado.  
  
 Embora, tecnicamente, as instâncias de LocalDB não sejam iguais às instâncias tradicionais do SQL Server, seu uso pretendido é similar. Eles são chamados *instâncias* para enfatizar essa similaridade e torná-las mais intuitiva para usuários do SQL Server.  
  
 O LocalDB oferece suporte a dois tipos de instâncias: AI (instâncias automáticas) e NI (instâncias nomeadas). O identificador de uma instância de LocalDB é o nome da instância.  
  
## <a name="automatic-localdb-instances"></a>Instâncias automáticas de LocalDB  
 Instâncias automáticas de LocalDB são "públicas"; eles são criados e gerenciados automaticamente para o usuário e pode ser usado por qualquer aplicativo. Existe uma instância de LocalDB automática para todas as versões de LocalDB está instalado no computador do usuário.  
  
 As instâncias automáticas de LocalDB fornecem gerenciamento de instância contínuo. O usuário não precisa criar a instância. Isso permite que os usuários instalem facilmente os aplicativos e migrem para computadores diferentes. Se o computador de destino tiver a versão especificada de LocalDB instalada, a instância automática de LocalDB para essa versão também estará disponível nesse computador.  
  
### <a name="automatic-instance-management"></a>Gerenciamento automático de instância  
 Um usuário não precisa criar uma instância automática de LocalDB. A instância lentamente é criada na primeira vez em que a instância é usada, desde que a versão especificada de LocalDB está disponível no computador do usuário. Do ponto de vista do usuário, a instância automática está sempre presente se os binários de LocalDB estiverem presentes.  
  
 Outras operações de gerenciamento de instância, como Excluir, Compartilhar e Descompartilhar, também funcionam para instâncias automáticas. Em particular, a exclusão de uma instância automática redefine a instância, que será recriada na próxima operação Iniciar. A exclusão de uma instância automática possivelmente será necessária se os bancos de dados do sistema forem danificados.  
  
### <a name="automatic-instance-naming-rules"></a>Regras de nomeação de instância automática  
 As instâncias automáticas de LocalDB têm um padrão especial para o nome de instância que pertence a um namespace reservado. Isso é necessário para impedir conflitos de nomes com instâncias de LocalDB nomeadas.  
  
 O nome de instância automática é o número da versão de linha de base do LocalDB versão precedido por um caractere único "v". Isso se parece com "v" mais dois números com um ponto entre eles; Por exemplo, v11.0 ou V12.00.  
  
 Exemplos de nomes de instância automática ilegais:  
  
-   11.0 (sem o caractere "v" no início)  
  
-   v11 (sem um ponto e o segundo número da versão)  
  
-   v11. (sem o segundo número da versão)  
  
-   v11.0.1.2 (o número de versão tem mais de duas partes)  
  
## <a name="named-localdb-instances"></a>Instancias de LocalDB nomeadas  
 Instâncias de LocalDB nomeadas são "privadas"; uma instância pertence a um único aplicativo que é responsável por criar e gerenciar a instância. As instâncias de LocalDB nomeadas fornecem isolamento e melhoram o desempenho.  
  
### <a name="named-instance-creation"></a>Criação da instância nomeada  
 O usuário deve criar as instâncias nomeadas explicitamente através da API de gerenciamento de LocalDB ou implicitamente através do arquivo app.config de um aplicativo gerenciado. Um aplicativo gerenciado também pode usar a API.  
  
 Cada instância nomeada tem uma versão de LocalDB associada; ou seja, ela indica um conjunto especificado de binários de LocalDB. A versão da instância nomeada é definida durante o processo de criação de instância.  
  
### <a name="named-instance-naming-rules"></a>Regras de nomeação de instância nomeada  
 Um nome de instância de LocalDB pode ter até 128 caracteres (o limite é imposto pelo tipo de dados `sysname`). Essa é uma diferença significativa se comparada aos nomes de instância tradicionais do SQL Server, que são limitados aos nomes NetBIOS de 16 caracteres ASCII. O motivo dessa diferença é que o LocalDB trata os bancos de dados como arquivos e, portanto, implica a semântica baseada em arquivo, portanto, é intuitivo para os usuários terão mais liberdade para escolher os nomes de instância.  
  
 Um nome de instância de LocalDB pode conter qualquer caractere Unicode que seja legal no componente de nome de arquivo. Caracteres ilegais em um componente de nome de arquivo geralmente incluem os seguintes caracteres: Caracteres ASCII/Unicode 31 por meio de 1, bem como aspas ("), menor que (\<), maior que (>), barra vertical (|), backspace (\b), guia (\t), dois-pontos (:), asterisco (*), ponto de interrogação (?), barra invertida (\\) e a barra (/). Observe que o caractere nulo (\0) é permitido porque é usado na terminação de cadeias de caracteres; tudo o que aparecer após o primeiro caractere nulo será ignorado.  
  
> [!NOTE]  
>  A lista de caracteres ilegais possivelmente dependerá do sistema operacional e mudará nas versões futuras.  
  
 Os espaços em branco à esquerda e à direita nos nomes de instância serão ignorados e cortados.  
  
 Para evitar conflitos, denominados LocalDB de nomenclatura instâncias não podem ter um nome que segue o padrão de nomenclatura para as instâncias automáticas, conforme descrito anteriormente em "Regras de nomenclatura de instância automática". Uma tentativa de criar uma instância nomeada com um nome que segue o padrão de nomeação de instância automática efetivamente cria uma instância padrão.  
  
## <a name="sql-server-express-localdb-reference-topics"></a>Tópicos de referência de LocalDB do SQL Server Express  
 [Cabeçalho e informações de versão de LocalDB do SQL Server Express](sql-server-express-localdb-header-and-version-information.md)  
 Fornece informações do arquivo de cabeçalho e chaves do Registro para localizar a API de instância de LocalDB.  
  
 [Ferramenta de gerenciamento de linha de comando: SqlLocalDB.exe](command-line-management-tool-sqllocaldb-exe.md)  
 Descreve o SqlLocalDB.exe, uma ferramenta para gerenciar instâncias de LocalDB na linha de comando.  
  
 [Função LocalDBCreateInstance](localdbcreateinstance-function.md)  
 Descreve a função que cria uma nova instância de LocalDB.  
  
 [Função LocalDBDeleteInstance](localdbdeleteinstance-function.md)  
 Descreve a função que remove uma instância de LocalDB.  
  
 [Função LocalDBFormatMessage](localdbformatmessage-function.md)  
 Descreve a função que retorna a descrição localizada de um erro de LocalDB.  
  
 [Função LocalDBGetInstanceInfo](localdbgetinstanceinfo-function.md)  
 Descreve a função que obtém informações sobre uma instância de LocalDB; por exemplo, se ela existe, as informações da versão, se ela está em execução etc.  
  
 [Função LocalDBGetInstances](localdbgetinstances-function.md)  
 Descreve a função que retorna todas as instância de LocalDB com uma versão especificada.  
  
 [Função LocalDBGetVersionInfo](localdbgetversioninfo-function.md)  
 Descreve a função que retorna informações sobre uma versão de LocalDB especificada.  
  
 [Função LocalDBGetVersions](localdbgetversions-function.md)  
 Descreve a função que retorna todas as versões de LocalDB disponíveis em um computador.  
  
 [Função LocalDBShareInstance](localdbshareinstance-function.md)  
 Descreve a função que compartilha uma instância de LocalDB especificada.  
  
 [Função LocalDBStartInstance](localdbstartinstance-function.md)  
 Descreve a função que inicia uma instância de LocalDB especificada.  
  
 [Função LocalDBStartTracing](localdbstarttracing-function.md)  
 Descreve a função que habilitar o rastreamento de API para um usuário.  
  
 [Função LocalDBStopInstance](localdbstopinstance-function.md)  
 Descreve a função que interrompe a execução de uma instância de LocalDB especificada.  
  
 [Função LocalDBStopTracing](localdbstoptracing-function.md)  
 Descreve a função que desabilita o rastramento de API para um usuário.  
  
 [Função LocalDBUnshareInstance](localdbunshareinstance-function.md)  
 Descreve a função que interrompe o compartilhamento de uma instância de LocalDB especificada.  
  
  
