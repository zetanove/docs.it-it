---
title: Analisi di stringhe numeriche in .NET
description: Analisi di stringhe numeriche in .NET
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: e393430a-731a-49fa-83de-ff7ed52d5704
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 85cd57d33b03f7a2105ee3f770b2f8bcc0a57ee4
ms.lasthandoff: 03/02/2017

---

# <a name="parsing-numeric-strings-in-net"></a>Analisi di stringhe numeriche in .NET

Tutti i tipi numerici hanno due metodi di analisi statici, `Parse` e `TryParse`, che è possibile usare per convertire la rappresentazione di stringa di un numero in un tipo numerico. Tali metodi consentono di analizzare le stringhe generate usando le stringhe di formato documentate in [Stringhe di formato numerico standard](standard-numeric.md) e [Stringhe di formato numerico personalizzato](custom-numeric.md). Per impostazione predefinita, i metodi `Parse` e `TryParse` consentono di convertire correttamente le stringhe contenenti cifre decimali integrali solo in valori integer. Consentono di convertire correttamente le stringhe che contengono cifre decimali integrali e frazionarie, separatori di gruppi e un separatore decimale in valori a virgola mobile. Il metodo `Parse` genera un'eccezione se l'operazione ha esito negativo, mentre il metodo `TryParse` restituisce `false`.

## <a name="parsing-and-format-providers"></a>Analisi e provider di formato

In genere, le rappresentazioni di stringa dei valori numerici differiscono in base alle impostazioni cultura. Gli elementi delle stringhe numeriche, ad esempio simboli di valuta, separatori di gruppi (o migliaia) e separatori decimali, variano in base alle impostazioni cultura. I metodi di analisi usano in modo implicito o esplicito un provider di formato che riconosce le variazioni specifiche delle impostazioni cultura. Se non viene specificato alcun provider di formato in una chiamata al metodo `Parse` o `TryParse`, viene usato il provider di formato associato alle impostazioni cultura del thread corrente, ossia l'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) restituito dalla proprietà [NumberFormatInfo.CurrentInfo](xref:System.Globalization.NumberFormatInfo.CurrentInfo). 

Un provider di formato è rappresentato da un'implementazione [IFormatProvider](xref:System.Globalization.NumberFormatInfo.CurrentInfo). Questa interfaccia ha un singolo membro, il metodo [GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)), il cui unico parametro è un oggetto [Type](xref:System.Type) che rappresenta il tipo da formattare. Questo metodo restituisce l'oggetto che fornisce le informazioni di formattazione. .NET supporta le due implementazioni [IFormatProvider](xref:System.Globalization.NumberFormatInfo.CurrentInfo) seguenti per l'analisi di stringhe numeriche:

* Un oggetto [CultureInfo](xref:System.Globalization.CultureInfo) il cui metodo [CultureInfo.GetFormat](xref:System.Globalization.CultureInfo.GetFormat(System.Type)) restituisce un oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) con informazioni di formattazione specifiche delle impostazioni cultura.

* Un oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) il cui metodo [NumberFormatInfo.GetFormat](xref:System.Globalization.NumberFormatInfo.GetFormat(System.Type)) restituisce se stesso.

