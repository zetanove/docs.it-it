---
title: Conversione di tipi
description: Conversione di tipi
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/22/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: c9a53222-89cb-47e5-983d-4f0f204e31ba
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 9f3f0dc381f8892dfb24d027ccc1f46a9b89135a

---

# <a name="type-conversion"></a>Conversione di tipi

A ogni valore è associato un tipo che definisce attributi quali la quantità di spazio allocato per il valore, l'intervallo di valori possibili supportati e i membri resi disponibili. Numerosi valori possono essere espressi mediante tipi diversi. Il valore `4`, ad esempio, può essere espresso come intero o come valore a virgola mobile. Mediante la conversione di tipi viene creato un valore in un nuovo tipo equivalente al valore del tipo precedente, ma non viene necessariamente mantenuta l'identità, o il valore esatto, dell'oggetto originale.

.NET supporta automaticamente le conversioni seguenti:

* Conversione da una classe derivata a una classe di base. Ciò significa ad esempio che un'istanza di qualsiasi classe o struttura può essere convertita in un'istanza [Object](xref:System.Object). Questa conversione non richiede un operatore di cast.

* Conversione da una classe di base a classe derivata originale. In C#, questa conversione richiede un operatore di cast. In Visual Basic, è necessario l'operatore `CType` se `Option Strict` è attivo. 

* Conversione da un tipo che implementa un'interfaccia a un oggetto di interfaccia che rappresenta tale interfaccia. Questa conversione non richiede un operatore di cast.

* Conversione da un oggetto di interfaccia al tipo originale che implementa l'interfaccia. In C#, questa conversione richiede un operatore di cast. In Visual Basic, è necessario l'operatore `CType` se `Option Strict` è attivo. 

Oltre a queste conversioni automatiche, .NET offre diverse funzionalità che supportano la conversione di tipo personalizzato. tra cui: 

