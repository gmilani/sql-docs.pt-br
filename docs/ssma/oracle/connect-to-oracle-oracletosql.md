---
title: Conectar-se ao Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 23a48cb6-ff30-49bb-b4a7-603ebcab336f
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 42ab1e77dbdb7cee237a9ec22c49a725a64390c0
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264479"
---
# <a name="connect-to-oracle-oracletosql"></a>Conectar-se ao Oracle (OracleToSQL)
Use o **conectar-se ao Oracle** caixa de diálogo para se conectar ao banco de dados Oracle que você deseja migrar.  
  
Para acessar essa caixa de diálogo, nos **arquivo** menu, selecione **conectar-se ao Oracle**. Se você tiver se conectado anteriormente, o comando é **reconectar-se ao Oracle**.  
  
## <a name="options"></a>Opções  
**Provedor**  
Selecione o provedor de acesso de dados para sua conexão ao banco de dados Oracle. Provedores disponíveis são o provedor de cliente Oracle e o provedor OLE DB. O padrão é o provedor de cliente Oracle.  
  
**Modo**  
Selecione o modo padrão, TNSNAME ou cadeia de caracteres de Conexão.  
  
-   No modo padrão, insira ou selecione valores para o provedor, nome do servidor, porta do servidor, Oracle SID, nome de usuário e senha.  
  
-   No modo TNSNAME, insira o identificador de conexão (alias TNS) do banco de dados Oracle, nome de usuário e senha.  
  
-   No modo de cadeia de caracteres de Conexão, você deve fornecer uma cadeia de caracteres de conexão.  
  
    > [!IMPORTANT]  
    > Não recomendamos que você use o modo de cadeia de caracteres de Conexão porque o texto pode incluir senhas, e ele é enviado como texto não criptografado.  
  
O padrão é o modo padrão.  
  
**Nome do servidor**  
Insira o nome do servidor Oracle. O nome do servidor padrão é o mesmo que o nome do computador. Essa é uma opção de modo padrão.  
  
**Porta do servidor**  
Se você estiver usando um número de porta diferente 1521 (padrão) para conexões com o Oracle, insira o número da porta. Essa é uma opção de modo padrão.  
  
**Conectar-se o identificador**  
Insira o Oracle conectar-se o identificador. Esse é o alias do banco de dados, conforme definido no arquivo tnsnames. ora local.  
  
Essa é uma opção de modo TNSNAME.  
  
**SID do Oracle**  
Insira o SID para o banco de dados. O SID é um identificador que distingue o banco de dados Oracle em um computador. O padrão de SID para um banco de dados é os oito primeiros caracteres do nome do banco de dados.  
  
Essa é uma opção de modo padrão.  
  
**Nome de usuário**  
Insira o nome de usuário que usará o SSMA para se conectar ao banco de dados Oracle.  
  
**Senha**  
Digite a senha para o nome de usuário.  
  
**Cadeia de conexão**  
> [!IMPORTANT]  
> Não recomendamos que você use o modo de cadeia de caracteres de Conexão porque o texto pode incluir senhas, e ele é enviado como texto não criptografado.  
  
Se você usar o modo de cadeia de caracteres de Conexão, insira a cadeia de conexão completa para a conexão ao Oracle.  
  
Cadeias de caracteres de Conexão consistem em pares de nome e valor do parâmetro.  
  
-   Para informações de cadeia de caracteres de conexão OLE DB, consulte [Microsoft OLE DB Provider for Oracle](https://go.microsoft.com/fwlink/?LinkId=85640) artigo na biblioteca MSDN.  
  
Para cadeias de caracteres de conexão do SSMA, sempre inclua o parâmetro de provedor. Além disso, certifique-se de que você inclua o parâmetro de porta ao conectar-se ao Oracle.  
  