Nell'esempio seguente si tenta di convertire ogni stringa in una matrice in un valore [Double](xref:System.Double). Per prima cosa si tenta di analizzare la stringa usando un provider di formato che riflette le convenzioni delle impostazioni cultura Inglese (Stati Uniti). Se questa operazione genera un'eccezione [FormatException](xref:System.FormatException), si tenta di analizzare la stringa usando un provider di formato che riflette le convenzioni delle impostazioni cultura Francese (Francia).

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      string[] values = { "1,304.16", "$1,456.78", "1,094", "152", 
                          "123,45 €", "1 304,16", "Ae9f" };
      double number;
      CultureInfo culture = null;

      foreach (string value in values) {
         try {
            culture = CultureInfo.CreateSpecificCulture("en-US");
            number = Double.Parse(value, culture);
            Console.WriteLine("{0}: {1} --> {2}", culture.Name, value, number);
         }   
         catch (FormatException) {
            Console.WriteLine("{0}: Unable to parse '{1}'.", 
                              culture.Name, value);
            culture = CultureInfo.CreateSpecificCulture("fr-FR");
            try {
               number = Double.Parse(value, culture);
               Console.WriteLine("{0}: {1} --> {2}", culture.Name, value, number);
            }
            catch (FormatException) {
               Console.WriteLine("{0}: Unable to parse '{1}'.", 
                                 culture.Name, value);
            }
         }
         Console.WriteLine();
      }   
   }
}
// The example displays the following output:
//    en-US: 1,304.16 --> 1304.16
//    
//    en-US: Unable to parse '$1,456.78'.
//    fr-FR: Unable to parse '$1,456.78'.
//    
//    en-US: 1,094 --> 1094
//    
//    en-US: 152 --> 152
//    
//    en-US: Unable to parse '123,45 €'.
//    fr-FR: Unable to parse '123,45 €'.
//    
//    en-US: Unable to parse '1 304,16'.
//    fr-FR: 1 304,16 --> 1304.16
//    
//    en-US: Unable to parse 'Ae9f'.
//    fr-FR: Unable to parse 'Ae9f'.
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim values() As String = { "1,304.16", "$1,456.78", "1,094", "152", 
                                 "123,45 €", "1 304,16", "Ae9f" }
      Dim number As Double
      Dim culture As CultureInfo = Nothing

      For Each value As String In values
         Try
            culture = CultureInfo.CreateSpecificCulture("en-US")
            number = Double.Parse(value, culture)
            Console.WriteLine("{0}: {1} --> {2}", culture.Name, value, number)
         Catch e As FormatException
            Console.WriteLine("{0}: Unable to parse '{1}'.", 
                              culture.Name, value)
            culture = CultureInfo.CreateSpecificCulture("fr-FR")
            Try
               number = Double.Parse(value, culture)
               Console.WriteLine("{0}: {1} --> {2}", culture.Name, value, number)
            Catch ex As FormatException
               Console.WriteLine("{0}: Unable to parse '{1}'.", 
                                 culture.Name, value)
            End Try
         End Try
         Console.WriteLine()
      Next
   End Sub
End Module
' The example displays the following output:
'    en-US: 1,304.16 --> 1304.16
'    
'    en-US: Unable to parse '$1,456.78'.
'    fr-FR: Unable to parse '$1,456.78'.
'    
'    en-US: 1,094 --> 1094
'    
'    en-US: 152 --> 152
'    
'    en-US: Unable to parse '123,45 €'.
'    fr-FR: Unable to parse '123,45 €'.
'    
'    en-US: Unable to parse '1 304,16'.
'    fr-FR: 1 304,16 --> 1304.16
'    
'    en-US: Unable to parse 'Ae9f'.
'    fr-FR: Unable to parse 'Ae9f'.
```

## <a name="parsing-and-numberstyles-values"></a>Analisi e valori NumberStyles

Gli elementi di stile, ad esempio spazi vuoti, separatori di gruppi e separatore decimale, che l'operazione di analisi è in grado di gestire sono definiti da un valore di enumerazione [NumberStyles](xref:System.Globalization.NumberStyles). Per impostazione predefinita, le stringhe che rappresentano i valori integer vengono analizzate usando il valore [NumberStyles.Integer](xref:System.Globalization.NumberStyles.Integer), che consente solo cifre numeriche, spazi vuoti iniziali e finali e un segno iniziale. Le stringhe che rappresentano valori a virgola mobile vengono analizzate usando una combinazione dei valori [NumberStyles.Float](xref:System.Globalization.NumberStyles.Float) e [NumberStyles.AllowThousands](xref:System.Globalization.NumberStyles.AllowThousands). Questo stile composto consente cifre decimali con spazi vuoti iniziali e finali, un segno iniziale, un separatore decimale, un separatore di gruppi e un esponente. Chiamando un overload del metodo `Parse` o `TryParse` che include un parametro di tipo [NumberStyles](xref:System.Globalization.NumberStyles) e impostando uno o più flag [NumberStyles](xref:System.Globalization.NumberStyles), è possibile stabilire quali elementi di stile possono essere presenti nella stringa per fare in modo che l'operazione di analisi abbia esito positivo. 

Ad esempio, una stringa contenente un separatore di gruppo non può essere convertita in un valore [Int32](xref:System.Int32) usando il metodo [Int32.Parse(String)](xref:System.Int32.Parse(System.String)). Tuttavia, la conversione viene completata correttamente se si utilizza il flag [NumberStyles.AllowThousands](xref:System.Globalization.NumberStyles.AllowThousands), come illustrato nell'esempio riportato di seguito.

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      string value = "1,304";
      int number;
      IFormatProvider provider = CultureInfo.CreateSpecificCulture("en-US");
      if (Int32.TryParse(value, out number))
         Console.WriteLine("{0} --> {1}", value, number);
      else
         Console.WriteLine("Unable to convert '{0}'", value);

      if (Int32.TryParse(value, NumberStyles.Integer | NumberStyles.AllowThousands, 
                        provider, out number))
         Console.WriteLine("{0} --> {1}", value, number);
      else
         Console.WriteLine("Unable to convert '{0}'", value);
   }
}
// The example displays the following output:
//       Unable to convert '1,304'
//       1,304 --> 1304
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim value As String = "1,304"
      Dim number As Integer
      Dim provider As IFormatProvider = CultureInfo.CreateSpecificCulture("en-US")
      If Int32.TryParse(value, number) Then
         Console.WriteLine("{0} --> {1}", value, number)
      Else
         Console.WriteLine("Unable to convert '{0}'", value)
      End If

      If Int32.TryParse(value, NumberStyles.Integer Or NumberStyles.AllowThousands, 
                        provider, number) Then
         Console.WriteLine("{0} --> {1}", value, number)
      Else
         Console.WriteLine("Unable to convert '{0}'", value)
      End If
   End Sub
End Module
' The example displays the following output:
'       Unable to convert '1,304'
'       1,304 --> 1304
```

