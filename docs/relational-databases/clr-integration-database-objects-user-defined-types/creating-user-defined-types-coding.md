---
title: Codificando tipos definidos pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- validation [CLR integration]
- UDTs [CLR integration], coding
- UserDefined serialization format [CLR integration]
- Point UDT
- Parse method
- null values [CLR integration]
- ToString method
- ValidatePoint method
- attributes [CLR integration]
- coding user-defined types [CLR integration]
- Read method
- Write method
- nullability [CLR integration]
- user-defined types [CLR integration], coding
- Currency UDT
- validating UDT values
- exposing UDT properties [CLR integration]
ms.assetid: 1e5b43b3-4971-45ee-a591-3f535e2ac722
author: rothja
ms.author: jroth
ms.openlocfilehash: 9a26fb1282eb9181af9b1b04f40fd7f7c45c688a
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907464"
---
# <a name="creating-user-defined-types---coding"></a>Criar tipos definidos pelo usuário – Codificação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Ao codificar a definição UDT (tipo definido pelo usuário), você deve implementar vários recursos, dependendo da implementação da UDT como classe ou estrutura, bem como das opções de formato e de serialização escolhidas.  
  
 O exemplo nesta seção ilustra a implementação de um **ponto** UDT como uma **struct** (ou **estrutura** em Visual Basic). O **ponto** UDT consiste em coordenadas X e Y implementadas como procedimentos de propriedade.  
  
 Os seguintes namespaces são obrigatórios na definição de uma UDT:  
  
```vb  
Imports System  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
```  
  
```csharp  
using System;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
```  
  
 O namespace **Microsoft. SqlServer. Server** contém os objetos necessários para vários atributos de UDT, e o namespace **System. Data. SqlTypes** contém as classes que representam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados nativos disponíveis para o assembly. É claro que talvez haja namespaces adicionais necessários ao funcionamento correto do assembly. O **ponto** UDT também usa o namespace **System. Text** para trabalhar com cadeias de caracteres.  
  
> [!NOTE]  
>  Objetos C++ de banco de dados Visual, como UDTs, compilados com **/CLR: Pure** não têm suporte para execução.  
  
## <a name="specifying-attributes"></a>Especificando atributos  
 Os atributos determinam como a serialização é usada para construir a representação de armazenamento de UDTs e transmiti-los por valor para o cliente.  
  
 O **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** é necessário. O atributo **Serializable** é opcional. Você também pode especificar o **Microsoft. SqlServer. Server. SqlFacetAttribute** para fornecer informações sobre o tipo de retorno de um UDT. Para obter mais informações, confira [Atributos personalizados para rotinas do CLR (Common Language Runtime)](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md).  
  
### <a name="point-udt-attributes"></a>Atributos da UDT Point  
 O **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** define o formato de armazenamento para o **ponto** UDT como **nativo**. **IsByteOrdered** é definido como **true**, o que garante que os resultados das comparações sejam os mesmos em SQL Server como se a mesma comparação tivesse ocorrido em código gerenciado. O UDT implementa a interface **System. Data. SqlTypes. INullable** para tornar o UDT nulo ciente.  
  
 O fragmento de código a seguir mostra os atributos para o **ponto** UDT.  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True)> _  
  Public Structure Point  
    Implements INullable  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true)]  
