---
title: srv_alloc (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: srv_alloc
apilocation: opends60.dll
apitype: DLLExport
dev_langs: C++
helpviewer_keywords: srv_alloc
ms.assetid: 91505c59-a273-452f-b71d-5e8205c21863
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a51631ea770f50051fba94ace61ea406d2a31c29
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="srvalloc-extended-stored-procedure-api"></a>srv_alloc (API do procedimento armazenado estendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Aloca memória dinamicamente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
void * srv_alloc ( DBINT  
size  
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *size*  
 Especifica o número de bytes para alocar.  
  
## <a name="returns"></a>Retorna  
 Um ponteiro para o espaço recentemente alocado. Se *size* bytes não puderem ser alocados, um ponteiro nulo será retornado.  
  
## <a name="remarks"></a>Comentários  
 A função **srv_alloc** é equivalente à função **GlobalAlloc** da API do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Funções normais de gerenciamento de memória em tempo de execução da API C do Windows podem ser usadas em um aplicativo de API de procedimento armazenado estendido.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  