> **Avviso**
>
> L'operazione di analisi usa sempre le convenzioni di formattazione di determinate impostazioni cultura. Se non si specificano le impostazioni cultura passando un oggetto [CultureInfo](xref:System.Globalization.CultureInfo) o [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo), vengono usate le impostazioni cultura associate al thread corrente.
 
Nella tabella seguente sono elencati i membri dell'enumerazione [NumberStyles](xref:System.Globalization.NumberStyles) e viene descritto l'effetto degli stessi sull'operazione di analisi.

Valore NumberStyles | Effetto sulla stringa da analizzare
------------------ | --------------------------------- 
[NumberStyles.None](xref:System.Globalization.NumberStyles.None) | Sono consentiti solo valori numerici.
[NumberStyles.AllowDecimalPoint](xref:System.Globalization.NumberStyles.AllowDecimalPoint) | Sono consentiti il separatore decimale e i numeri frazionari. Per i valori integer è consentito solo lo zero come numero frazionario. I separatori decimali validi sono determinati dalla proprietà [NumberFormatInfo.NumberDecimalSeparator](xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator) o [NumberFormatInfo.CurrencyDecimalSeparator](xref:System.Globalization.NumberFormatInfo.CurrencyDecimalSeparator).
[NumberStyles.AllowExponent](xref:System.Globalization.NumberStyles.AllowExponent) | Il carattere "e" o "E" può essere usato per indicare la notazione esponenziale.
[NumberStyles.AllowLeadingWhite](xref:System.Globalization.NumberStyles.AllowLeadingWhite) | È consentito lo spazio vuoto iniziale.
[NumberStyles.AllowTrailingWhite](xref:System.Globalization.NumberStyles.AllowTrailingWhite) | È consentito lo spazio vuoto finale.
[NumberStyles.AllowLeadingSign](xref:System.Globalization.NumberStyles.AllowLeadingSign) | Un segno positivo o negativo può precedere le cifre numeriche.
[NumberStyles.AllowTrailingSign](xref:System.Globalization.NumberStyles.AllowTrailingSign) | Un segno positivo o negativo può seguire le cifre numeriche.
[NumberStyles.AllowParentheses](xref:System.Globalization.NumberStyles.AllowParentheses) | Si possono usare parentesi per indicare i valori negativi.
[NumberStyles.AllowThousands](xref:System.Globalization.NumberStyles.AllowThousands) | È consentito il separatore di gruppi. Il carattere separatore di gruppi è determinato dalla proprietà [NumberFormatInfo.NumberGroupSeparator](xref:System.Globalization.NumberFormatInfo.NumberGroupSeparator) o [NumberFormatInfo.CurrencyGroupSeparator](xref:System.Globalization.NumberFormatInfo.CurrencyGroupSeparator).
[NumberStyles.AllowCurrencySymbol](xref:System.Globalization.NumberStyles.AllowCurrencySymbol) | È consentito il simbolo di valuta. Il simbolo di valuta è definito dalla proprietà [NumberFormatInfo.CurrencySymbol](xref:System.Globalization.NumberFormatInfo.CurrencySymbol).
[NumberStyles.AllowHexSpecifier](xref:System.Globalization.NumberStyles.AllowHexSpecifier) | La stringa da analizzare viene interpretata come numero esadecimale. Può includere le cifre esadecimali 0-9, A-F e a-f. Questo flag può essere usato solo per analizzare i valori integer.
 