public struct Point : INullable  
{  
```  
  
## <a name="implementing-nullability"></a>Implementando a nulidade  
 Além de especificar corretamente os atributos dos assemblies, a UDT também precisa oferecer suporte à nulidade. Os UDTs carregados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm reconhecimento de nulo, mas, para que o UDT reconheça um valor nulo, o UDT deve implementar a interface **System. Data. SqlTypes. INullable** .  
  
 Você deve criar uma propriedade chamada **IsNull**, que é necessária para determinar se um valor é nulo no código CLR. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontra uma instância nula de uma UDT, esta é mantida, usando métodos manipulação de nulos normais. O servidor não perde tempo serializando ou desserializando a UDT caso não precise, e ele não perde espaço armazenando uma UDT nula. Essa verificação de nulos é realizada sempre que uma UDT passa pelo CLR, o que significa que usar a construção [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL para verificar se há UDTs nulas deve funcionar sempre. A propriedade **IsNull** também é usada pelo servidor para testar se uma instância é nula. Quando determina que a UDT é nula, o servidor pode usar a manipulação de nulos nativa.  
  
 O método **Get ()** de **IsNull** não é especial em nenhuma forma. Se uma variável de **ponto** **\@p** for **NULL**, **\@p. IsNull** será, por padrão, avaliar como "NULL", e não "1". Isso ocorre porque o atributo **SqlMethod (OnNullCall)** do método **Get ()** do padrão IsNull é false. Como o objeto é **nulo**, quando a propriedade é solicitada, o objeto não é desserializado, o método não é chamado e um valor padrão de "NULL" é retornado.  
  
### <a name="example"></a>Exemplo  
 No seguinte exemplo, a variável `is_Null` é privada e mantém o estado de nulidade para a instância da UDT. O código deve manter um valor apropriado para `is_Null`. O UDT também deve ter uma propriedade estática denominada **NULL** que retorna uma instância de valor nulo de UDT. Isso permite que a UDT retorne um valor nulo caso a instância seja realmente nula no banco de dados.  
  
```vb  
Private is_Null As Boolean  
  
Public ReadOnly Property IsNull() As Boolean _  
   Implements INullable.IsNull  
    Get  
        Return (is_Null)  
    End Get  
End Property  
  
Public Shared ReadOnly Property Null() As Point  
    Get  
        Dim pt As New Point  
        pt.is_Null = True  
        Return (pt)  
    End Get  
End Property  
```  
  
```csharp  
private bool is_Null;  
  
public bool IsNull  
{  
    get  
    {  
        return (is_Null);  
    }  
}  
  
public static Point Null  
{  
    get  
    {  
        Point pt = new Point();  
        pt.is_Null = true;  
        return pt;  
    }  
}  
```  
  
### <a name="is-null-vs-isnull"></a>IS NULL X IsNull  
 Considere uma tabela que contém os pontos de esquema (id int, ponto de localização), em que **Point** é um CLR UDT e as seguintes consultas:  
  
```  
--Query 1  
SELECT ID  
FROM Points  
WHERE NOT (location IS NULL) -- Or, WHERE location IS NOT NULL;  
```  
  
```  
--Query 2:  
SELECT ID  
FROM Points  
WHERE location.IsNull = 0;  
```  
  
 Ambas as consultas retornam as IDs de pontos com locais não**nulos** . Na Consulta 1, é usada a manipulação de nulos normal, não havendo nenhuma desserialização das UDTs obrigatória. A consulta 2, por outro lado, precisa desserializar cada objeto não**nulo** e chamar o CLR para obter o valor da propriedade **IsNull** . Claramente, o uso de **is NULL** apresentará um melhor desempenho e nunca deve haver um motivo para ler a propriedade **IsNull** de um UDT de [!INCLUDE[tsql](../../includes/tsql-md.md)] código.  
  
 Então, qual é o uso da propriedade **IsNull** ? Primeiro, é necessário determinar se um valor é **nulo** no código CLR. Em segundo lugar, o servidor precisa de uma maneira de testar se uma instância é **nula**, portanto, essa propriedade é usada pelo servidor. Depois de determinar que ele é **nulo**, ele pode usar sua manipulação de NULL nativo para tratá-lo.  
  
## <a name="implementing-the-parse-method"></a>Implementando o método Parse  
 Os métodos **Parse** e **ToString** permitem conversões de e para representações de cadeia de caracteres do UDT. O método **Parse** permite que uma cadeia de caracteres seja convertida em UDT. Ele deve ser declarado como **estático** (ou **compartilhado** em Visual Basic) e pegar um parâmetro do tipo **System. Data. SqlTypes. SqlString**.  
  
 O código a seguir implementa o método **Parse** para o **ponto** UDT, que separa as coordenadas X e Y. O método **Parse** tem um único argumento do tipo **System. Data. SqlTypes. SqlString**e pressupõe que os valores X e Y sejam fornecidos como uma cadeia de caracteres delimitada por vírgula. Definir o atributo **Microsoft. SqlServer. Server. SqlMethodAttribute. OnNullCall** como **false** impede que o método **Parse** seja chamado a partir de uma instância nula de Point.  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
    return pt;  
}  
```  
  
## <a name="implementing-the-tostring-method"></a>Implementando o método ToString  
 O método **ToString** converte o **ponto** UDT em um valor de cadeia de caracteres. Nesse caso, a cadeia de caracteres "NULL" é retornada para uma instância nula do tipo **Point** . O método **ToString** reverte o método **Parse** usando um **System. Text. StringBuilder** para retornar um **sistema. String** delimitado por vírgulas que consistem nos valores de coordenadas X e Y. Como **InvokeIfReceiverIsNull** assume false como padrão, a verificação de uma instância nula de **Point** é desnecessária.  
  
```vb  
Private _x As Int32  
Private _y As Int32  
  
Public Overrides Function ToString() As String  
    If Me.IsNull Then  
        Return "NULL"  
    Else  
        Dim builder As StringBuilder = New StringBuilder  
        builder.Append(_x)  
        builder.Append(",")  
        builder.Append(_y)  
        Return builder.ToString  
    End If  
End Function  
```  
  
```csharp  
private Int32 _x;  
private Int32 _y;  
  
public override string ToString()  
{  
    if (this.IsNull)  
        return "NULL";  
    else  
    {  
        StringBuilder builder = new StringBuilder();  
        builder.Append(_x);  
        builder.Append(",");  
        builder.Append(_y);  
        return builder.ToString();  
    }  
}  
```  
  
## <a name="exposing-udt-properties"></a>Expondo propriedades da UDT  
 O **ponto** UDT expõe coordenadas X e Y que são implementadas como propriedades públicas de leitura/gravação do tipo **System. Int32**.  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _x = Value  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _y = Value  
    End Set  
End Property  
```  
  
```csharp  
public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    set   
    {  
        _x = value;  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        _y = value;  
    }  
}  
```  
  
## <a name="validating-udt-values"></a>Validando valores de UDT  
 Ao trabalhar com dados de UDT, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] converte automaticamente valores binários em valores de UDT. Esse processo de conversão envolve verificar se os valores são apropriados ao formato de serialização do tipo e garantir que o valor possa ser desserializado corretamente. Isso garante que o valor possa ser convertido de volta em formato binário. No caso das UDTs ordenadas por byte, isso também garante que o valor binário resultante corresponda ao valor binário original. Isso impede a manutenção de valores inválidos no banco de dados. Em alguns casos, esse nível de verificação pode ser inadequado. Talvez seja obrigatória uma validação adicional quando os valores de UDT devem estar em um domínio ou intervalo esperado. Por exemplo, uma UDT que implementa uma data pode exigir que o valor de dia seja um número positivo e que esteja em um determinado intervalo de valores válidos.  
  
 A propriedade **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute. ValidationMethodName** do **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** permite que você forneça o nome de um método de validação que o servidor executa Quando os dados são atribuídos a um UDT ou convertidos em UDT. **ValidationMethodName** também é chamado durante a execução das operações do utilitário bcp, BULK INSERT, DBCC CHECKDB, DBCC CHECKFILEGROUP, DBCC CHECKTABLE, consulta distribuída e RPC (chamada de procedimento remoto) TDS. O valor padrão de **ValidationMethodName** é NULL, indicando que não há nenhum método de validação.  
  
### <a name="example"></a>Exemplo  
 O fragmento de código a seguir mostra a declaração da classe **Point** , que especifica um **ValidationMethodName** de **ValidatePoint**.  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True, _  
  ValidationMethodName:="ValidatePoint")> _  
  Public Structure Point  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true,   
  ValidationMethodName = "ValidatePoint")]  
public struct Point : INullable  
{  
```  
  
 Caso seja especificado, um método de validação deve ter uma assinatura semelhante ao seguinte fragmento de código.  
  
