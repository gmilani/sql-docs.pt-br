---
title: 'ISSCommandWithParameters:: ParameterProperties (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 696b170c81177129e6e91cf65a37f2d1146a4133
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761977"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Retorna uma matriz de estruturas de conjuntos de propriedades SSPARAMPROPS, um conjunto de propriedades SSPARAMPROPS para cada parâmetro XML ou UDT.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pcParams*[out][in]  
 Um ponteiro para a memória que contém o número de estruturas SSPARAMPROPS retornadas em *prgParamProperties*.  
  
 *prgParamProperties*[out]  
 Um ponteiro para memória na qual uma matriz de estrutura SSPARAMPROPS é retornada. O provedor aloca memória para as estruturas e retorna o endereço para essa memória; o consumidor libera essa memória com **IMalloc:: Free** quando ela não precisa mais das estruturas. Antes de chamar **IMalloc:: Free** para *prgParamProperties*, o consumidor também deve chamar **VariantClear** para a propriedade *vValue* de cada estrutura DBPROP a fim de evitar um vazamento de memória nos casos em que a variante contiver um tipo de referência (como um BSTR.) Se *pcParams* for zero na saída ou um erro diferente de DB_E_ERRORSOCCURRED ocorrer, o provedor não alocará memória e garantirá que *prgParamProperties* seja um ponteiro nulo na saída.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 O método **ParameterProperties** retorna os mesmos códigos de erro que o método principal OLE DB **ICommandProperties:: GetProperties** , exceto que DB_S_ERRORSOCCURRED e DB_E_ERRORSOCCURED não podem ser gerados.  
  
## <a name="remarks"></a>Comentários  
 **ISSCommandWithParameters:: ParameterProperties** se comporta consistentemente em relação a **GetParameterInfo**. Se [ISSCommandWithParameters:: ParameterProperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) ou **SetParameterInfo** não tiver sido chamado ou tiver sido chamado com cParams igual a zero, **GetParameterInfo** derivará informações de parâmetro e retornará isso. Se **ISSCommandWithParameters:: ParameterProperties** ou **SetParameterInfo** tiver sido chamado para pelo menos um parâmetro, **ISSCommandWithParameters:: ParameterProperties** retornará propriedades somente para esses parâmetros para que **ISSCommandWithParameters:: ParameterProperties** foi chamado. Se **ISSCommandWithParameters:: ParameterProperties** for chamado após **ISSCommandWithParameters:: ParameterProperties** ou **GetParameterInfo**, as chamadas subsequentes para **ISSCommandWithParameters:: ParameterProperties** retorna os valores substituídos para os parâmetros para os quais **ISSCommandWithParameters:: ParameterProperties** foi chamado.  
  
 A estrutura SSPARAMPROPS é definida da seguinte maneira:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|Membro|Descrição|  
|------------|-----------------|  
|*iOrdinal*|O ordinal do parâmetro passado.|  
|*cPropertySets*|O número de estruturas DBPROPSET em *rgPropertySets*.|  
|*rgPropertySets*|Um ponteiro para a memória no qual uma matriz de estruturas DBPROPSET deve ser retornada.|  
  
## <a name="see-also"></a>Consulte também  
 [OLE DB &#40;ISSCommandWithParameters&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