L'enumerazione [NumberStyles](xref:System.Globalization.NumberStyles) usa anche i seguenti stili compositi, che includono più flag [NumberStyles](xref:System.Globalization.NumberStyles). 

Valore composito NumberStyles | Include i membri
---------------------------- | ---------------- 
[NumberStyles.Integer](xref:System.Globalization.NumberStyles.Integer) | Include gli stili [NumberStyles.AllowLeadingWhite](xref:System.Globalization.NumberStyles.AllowLeadingWhite), [NumberStyles.AllowTrailingWhite](xref:System.Globalization.NumberStyles.AllowTrailingWhite) e [NumberStyles.AllowLeadingSign](xref:System.Globalization.NumberStyles.AllowLeadingSign). Questo è lo stile predefinito usato per analizzare i valori integer.
[NumberStyles.Number](xref:System.Globalization.NumberStyles.Number) | Include gli stili [NumberStyles.AllowLeadingWhite](xref:System.Globalization.NumberStyles.AllowLeadingWhite), [NumberStyles.AllowTrailingWhite](xref:System.Globalization.NumberStyles.AllowTrailingWhite), [NumberStyles.AllowLeadingSign](xref:System.Globalization.NumberStyles.AllowLeadingSign), [NumberStyles.AllowTrailingSign](xref:System.Globalization.NumberStyles.AllowTrailingSign), [NumberStyles.AllowDecimalPoint](xref:System.Globalization.NumberStyles.AllowDecimalPoint) e [NumberStyles.AllowThousands](xref:System.Globalization.NumberStyles.AllowThousands).
[NumberStyles.Float](xref:System.Globalization.NumberStyles.Float) | Include gli stili [NumberStyles.AllowLeadingWhite](xref:System.Globalization.NumberStyles.AllowLeadingWhite), [NumberStyles.AllowTrailingWhite](xref:System.Globalization.NumberStyles.AllowTrailingWhite), [NumberStyles.AllowLeadingSign](xref:System.Globalization.NumberStyles.AllowLeadingSign), [NumberStyles.AllowDecimalPoint](xref:System.Globalization.NumberStyles.AllowDecimalPoint) e [NumberStyles.AllowExponent](xref:System.Globalization.NumberStyles.AllowExponent).
[NumberStyles.Currency](xref:System.Globalization.NumberStyles.Currency) | Include tutti gli stili tranne [NumberStyles.AllowExponent](xref:System.Globalization.NumberStyles.AllowExponent) e [NumberStyles.AllowHexSpecifier](xref:System.Globalization.NumberStyles.AllowHexSpecifier).
[NumberStyles.Any](xref:System.Globalization.NumberStyles.Any) | Include tutti gli stili tranne [NumberStyles.AllowHexSpecifier](xref:System.Globalization.NumberStyles.AllowHexSpecifier).
[NumberStyles.HexNumber](xref:System.Globalization.NumberStyles.HexNumber) | Include gli stili [NumberStyles.AllowLeadingWhite](xref:System.Globalization.NumberStyles.AllowLeadingWhite), [NumberStyles.AllowTrailingWhite](xref:System.Globalization.NumberStyles.AllowTrailingWhite) e [NumberStyles.AllowHexSpecifier](xref:System.Globalization.NumberStyles.AllowHexSpecifier).
 