```vb  
Private Function ValidationFunction() As Boolean  
    If (validation logic here) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidationFunction()  
{  
    if (validation logic here)  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
 O método de validação pode ter qualquer escopo e deve retornar **true** se o valor for válido e **false** caso contrário. Se o método retornar **false** ou lançar uma exceção, o valor será tratado como inválido e um erro será gerado.  
  
 No exemplo abaixo, o código só permite valores iguais a zero ou maiores que as coordenadas X e Y.  
  
```vb  
Private Function ValidatePoint() As Boolean  
    If (_x >= 0) And (_y >= 0) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidatePoint()  
{  
    if ((_x >= 0) && (_y >= 0))  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
### <a name="validation-method-limitations"></a>Limitações do método de validação  
 O servidor chama o método de validação ao realizar conversões, e não quando os dados são inseridos definindo propriedades individuais, ou quando eles são inseridos usando uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT.  
  
 Você deve chamar explicitamente o método de validação de setters de propriedade e o método **Parse** se desejar que o método de validação seja executado em todas as situações. Não se trata de um requisito e, em alguns casos, talvez não seja sequer desejável.  
  
### <a name="parse-validation-example"></a>Exemplo de validação de Parse  
 Para garantir que o método **ValidatePoint** seja invocado na classe **Point** , você deve chamá-lo do método **Parse** e dos procedimentos de propriedade que definem os valores de coordenadas X e Y. O fragmento de código a seguir mostra como chamar o método de validação **ValidatePoint** da função **Parse** .  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
  
    ' Call ValidatePoint to enforce validation  
    ' for string conversions.  
    If Not pt.ValidatePoint() Then  
        Throw New ArgumentException("Invalid XY coordinate values.")  
    End If  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
  
    // Call ValidatePoint to enforce validation  
    // for string conversions.  
    if (!pt.ValidatePoint())   
        throw new ArgumentException("Invalid XY coordinate values.");  
    return pt;  
}  
```  
  
### <a name="property-validation-example"></a>Exemplo de validação da propriedade  
 O fragmento de código a seguir mostra como chamar o método de validação **ValidatePoint** a partir dos procedimentos de propriedade que definem as coordenadas X e Y.  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _x  
        _x = Value  
        If Not ValidatePoint() Then  
            _x = temp  
            Throw New ArgumentException("Invalid X coordinate value.")  
        End If  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _y  
        _y = Value  
        If Not ValidatePoint() Then  
            _y = temp  
            Throw New ArgumentException("Invalid Y coordinate value.")  
        End If  
    End Set  
End Property  
```  
  
