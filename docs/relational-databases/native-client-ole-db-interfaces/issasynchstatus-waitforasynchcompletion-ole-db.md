---
title: 'ISSAsynchStatus:: WaitForAsynchCompletion (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
apitype: COM
helpviewer_keywords:
- WaitForAsynchCompletion method
ms.assetid: 9f65e9e7-eb93-47a1-bc42-acd4649fbd0e
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 50751cdbb4a488913a9673d00195b4b6000f54ad
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73762627"
---
# <a name="issasynchstatuswaitforasynchcompletion-ole-db"></a>ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Aguarda até que a operação com execução assíncrona seja concluída ou que um tempo limite seja atingido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT WaitForAsynchCompletion(   
        DWORD dwMillisecTimeOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *dwMillisecTimeOut*[in]  
 Tempo limite em milissegundos.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi bem-sucedido.  
  
 E_UNEXPECTED  
 Um conjunto de linhas está em um estado não usado porque **ITransaction::Commit** ou **ITransaction::Abort** foi chamado ou o conjunto de linhas foi cancelado durante sua fase de inicialização.  
  
 DB_E_CANCELED  
 O processamento assíncrono foi cancelado durante a população do conjunto de linhas ou a inicialização de objeto de fonte de dados.  
  
 DB_S_ASYNCHRONOUS  
 A operação ainda não foi concluída, embora o tempo limite especificado tenha sido atingido.  
  
> [!NOTE]  
>  Além dos valores de código de retorno listados anteriormente, o método **ISSAsynchStatus::WaitForAsynchCompletion** também dá suporte aos valores de código de retorno retornados pelos principais métodos **ICommand::Execute** e **IDBInitialize::Initialize** do OLE DB.  
  
## <a name="remarks"></a>Comentários  
 O método **ISSAsynchStatus::WaitForAsynchCompletion** não será retornado enquanto o valor de tempo limite (em milissegundos) não se esgotar ou a operação pendente não for concluída. O objeto **Command** tem uma propriedade **CommandTimeout** que controla o número de segundos que uma consulta será executada antes de atingir o tempo limite. A propriedade **CommandTimeout** será ignorada se usada em conjunto com o método **ISSAsynchStatus:: WaitForAsynchCompletion** .  
  
 A propriedade de tempo limite é ignorada para operações assíncronas. O parâmetro de tempo limite de **ISSAsynchStatus::WaitForAsynchCompletion** especifica o tempo máximo decorrido antes de o controle ser retornado ao chamador. Se esse tempo limite expirar, DB_S_ASYNCHRONOUS será retornado. Os tempos limite nunca cancelam operações assíncronas. Se o aplicativo precisar cancelar uma operação assíncrona que não tenha sido concluída dentro de um tempo limite, ele deverá aguardar o tempo limite e, em seguida, cancelar explicitamente a operação, caso DB_S_ASYNCHRONOUS seja retornado.  
  
> [!NOTE]  
>  Quando os Componentes de Serviço do OLE DB são usados, S_OK pode ser retornado quando DB_S_ASYNCHRONOUS é esperado, de forma que os aplicativos devam chamar [ISSAsynchStatus::GetStatus](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) para verificar a conclusão quando S_OK ou DB_S_ASYNCHRONOUS é retornado.  
  
 Se o valor de *dwMillisecTimeOut* for definido como INFINITE, o método **ISSAsynchStatus::WaitForAsynchCompletion** será bloqueado até a conclusão da operação. Se o valor de *dwMillisecTimeOut* for definido como 0, o método será retornado imediatamente com o status da operação pendente. Se o tempo limite expirar antes da conclusão da operação, DB_S_ASYNCHRONOUS será retornado.  
  
 Se a operação for concluída antes da expiração do tempo limite, o HRESULT retornado será o HRESULT retornado pela operação (o HRESULT retornado executou a operação de forma síncrona).  
  
 Além disso, a propriedade SSPROP_ISSAsynchStatus foi adicionada ao conjunto de propriedades DBPROPSET_SQLSERVERROWSET. Os provedores que dão suporte à interface [ISSAsynchStatus](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md) precisam implementar essa propriedade com um valor de VARIANT_TRUE.  
  
## <a name="see-also"></a>Consulte também  
 [Executando operações assíncronas](../../relational-databases/native-client/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