* Operatore `Implicit` che definisce le conversioni tra tipi verso un tipo di dati più grande. Per altre informazioni, vedere la sezione [Conversione implicita con l'operatore Implicit](#implicit-conversion-with-the-implicit-operator).

* Operatore `Explicit` che definisce le conversioni tra tipi verso un tipo di dati più piccolo. Per altre informazioni, vedere la sezione [Conversione esplicita con l'operatore Explicit](#explicit-conversion-with-the-explicit-operator).

* Interfaccia [IConvertible](xref:System.IConvertible) che definisce le conversioni in ognuno dei tipi di dati .NET di base. Per altre informazioni, vedere la sezione [Interfaccia IConvertible](#the-iconvertible-interface).

* Classe [Convert](xref:System.Convert) che offre un set di metodi che implementano i metodi nell'interfaccia `IConvertible`. Per altre informazioni, vedere la sezione [Classe Convert](#the-convert-class).

* Classe [TypeConverter](xref:System.ComponentModel.TypeConverter), una classe di base che può essere estesa per supportare la conversione di un tipo specifico in qualsiasi altro tipo. Per altre informazioni, vedere la sezione [Classe TypeConverter](#the-typeconverter-class).

## <a name="implicit-conversion-with-the-implicit-operator"></a>Conversione implicita con l'operatore Implicit

Le conversioni verso un tipo di dati più grande comportano la creazione di un nuovo valore dal valore di un tipo esistente che dispone di un intervallo più restrittivo o di un elenco di membri più limitato rispetto al tipo di destinazione. Le conversioni verso un tipo di dati più grande non possono comportare perdita di dati, ma è possibile che comportino una perdita di precisione. Poiché i dati non possono venire persi, i compilatori possono gestire la conversione in modo implicito o trasparente, senza la necessità di utilizzare un metodo di conversione esplicito o un operatore di cast.

> [!NOTE]
> Sebbene il codice che esegue una conversione esplicita sia in grado di chiamare un metodo di conversione o di utilizzare un operatore di cast, l'utilizzo di tali elementi non è richiesto dai compilatori che supportano le conversioni implicite.

Ad esempio, il tipo [Decimal](xref:System.Decimal) supporta conversioni implicite da valori [Byte](xref:System.Byte), [Char](xref:System.Char), [Int16](xref:System.Int16), [Int32](xref:System.Int32), [Int64](xref:System.Int64), [SByte](xref:System.SByte), [UInt16](xref:System.UInt16), [UInt32](xref:System.UInt32) e [UInt64](xref:System.UInt64). Nell'esempio seguente vengono illustrate alcune conversioni implicite nell'assegnazione di valori a una variabile `Decimal`.

```csharp
byte byteValue = 16;
short shortValue = -1024;
int intValue = -1034000;
long longValue = 1152921504606846976;
ulong ulongValue = UInt64.MaxValue;

decimal decimalValue;

decimalValue = byteValue;
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.", 
                  byteValue.GetType().Name, decimalValue); 

decimalValue = shortValue;
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.", 
                  shortValue.GetType().Name, decimalValue); 

decimalValue = intValue;
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.", 
                  intValue.GetType().Name, decimalValue); 

decimalValue = longValue;
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.", 
                  longValue.GetType().Name, decimalValue); 

decimalValue = ulongValue;
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.", 
                  longValue.GetType().Name, decimalValue); 
// The example displays the following output:
//    After assigning a Byte value, the Decimal value is 16.
//    After assigning a Int16 value, the Decimal value is -1024.
//    After assigning a Int32 value, the Decimal value is -1034000.
//    After assigning a Int64 value, the Decimal value is 1152921504606846976.
//    After assigning a Int64 value, the Decimal value is 18446744073709551615.
```

```vb
Dim byteValue As Byte = 16
Dim shortValue As Short = -1024
Dim intValue As Integer = -1034000
Dim longValue As Long = CLng(1024^6)
Dim ulongValue As ULong = ULong.MaxValue

Dim decimalValue As Decimal

decimalValue = byteValue
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.",
                  byteValue.GetType().Name, decimalValue) 

decimalValue = shortValue
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.",
                  shortValue.GetType().Name, decimalValue) 

decimalValue = intValue
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.",
                  intValue.GetType().Name, decimalValue) 

decimalValue = longValue
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.",
                  longValue.GetType().Name, decimalValue) 

decimalValue = ulongValue
Console.WriteLine("After assigning a {0} value, the Decimal value is {1}.",
                  longValue.GetType().Name, decimalValue) 
' The example displays the following output:
'    After assigning a Byte value, the Decimal value is 16.
'    After assigning a Int16 value, the Decimal value is -1024.
'    After assigning a Int32 value, the Decimal value is -1034000.
'    After assigning a Int64 value, the Decimal value is 1152921504606846976.
'    After assigning a Int64 value, the Decimal value is 18446744073709551615.
```

Se un determinato compilatore di linguaggio supporta gli operatori personalizzati, è anche possibile definire le conversioni implicite nei tipi personalizzati. Nell'esempio seguente viene fornita un'implementazione parziale di un tipo di dati Signed Byte denominato `ByteWithSign` che utilizza la rappresentazione di segno e grandezza. Il tipo supporta la conversione implicita di valori [Byte](xref:System.Byte) e [SByte](xref:System.SByte) in valori `ByteWithSign`.

```csharp
public struct ByteWithSign
{
   private SByte signValue; 
   private Byte value;

   public static implicit operator ByteWithSign(SByte value) 
   {
      ByteWithSign newValue;
      newValue.signValue = (SByte) Math.Sign(value);
      newValue.value = (byte) Math.Abs(value);
      return newValue;
   }  

   public static implicit operator ByteWithSign(Byte value)
   {
      ByteWithSign  newValue;
      newValue.signValue = 1;
      newValue.value = value;
      return newValue;
   }

   public override string ToString()
   { 
      return (signValue * value).ToString();
   }
}
```

```vb
Public Structure ByteWithSign
   Private signValue As SByte 
   Private value As Byte

   Public Overloads Shared Widening Operator CType(value As SByte) As ByteWithSign
      Dim newValue As ByteWithSign
      newValue.signValue = CSByte(Math.Sign(value))
      newValue.value = CByte(Math.Abs(value))
      Return newValue
   End Operator  

   Public Overloads Shared Widening Operator CType(value As Byte) As ByteWithSign
      Dim NewValue As ByteWithSign
      newValue.signValue = 1
      newValue.value = value
      Return newValue
   End Operator

   Public Overrides Function ToString() As String 
      Return (signValue * value).ToString()
   End Function
End Structure
```

Il codice client può quindi dichiarare una variabile `ByteWithSign` e assegnare alla variabile valori [Byte](xref:System.Byte) e [SByte](xref:System.SByte) senza eseguire alcuna conversione esplicita né usare operatori di cast, come visualizzato nell'esempio seguente.

```csharp
SByte sbyteValue = -120;
ByteWithSign value = sbyteValue;
Console.WriteLine(value);
value = Byte.MaxValue;
Console.WriteLine(value);
// The example displays the following output:
//       -120
//       255
```

```vb
Dim sbyteValue As SByte = -120
Dim value As ByteWithSign = sbyteValue
Console.WriteLine(value.ToString()) 
value = Byte.MaxValue
Console.WriteLine(value.ToString()) 
' The example displays the following output:
'       -120
'       255
```

## <a name="explicit-conversion-with-the-explicit-operator"></a>Conversione esplicita con l'operatore Explicit

Le conversioni verso un tipo di dati più piccolo comportano la creazione di un nuovo valore dal valore di un tipo esistente che dispone di un intervallo più ampio o di un elenco di membri più grande rispetto al tipo di destinazione. Poiché una conversione verso un tipo di dati più piccolo può comportare una perdita di dati, i compilatori spesso richiedono che tale conversione sia resa esplicita tramite una chiamata a un metodo di conversione o a un operatore di cast. È quindi necessario gestire la conversione in modo esplicito nel codice dello sviluppatore. 

> [!NOTE]
> Lo scopo principale della richiesta di un metodo di conversione o di un operatore di cast per le conversioni verso un tipo di dati più piccolo è rendere lo sviluppatore consapevole della possibilità di perdita dei dati o del verificarsi di un'eccezione [OverflowException](xref:System.OverflowException), in modo che tale eventualità venga gestita nel codice. In alcuni compilatori tuttavia questo requisito non è sempre rispettato. In Visual Basic, ad esempio, se l'opzione `Option Strict` è disattivata (impostazione predefinita), il compilatore tenta di eseguire le conversioni verso un tipo di dati più piccolo in modo implicito.

Ad esempio i tipi di dati [UInt32](xref:System.UInt32), [Int64](xref:System.Int64) e [UInt64](xref:System.UInt64) hanno intervalli più ampi del tipo di dati [Int32](xref:System.Int32), come illustrato nella tabella seguente.

Tipo | Confronto con intervallo di Int32
---- | ------------------------------
[Int64](xref:System.Int64) | [Int64. MaxValue](xref:System.Int64.MaxValue) è maggiore di [Int32. MaxValue](xref:System.Int32#System_Int32_MaxValue) e [Int64.MinValue](xref:System.Int64.MinValue) è minore di (dispone di un intervallo negativo più ampio di) [Int32.MinValue](xref:System.Int32#System_Int32_MinValue).
[UInt32](xref:System.UInt32) | [UInt32.MaxValue](xref:System.UInt32.MaxValue) è maggiore di [Int32. MaxValue](xref:System.Int32.MaxValue).
[UInt64](xref:System.UInt64) | [UInt64.MaxValue](xref:System.UInt64.MaxValue) è maggiore di [Int32. MaxValue](xref:System.Int32.MaxValue).

Per gestire le conversioni verso un tipo di dati più piccolo, .NET consente ai tipi di definire un operatore `Explicit`. I singoli compilatori di linguaggio possono quindi implementare questo operatore usando la propria sintassi oppure è possibile chiamare un membro della classe [Convert](xref:System.Convert) per eseguire la conversione. Per altre informazioni sulla classe `Convert`, vedere la sezione [Classe Convert](#the-convert-class) più avanti in questo argomento. L'esempio seguente illustra l'uso delle funzionalità del linguaggio per gestire la conversione esplicita di questi valori Integer potenzialmente esterni all'intervallo in valori [Int32](xref:System.Int32). 

```csharp
long number1 = int.MaxValue + 20L;
uint number2 = int.MaxValue - 1000;
ulong number3 = int.MaxValue;

int intNumber;

try {
   intNumber = checked((int) number1);
   Console.WriteLine("After assigning a {0} value, the Integer value is {1}.", 
                     number1.GetType().Name, intNumber); 
}
catch (OverflowException) {
   if (number1 > int.MaxValue)
      Console.WriteLine("Conversion failed: {0} exceeds {1}.", 
                        number1, int.MaxValue);
   else
      Console.WriteLine("Conversion failed: {0} is less than {1}.", 
                        number1, int.MinValue);
}

try {
   intNumber = checked((int) number2);
   Console.WriteLine("After assigning a {0} value, the Integer value is {1}.", 
                     number2.GetType().Name, intNumber); 
}
catch (OverflowException) {
   Console.WriteLine("Conversion failed: {0} exceeds {1}.", 
                     number2, int.MaxValue);
}

try {
   intNumber = checked((int) number3);
   Console.WriteLine("After assigning a {0} value, the Integer value is {1}.", 
                     number3.GetType().Name, intNumber); 
}
catch (OverflowException) {
   Console.WriteLine("Conversion failed: {0} exceeds {1}.", 
                     number1, int.MaxValue);
}

// The example displays the following output:
//    Conversion failed: 2147483667 exceeds 2147483647.
//    After assigning a UInt32 value, the Integer value is 2147482647.
//    After assigning a UInt64 value, the Integer value is 2147483647.
```

```vb
Dim number1 As Long = Integer.MaxValue + 20L
Dim number2 As UInteger = Integer.MaxValue - 1000
Dim number3 As ULong = Integer.MaxValue

Dim intNumber As Integer

Try
   intNumber = CInt(number1)
   Console.WriteLine("After assigning a {0} value, the Integer value is {1}.", 
                       number1.GetType().Name, intNumber)
Catch e As OverflowException
   If number1 > Integer.MaxValue Then
      Console.WriteLine("Conversion failed: {0} exceeds {1}.", 
                                        number1, Integer.MaxValue)
   Else
      Console.WriteLine("Conversion failed: {0} is less than {1}.\n", 
                                        number1, Integer.MinValue)
   End If
End Try

Try
   intNumber = CInt(number2)
   Console.WriteLine("After assigning a {0} value, the Integer value is {1}.", 
                       number2.GetType().Name, intNumber)
Catch e As OverflowException
   Console.WriteLine("Conversion failed: {0} exceeds {1}.", 
                                     number2, Integer.MaxValue)
End Try

Try
   intNumber = CInt(number3)
   Console.WriteLine("After assigning a {0} value, the Integer value is {1}.", 
                       number3.GetType().Name, intNumber)
Catch e As OverflowException
   Console.WriteLine("Conversion failed: {0} exceeds {1}.",
                                     number1, Integer.MaxValue)
End Try
' The example displays the following output:
'    Conversion failed: 2147483667 exceeds 2147483647.
'    After assigning a UInt32 value, the Integer value is 2147482647.
'    After assigning a UInt64 value, the Integer value is 2147483647.
```

Le conversioni esplicite possono produrre risultati diversi in linguaggi diversi e tali risultati possono differire dal valore restituito dal metodo [Convert](xref:System.Convert) corrispondente. Se ad esempio il valore [Double](xref:System.Double) **12.63251** viene convertito in [Int32](xref:System.Int32), sia il metodo .NET [Convert.ToInt32(Double)](xref:System.Convert.ToInt32(System.Double)) sia il metodo Visual Basic `CInt` arrotondano il valore [Double](xref:System.Double) per restituire **13**, ma l'operatore C# `(int)` tronca il valore [Double](xref:System.Double) e restituisce **12**. Analogamente, l'operatore C# `(int)` non supporta la conversione da valore booleano a valore intero, mentre il metodo Visual Basic `CInt` consente di convertire un valore `true` in **-1**. Per contro, il metodo [Convert.ToInt32(Boolean)](xref:System.Convert.ToInt32(System.Boolean)) consente di convertire un valore `true` in **1**.

La maggior parte dei compilatori consente l'esecuzione di conversioni esplicite in modalità controllata o non controllata. Quando viene eseguita una conversione controllata, viene generato un evento [OverflowException](xref:System.OverflowException) se il valore del tipo da convertire non rientra nell'intervallo del tipo di destinazione. Quando viene eseguita una conversione non controllata nelle stesse condizioni, potrebbe non venire generata un'eccezione, ma il comportamento esatto della conversione risulterà non definito e potrebbe venire restituito un valore non corretto.

> [!NOTE]
> In C# è possibile eseguire conversioni controllate utilizzando la parola chiave `checked` con l'operatore di cast o specificando l'opzione del compilatore `/checked+`. Viceversa, le conversioni in modalità non controllata possono essere eseguite utilizzando la parola chiave `unchecked` con l'operatore di cast o specificando l'opzione del compilatore `/checked-`. Per impostazione predefinita, le conversioni esplicite vengono eseguite in modalità non controllata. In Visual Basic, le conversioni controllate possono essere eseguite specificando l'opzione del compilatore `/removeintchecks-`. Per contro, le conversioni non controllate possono essere eseguite specificando l'opzione del compilatore `/removeintchecks+`. Per impostazione predefinita, le conversioni esplicite vengono eseguite in modalità controllata.

Nell'esempio C# seguente vengono usate le parole chiave `checked` e `unchecked` per illustrare la differenza nel comportamento quando un valore al di fuori dell'intervallo di un tipo [Byte](xref:System.Byte) viene convertito in `Byte`. La conversione controllata genera un'eccezione, mentre la conversione non controllata assegna [Byte.MaxValue](xref:System.Byte.MaxValue) alla variabile `Byte`.

```csharp
int largeValue = Int32.MaxValue;
byte newValue;

try {
   newValue = unchecked((byte) largeValue);
   Console.WriteLine("Converted the {0} value {1} to the {2} value {3}.", 
                     largeValue.GetType().Name, largeValue,
                     newValue.GetType().Name, newValue);
}
catch (OverflowException) {
   Console.WriteLine("{0} is outside the range of the Byte data type.", 
                     largeValue);
}

try {
   newValue = checked((byte) largeValue);
   Console.WriteLine("Converted the {0} value {1} to the {2} value {3}.", 
                     largeValue.GetType().Name, largeValue,
                     newValue.GetType().Name, newValue);
}
catch (OverflowException) {
   Console.WriteLine("{0} is outside the range of the Byte data type.", 
                     largeValue);
}
// The example displays the following output:
//    Converted the Int32 value 2147483647 to the Byte value 255.
//    2147483647 is outside the range of the Byte data type.
```

Se un determinato compilatore di linguaggio supporta gli operatori di overload personalizzati, è anche possibile definire conversioni esplicite nei tipi personalizzati. Nell'esempio seguente viene fornita un'implementazione parziale di un tipo di dati Signed Byte denominato `ByteWithSign` che utilizza la rappresentazione di segno e grandezza. Il tipo supporta la conversione esplicita di valori [Int32](xref:System.Int32) e [UInt32](xref:System.UInt32) in valori `ByteWithSign`.

```csharp
public struct ByteWithSign
{
   private SByte signValue; 
   private Byte value;

   private const byte MaxValue = byte.MaxValue;
   private const int MinValue = -1 * byte.MaxValue;

   public static explicit operator ByteWithSign(int value) 
   {
      // Check for overflow.
      if (value > ByteWithSign.MaxValue || value < ByteWithSign.MinValue)
         throw new OverflowException(String.Format("'{0}' is out of range of the ByteWithSign 
                                                   data type.", 
                                                   value));

      ByteWithSign newValue;
      newValue.signValue = (SByte) Math.Sign(value);
      newValue.value = (byte) Math.Abs(value);
      return newValue;
   }  

   public static explicit operator ByteWithSign(uint value)
   {
      if (value > ByteWithSign.MaxValue) 
         throw new OverflowException(String.Format("'{0}' is out of range of the ByteWithSign 
                                                   data type.", 
                                                   value));

      ByteWithSign newValue;
      newValue.signValue = 1;
      newValue.value = (byte) value;
      return newValue;
   }

   public override string ToString()
   { 
      return (signValue * value).ToString();
   }
}
```

```vb
Public Structure ByteWithSign
   Private signValue As SByte 
   Private value As Byte

   Private Const MaxValue As Byte = Byte.MaxValue
   Private Const MinValue As Integer = -1 * Byte.MaxValue

   Public Overloads Shared Narrowing Operator CType(value As Integer) As ByteWithSign
      ' Check for overflow.
      If value > ByteWithSign.MaxValue Or value < ByteWithSign.MinValue Then
         Throw New OverflowException(String.Format("'{0}' is out of range of the ByteWithSign 
                                                   data type.", value))
      End If

      Dim newValue As ByteWithSign

      newValue.signValue = CSByte(Math.Sign(value))
      newValue.value = CByte(Math.Abs(value))
      Return newValue
   End Operator

   Public Overloads Shared Narrowing Operator CType(value As UInteger) As ByteWithSign
      If value > ByteWithSign.MaxValue Then 
         Throw New OverflowException(String.Format("'{0}' is out of range of the ByteWithSign 
                                                   data type.", value))
      End If

      Dim NewValue As ByteWithSign

      newValue.signValue = 1
      newValue.value = CByte(value)
      Return newValue
   End Operator

   Public Overrides Function ToString() As String 
      Return (signValue * value).ToString()
   End Function
End Structure
```

Il codice client può quindi dichiarare una variabile `ByteWithSign` e assegnare a tale variabile valori [Int32](xref:System.Int32) e [UInt32](xref:System.UInt32) se le assegnazioni includono un operatore di cast o un metodo di conversione, come visualizzato nell'esempio seguente.

```csharp
ByteWithSign value;

try {
   int intValue = -120;
   value = (ByteWithSign) intValue;
   Console.WriteLine(value);
}
catch (OverflowException e) {
   Console.WriteLine(e.Message);
}

try {
   uint uintValue = 1024;
   value = (ByteWithSign) uintValue;
   Console.WriteLine(value);
}
catch (OverflowException e) {
    Console.WriteLine(e.Message);
}
// The example displays the following output:
//       -120
//       '1024' is out of range of the ByteWithSign data type.
```

```vb
Dim value As ByteWithSign

Try  
   Dim intValue As Integer = -120
   value = CType(intValue, ByteWithSign)
   Console.WriteLine(value) 
Catch e As OverflowException
   Console.WriteLine(e.Message)
End Try

Try
   Dim uintValue As UInteger = 1024
   value = CType(uintValue, ByteWithSign)
   Console.WriteLine(value) 
Catch e As OverflowException
   Console.WriteLine(e.Message)
End Try
' The example displays the following output:
'       -120
'       '1024' is out of range of the ByteWithSign data type.
```

## <a name="the-iconvertible-interface"></a>Interfaccia IConvertible

Per supportare la conversione di un tipo qualsiasi in un tipo di base Common Language Runtime, in .NET è disponibile l'interfaccia [IConvertible](xref:System.IConvertible). È necessario che il tipo di implementazione fornisca gli elementi seguenti:

* Un metodo che restituisce l'oggetto [TypeCode](xref:System.TypeCode) del tipo di implementazione.

* Metodi per convertire il tipo di implementazione in ognuno dei tipi di base di Common Language Runtime ([Boolean](xref:System.Boolean), [Byte](xref:System.Byte), [DateTime](xref:System.DateTime), [Decimal](xref:System.Decimal), [Double](xref:System.Double) e così via).

* Un metodo di conversione generalizzato per convertire un'istanza del tipo di implementazione in un altro tipo specificato. Le conversioni non supportate devono generare un evento [InvalidCastException](xref:System.InvalidCastException).

Tutti i tipi di base di Common Language Runtime (ovvero [Boolean](xref:System.Boolean), [Byte](xref:System.Byte), [Char](xref:System.Char), [DateTime](xref:System.DateTime), [Decimal](xref:System.Decimal), [Double](xref:System.Double), [Int16](xref:System.Int16), [Int32](xref:System.Int32), [Int64](xref:System.Int64), [SByte](xref:System.SByte), [Single](xref:System.Single), [String](xref:System.String), [UInt16](xref:System.UInt16), [UInt32](xref:System.UInt32) e [UInt64](xref:System.UInt64), nonché i tipi [DBNull](xref:System.DBNull) e [Enum](xref:System.Enum) implementano l'interfaccia [IConvertible](xref:System.IConvertible). Si tratta tuttavia di implementazioni esplicite dell'interfaccia: il metodo di conversione può essere chiamato solo tramite una variabile dell'interfaccia [IConvertible](xref:System.IConvertible), come visualizzato nell'esempio seguente. In questo esempio un valore [Int32](xref:System.Int32) viene convertito nel valore [Char](xref:System.Char) equivalente.

```csharp
int codePoint = 1067;
IConvertible iConv = codePoint;
char ch = iConv.ToChar(null);
Console.WriteLine("Converted {0} to {1}.", codePoint, ch);
```

```vb
Dim codePoint As Integer = 1067
Dim iConv As IConvertible = codePoint
Dim ch As Char = iConv.ToChar(Nothing)
Console.WriteLine("Converted {0} to {1}.", codePoint, ch)
```

Il requisito che il metodo di conversione venga chiamato sull'interfaccia anziché sul tipo di implementazione rende relativamente costose le implementazioni esplicite dell'interfaccia. In alternativa è consigliabile chiamare il membro appropriato della classe [Convert](xref:System.Convert) per eseguire la conversione tra tipi di base di Common Language Runtime. Per altre informazioni, vedere la sezione successiva [Classe Convert](#the-convert-class). 

> [!NOTE]
> Oltre all'interfaccia [IConvertible](xref:System.IConvertible) e alla classe [Convert](xref:System.Convert) offerte da .NET, nei singoli linguaggi possono essere disponibili altre modalità per eseguire le conversioni. In C# vengono ad esempio utilizzati gli operatori di cast mentre in Visual Basic vengono utilizzate funzioni di conversione implementate dal compilatore quali `CType`, `CInt` e `DirectCast`.

L'interfaccia [IConvertible](xref:System.IConvertible) è principalmente progettata per supportare la conversione tra tipi di base in .NET. L'interfaccia può tuttavia anche essere implementata da un tipo personalizzato per supportare la conversione di tale tipo in altri tipi personalizzati. Per altre informazioni, vedere la sezione [Conversioni personalizzate con il metodo ChangeType](#custom-conversions-with-the-changetype-method) più avanti in questo argomento.

## <a name="the-convert-class"></a>Classe Convert

Benché sia possibile chiamare l'implementazione dell'interfaccia [IConvertible](xref:System.IConvertible) di ogni tipo di base per eseguire una conversione di tipi, l'approccio indipendente dal linguaggio consigliato per convertire un tipo di base in un altro consiste nel chiamare i metodi della classe [System.Convert](xref:System.Convert). È anche possibile usare il metodo [Convert.ChangeType(Object, Type, IFormatProvider)](xref:System.Convert.ChangeType(System.Object,System.Type,System.IFormatProvider)) per eseguire la conversione da un tipo personalizzato specificato a un altro. 

### <a name="conversions-between-base-types"></a>Conversioni tra tipi di base

La classe [Convert](xref:System.Convert) consente di eseguire conversioni indipendenti dal linguaggio tra tipi di base ed è disponibile in tutti i linguaggi destinati a Common Language Runtime. Questa classe offre un set completo di metodi per le conversioni verso un tipo di dati più piccolo e per le conversioni verso un tipo di dati più grande e genera un evento [InvalidCastException](xref:System.InvalidCastException) per le conversioni non supportate (ad esempio la conversione di un valore [DateTime](xref:System.DateTime) in un valore intero). Le conversioni verso un tipo di dati più piccolo vengono eseguite in un contesto controllato (checked) e, se la conversione ha esito negativo, viene generato un evento [OverflowException](xref:System.OverflowException).

> [!IMPORTANT]
> Poiché la classe [Convert](xref:System.Convert) include metodi per la conversione in e da ogni tipo di base, non occorre chiamare l'implementazione esplicita dell'interfaccia [IConvertible](xref:System.IConvertible) di ogni tipo di base.

Nell'esempio seguente viene illustrato l'uso della classe [System.Convert](xref:System.Convert) per eseguire diverse conversioni verso un tipo di dati più grande e più piccolo tra tipi di base .NET.

```csharp
// Convert an Int32 value to a Decimal (a widening conversion).
int integralValue = 12534;
decimal decimalValue = Convert.ToDecimal(integralValue);
Console.WriteLine("Converted the {0} value {1} to " +  
                                  "the {2} value {3:N2}.", 
                                  integralValue.GetType().Name, 
                                  integralValue, 
                                  decimalValue.GetType().Name, 
                                  decimalValue);
// Convert a Byte value to an Int32 value (a widening conversion).
byte byteValue = Byte.MaxValue;
int integralValue2 = Convert.ToInt32(byteValue);                                  
Console.WriteLine("Converted the {0} value {1} to " +  
                                  "the {2} value {3:G}.", 
                                  byteValue.GetType().Name, 
                                  byteValue, 
                                  integralValue2.GetType().Name, 
                                  integralValue2);

// Convert a Double value to an Int32 value (a narrowing conversion).
double doubleValue = 16.32513e12;
try {
   long longValue = Convert.ToInt64(doubleValue);
   Console.WriteLine("Converted the {0} value {1:E} to " +  
                                     "the {2} value {3:N0}.", 
                                     doubleValue.GetType().Name, 
                                     doubleValue, 
                                     longValue.GetType().Name, 
                                     longValue);
}
catch (OverflowException) {
   Console.WriteLine("Unable to convert the {0:E} value {1}.", 
                                     doubleValue.GetType().Name, doubleValue);
}

// Convert a signed byte to a byte (a narrowing conversion).     
sbyte sbyteValue = -16;
try {
   byte byteValue2 = Convert.ToByte(sbyteValue);
   Console.WriteLine("Converted the {0} value {1} to " +  
                                     "the {2} value {3:G}.", 
                                     sbyteValue.GetType().Name, 
                                     sbyteValue, 
                                     byteValue2.GetType().Name, 
                                     byteValue2);
}
catch (OverflowException) {
   Console.WriteLine("Unable to convert the {0} value {1}.", 
                                     sbyteValue.GetType().Name, sbyteValue);
}                                         
// The example displays the following output:
//       Converted the Int32 value 12534 to the Decimal value 12,534.00.
//       Converted the Byte value 255 to the Int32 value 255.
//       Converted the Double value 1.632513E+013 to the Int64 value 16,325,130,000,000.
//       Unable to convert the SByte value -16.
```

```vb
' Convert an Int32 value to a Decimal (a widening conversion).
Dim integralValue As Integer = 12534
Dim decimalValue As Decimal = Convert.ToDecimal(integralValue)
Console.WriteLine("Converted the {0} value {1} to the {2} value {3:N2}.", 
                  integralValue.GetType().Name,
                  integralValue,
                  decimalValue.GetType().Name,
                  decimalValue)

' Convert a Byte value to an Int32 value (a widening conversion).
Dim byteValue As Byte = Byte.MaxValue
Dim integralValue2 As Integer = Convert.ToInt32(byteValue)                                  
Console.WriteLine("Converted the {0} value {1} to " + 
                                  "the {2} value {3:G}.",
                                  byteValue.GetType().Name,
                                  byteValue,
                                  integralValue2.GetType().Name,
                                  integralValue2)

' Convert a Double value to an Int32 value (a narrowing conversion).
Dim doubleValue As Double = 16.32513e12
Try
   Dim longValue As Long = Convert.ToInt64(doubleValue)
   Console.WriteLine("Converted the {0} value {1:E} to " + 
                                     "the {2} value {3:N0}.",
                                     doubleValue.GetType().Name,
                                     doubleValue,
                                     longValue.GetType().Name,
                                     longValue)
Catch e As OverflowException
   Console.WriteLine("Unable to convert the {0:E} value {1}.",
                                     doubleValue.GetType().Name, doubleValue)
End Try                                                             

' Convert a signed byte to a byte (a narrowing conversion).     
Dim sbyteValue As SByte = -16
Try
   Dim byteValue2 As Byte = Convert.ToByte(sbyteValue)
   Console.WriteLine("Converted the {0} value {1} to " + 
                                     "the {2} value {3:G}.",
                                     sbyteValue.GetType().Name,
                                     sbyteValue,
                                     byteValue2.GetType().Name,
                                     byteValue2)
Catch e As OverflowException
   Console.WriteLine("Unable to convert the {0} value {1}.",
                                     sbyteValue.GetType().Name, sbyteValue)
End Try 
' The example displays the following output:
'       Converted the Int32 value 12534 to the Decimal value 12,534.00.
'       Converted the Byte value 255 to the Int32 value 255.
'       Converted the Double value 1.632513E+013 to the Int64 value 16,325,130,000,000.
'       Unable to convert the SByte value -16.
```

Talvolta, in particolare nel caso di conversione verso e da valori a virgola mobile, una conversione può comportare una perdita di precisione, anche se non viene generato un evento [OverflowException](xref:System.OverflowException). Nell'esempio seguente viene illustrata questa perdita di precisione. Nel primo caso, un valore [Decimal](xref:System.Decimal) è meno preciso (meno cifre significative) quando viene convertito in [Double](xref:System.Double). Nel secondo caso, un valore [Double](xref:System.Double) viene arrotondato da **42,72** a **43** per completare la conversione.

```csharp
double doubleValue; 

// Convert a Double to a Decimal.
decimal decimalValue = 13956810.96702888123451471211m;
doubleValue = Convert.ToDouble(decimalValue);
Console.WriteLine("{0} converted to {1}.", decimalValue, doubleValue);

doubleValue = 42.72;
try {
   int integerValue = Convert.ToInt32(doubleValue);
   Console.WriteLine("{0} converted to {1}.", 
                                     doubleValue, integerValue);
}
catch (OverflowException) {      
   Console.WriteLine("Unable to convert {0} to an integer.", 
                                     doubleValue);
}   
// The example displays the following output:
//       13956810.96702888123451471211 converted to 13956810.9670289.
//       42.72 converted to 43.
```

```vb
Dim doubleValue As Double 

' Convert a Double to a Decimal.
Dim decimalValue As Decimal = 13956810.96702888123451471211d
doubleValue = Convert.ToDouble(decimalValue)
Console.WriteLine("{0} converted to {1}.", decimalValue, doubleValue)

doubleValue = 42.72
Try
   Dim integerValue As Integer = Convert.ToInt32(doubleValue)
   Console.WriteLine("{0} converted to {1}.",
                                     doubleValue, integerValue)
Catch e As OverflowException
   Console.WriteLine("Unable to convert {0} to an integer.",
                                     doubleValue)
End Try   
' The example displays the following output:
'       13956810.96702888123451471211 converted to 13956810.9670289.
'       42.72 converted to 43.
```

Per una tabella che elenca le conversioni verso un tipo di dati più piccolo e più grande supportate dalla classe [Convert](xref:System.Convert), vedere [Tabelle di conversione dei tipi](conversion-tables.md).

### <a name="custom-conversions-with-the-changetype-method"></a>Conversioni personalizzate con il metodo ChangeType

Oltre a supportare le conversioni in ognuno dei tipi di base, la classe [Convert](xref:System.Convert) può essere usata per convertire un tipo personalizzato in uno o più tipi predefiniti. Questa conversione viene eseguita dal metodo [Convert.ChangeType(Object, Type, IFormatProvider)](xref:System.Convert.ChangeType(System.Object,System.Type,System.IFormatProvider)), che a sua volta esegue il wrapping di una chiamata al metodo [IConvertible.ToType](xref:System.IConvertible.ToType(System.Type,System.IFormatProvider)) del parametro value. Questo significa che l'oggetto rappresentato dal parametro value deve offrire un'implementazione dell'interfaccia [IConvertible](xref:System.IConvertible).

> [!NOTE]
> Poiché i metodi [Convert.ChangeType(Object, Type)](xref:System.Convert.ChangeType(System.Object,System.Type)) e [Convert.ChangeType(Object, Type, IFormatProvider)](xref:System.Convert.ChangeType(System.Object,System.Type,System.IFormatProvider)) usano un oggetto [Type](xref:System.Type) per specificare il tipo di destinazione in cui viene convertito value, possono essere usati per eseguire una conversione dinamica a un oggetto il cui tipo non è noto in fase di compilazione. Tuttavia, si noti che l'implementazione [IConvertible](xref:System.IConvertible) di value deve comunque supportare questa conversione. 

Nell'esempio seguente viene illustrata una possibile implementazione dell'interfaccia [IConvertible](xref:System.IConvertible) che consente la conversione di un oggetto `TemperatureCelsius` in un oggetto `TemperatureFahrenheit` e viceversa. Nell'esempio viene definita una classe di base, `Temperature`, che implementa l'interfaccia [IConvertible](xref:System.IConvertible) ed esegue l'override del metodo [Object.ToString](xref:System.Object.ToString). Le classi `TemperatureCelsius` e `TemperatureFahrenheit` derivate eseguono ognuna l'override dei metodi `ToType` e `ToString` della classe di base. 

```csharp
using System;

public abstract class Temperature : IConvertible
{
   protected decimal temp;

   public Temperature(decimal temperature)
   {
      this.temp = temperature;
   }

   public decimal Value
   { 
      get { return this.temp; } 
      set { this.temp = Value; }        
   }

   public override string ToString()
   {
      return temp.ToString(null as IFormatProvider) + "º";
   }

   // IConvertible implementations.
   public TypeCode GetTypeCode() { 
      return TypeCode.Object;
   }   

   public bool ToBoolean(IFormatProvider provider) {
      throw new InvalidCastException(String.Format("Temperature-to-Boolean conversion is not supported."));
   }

   public byte ToByte(IFormatProvider provider) {
      if (temp < Byte.MinValue || temp > Byte.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the Byte data type.", temp));
      else
         return (byte) temp;
   }

   public char ToChar(IFormatProvider provider) {
      throw new InvalidCastException("Temperature-to-Char conversion is not supported.");
   }

   public DateTime ToDateTime(IFormatProvider provider) {
      throw new InvalidCastException("Temperature-to-DateTime conversion is not supported.");
   }

   public decimal ToDecimal(IFormatProvider provider) {
      return temp;
   }

   public double ToDouble(IFormatProvider provider) {
      return (double) temp;
   }

   public short ToInt16(IFormatProvider provider) {
      if (temp < Int16.MinValue || temp > Int16.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the Int16 data type.", temp));
      else
         return (short) Math.Round(temp);
   }

   public int ToInt32(IFormatProvider provider) {
      if (temp < Int32.MinValue || temp > Int32.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the Int32 data type.", temp));
      else
         return (int) Math.Round(temp);
   }

   public long ToInt64(IFormatProvider provider) {
      if (temp < Int64.MinValue || temp > Int64.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the Int64 data type.", temp));
      else
         return (long) Math.Round(temp);
   }

   public sbyte ToSByte(IFormatProvider provider) {
      if (temp < SByte.MinValue || temp > SByte.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the SByte data type.", temp));
      else
         return (sbyte) temp;
   }

   public float ToSingle(IFormatProvider provider) {
      return (float) temp;
   }

   public virtual string ToString(IFormatProvider provider) {
      return temp.ToString(provider) + "°";
   }

   // If conversionType is implemented by another IConvertible method, call it.
   public virtual object ToType(Type conversionType, IFormatProvider provider) {
      switch (Type.GetTypeCode(conversionType))
      {
         case TypeCode.Boolean:
            return this.ToBoolean(provider);
         case TypeCode.Byte:
            return this.ToByte(provider);
         case TypeCode.Char:
            return this.ToChar(provider);
         case TypeCode.DateTime:
            return this.ToDateTime(provider);
         case TypeCode.Decimal:
            return this.ToDecimal(provider);
         case TypeCode.Double:
            return this.ToDouble(provider);
         case TypeCode.Empty:
            throw new NullReferenceException("The target type is null.");
         case TypeCode.Int16:
            return this.ToInt16(provider);
         case TypeCode.Int32:
            return this.ToInt32(provider);
         case TypeCode.Int64:
            return this.ToInt64(provider);
         case TypeCode.Object:
            // Leave conversion of non-base types to derived classes.
            throw new InvalidCastException(String.Format("Cannot convert from Temperature to {0}.", 
                                           conversionType.Name));
         case TypeCode.SByte:
            return this.ToSByte(provider);
         case TypeCode.Single:
            return this.ToSingle(provider);
         case TypeCode.String:
            IConvertible iconv = this;
            return iconv.ToString(provider);
         case TypeCode.UInt16:
            return this.ToUInt16(provider);
         case TypeCode.UInt32:
            return this.ToUInt32(provider);
         case TypeCode.UInt64:
            return this.ToUInt64(provider);
         default:
            throw new InvalidCastException("Conversion not supported.");
      }
   }

   public ushort ToUInt16(IFormatProvider provider) {
      if (temp < UInt16.MinValue || temp > UInt16.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the UInt16 data type.", temp));
      else
         return (ushort) Math.Round(temp);
   }

   public uint ToUInt32(IFormatProvider provider) {
      if (temp < UInt32.MinValue || temp > UInt32.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the UInt32 data type.", temp));
      else
         return (uint) Math.Round(temp);
   }

   public ulong ToUInt64(IFormatProvider provider) {
      if (temp < UInt64.MinValue || temp > UInt64.MaxValue)
         throw new OverflowException(String.Format("{0} is out of range of the UInt64 data type.", temp));
      else
         return (ulong) Math.Round(temp);
   }
}

public class TemperatureCelsius : Temperature, IConvertible
{
   public TemperatureCelsius(decimal value) : base(value)
   {
   }

   // Override ToString methods.
   public override string ToString()
   {
      return this.ToString(null);
   }

   public override string ToString(IFormatProvider provider)
   {
      return temp.ToString(provider) + "°C"; 
   }

   // If conversionType is a implemented by another IConvertible method, call it.
   public override object ToType(Type conversionType, IFormatProvider provider) {
      // For non-objects, call base method.
      if (Type.GetTypeCode(conversionType) != TypeCode.Object) {
         return base.ToType(conversionType, provider);
      }   
      else
      {   
         if (conversionType.Equals(typeof(TemperatureCelsius)))
            return this;
         else if (conversionType.Equals(typeof(TemperatureFahrenheit)))
            return new TemperatureFahrenheit((decimal) this.temp * 9 / 5 + 32);
         else
            throw new InvalidCastException(String.Format("Cannot convert from Temperature to {0}.", 
                                           conversionType.Name));
      }
   }
}

public class TemperatureFahrenheit : Temperature, IConvertible 
{
   public TemperatureFahrenheit(decimal value) : base(value)
   {
   }

   // Override ToString methods.
   public override string ToString()
   {
      return this.ToString(null);
   }

   public override string ToString(IFormatProvider provider)
   {
      return temp.ToString(provider) + "°F"; 
   }

   public override object ToType(Type conversionType, IFormatProvider provider)
   { 
      // For non-objects, call base methood.
      if (Type.GetTypeCode(conversionType) != TypeCode.Object) {
         return base.ToType(conversionType, provider);
      }   
      else
      {   
         // Handle conversion between derived classes.
         if (conversionType.Equals(typeof(TemperatureFahrenheit))) 
            return this;
         else if (conversionType.Equals(typeof(TemperatureCelsius)))
            return new TemperatureCelsius((decimal) (this.temp - 32) * 5 / 9);
         // Unspecified object type: throw an InvalidCastException.
         else
            throw new InvalidCastException(String.Format("Cannot convert from Temperature to {0}.", 
                                           conversionType.Name));
      }                                 
   }
}
```

```vb
Public MustInherit Class Temperature
   Implements IConvertible

   Protected temp As Decimal

   Public Sub New(temperature As Decimal)
      Me.temp = temperature
   End Sub

   Public Property Value As Decimal
      Get 
         Return Me.temp
      End Get
      Set
         Me.temp = Value
      End Set   
   End Property

   Public Overrides Function ToString() As String
      Return temp.ToString() & "º"
   End Function

   ' IConvertible implementations.
   Public Function GetTypeCode() As TypeCode Implements IConvertible.GetTypeCode
      Return TypeCode.Object
   End Function   

   Public Function ToBoolean(provider As IFormatProvider) As Boolean Implements IConvertible.ToBoolean
      Throw New InvalidCastException(String.Format("Temperature-to-Boolean conversion is not supported."))
   End Function

   Public Function ToByte(provider As IFormatProvider) As Byte Implements IConvertible.ToByte
      If temp < Byte.MinValue Or temp > Byte.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the Byte data type.", temp))
      Else
         Return CByte(temp)
      End If    
   End Function

   Public Function ToChar(provider As IFormatProvider) As Char Implements IConvertible.ToChar
      Throw New InvalidCastException("Temperature-to-Char conversion is not supported.")
   End Function

   Public Function ToDateTime(provider As IFormatProvider) As DateTime Implements IConvertible.ToDateTime
      Throw New InvalidCastException("Temperature-to-DateTime conversion is not supported.")
   End Function

   Public Function ToDecimal(provider As IFormatProvider) As Decimal Implements IConvertible.ToDecimal
      Return temp
   End Function

   Public Function ToDouble(provider As IFormatProvider) As Double Implements IConvertible.ToDouble
      Return CDbl(temp)
   End Function

   Public Function ToInt16(provider As IFormatProvider) As Int16 Implements IConvertible.ToInt16
      If temp < Int16.MinValue Or temp > Int16.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the Int16 data type.", temp))
      End If
      Return CShort(Math.Round(temp))
   End Function

   Public Function ToInt32(provider As IFormatProvider) As Int32 Implements IConvertible.ToInt32
      If temp < Int32.MinValue Or temp > Int32.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the Int32 data type.", temp))
      End If
      Return CInt(Math.Round(temp))
   End Function

   Public Function ToInt64(provider As IFormatProvider) As Int64 Implements IConvertible.ToInt64
      If temp < Int64.MinValue Or temp > Int64.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the Int64 data type.", temp))
      End If
      Return CLng(Math.Round(temp))
   End Function

   Public Function ToSByte(provider As IFormatProvider) As SByte Implements IConvertible.ToSByte
      If temp < SByte.MinValue Or temp > SByte.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the SByte data type.", temp))
      Else
         Return CSByte(temp)
      End If    
   End Function

   Public Function ToSingle(provider As IFormatProvider) As Single Implements IConvertible.ToSingle
      Return CSng(temp)
   End Function

   Public Overridable Overloads Function ToString(provider As IFormatProvider) As String Implements IConvertible.ToString
      Return temp.ToString(provider) & " °C"
   End Function

   ' If conversionType is a implemented by another IConvertible method, call it.
   Public Overridable Function ToType(conversionType As Type, provider As IFormatProvider) As Object Implements IConvertible.ToType
      Select Case Type.GetTypeCode(conversionType)
         Case TypeCode.Boolean
            Return Me.ToBoolean(provider)
         Case TypeCode.Byte
            Return Me.ToByte(provider)
         Case TypeCode.Char
            Return Me.ToChar(provider)   
         Case TypeCode.DateTime
            Return Me.ToDateTime(provider)
         Case TypeCode.Decimal
            Return Me.ToDecimal(provider)
         Case TypeCode.Double
            Return Me.ToDouble(provider)
         Case TypeCode.Empty
            Throw New NullReferenceException("The target type is null.")
         Case TypeCode.Int16
            Return Me.ToInt16(provider)
         Case TypeCode.Int32
            Return Me.ToInt32(provider)
         Case TypeCode.Int64
            Return Me.ToInt64(provider)
         Case TypeCode.Object
            ' Leave conversion of non-base types to derived classes.
            Throw New InvalidCastException(String.Format("Cannot convert from Temperature to {0}.", _
                                           conversionType.Name))
         Case TypeCode.SByte
            Return Me.ToSByte(provider)
         Case TypeCode.Single
            Return Me.ToSingle(provider)
         Case TypeCode.String
            Return Me.ToString(provider)
         Case TypeCode.UInt16
            Return Me.ToUInt16(provider)
         Case TypeCode.UInt32
            Return Me.ToUInt32(provider)
         Case TypeCode.UInt64
            Return Me.ToUInt64(provider)
         Case Else
            Throw New InvalidCastException("Conversion not supported.")   
      End Select
   End Function

   Public Function ToUInt16(provider As IFormatProvider) As UInt16 Implements IConvertible.ToUInt16
      If temp < UInt16.MinValue Or temp > UInt16.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the UInt16 data type.", temp))
      End If
      Return CUShort(Math.Round(temp))
   End Function

   Public Function ToUInt32(provider As IFormatProvider) As UInt32 Implements IConvertible.ToUInt32
      If temp < UInt32.MinValue Or temp > UInt32.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the UInt32 data type.", temp))
      End If
      Return CUInt(Math.Round(temp))
   End Function

   Public Function ToUInt64(provider As IFormatProvider) As UInt64 Implements IConvertible.ToUInt64
      If temp < UInt64.MinValue Or temp > UInt64.MaxValue Then
         Throw New OverflowException(String.Format("{0} is out of range of the UInt64 data type.", temp))
      End If
      Return CULng(Math.Round(temp))
   End Function
End Class

Public Class TemperatureCelsius : Inherits Temperature : Implements IConvertible
   Public Sub New(value As Decimal)
      MyBase.New(value)
   End Sub

   ' Override ToString methods.
   Public Overrides Function ToString() As String
      Return Me.ToString(Nothing)
   End Function

   Public Overrides Function ToString(provider As IFormatProvider ) As String
      Return temp.ToString(provider) + "°C" 
   End Function

  ' If conversionType is a implemented by another IConvertible method, call it.
   Public Overrides Function ToType(conversionType As Type, provider As IFormatProvider) As Object
      ' For non-objects, call base method.
      If Type.GetTypeCode(conversionType) <> TypeCode.Object Then
         Return MyBase.ToType(conversionType, provider)
      Else   
         If conversionType.Equals(GetType(TemperatureCelsius)) Then
            Return Me
         ElseIf conversionType.Equals(GetType(TemperatureFahrenheit))
            Return New TemperatureFahrenheit(CDec(Me.temp * 9 / 5 + 32))
         ' Unspecified object type: throw an InvalidCastException.
         Else
            Throw New InvalidCastException(String.Format("Cannot convert from Temperature to {0}.", _ 
                                           conversionType.Name))
         End If
      End If                                  
   End Function
End Class

Public Class TemperatureFahrenheit : Inherits Temperature : Implements IConvertible
   Public Sub New(value As Decimal)
      MyBase.New(value)
   End Sub

   ' Override ToString methods.
   Public Overrides Function ToString() As String
      Return Me.ToString(Nothing)
   End Function

   Public Overrides Function ToString(provider As IFormatProvider ) As String
      Return temp.ToString(provider) + "°F" 
   End Function

   Public Overrides Function ToType(conversionType As Type, provider As IFormatProvider) As Object
      ' For non-objects, call base methood.
      If Type.GetTypeCode(conversionType) <> TypeCode.Object Then
         Return MyBase.ToType(conversionType, provider)
      Else   
         ' Handle conversion between derived classes.
         If conversionType.Equals(GetType(TemperatureFahrenheit)) Then 
            Return Me
         ElseIf conversionType.Equals(GetType(TemperatureCelsius))
            Return New TemperatureCelsius(CDec((MyBase.temp - 32) * 5 / 9))
         ' Unspecified object type: throw an InvalidCastException.
         Else
            Throw New InvalidCastException(String.Format("Cannot convert from Temperature to {0}.", _
                                           conversionType.Name))
         End If
      End If                                  
   End Function
End Class
```

Nell'esempio seguente vengono illustrate diverse chiamate a queste implementazioni di [IConvertible](xref:System.IConvertible) per convertire oggetti `TemperatureCelsius` in oggetti `TemperatureFahrenheit` e viceversa.

```csharp
TemperatureCelsius tempC1 = new TemperatureCelsius(0);
TemperatureFahrenheit tempF1 = (TemperatureFahrenheit) Convert.ChangeType(tempC1, typeof(TemperatureFahrenheit), null);
Console.WriteLine("{0} equals {1}.", tempC1, tempF1);
TemperatureCelsius tempC2 = (TemperatureCelsius) Convert.ChangeType(tempC1, typeof(TemperatureCelsius), null);
Console.WriteLine("{0} equals {1}.", tempC1, tempC2);
TemperatureFahrenheit tempF2 = new TemperatureFahrenheit(212);
TemperatureCelsius tempC3 = (TemperatureCelsius) Convert.ChangeType(tempF2, typeof(TemperatureCelsius), null);
Console.WriteLine("{0} equals {1}.", tempF2, tempC3);
TemperatureFahrenheit tempF3 = (TemperatureFahrenheit) Convert.ChangeType(tempF2, typeof(TemperatureFahrenheit), null);
Console.WriteLine("{0} equals {1}.", tempF2, tempF3);
// The example displays the following output:
//       0°C equals 32°F.
//       0°C equals 0°C.
//       212°F equals 100°C.
//       212°F equals 212°F.
```

```vb
Dim tempC1 As New TemperatureCelsius(0)
Dim tempF1 As TemperatureFahrenheit = CType(Convert.ChangeType(tempC1, GetType(TemperatureFahrenheit), Nothing), TemperatureFahrenheit)
Console.WriteLine("{0} equals {1}.", tempC1, tempF1) 
Dim tempC2 As TemperatureCelsius = CType(Convert.ChangeType(tempC1, GetType(TemperatureCelsius), Nothing), TemperatureCelsius)
Console.WriteLine("{0} equals {1}.", tempC1, tempC2) 
Dim tempF2 As New TemperatureFahrenheit(212)
Dim tempC3 As TEmperatureCelsius = CType(Convert.ChangeType(tempF2, GEtType(TemperatureCelsius), Nothing), TemperatureCelsius)
Console.WriteLine("{0} equals {1}.", tempF2, tempC3) 
Dim tempF3 As TemperatureFahrenheit = CType(Convert.ChangeType(tempF2, GetType(TemperatureFahrenheit), Nothing), TemperatureFahrenheit)
Console.WriteLine("{0} equals {1}.", tempF2, tempF3)
' The example displays the following output:
'       0°C equals 32°F.
'       0°C equals 0°C.
'       212°F equals 100°C.
'       212°F equals 212°F.
```

## <a name="the-typeconverter-class"></a>Classe TypeConverter

In .NET è anche possibile definire un convertitore di tipi per un tipo personalizzato mediante l'estensione della classe [System.ComponentModel.TypeConverter](xref:System.ComponentModel.TypeConverter) e l'associazione del convertitore di tipi al tipo tramite un attributo [System.ComponentModel.TypeConverterAttribute](xref:System.ComponentModel.TypeConverterAttribute). Nella tabella seguente sono evidenziate le differenze tra questo approccio e l'implementazione dell'interfaccia [IConvertible](xref:System.IConvertible) per un tipo personalizzato.

> [!NOTE]
> È possibile fornire supporto per un tipo personalizzato in fase di progettazione solo se per tale tipo è stato definito un convertitore di tipi.

Conversione mediante TypeConverter | Conversione mediante IConvertible
------------------------------ | -----------------------------
Implementata per un tipo personalizzato derivando una classe separata da [TypeConverter](xref:System.ComponentModel.TypeConverter). Questa classe derivata viene associata al tipo personalizzato applicando un attributo [TypeConverterAttribute](xref:System.ComponentModel.TypeConverterAttribute). | Implementata da un tipo personalizzato per eseguire la conversione. Un utente di tale tipo chiama sul tipo stesso un metodo di conversione [IConvertible](xref:System.IConvertible).
Utilizzabile sia in fase di progettazione che in fase di esecuzione. | Utilizzabile solo in fase di esecuzione.
Usa la reflection ed è quindi più lenta della conversione consentita da [IConvertible](xref:System.IConvertible). | Non utilizza la reflection.
Consente di eseguire conversioni bidirezionali, dal tipo personalizzato ad altri tipi di dati e da altri tipi di dati al tipo personalizzato. Ad esempio, un [TypeConverter](xref:System.ComponentModel.TypeConverter) definito per `MyType` consente le conversioni da `MyType` a [String](xref:System.String) e da [String](xref:System.String) a `MyType`. | Consente la conversione da un tipo personalizzato ad altri tipi di dati, ma non da altri tipi di dati al tipo personalizzato.

Per altre informazioni sull'uso di convertitori di tipi per l'esecuzione di conversioni, vedere [System.ComponentModel.TypeConverter](xref:System.ComponentModel.TypeConverter).

## <a name="see-also"></a>Vedere anche

[System.Convert](xref:System.Convert)

[IConvertible](xref:System.IConvertible)

[Tabelle di conversione dei tipi](conversion-tables.md)


<!--HONumber=Nov16_HO3-->