```csharp  
    public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    // Call ValidatePoint to ensure valid range of Point values.  
    set   
    {  
        Int32 temp = _x;  
        _x = value;  
        if (!ValidatePoint())  
        {  
            _x = temp;  
            throw new ArgumentException("Invalid X coordinate value.");  
        }  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        Int32 temp = _y;  
        _y = value;  
        if (!ValidatePoint())  
        {  
            _y = temp;  
            throw new ArgumentException("Invalid Y coordinate value.");  
        }  
    }  
}  
```  
  
## <a name="coding-udt-methods"></a>Codificando métodos de UDT  
 Durante a codificação dos métodos de UDT, considere se o algoritmo usado pode ser alterado com o passar do tempo. Em caso positivo, você talvez queira considerar a criação de uma classe separada para os métodos usados pela UDT. Caso o algoritmo seja alterado, é possível recompilar a classe com o novo código e carregar o assembly em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem afetar a UDT. Em muitos casos, as UDTs podem ser recarregadas usando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY, mas isso pode causar problemas nos dados existentes. Por exemplo, o UDT de **moeda** incluído com o banco de dados de exemplo **AdventureWorks** usa uma função **ConvertCurrency** para converter valores de moeda, que são implementados em uma classe separada. É possível que algoritmos de conversão sejam alterados de maneiras imprevisíveis no futuro, ou que uma nova funcionalidade seja obrigatória. Separar a função **ConvertCurrency** da implementação de UDT de **moeda** fornece maior flexibilidade ao planejar alterações futuras.  
  
### <a name="example"></a>Exemplo  
 A classe **Point** contém três métodos simples para calcular a distância: **Distance**, **DistanceFrom** e **DistanceFromXY**. Cada retorna um **Double** calculando a distância de **ponto** para zero, a distância de um ponto especificado até o **ponto**e a distância das coordenadas X e Y especificadas a serem **apontadas**. **Distância** e **DistanceFrom** cada chamada **DistanceFromXY**e demonstram como usar argumentos diferentes para cada método.  
  
