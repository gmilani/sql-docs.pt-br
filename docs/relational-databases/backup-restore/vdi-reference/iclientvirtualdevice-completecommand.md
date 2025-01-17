---
title: IClientVirtualDevice::CompleteCommand
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IClientVirtualDevice::CompleteCommand.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0fb96d94ae330fdf55d82625ed71217ba71e50ff
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847397"
---
# <a name="iclientvirtualdevicecompletecommand-vdi"></a>IClientVirtualDevice::CompleteCommand (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **CompleteCommand** é usada para notificar o SQL Server de que um comando foi concluído. As informações de conclusão apropriadas para o comando devem ser retornadas.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IClientVirtualDevice::CompleteCommand (
   VDC_Command*         const pCmd,
   UINT32               dwCompletionCode,
   UINT32               dwBytesTransferred,
   UINT64               dwlPosition
);
```

## <a name="parameters"></a>Parâmetros

*pCmd* Esse é o endereço de um comando retornado anteriormente de IClientVirtualDevice::GetCommand.

*dwCompletionCode* Esse é um código de status do Win32 que indica o status de conclusão. Esse parâmetro precisa ser retornado para todos os comandos. O código retornado deve ser apropriado para o comando que está sendo executado. ERROR_SUCCESS é usado em todos os casos para indicar um comando executado com êxito. Para obter a lista completa de códigos possíveis, confira o arquivo Winerror.h. Uma lista de códigos de status típicos para cada comando é exibida em Comandos.

*dwBytesTransferred* Esse é o número de bytes transferidos com êxito. Isso é retornado somente para comandos de transferência de dados Leitura e Gravação.

*dwlPosition* Essa é uma resposta somente ao comando GetPosition.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | A conclusão foi anotada corretamente. |
| VD_E_INVALID | pCmd não era um comando ativo. |
| VD_E_ABORT | A anulação foi sinalizada. |
| VD_E_PROTOCOL | O dispositivo não está aberto. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
