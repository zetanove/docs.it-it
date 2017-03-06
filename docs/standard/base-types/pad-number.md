---
title: 'Procedura: Aggiungere zeri iniziali a un numero'
description: Come aggiungere zeri iniziali a un numero
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: a517c066-b11e-4815-826b-9262611eac40
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 92f8796eae0f269cacfa4cf70330c5e3c0826717
ms.lasthandoff: 03/02/2017

---

# <a name="how-to-pad-a-number-with-leading-zeros"></a>Procedura: Aggiungere zeri iniziali a un numero

È possibile aggiungere degli zeri iniziali a un numero intero usando la [stringa di formato numerico standard](standard-numeric.md) "D" con un identificatore di precisione. È possibile aggiungere zeri iniziali sia ai numeri interi che ai numeri a virgola mobile usando una [stringa di formato numerico personalizzata](custom-numeric.md). In questo argomento viene illustrato come usare entrambi i metodi per aggiungere un numero con gli zeri iniziali.

## <a name="to-pad-an-integer-with-leading-zeros-to-a-specific-length"></a>Per aggiungere un intero con gli zeri iniziali a una lunghezza specifica

1. Determinare il numero minimo di cifre da visualizzare nel valore di tipo Integer. Includere eventuali cifre iniziali nel numero.

2. Determinare se si vuole visualizzare il valore di tipo Integer come valore decimale o esadecimale.

    * Per visualizzare il numero intero come valore decimale, chiamare il metodo `ToString(String)` e passare la stringa "D*n*" come valore del parametro format, dove *n* rappresenta la lunghezza minima della stringa.
    
    * Per visualizzare il numero intero come valore esadecimale, chiamare il metodo `ToString(String)` e passare la stringa "X*n*" come valore del parametro format, dove *n* rappresenta la lunghezza minima della stringa.
    
  È anche possibile usare la stringa di formato in un metodo, ad esempio [Console.WriteLine](xref:System.Console.WriteLine) o [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)), che usa la [formattazione composta](composite-format.md).  
  
Il seguente esempio formatta diversi valori di tipo Integer con gli zeri iniziali in modo che la lunghezza totale del numero formattato sia almeno di otto caratteri.

```csharp
byte byteValue = 254;
short shortValue = 10342;
int intValue = 1023983;
long lngValue = 6985321;               
ulong ulngValue = UInt64.MaxValue;

// Display integer values by calling the ToString method.
Console.WriteLine("{0,22} {1,22}", byteValue.ToString("D8"), byteValue.ToString("X8"));
Console.WriteLine("{0,22} {1,22}", shortValue.ToString("D8"), shortValue.ToString("X8"));
Console.WriteLine("{0,22} {1,22}", intValue.ToString("D8"), intValue.ToString("X8"));
Console.WriteLine("{0,22} {1,22}", lngValue.ToString("D8"), lngValue.ToString("X8"));
Console.WriteLine("{0,22} {1,22}", ulngValue.ToString("D8"), ulngValue.ToString("X8"));
Console.WriteLine();

// Display the same integer values by using composite formatting.
Console.WriteLine("{0,22:D8} {0,22:X8}", byteValue);
Console.WriteLine("{0,22:D8} {0,22:X8}", shortValue);
Console.WriteLine("{0,22:D8} {0,22:X8}", intValue);
Console.WriteLine("{0,22:D8} {0,22:X8}", lngValue);
Console.WriteLine("{0,22:D8} {0,22:X8}", ulngValue);
// The example displays the following output:
//                     00000254               000000FE
//                     00010342               00002866
//                     01023983               000F9FEF
//                     06985321               006A9669
//         18446744073709551615       FFFFFFFFFFFFFFFF
//       
//                     00000254               000000FE
//                     00010342               00002866
//                     01023983               000F9FEF
//                     06985321               006A9669
//         18446744073709551615       FFFFFFFFFFFFFFFF
//         18446744073709551615       FFFFFFFFFFFFFFFF
```