```vb  
' Distance from 0 to Point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function Distance() As Double  
    Return DistanceFromXY(0, 0)  
End Function  
  
' Distance from Point to the specified point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFrom(ByVal pFrom As Point) As Double  
    Return DistanceFromXY(pFrom.X, pFrom.Y)  
End Function  
  
' Distance from Point to the specified x and y values.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFromXY(ByVal ix As Int32, ByVal iy As Int32) _  
    As Double  
    Return Math.Sqrt(Math.Pow(ix - _x, 2.0) + Math.Pow(iy - _y, 2.0))  
End Function  
```  
  
```csharp  
// Distance from 0 to Point.  
[SqlMethod(OnNullCall = false)]  
public Double Distance()  
{  
    return DistanceFromXY(0, 0);  
}  
  
// Distance from Point to the specified point.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFrom(Point pFrom)  
{  
    return DistanceFromXY(pFrom.X, pFrom.Y);  
}  
  
// Distance from Point to the specified x and y values.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFromXY(Int32 iX, Int32 iY)  
{  
    return Math.Sqrt(Math.Pow(iX - _x, 2.0) + Math.Pow(iY - _y, 2.0));  
}  
```  
  
### <a name="using-sqlmethod-attributes"></a>Usando atributos SqlMethod  
 A classe **Microsoft. SqlServer. Server. SqlMethodAttribute** fornece atributos personalizados que podem ser usados para marcar definições de método a fim de especificar o determinante, o comportamento de chamada nula e especificar se um método é um modificador. Os valores padrão dessas propriedades são pressupostos, e o atributo personalizado só é usado quando um valor não padrão é necessário.  
  
> [!NOTE]  
>  A classe **SqlMethodAttribute** herda da classe **SqlFunctionAttribute** , portanto **SqlMethodAttribute** herda os campos **FillRowMethodName** e **TableDefinition** de **SqlFunctionAttribute**. Isso indica que é possível escrever um método com valor de tabela, o que não é o caso. O método é compilado e o assembly é implantado, mas um erro sobre o tipo de retorno **IEnumerable** é gerado em tempo de execução com a seguinte mensagem: "método, propriedade ou campo"\<nome > "na classe"\<classe > "no assembly"\<o assembly > ' tem um tipo de retorno inválido. "  
  
 A tabela a seguir descreve algumas das propriedades relevantes do **Microsoft. SqlServer. Server. SqlMethodAttribute** que podem ser usadas em métodos UDT e lista seus valores padrão.  
  
 DataAccess  
 Indica se a função envolve o acesso a dados de usuário armazenados na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O padrão é **DataAccessKind**. **Nenhum**.  
  
 IsDeterministic  
 Indica se a função produz os mesmos valores de saída, dados os mesmos valores de entrada e o mesmo estado de banco de dados. O padrão é **false**.  
  
 IsMutator  
 Indica se o método causa uma alteração de estado na instância da UDT. O padrão é **false**.  
  
 IsPrecise  
 Indica se a função envolve computações imprecisas como, por exemplo, operações de ponto flutuante. O padrão é **false**.  
  
 OnNullCall  
 Indica se o método é chamado quando são especificados argumentos de entrada de referência nulos. O padrão é **true**.  
  
### <a name="example"></a>Exemplo  
 A propriedade **Microsoft. SqlServer. Server. SqlMethodAttribute. IsMutator** permite marcar um método que permite uma alteração no estado de uma instância de UDT. A [!INCLUDE[tsql](../../includes/tsql-md.md)] não permite definir duas propriedades de UDT na cláusula SET de uma instrução UPDATE. No entanto, é possível ter um método marcado como um modificador que altera os dois membros.  
  
