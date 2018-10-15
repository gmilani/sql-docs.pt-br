---
title: Conceitos de segurança para o cluster de big data do SQL Server | Microsoft Docs
description: ''
author: nelgson
ms.author: negust
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: bd9e49344108b65898e38065ed88fd06467803cf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795846"
---
# <a name="security-concepts-for-sql-server-big-data-cluster"></a>Conceitos de segurança para o cluster de big data do SQL Server

Um cluster de Big Data seguro implica suporte consistente e coerente para cenários de autenticação e autorização, entre o SQL Server e o HDFS/Spark. A autenticação é o processo de verificação da identidade de um usuário ou serviço e garantir que eles são quem eles são afirmando ser. Autorização refere-se para conceder ou negar o acesso a recursos específicos com base na identidade do usuário solicitante. Esta etapa é executada depois que um usuário é identificado por meio da autenticação.

Autorização no contexto de Big Data geralmente é feita por meio de listas de controle de acesso (ACLs) que associam identidades de usuário com permissões específicas. HDFS dá suporte a autorização, limitando o acesso a APIs do serviço, arquivos HDFS e execução do trabalho.

Este artigo abordará os principais conceitos de segurança do cluster de Big Data.

## <a name="cluster-endpoints"></a>Pontos de extremidade do cluster

Há três pontos de entrada para o cluster de big data

* Gateway HDFS/Spark (Knox) – isso é um ponto de extremidade com base em HTTPS. Outros pontos de extremidade são transmitidas por proxy por meio deste. Gateway HDFS/Spark é usado para acessar serviços como o webHDFS e Livy. Sempre que você veja referências a Knox, esse é o ponto de extremidade.

* Ponto de extremidade controlador – serviço de gerenciamento de cluster de big data que expõe as APIs REST para gerenciar o cluster. Algumas ferramentas, como o portal de administração, também são acessadas por meio desse ponto de extremidade.

* Instância mestre - ponto de extremidade TDS para ferramentas de banco de dados e aplicativos para se conectar à instância mestre do SQL Server no cluster.

![Pontos de extremidade do cluster](media/concept-security/cluster_endpoints.png)

Atualmente, não há nenhuma opção de abrir portas adicionais para acessar o cluster de fora.

### <a name="how-endpoints-are-secured"></a>Como os pontos de extremidade são protegidos

Proteger os pontos de extremidade no cluster de big data é feito utilizando senhas que podem ser conjunto/atualizada usando variáveis de ambiente ou comandos da CLI. Todas as senhas interno do cluster são armazenadas como segredos do Kubernetes.  

# <a name="authentication"></a>Autenticação

Após o provisionamento do cluster, um número de logons é criado.

Alguns desses logons são para os serviços se comunicam entre si e outros são para os usuários finais acessem o cluster.

## <a name="end-user-authentication"></a>Autenticação do usuário final
Após o provisionamento do cluster, um número de senhas do usuário final precisa ser definido usando variáveis de ambiente. Estas são as senhas que os administradores do SQL e os administradores de cluster usam para acessar serviços:

Nome de usuário do controlador:
 + CONTROLLER_USERNAME = < controller_username >

Senha do controlador:  
 + CONTROLLER_PASSWORD = < controller_password >

Senha de SA do SQL Master: 
 + MSSQL_SA_PASSWORD = < controller_sa_password >

Senha para acessar o ponto de extremidade HDFS/Spark:
 + KNOX_PASSWORD = < knox_password >

## <a name="intra-cluster-authentication"></a>Autenticação de dentro do cluster

 Após a implantação do cluster, um número de logons do SQL Server é criado:

* Um logon SQL especial é criado na instância do SQL do controlador que é gerenciado, com a função sysadmin do sistema. A senha para esse logon é capturada como um segredo K8s.

* Um logon de sysadmin é criado em todas as instâncias do SQL no cluster, que o controlador possui e gerencia. Ele é necessário para o controlador executar tarefas administrativas, como instalação de alta disponibilidade ou atualização, nessas instâncias. Esses logons também são usados para comunicação dentro do cluster entre instâncias do SQL, como a instância mestre do SQL se comunicando com um pool de dados.

> [!NOTE]
> No CTP 2.0, há suporte para somente a autenticação básica. Controle de acesso refinado para objetos do HDFS e SQL grande cluster computação e dados de pools de dados, ainda não está disponível.

## <a name="intra-cluster-communication"></a>Comunicação interna do cluster

Comunicação com os serviços não-SQL dentro do cluster de big data, como o Livy Spark ou do Spark ao pool de armazenamento, é protegida usando certificados. Todos os SQL Server para comunicação do SQL Server é protegida usando logons do SQL Server.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de grandes dados do SQL Server, consulte os seguintes artigos:

- [O que é o SQL Server 2019 clusters de big data?](big-data-cluster-overview.md)
- [Início rápido: Implantar um cluster de big data do SQL Server no Kubernetes](quickstart-big-data-cluster-deploy.md)