```vb
Dim byteValue As Byte = 254
Dim shortValue As Short = 10342
Dim intValue As Integer = 1023983
Dim lngValue As Long = 6985321               
Dim ulngValue As ULong = UInt64.MaxValue

' Display integer values by calling the ToString method.
Console.WriteLine("{0,22} {1,22}", byteValue.ToString("D8"), byteValue.ToString("X8"))
Console.WriteLine("{0,22} {1,22}", shortValue.ToString("D8"), shortValue.ToString("X8"))
Console.WriteLine("{0,22} {1,22}", intValue.ToString("D8"), intValue.ToString("X8"))
Console.WriteLine("{0,22} {1,22}", lngValue.ToString("D8"), lngValue.ToString("X8"))
Console.WriteLine("{0,22} {1,22}", ulngValue.ToString("D8"), ulngValue.ToString("X8"))
Console.WriteLine()

' Display the same integer values by using composite formatting.
Console.WriteLine("{0,22:D8} {0,22:X8}", byteValue)
Console.WriteLine("{0,22:D8} {0,22:X8}", shortValue)
Console.WriteLine("{0,22:D8} {0,22:X8}", intValue)
Console.WriteLine("{0,22:D8} {0,22:X8}", lngValue)
Console.WriteLine("{0,22:D8} {0,22:X8}", ulngValue)
' The example displays the following output:
'                     00000254               000000FE
'                     00010342               00002866
'                     01023983               000F9FEF
'                     06985321               006A9669
'         18446744073709551615       FFFFFFFFFFFFFFFF
'       
'                     00000254               000000FE
'                     00010342               00002866
'                     01023983               000F9FEF
'                     06985321               006A9669
'         18446744073709551615       FFFFFFFFFFFFFFFF
```

## <a name="to-pad-an-integer-with-a-specific-number-of-leading-zeros"></a>Per aggiungere un intero con un determinato numero di zeri iniziali

1. Determinare il numero di zeri iniziali da visualizzare nel valore di tipo Integer.

2. Determinare se si vuole visualizzare il valore di tipo Integer come valore decimale o esadecimale. Se si formatta come valore decimale, è necessario usare l'identificatore di formato standard "D", mentre come valore esadecimale è necessario usare l'identificatore di formato "X".

3. Determine la lunghezza della stringa numerica non aggiunta chiamando il metodo `ToString("D").Length` o `ToString("X").Length` del valore di tipo Integer. 

4. Aggiungere il numero di zeri iniziali da includere nella stringa formattata nella lunghezza della stringa numerica non aggiunta. In questo modo si definisce la lunghezza totale della stringa aggiunta.

5. Chiamare il metodo `ToString(String)` del valore integer e passare la stringa "D*n*" per le stringhe decimali e la stringa "X*n*" per quelle esadecimali, dove *n* rappresenta la lunghezza totale della stringa aggiunta. È anche possibile usare la stringa di formato "D*n*" o "X*n*" in un metodo che supporta la formattazione composta.

Il seguente esempio aggiunge un valore di tipo Integer con cinque zeri iniziali.

```csharp
int value = 160934;
int decimalLength = value.ToString("D").Length + 5;
int hexLength = value.ToString("X").Length + 5;
Console.WriteLine(value.ToString("D" + decimalLength.ToString()));
Console.WriteLine(value.ToString("X" + hexLength.ToString()));
// The example displays the following output:
//       00000160934
//       00000274A6
```

```vb
Dim value As Integer = 160934
Dim decimalLength As Integer = value.ToString("D").Length + 5
Dim hexLength As Integer = value.ToString("X").Length + 5
Console.WriteLine(value.ToString("D" + decimalLength.ToString()))
Console.WriteLine(value.ToString("X" + hexLength.ToString()))
' The example displays the following output:
'       00000160934
'       00000274A6 
```

## <a name="to-pad-a-numeric-value-with-leading-zeros-to-a-specific-length"></a>Per aggiungere un valore numerico con gli zeri iniziali a una lunghezza specifica

1. Determinare il numero di cifre alla sinistra del decimale che deve avere la rappresentazione della stringa del numero. Includere gli eventuali zeri iniziali nel numero totale di cifre.

2. Definire una stringa di formato numerico personalizzata in cui è usato un segnaposto zero ("0") per rappresentare il numero minimo di zeri.

3. Chiamare il metodo `ToString(String)` del numero e passarlo alla stringa di formato personalizzata. È anche possibile usare la stringa di formato personalizzata con un metodo che supporta la formattazione composta.

Il seguente esempio formatta diversi valori numerici con gli zeri iniziali in modo che la lunghezza totale del numero formattato sia almeno di otto caratteri alla sinistra del decimale.

```csharp
string fmt = "00000000.##";
int intValue = 1053240;
decimal decValue = 103932.52m;
float sngValue = 1549230.10873992f;
double dblValue = 9034521202.93217412;

// Display the numbers using the ToString method.
Console.WriteLine(intValue.ToString(fmt));
Console.WriteLine(decValue.ToString(fmt));           
Console.WriteLine(sngValue.ToString(fmt));
Console.WriteLine(dblValue.ToString(fmt));           
Console.WriteLine();

// Display the numbers using composite formatting.
string formatString = " {0,15:" + fmt + "}";
Console.WriteLine(formatString, intValue);      
Console.WriteLine(formatString, decValue);      
Console.WriteLine(formatString, sngValue);      
Console.WriteLine(formatString, dblValue);      
// The example displays the following output:
//       01053240
//       00103932.52
//       01549230
//       9034521202.93
//       
//               01053240
//            00103932.52
//               01549230
//          9034521202.93  
```

