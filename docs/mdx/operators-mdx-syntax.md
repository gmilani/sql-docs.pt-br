---
title: Operadores (sintaxe MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5067793ae0f5533a889973e18f7b300914df9092
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892111"
---
# <a name="operators-mdx-syntax"></a>Operadores (sintaxe MDX)


  Na linguagem MDX, os operadores permitem executar as seguintes ações:  
  
-   Alterar os dados, permanente ou temporariamente.  
  
-   Procurar valores ou objetos que atendam condições específicas.  
  
-   Implementar uma decisão entre valores ou expressões.  
  
-   Testar condições específicas antes de iniciar ou confirmar uma transação ou antes de executar instruções específicas.  
  
 O MDX oferece suporte para os operadores listados na tabela a seguir:  
  
|Para executar este tipo de operação|Use|  
|---------------------------------------|---------|  
|Atribuir um valor a uma variável ou associar uma coluna de conjunto de resultados a um alias.|[Operadores de atribuição](../mdx/assignment-operators.md)|  
|Adicionar, subtrair, multiplicar, dividir.|[Operadores aritméticos](../mdx/arithmetic-operators.md)|  
|Testar a legitimidade de uma condição, como AND, OR, NOT e XOR.|[Operadores bit a bit](../mdx/bitwise-operators.md)|  
|Comparar um valor com outro valor ou uma expressão.|[Operadores de comparação](../mdx/comparison-operators.md)|  
|Combinar permanente ou temporariamente duas cadeias de caracteres em uma.|[Operadores de concatenação](../mdx/concatenation-operators.md)|  
|Combinar permanente ou temporariamente duas expressões de conjunto em um único conjunto.|[Operadores de conjunto](../mdx/set-operators.md)|  
|Executar uma operação em um operando.|[Operadores unários](../mdx/unary-operators.md)|  
  
> [!NOTE]  
>  Em consultas, qualquer um que possa ver os dados no cubo a ser usado com algum tipo de operador pode executar operações. No entanto, você precisa ter as permissões apropriadas antes de poder alterar os dados com êxito.  
  
 Ao usar vários operadores, a ordem em que o MDX avalia os operadores é importante. Similarmente, o usuário dos operadores pode exigir que apenas um tipo de dados seja convertido em outro tipo de dados antes que os operadores possam ser avaliados.  
  
## <a name="evaluating-complex-expressions"></a>Avaliando expressões complexas  
 Você pode criar uma expressão usando os operadores para combinar várias expressões menores. Nessas expressões complexas, a linguagem MDX avalia os operadores em ordem com base na definição de precedência de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]operador usada pelo. O MDX executa os operadores com prioridade mais alta antes de executar os operadores com prioridade mais baixa.  
  
### <a name="understanding-operator-precedence"></a>Entendendo a prioridade dos operadores  
 A lista a seguir mostra a prioridade dos operadores, da mais alta para a mais baixa. Os operadores que estão na mesma linha têm a mesma prioridade e são avaliados da esquerda para a direita, a não ser que seja definido de outro modo pelos parênteses:  
  
-   IS  
  
-   AS  
  
-   DISTINCT  
  
-   :  
  
-   ^  
  
-   /, *  
  
-   +, -  
  
-   EXISTING  
  
-   <>, >=, =, \<=, >, <  
  
-   NOT  
  
-   AND  
  
-   XOR  
  
-   OU  
  
 Para obter mais informações sobre operadores em MDX, consulte MDX de [ &#40;referência&#41;de operador MDX](../mdx/mdx-operator-reference-mdx.md).  
  
### <a name="determining-results"></a>Determinando resultados  
 Ao combinar expressões simples para formar uma expressão complexa, as regras dos operadores combinadas com as regras de prioridade do tipo de dados determinam o tipo de dados do valor resultante.  
  
 Se o resultado for um caractere ou valor Unicode, as regras dos operadores combinadas com as regras de prioridade das ordenações determinam a ordenação do resultado. Para obter mais informações sobre agrupamentos, consulte [idiomas &#40;e agrupamentos&#41;Analysis Services](https://docs.microsoft.com/analysis-services/languages-and-collations-analysis-services).  
  
 Há também regras que determinam a precisão, a escala e a extensão do resultado, com base na precisão, na escala e na extensão das expressões simples.  
  
## <a name="converting-data-types"></a>Convertendo tipos de dados  
 O MDX converte implicitamente um objeto em um tipo diferente quando esse objeto é usado em uma expressão que requer um tipo diferente. A tabela a seguir define as regras de conversão para cada objeto.  
  
|Tipo original|Tipo necessário|Conversão|  
|-------------------|-----------------|----------------|  
|Nível|Defina|\<> de nível. Members|  
|Hierarquia|Membro|\<hierarchy>.defaultmember|  
|Membro|Tupla|(\<Membro >)|  
|Tupla|Membro|\<> de tupla. Item (0)|  
|Tupla|Escalar|\<> de tupla. valor|  
  
## <a name="see-also"></a>Consulte também  
 [MDX de referência &#40;de operador MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Elementos &#40;de sintaxe MDX MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
