---
title: Executando comandos que contêm parâmetros com valor de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, executing commands containing
ms.assetid: 7ecba6f6-fe7a-462a-9aa3-d5115b6d4529
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae08a79bcfe1e4befcad8559e82bdfba5b347fc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63228564"
---
# <a name="executing-commands-containing-table-valued-parameters"></a>Executando comandos que contêm parâmetros com valor de tabela
  A execução de um comando que contém parâmetros com valor de tabela exige duas fases:  
  
1.  Especificar os tipos de parâmetros.  
  
2.  Associar os dados de parâmetro.  
  
## <a name="table-valued-parameter-specification"></a>Especificação de parâmetros com valor de tabela  
 O consumidor pode especificar o tipo do parâmetro com valor de tabela. Estas informações incluem o nome do tipo de parâmetro com valor de tabela. Elas também incluem o nome do esquema, se o tipo de tabela definido pelo usuário para o parâmetro com valor de tabela não estiver no esquema padrão atual para a conexão. Dependendo do suporte do servidor, o consumidor também pode especificar informações de metadados opcionais, como a classificação de colunas, e pode especificar que todas as linhas de determinadas colunas tenham os valores padrão.  
  
 Para especificar um parâmetro com valor de tabela, o consumidor chama ISSCommandWithParameter::SetParameterInfo e, opcionalmente, chama isscommandwithparameters:: SetParameterProperties. Para um parâmetro com valor de tabela, o campo *pwszDataSourceType* na estrutura DBPARAMBINDINFO tem um valor DBTYPE_TABLE. O campo *ulParamSize* é definido como ~0 para indicar que esse tamanho é desconhecido. Propriedades específicas para parâmetros com valor de tabela, como o nome do esquema, nome do tipo, ordem de coluna e colunas padrão, podem ser definidas por meio de isscommandwithparameters:: SetParameterProperties.  
  
## <a name="table-valued-parameter-binding"></a>Associação de parâmetros com valor de tabela  
 Um parâmetro com valor de tabela pode ser qualquer objeto de conjunto de linhas. O provedor faz a leitura a partir deste objeto enquanto envia parâmetros com valor de tabela ao servidor durante a execução.  
  
 Para associar o parâmetro com valor de tabela, o consumidor chama IAccessor:: CreateAccessor. O campo *wType* da estrutura DBBINDING para o parâmetro com valor de tabela é definido como DBTYPE_TABLE. O membro *pObject* da estrutura DBBINDING é não NULL, e o membro *iid* de *pObject* é definido como IID_IRowset ou como qualquer outra interface de objetos de conjunto de linhas do parâmetro com valor de tabela. Os campos restantes na estrutura DBBINDING devem ser definidos da mesma forma que são definidos para BLOBs transmitidos.  
  
 Nas associações para o parâmetro com valor de tabela e o objeto de conjunto de linhas associado a um parâmetro com valor de tabela, as seguintes restrições se aplicam:  
  
-   Os únicos valores de status permitidos para dados da coluna do conjunto de linhas do parâmetro com valor de tabela são DBSTATUS_S_ISNULL e DBSTATUS_S_OK. DBSTATUS_S_DEFAULT resultará em falha e o valor de status associado será definido como DBSTATUS_E_BADSTATUS.  
  
-   Um parâmetro com valor de tabela pode ser marcado com o status DBSTATUS_S_DEFAULT. Os únicos valores válidos são DBSTATUS_S_DEFAULT e DBSTATUS_S_OK. Quando o status é definido como DBSTATUS_S_DEFAULT, o valor do parâmetro com valor de tabela corresponde a uma tabela vazia.  
  
-   As colunas somente leitura em parâmetros com valor de tabela (colunas de identidade ou computadas) devem ser marcadas como padrão usando a propriedade SSPROP_PARAM_TABLE_DEFAULT_COLUMNS. As colunas que têm um valor padrão também devem ser marcadas como padrão por meio da propriedade SSPROP_PARAM_TABLE_DEFAULT_COLUMNS para permitir que o valor padrão a ser usado para valores de dados da coluna para um determinado parâmetro com valor de tabela. O provedor irá ignorar os valores de dados associados com as colunas marcadas como padrão.  
  
-   Os dados serão enviados ao servidor para colunas com DBPROP_COL_AUTOINCREMENT ou SSPROP_COL_COMPUTED, a menos que SSPROP_PARAM_TABLE_DEFAULT também esteja definido.  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