```vb
Dim fmt As String = "00000000.##"
Dim intValue As Integer = 1053240
Dim decValue As Decimal = 103932.52d
Dim sngValue As Single = 1549230.10873992
Dim dblValue As Double = 9034521202.93217412

' Display the numbers using the ToString method.
Console.WriteLine(intValue.ToString(fmt))
Console.WriteLine(decValue.ToString(fmt))            
Console.WriteLine(sngValue.ToString(fmt))
Console.WriteLine(dblValue.ToString(fmt))            
Console.WriteLine()

' Display the numbers using composite formatting.
Dim formatString As String = " {0,15:" + fmt + "}"
Console.WriteLine(formatString, intValue)      
Console.WriteLine(formatString, decValue)      
Console.WriteLine(formatString, sngValue)      
Console.WriteLine(formatString, dblValue)      
' The example displays the following output:
'       01053240
'       00103932.52
'       01549230
'       9034521202.93
'       
'               01053240
'            00103932.52
'               01549230
'          9034521202.93
```

## <a name="to-pad-a-numeric-value-with-a-specific-number-of-leading-zeros"></a>Per aggiungere un valore numerico con un determinato numero di zeri iniziali

1. Determinare il numero di zeri iniziali che deve avere il valore numerico.

2. Determine il numero di cifre alla sinistra del decimale nella stringa numerica non aggiunta. Per eseguire questa operazione:

    a. Determinare se la rappresentazione della stringa di un numero include un simbolo di separatore decimale.
    
    b. In questo caso, determinare il numero di caratteri alla sinistra del separatore decimale.       
    
    -oppure-
       
    In caso contrario, determinare la lunghezza della stringa. 
       
3. Creare una stringa di formato personalizzata in cui è usato il segnaposto zero ("0") per ciascuno degli zeri iniziali da visualizzare nella stringa e il segnaposto zero o il segnaposto cifra ("#") per rappresentare ciascuna cifra nella stringa predefinita. 

4. Specificare la stringa di formato personalizzata come parametro nel metodo ToString(String) del numero o in un metodo che supporta la formattazione composta.

Il seguente esempio aggiunge due valori [Double](xref:System.Double) con cinque zeri iniziali.

```csharp
double[] dblValues = { 9034521202.93217412, 9034521202 };
foreach (double dblValue in dblValues)
{
   string decSeparator = System.Globalization.NumberFormatInfo.CurrentInfo.NumberDecimalSeparator;
   string fmt, formatString;

   if (dblValue.ToString().Contains(decSeparator))
   {
      int digits = dblValue.ToString().IndexOf(decSeparator);
      fmt = new String('0', 5) + new String('#', digits) + ".##";
   }
   else
   {
      fmt = new String('0', dblValue.ToString().Length);   
   }
   formatString = "{0,20:" + fmt + "}";

   Console.WriteLine(dblValue.ToString(fmt));
   Console.WriteLine(formatString, dblValue);
}
// The example displays the following output:
//       000009034521202.93
//         000009034521202.93
//       9034521202
//                 9034521202 
```

```vb
Dim dblValues() As Double = { 9034521202.93217412, 9034521202 }
For Each dblValue As Double In dblValues
   Dim decSeparator As String = System.Globalization.NumberFormatInfo.CurrentInfo.NumberDecimalSeparator
   Dim fmt, formatString As String

   If dblValue.ToString.Contains(decSeparator) Then
      Dim digits As Integer = dblValue.ToString().IndexOf(decSeparator)
      fmt = New String("0"c, 5) + New String("#"c, digits) + ".##"
   Else
      fmt = New String("0"c, dblValue.ToString.Length)   
   End If
   formatString = "{0,20:" + fmt + "}"

   Console.WriteLine(dblValue.ToString(fmt))
   Console.WriteLine(formatString, dblValue)
Next
' The example displays the following output:
'       000009034521202.93
'         000009034521202.93
'       9034521202
'                 9034521202
```

## <a name="see-also"></a>Vedere anche

[Stringhe di formato numerico standard](standard-numeric.md)

[Stringhe di formato numerico personalizzato](custom-numeric.md)

[Formattazione composita](composite-format.md)


