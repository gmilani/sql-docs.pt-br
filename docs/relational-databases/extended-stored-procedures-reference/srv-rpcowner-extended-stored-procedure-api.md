---
title: srv_rpcowner (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_rpcowner
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcowner
ms.assetid: e81a60e6-14ea-47bc-a11c-3d7635344447
author: rothja
ms.author: jroth
ms.openlocfilehash: 3bb52186b88b678f9abe276fb5f18f1dd7505b96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119688"
---
# <a name="srv_rpcowner-extended-stored-procedure-api"></a>srv_rpcowner (API de procedimento armazenado estendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Retorna o componente proprietário de procedimento para o procedimento armazenado remoto atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DBCHAR * srv_rpcowner (  
SRV_PROC *  
srvproc  
,  
int *  
len   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que é o identificador de uma conexão de cliente específica (neste caso, o identificador que recebeu o procedimento armazenado remoto). A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *len*  
 É um ponteiro para uma variável inteira que recebe o comprimento do nome do proprietário. O parâmetro *len* pode ser NULL, caso em que o tamanho do componente do proprietário não é retornado.  
  
## <a name="returns"></a>Retorna  
 Um ponteiro DBCHAR ponteiro para o componente do proprietário com terminação nula para o procedimento armazenado remoto atual. Se não houver um procedimento armazenado remoto atual, NULL será retornado e *len* será definido como -1.  
  
## <a name="remarks"></a>Remarks  
 Essa função retorna apenas o componente proprietário do procedimento armazenado remoto. Ela não inclui os especificadores opcionais para nome, nome de procedimento armazenado remoto e número de procedimento armazenado remoto.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
