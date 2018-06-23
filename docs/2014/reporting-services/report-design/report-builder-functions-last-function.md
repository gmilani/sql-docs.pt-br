---
title: Função Last (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 123b78a0-d6c9-4f78-b0e7-73b21854a250
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: c9dc383d9a895218cf644bafc53be3b43cdc698a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116304"
---
# <a name="last-function-report-builder-and-ssrs"></a>Função Last (Construtor de Relatórios e SSRS)
  Retorna o último valor no escopo fornecido da expressão especificada.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Last(expression, scope)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Expressão*  
 (`Variant` ou `Binary`) a expressão na qual executar a agregação, por exemplo, `=Fields!Fieldname.Value`.  
  
 *escopo*  
 (`String`) (Opcional) O nome de um conjunto de dados, região de dados ou grupo que contém os itens do relatório aos quais a função de agregação deve ser aplicada. Se *scope* não estiver especificado, será usado o escopo atual.  
  
## <a name="return-type"></a>Tipo de retorno  
 Determinado pelo tipo de expressão.  
  
## <a name="remarks"></a>Remarks  
 A função `Last` retorna o valor final em um conjunto de dados depois que toda a classificação e filtragem tiverem sido aplicadas no escopo especificado.  
  
 O `Last` função não pode ser usada em expressões de filtro de grupo com qualquer coisa, exceto o escopo atual (padrão).  
  
 Você também pode usar `Last` em um cabeçalho de página para retornar o último valor da `ReportItems` coleção de uma página para produzir cabeçalhos em estilo de dicionário que exibem as entradas e o sobrenome em uma página.  
  
 O valor de *scope* deve ser uma constante de cadeia de caracteres e não pode ser uma expressão. Para agregações externas ou que não especificam outras agregações, *scope* deve se referir ao escopo atual ou a um escopo contentor. Para agregações de agregações, as agregações aninhadas podem especificar um escopo filho.  
  
 *Expression* pode conter chamadas para funções de agregação aninhadas com as seguintes exceções e condições:  
  
-   *Scope* para agregações aninhadas deve ser igual ao escopo da agregação externa ou deve estar contido nela. Para todos os escopos distintos na expressão, um escopo deve estar em uma relação filho com todos os outros escopos.  
  
-   *Scope* para agregações aninhadas não pode ser o nome de um conjunto de dados.  
  
-   *Expressão* não deve conter `First`, `Last`, `Previous`, ou `RunningValue` funções.  
  
-   *Expression* não deve conter agregações aninhadas que especifiquem *recursive*.  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para obter mais informações sobre agregações recursivas, consulte [Criando grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir retorna o número do último produto no grupo `Category` de uma região de dados.  
  
```  
=Last(Fields!ProductNumber.Value, "Category")  
```  
  
## <a name="see-also"></a>Consulte também  
 [Expressão usa relatórios de &#40;SSRS e construtor de relatórios&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;SSRS e construtor de relatórios&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  