> [!NOTE]  
>  Os métodos Mutator não são permitidos em consultas. Eles só podem ser chamados em instruções de atribuição ou de modificação de dados. Se um método marcado como modificador não retornar **void** (ou não for um **sub** no Visual Basic), criar tipo falhará com um erro.  
  
 A instrução a seguir pressupõe a existência de um UDT de **triângulos** que tem um método **Rotate** . A instrução UPDATE [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir invoca o método **Rotate** :  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 O método **Rotate** é decorado com o atributo **SqlMethod** definindo **IsMutator** como **true** para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possa marcar o método como um método modificador. O código também define **OnNullCall** como **false**, que indica ao servidor que o método retorna uma referência nula (**Nothing** em Visual Basic) se qualquer um dos parâmetros de entrada forem referências nulas.  
  
```vb  
<SqlMethod(IsMutator:=True, OnNullCall:=False)> _  
Public Sub Rotate(ByVal anglex as Double, _  
  ByVal angley as Double, ByVal anglez As Double)   
   RotateX(anglex)  
   RotateY(angley)  
   RotateZ(anglez)  
End Sub  
```  
  
```csharp  
[SqlMethod(IsMutator = true, OnNullCall = false)]  
public void Rotate(double anglex, double angley, double anglez)   
{  
   RotateX(anglex);  
   RotateY(angley);  
   RotateZ(anglez);  
}  
```  
  
## <a name="implementing-a-udt-with-a-user-defined-format"></a>Implementando uma UDT com um formato definido pelo usuário  
 Ao implementar um UDT com um formato definido pelo usuário, você deve implementar métodos de **leitura** e **gravação** que implementam a interface Microsoft. SqlServer. Server. ibinaryserializedmd para lidar com a serialização e desserialização de dados UDT. Você também deve especificar a propriedade **MaxByteSize** do **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute**.  
  
### <a name="the-currency-udt"></a>A UDT Currency  
 O UDT de **moeda** está incluído com os exemplos de CLR que podem ser instalados com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 A **moeda** UDT dá suporte à manipulação de quantias de dinheiro no sistema monetário de uma cultura específica. Você deve definir dois campos: uma **cadeia de caracteres** para **CultureInfo**, que especifica quem emitiu a moeda (en-US, por exemplo) e um **decimal** para **CurrencyValue**, a quantidade de dinheiro.  
  
 Embora não seja usado pelo servidor para executar comparações, a **moeda** UDT implementa a interface **System. IComparable** , que expõe um único método, **System. IComparable. CompareTo**. Isso é usado do lado de cliente, em situações nas quais é desejável comparar com precisão ou ordenar valores de moeda dentro de culturas.  
  
 O código em execução no CLR compara a cultura separadamente do valor de moeda. Para o código [!INCLUDE[tsql](../../includes/tsql-md.md)], as seguintes ações determinam a comparação:  
  
1.  Defina o atributo **IsByteOrdered** como true, que informa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usar a representação binária persistente em disco para comparações.  
  
2.  Use o método de **gravação** para o UDT da **moeda** para determinar como o UDT é persistido no disco e, portanto, como os valores UDT são comparados e ordenados para operações de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
3.  Salve a **moeda** UDT usando o seguinte formato binário:  

    1.  Salve a cultura como uma cadeia de caracteres codificada UTF-16 para bytes de 0 a 19 com preenchimento à direita com caracteres nulos.  
  
    2.  Use bytes 20 e acima para conter o valor decimal da moeda.  
  
 O propósito do preenchimento é assegurar que a cultura seja totalmente separada do valor de moeda, para que quando uma UDT seja comparada com outra no código [!INCLUDE[tsql](../../includes/tsql-md.md)], os bytes de cultura sejam comparados com os bytes de cultura e os valores de byte da moeda, com os valores de byte da moeda.  
  
 Para obter a listagem de código completa para o UDT de **moeda** , siga as instruções para instalar os exemplos de CLR em [exemplos de mecanismo de banco de dados de SQL Server](https://msftengprodsamples.codeplex.com/).  
  
### <a name="currency-attributes"></a>Atributos Currency  
 O UDT de **moeda** é definido com os seguintes atributos.  
  
```vb  
<Serializable(), Microsoft.SqlServer.Server.SqlUserDefinedType( _  
    Microsoft.SqlServer.Server.Format.UserDefined, _  
    IsByteOrdered:=True, MaxByteSize:=32), _  
    CLSCompliant(False)> _  
Public Structure Currency  
Implements INullable, IComparable, _  
Microsoft.SqlServer.Server.IBinarySerialize  
```  
  
```csharp  
[Serializable]  
[SqlUserDefinedType(Format.UserDefined,   
    IsByteOrdered = true, MaxByteSize = 32)]  
    [CLSCompliant(false)]  
    public struct Currency : INullable, IComparable, IBinarySerialize  
    {  
```  
  
## <a name="creating-read-and-write-methods-with-ibinaryserialize"></a>Criando métodos Read e Write com IBinarySerialize  
 Ao escolher o formato de serialização **UserDefined** , você também deve implementar a interface **ibinaryserializedmd** e criar seus próprios métodos de **leitura** e **gravação** . Os procedimentos a seguir da **moeda** UDT usam **System. IO. BinaryReader** e **System. IO. BinaryWriter** para ler e gravar no UDT.  
  
```vb  
' IBinarySerialize methods  
' The binary layout is as follow:  
'    Bytes 0 - 19: Culture name, padded to the right with null  
'    characters, UTF-16 encoded  
'    Bytes 20+: Decimal value of money  
' If the culture name is empty, the currency is null.  
Public Sub Write(ByVal w As System.IO.BinaryWriter) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Write  
    If Me.IsNull Then  
        w.Write(nullMarker)  
        w.Write(System.Convert.ToDecimal(0))  
        Return  
    End If  
  
    If cultureName.Length > cultureNameMaxSize Then  
        Throw New ApplicationException(String.Format(CultureInfo.CurrentUICulture, _  
           "{0} is an invalid culture name for currency as it is too long.", cultureNameMaxSize))  
    End If  
  
    Dim paddedName As String = cultureName.PadRight(cultureNameMaxSize, CChar(vbNullChar))  
  
    For i As Integer = 0 To cultureNameMaxSize - 1  
        w.Write(paddedName(i))  
    Next i  
  
    ' Normalize decimal value to two places  
    currencyVal = Decimal.Floor(currencyVal * 100) / 100  
    w.Write(currencyVal)  
End Sub  
  
Public Sub Read(ByVal r As System.IO.BinaryReader) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Read  
    Dim name As Char() = r.ReadChars(cultureNameMaxSize)  
    Dim stringEnd As Integer = Array.IndexOf(name, CChar(vbNullChar))  
  
    If stringEnd = 0 Then  
        cultureName = Nothing  
        Return  
    End If  
  
    cultureName = New String(name, 0, stringEnd)  
    currencyVal = r.ReadDecimal()  
End Sub  
  
```  
  
```csharp  
// IBinarySerialize methods  
// The binary layout is as follow:  
//    Bytes 0 - 19:Culture name, padded to the right   
//    with null characters, UTF-16 encoded  
//    Bytes 20+:Decimal value of money  
// If the culture name is empty, the currency is null.  
public void Write(System.IO.BinaryWriter w)  
{  
    if (this.IsNull)  
    {  
        w.Write(nullMarker);  
        w.Write((decimal)0);  
        return;  
    }  
  
    if (cultureName.Length > cultureNameMaxSize)  
    {  
        throw new ApplicationException(string.Format(  
            CultureInfo.InvariantCulture,   
            "{0} is an invalid culture name for currency as it is too long.",   
            cultureNameMaxSize));  
    }  
  
    String paddedName = cultureName.PadRight(cultureNameMaxSize, '\0');  
    for (int i = 0; i < cultureNameMaxSize; i++)  
    {  
        w.Write(paddedName[i]);  
    }  
  
    // Normalize decimal value to two places  
    currencyValue = Decimal.Floor(currencyValue * 100) / 100;  
    w.Write(currencyValue);  
}  
public void Read(System.IO.BinaryReader r)  
{  
    char[] name = r.ReadChars(cultureNameMaxSize);  
    int stringEnd = Array.IndexOf(name, '\0');  
  
    if (stringEnd == 0)  
    {  
        cultureName = null;  
        return;  
    }  
  
    cultureName = new String(name, 0, stringEnd);  
    currencyValue = r.ReadDecimal();  
}  
```  
  
 Para obter a listagem de código completa para o UDT da **moeda** , consulte [SQL Server mecanismo de banco de dados Samples](https://msftengprodsamples.codeplex.com/).  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um tipo definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