## <a name="parsing-and-unicode-digits"></a>Analisi e cifre Unicode

Lo standard Unicode definisce gli elementi di codice per le cifre in diversi sistemi di scrittura. Ad esempio, gli elementi di codice compresi tra U+0030 e U+0039 rappresentano le cifre latine di base da 0 a 9, gli elementi di codice compresi tra U+09E6 e U+09EF rappresentano le cifre bengalesi da 0 a 9 e gli elementi di codice compresi tra U+FF10 e U+FF19 rappresentano le cifre Fullwidth da 0 a 9. Tuttavia, solo cifre numeriche riconosciute dai metodi di analisi sono le cifre latine di base da 0 a 9 con elementi di codice da U+0030 a U+0039. Se a un metodo di analisi numerico viene passata una stringa che contiene altre cifre, il metodo genera un'eccezione [FormatException](xref:System.FormatException).

Nell'esempio seguente viene usato il metodo [Int32.Parse](xref:System.Int32.Parse(System.String)) per analizzare le stringhe costituite da cifre in diversi sistemi di scrittura. Come illustrato nell'output dell'esempio, il tentativo di analizzare le cifre latine di base ha esito positivo, mentre il tentativo di analisi delle cifre Fullwidth, indoarabiche e bengalesi ha esito negativo.

```csharp
using System;

public class Example
{
   public static void Main()
   {
      string value;
      // Define a string of basic Latin digits 1-5.
      value = "\u0031\u0032\u0033\u0034\u0035";
      ParseDigits(value);

      // Define a string of Fullwidth digits 1-5.
      value = "\uFF11\uFF12\uFF13\uFF14\uFF15";
      ParseDigits(value);

      // Define a string of Arabic-Indic digits 1-5.
      value = "\u0661\u0662\u0663\u0664\u0665";
      ParseDigits(value);

      // Define a string of Bangla digits 1-5.
      value = "\u09e7\u09e8\u09e9\u09ea\u09eb";
      ParseDigits(value);
   }

   static void ParseDigits(string value)
   {
      try {
         int number = Int32.Parse(value);
         Console.WriteLine("'{0}' --> {1}", value, number);
      }   
      catch (FormatException) {
         Console.WriteLine("Unable to parse '{0}'.", value);      
      }     
   }
}
// The example displays the following output:
//       '12345' --> 12345
//       Unable to parse '１２３４５'.
//       Unable to parse '١٢٣٤٥'.
//       Unable to parse '১২৩৪৫'.
```

```vb
Module Example
   Public Sub Main()
      Dim value As String
      ' Define a string of basic Latin digits 1-5.
      value = ChrW(&h31) + ChrW(&h32) + ChrW(&h33) + ChrW(&h34) + ChrW(&h35)
      ParseDigits(value)

      ' Define a string of Fullwidth digits 1-5.
      value = ChrW(&hff11) + ChrW(&hff12) + ChrW(&hff13) + ChrW(&hff14) + ChrW(&hff15)
      ParseDigits(value)

      ' Define a string of Arabic-Indic digits 1-5.
      value = ChrW(&h661) + ChrW(&h662) + ChrW(&h663) + ChrW(&h664) + ChrW(&h665)
      ParseDigits(value)

      ' Define a string of Bangla digits 1-5.
      value = ChrW(&h09e7) + ChrW(&h09e8) + ChrW(&h09e9) + ChrW(&h09ea) + ChrW(&h09eb)
      ParseDigits(value)
   End Sub

   Sub ParseDigits(value As String)
      Try
         Dim number As Integer = Int32.Parse(value)
         Console.WriteLine("'{0}' --> {1}", value, number)
      Catch e As FormatException
         Console.WriteLine("Unable to parse '{0}'.", value)      
      End Try     
   End Sub
End Module
' The example displays the following output:
'       '12345' --> 12345
'       Unable to parse '１２３４５'.
'       Unable to parse '١٢٣٤٥'.
'       Unable to parse '১২৩৪৫'.
```

## <a name="see-also"></a>Vedere anche

[System.Globalization.NumberStyles](xref:System.Globalization.NumberStyles)

[Analisi di stringhe in .NET](parsing-strings.md)

[Formattazione di tipi in .NET](formatting-types.md)


