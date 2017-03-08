---
title: Stringhe di formato di data e ora personalizzato
description: Stringhe di formato di data e ora personalizzato
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/25/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 45f286f5-92c9-4150-957c-fa6d394bc29b
translationtype: Human Translation
ms.sourcegitcommit: 28625def4199a660fe0ea04ab75f4f65d2e0c9c4
ms.openlocfilehash: 285e4bfd6a53d576ce4538b09a2561065c93e399
ms.lasthandoff: 02/23/2017

---

# <a name="custom-date-and-time-format-strings"></a>Stringhe di formato di data e ora personalizzato

Una stringa di formato di data e ora definisce la rappresentazione di testo di un valore [DateTime](xref:System.DateTime) o [DateTimeOffset](xref:System.DateTimeOffset) risultante da un'operazione di formattazione. Può anche definire la rappresentazione di un valore di data e ora richiesto in un'operazione di analisi per convertire correttamente la stringa in una data e ora. Una stringa di formato personalizzata è costituita da uno o più identificatori di formato di data e ora personalizzati. Qualsiasi stringa diversa da una [stringa di formato di data e ora standard](standard-datetime.md) viene interpretata come stringa di formato di data e ora personalizzato. 

Le stringhe di formato data e ora personalizzato possono essere usate con valori [DateTime](xref:System.DateTime) e [DateTimeOffset](xref:System.DateTimeOffset).

Nelle operazioni di formattazione, le stringhe di formato di data e ora personalizzate possono essere usate con il metodo `ToString` di un'istanza di data e ora o con un metodo che supporta la formattazione composita. Nell'esempio seguente vengono illustrati entrambi gli usi. 

```csharp
DateTime thisDate1 = new DateTime(2011, 6, 10);
Console.WriteLine("Today is " + thisDate1.ToString("MMMM dd, yyyy") + ".");

DateTimeOffset thisDate2 = new DateTimeOffset(2011, 6, 10, 15, 24, 16, 
                                              TimeSpan.Zero);
Console.WriteLine("The current date and time: {0:MM/dd/yy H:mm:ss zzz}", 
                   thisDate2); 
// The example displays the following output:
//    Today is June 10, 2011.
//    The current date and time: 06/10/11 15:24:16 +00:00
```

```vb
Dim thisDate1 As Date = #6/10/2011#
Console.WriteLine("Today is " + thisDate1.ToString("MMMM dd, yyyy") + ".")

Dim thisDate2 As New DateTimeOffset(2011, 6, 10, 15, 24, 16, TimeSpan.Zero)
Console.WriteLine("The current date and time: {0:MM/dd/yy H:mm:ss zzz}", 
                   thisDate2) 
' The example displays the following output:
'    Today is June 10, 2011.
'    The current date and time: 06/10/11 15:24:16 +00:00
```

Nelle operazioni di formattazione, le stringhe di formato di data e ora personalizzato possono essere usate con i metodi [DateTime.ParseExact](xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider)), [DateTime.TryParseExact](xref:System.DateTime.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles,System.DateTime@)), [DateTimeOffset.ParseExact](xref:System.DateTimeOffset.ParseExact(System.String,System.String,System.IFormatProvider)) e [DateTimeOffset.TryParseExact](xref:System.DateTimeOffset.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles,System.DateTimeOffset@)). Questi metodi richiedono che una stringa di input sia esattamente conforme a un modello specifico affinché l'operazione di analisi abbia esito positivo. Nell'esempio seguente viene illustrata una chiamata al metodo [DateTimeOffset.ParseExact(String, String, IFormatProvider)](xref:System.DateTimeOffset.ParseExact(System.String,System.String,System.IFormatProvider)) per analizzare una data che deve includere un giorno, un mese e un anno a due cifre.

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      string[] dateValues = { "30-12-2011", "12-30-2011", 
                              "30-12-11", "12-30-11" };
      string pattern = "MM-dd-yy";
      DateTime parsedDate;

      foreach (var dateValue in dateValues) {
         if (DateTime.TryParseExact(dateValue, pattern, null, 
                                   DateTimeStyles.None, out parsedDate))
            Console.WriteLine("Converted '{0}' to {1:d}.", 
                              dateValue, parsedDate);
         else
            Console.WriteLine("Unable to convert '{0}' to a date and time.", 
                              dateValue);
      }
   }
}
// The example displays the following output:
//    Unable to convert '30-12-2011' to a date and time.
//    Unable to convert '12-30-2011' to a date and time.
//    Unable to convert '30-12-11' to a date and time.
//    Converted '12-30-11' to 12/30/2011.
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim dateValues() As String = { "30-12-2011", "12-30-2011", 
                                      "30-12-11", "12-30-11" }
      Dim pattern As String = "MM-dd-yy"
      Dim parsedDate As Date

      For Each dateValue As String In dateValues
         If DateTime.TryParseExact(dateValue, pattern, Nothing, 
                                   DateTimeStyles.None, parsedDate) Then
            Console.WriteLine("Converted '{0}' to {1:d}.", 
                              dateValue, parsedDate)
         Else
            Console.WriteLine("Unable to convert '{0}' to a date and time.", 
                              dateValue)
         End If                                                         
      Next
   End Sub
End Module
' The example displays the following output:
'    Unable to convert '30-12-2011' to a date and time.
'    Unable to convert '12-30-2011' to a date and time.
'    Unable to convert '30-12-11' to a date and time.
'    Converted '12-30-11' to 12/30/2011.
```

Nella tabella seguente vengono descritti gli identificatori di formato data e ora personalizzati e viene visualizzata una stringa di risultato prodotta da ogni identificatore di formato. Per impostazione predefinita, le stringhe di risultato riflettono le convenzioni di formattazione delle impostazioni cultura en-US. Se un identificatore di formato specifico produce una stringa di risultato localizzata, nell'esempio vengono anche indicate le impostazioni cultura alle quali si applica la stringa di risultato. Vedere la sezione Note per altre informazioni sull'uso di stringhe di formato di data e ora personalizzate.

Identificatore di formato | Descrizione | Esempi
---------------- | ----------- | --------
"d" | Giorno del mese, da 1 a 31. | `2019-06-01T13:45:30 -> 1`; `2019-06-15T13:45:30 -> 15`
"dd" | Giorno del mese, da 01 a 31. | `2019-06-01T13:45:30 -> 1`; `2019-06-15T13:45:30 -> 15`
"ddd" | Nome abbreviato del giorno della settimana. | `2019-06-15T13:45:30 -> Mon (en-US)`; `2019-06-15T13:45:30 -> Пн (ru-RU)`; `2019-06-15T13:45:30 -> lun. (fr-FR)`
"dddd" | Nome completo del giorno della settimana. | `2019-06-15T13:45:30 -> Monday (en-US)`; `2019-06-15T13:45:30 -> понедельник (ru-RU)`; `2019-06-15T13:45:30 -> lundi (fr-FR)`
"f" | Decimi di secondo in un valore data e ora. | `2019-06-15T13:45:30.6170000 -> 6`; `2019-06-15T13:45:30.05 -> 0` 
"ff" | Centesimi di secondo in un valore data e ora. | `2019-06-15T13:45:30.6170000 -> 61`; `2019-06-15T13:45:30.0050000 -> 00`
"fff" | Millisecondi in un valore data e ora. | `6/15/2019 13:45:30.617 -> 617`; `6/15/2019 13:45:30.0005 -> 000`
"ffff" | Decimillesimi di secondo in un valore data e ora. | `2019-06-15T13:45:30.6175000 -> 6175`; `2019-06-15T13:45:30.0000500 -> 0000`
"fffff" | Centomillesimi di secondo in un valore data e ora. | `2019-06-15T13:45:30.6175400 -> 61754`; `6/15/2019 13:45:30.000005 -> 00000`
"ffffff" | Milionesimi di secondo in un valore data e ora. | `2019-06-15T13:45:30.6175420 -> 617542`; `2019-06-15T13:45:30.0000005 -> 000000`
"fffffff" | Decine di milionesimi di secondo in un valore data e ora. | `2019-06-15T13:45:30.6175425 -> 6175425`;`2019-06-15T13:45:30.0001150 -> 0001150`
"F" | Se diverso da zero, decimi di secondo in un valore data e ora. | `2019-06-15T13:45:30.6170000 -> 6`; `2019-06-15T13:45:30.0500000 -> (no output)`
"FF" | Se diverso da zero, centesimi di secondo in un valore data e ora. | `2019-06-15T13:45:30.6170000 -> 61`; `2019-06-15T13:45:30.0050000 -> (no output)`
"FFF" | Se diverso da zero, millisecondi in un valore data e ora. | `2019-06-15T13:45:30.6170000 -> 617`; `2019-06-15T13:45:30.0005000 -> (no output)`
"FFFF" | Se diverso da zero, decimillesimi di secondo in un valore data e ora. | `2019-06-15T13:45:30.5275000 -> 5275`; `2019-06-15T13:45:30.0000500 -> (no output)`
"FFFFF" | Se diverso da zero, centomillesimi di secondo in un valore data e ora. | `2019-06-15T13:45:30.6175400 -> 61754`; `2019-06-15T13:45:30.0000050 -> (no output)`
"FFFFFF" | Se diverso da zero, milionesimi di secondo in un valore data e ora. | `2019-06-15T13:45:30.6175420 -> 617542`; `2019-06-15T13:45:30.0000005 -> (no output)`
"FFFFFFF" | Se diverso da zero, decimilionesimi di secondo in un valore data e ora. | `2019-06-15T13:45:30.6175425 -> 6175425`; `2019-06-15T13:45:30.0001150 -> 000115`
"g", "gg" | Periodo o era. | `2019-06-15T13:45:30.6170000 -> A.D.`
"h" | Ora, usando un orario in formato 12 ore da 1 a 12. | `2019-06-15T01:45:30 -> 1`; `2019-06-15T13:45:30 -> 1`
"hh" | Ora, usando un orario in formato 12 ore da 01 a 12. | `2019-06-15T01:45:30 -> 01`; `2019-06-15T13:45:30 -> 01`
"H" | Ora, usando un orario in formato 24 ore da 0 a 23. | `2019-06-15T01:45:30 -> 1`; `2019-06-15T13:45:30 -> 13`
"HH" | Ora, usando un orario in formato 24 ore da 00 a 23. | `2019-06-15T01:45:30 -> 01`; `2019-06-15T13:45:30 -> 13`
"K" | Informazioni sul fuso orario. | Con valori [DateTime](xref:System.DateTime): `2019-06-15T13:45:30, Kind Unspecified ->`; `2019-06-15T13:45:30, Kind Utc -> Z`; `2019-06-15T13:45:30, Kind Local -> -07:00 (depends on local computer settings)`; con valori [DateTimeOffset](xref:System.DateTimeOffset): `2019-06-15T01:45:30-07:00 --> -07:00`; `2019-06-15T08:45:30+00:00 --> +00:00`
"m" | Minuti, da 0 a 59. | `2019-06-15T01:09:30 -> 9`; `2019-06-15T13:29:30 -> 29`
"mm" | Minuti, da 00 a 59. | `2019-06-15T01:09:30 -> 09`; `2019-06-15T01:45:30 -> 45`
"M" | Mese, da 1 a 12. | `2019-06-15T13:45:30 -> 6`
"MM" | Mese, da 01 a 12. | `2019-06-15T13:45:30 -> 06`
"MMM" | Nome abbreviato del mese. | `2019-06-15T13:45:30 -> Jun (en-US)`; `2019-06-15T13:45:30 -> juin (fr-FR)`; `2019-06-15T13:45:30 -> Jun (zu-ZA)`
"MMMM" | Nome completo del mese. | `2019-06-15T13:45:30 -> June (en-US)`; `2019-06-15T13:45:30 -> juni (da-DK)`; `2019-06-15T13:45:30 -> uJuni (zu-ZA)`
"s" | Secondi, da 0 a 59. | `2019-06-15T13:45:09 -> 9`
"ss" | Secondi, da 00 a 59. | `2019-06-15T13:45:09 -> 09`
"t" | Primo carattere dell'indicatore AM/PM. | `2019-06-15T13:45:30 -> P (en-US)`; `2019-06-15T13:45:30 -> 午 (ja-JP)`; `2019-06-15T13:45:30 -> (fr-FR)`
"tt" | Indicatore AM/PM. | `2019-06-15T13:45:30 -> PM (en-US)`; `2019-06-15T13:45:30 -> 午後 (ja-JP)`; `2019-06-15T13:45:30 -> (fr-FR)`
"y" | Anno, da 0 a 99. | `0001-01-01T00:00:00 -> 1`; `0900-01-01T00:00:00 -> 0`; `1900-01-01T00:00:00 -> 0`; `2019-06-15T13:45:30 -> 9`; `2019-06-15T13:45:30 -> 19`
"yy" | Anno, da 00 a 99. | `0001-01-01T00:00:00 -> 01`; `0900-01-01T00:00:00 -> 00`; `1900-01-01T00:00:00 -> 00`; `2019-06-15T13:45:30 -> 19`
"yyy" | Anno, con un minimo di tre cifre. | `0001-01-01T00:00:00 -> 001`; `0900-01-01T00:00:00 -> 900`; `1900-01-01T00:00:00 -> 1900`; `2019-06-15T13:45:30 -> 2019`
"yyyy" | Anno, come numero a quattro cifre. | `0001-01-01T00:00:00 -> 0001`; `0900-01-01T00:00:00 -> 0900`; `1900-01-01T00:00:00 -> 1900`; `2019-06-15T13:45:30 -> 2019`
"yyyyy" | Anno, come numero a cinque cifre. | `0001-01-01T00:00:00 -> 00001`; `2019-06-15T13:45:30 -> 02019`
"z" | Offset delle ore rispetto a UTC, senza zeri iniziali. | `2019-06-15T13:45:30-07:00 -> -7`
"zz" | Offset delle ore rispetto a UTC, con uno zero iniziale per un valore a una sola cifra. | `2019-06-15T13:45:30-07:00 -> -07`
"zzz" | Offset di ore e minuti rispetto a UTC. | `2019-06-15T13:45:30-07:00 -> -07:00`
":" | Separatore dell'ora. | `2019-06-15T13:45:30 -> : (en-US)`; `2019-06-15T13:45:30 -> . (it-IT)`; `2019-06-15T13:45:30 -> : (ja-JP)`
"/" | Separatore di data. | `2019-06-15T13:45:30 -> / (en-US)`; `2019-06-15T13:45:30 -> - (ar-DZ)`; `2019-06-15T13:45:30 -> . (tr-TR)`
"string", 'string' | Delimitatore di stringa letterale. | `2019-06-15T13:45:30 ("arr:" h:m t) -> arr: 1:45 P`; `2019-06-15T13:45:30 ('arr:' h:m t) -> arr: 1:45 P`
% | Definisce il carattere seguente come identificatore di formato personalizzato. | `2019-06-15T13:45:30 (%h) -> 1`
\ | Carattere di escape. | `2019-06-15T13:45:30 (h \h) -> 1 h`
Qualsiasi altro carattere | Il carattere viene copiato nella stringa di risultato senza alcuna modifica. | `2019-06-15T01:45:30 (arr hh:mm t) -> arr 01:45 A`

Nelle sezioni seguenti vengono fornite altre informazioni su ogni identificatore di formato data e ora personalizzato. Se non specificato diversamente, ogni identificatore genera una rappresentazione di stringa identica, indipendentemente dal fatto che venga usato con un valore [DateTime](xref:System.DateTime) o con un valore [DateTimeOffset](xref:System.DateTimeOffset). 

## <a name="the-d-custom-format-specifier"></a>Identificatore di formato personalizzato "d"

L'identificatore di formato personalizzato "d" rappresenta il giorno del mese come numero compreso tra 1 e 31. Un giorno a una sola cifra viene formattato senza uno zero iniziale. 

Se l'identificatore di formato "d" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard "d". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#using-single-custom-format-specifiers) più avanti in questo argomento.

L'esempio seguente include l'identificatore di formato personalizzato "d" in diverse stringhe di formato. 

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15); 

Console.WriteLine(date1.ToString("d, M", 
                  CultureInfo.InvariantCulture)); 
// Displays 29, 8

Console.WriteLine(date1.ToString("d MMMM", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays 29 August
Console.WriteLine(date1.ToString("d MMMM", 
                  CultureInfo.CreateSpecificCulture("es-MX")));
// Displays 29 agosto  
```

```vb
Dim date1 As Date = #08/29/2008 7:27:15PM#

Console.WriteLine(date1.ToString("d, M", _
                  CultureInfo.InvariantCulture)) 
' Displays 29, 8

Console.WriteLine(date1.ToString("d MMMM", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays 29 August
Console.WriteLine(date1.ToString("d MMMM", _
                  CultureInfo.CreateSpecificCulture("es-MX")))
' Displays 29 agosto 
```

## <a name="the-dd-custom-format-specifier"></a>Identificatore di formato personalizzato "dd"

La stringa di formato personalizzata "dd" rappresenta il giorno del mese come numero compreso tra 01 e 31. Un giorno a una sola cifra viene formattato con uno zero iniziale. 

L'esempio seguente include l'identificatore di formato personalizzato "dd" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(2008, 1, 2, 6, 30, 15);

Console.WriteLine(date1.ToString("dd, MM", 
                  CultureInfo.InvariantCulture)); 
// 02, 01
```

```vb
Dim date1 As Date = #1/2/2008 6:30:15AM#

Console.WriteLine(date1.ToString("dd, MM", _
                  CultureInfo.InvariantCulture)) 
' 02, 01
```

## <a name="the-ddd-custom-format-specifier"></a>Identificatore di formato personalizzato "ddd"

L'identificatore di formato personalizzato "ddd" rappresenta il nome abbreviato del giorno della settimana. Il nome abbreviato localizzato del giorno della settimana viene recuperato dalla proprietà [DateTimeFormatInfo.AbbreviatedDayNames](xref:System.Globalization.DateTimeFormatInfo.AbbreviatedDayNames) delle impostazioni cultura correnti o specificate. 

L'esempio seguente include l'identificatore di formato personalizzato "ddd" in una stringa di formato personalizzata. 

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15);

Console.WriteLine(date1.ToString("ddd d MMM", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Fri 29 Aug
Console.WriteLine(date1.ToString("ddd d MMM", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays ven. 29 août    
```

```vb
Dim date1 As Date = #08/29/2008 7:27:15PM#

Console.WriteLine(date1.ToString("ddd d MMM", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays Fri 29 Aug
Console.WriteLine(date1.ToString("ddd d MMM", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays ven. 29 août
```

## <a name="the-dddd-custom-format-specifier"></a>Identificatore di formato personalizzato "dddd"

L'identificatore di formato personalizzato "dddd" (più qualsiasi numero di identificatori "d" aggiuntivi) rappresenta il nome completo del giorno della settimana. Il nome localizzato del giorno della settimana viene recuperato dalla proprietà [DateTimeFormatInfo.DayNames](xref:System.Globalization.DateTimeFormatInfo.DayNames) delle impostazioni cultura correnti o specificate. 

L'esempio seguente include l'identificatore di formato personalizzato "dddd" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15);

Console.WriteLine(date1.ToString("dddd dd MMMM", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Friday 29 August
Console.WriteLine(date1.ToString("dddd dd MMMM", 
                  CultureInfo.CreateSpecificCulture("it-IT")));
// Displays venerdì 29 agosto    
```

```vb
Dim date1 As Date = #08/29/2008 7:27:15PM#

Console.WriteLine(date1.ToString("dddd dd MMMM", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays Friday 29 August
Console.WriteLine(date1.ToString("dddd dd MMMM", _
                  CultureInfo.CreateSpecificCulture("it-IT")))
' Displays venerdì 29 agosto                                          
```

## <a name="the-f-custom-format-specifier"></a>Identificatore di formato personalizzato "f"

L'identificatore di formato personalizzato "f" rappresenta la cifra più significativa della frazione di secondi, ovvero i decimi di secondo in un valore di data e ora.

Se l'identificatore di formato "f" viene usato senza altri identificatori di formato, viene interpretato come l'identificatore di formato di data e ora standard "f". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#using-single-custom-format-specifiers) più avanti in questo argomento.

Quando si usano identificatori di formato "f" come parte di una stringa di formato fornita con il metodo [DateTime.ParseExact](xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider)), [DateTime.TryParseExact](xref:System.DateTime.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles,System.DateTime@)), [DateTimeOffset.ParseExact](xref:System.DateTimeOffset.ParseExact(System.String,System.String,System.IFormatProvider)) o [DateTimeOffset.TryParseExact](xref:System.DateTimeOffset.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles,System.DateTimeOffset@)), il numero di identificatori di formato "f" indica il numero di cifre più significative della frazione di secondi che devono essere presenti per analizzare correttamente la stringa.

L'esempio seguente include l'identificatore di formato personalizzato "f" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15, 18);
CultureInfo ci = CultureInfo.InvariantCulture;

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci));
// Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci));
// Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci));
// Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci));
// Displays 07:27:15.018
```

```vb
Dim date1 As New Date(2008, 8, 29, 19, 27, 15, 018)
Dim ci As CultureInfo = CultureInfo.InvariantCulture

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci))
' Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci))
' Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci))
' Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci))
' Displays 07:27:15.018
```

## <a name="the-ff-custom-format-specifier"></a>Identificatore di formato personalizzato "ff"

L'identificatore di formato personalizzato "ff" rappresenta le due cifre più significative della frazione di secondi, ovvero i centesimi di secondo in un valore di data e ora. 

L'esempio seguente include l'identificatore di formato personalizzato "ff" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15, 18);
CultureInfo ci = CultureInfo.InvariantCulture;

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci));
// Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci));
// Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci));
// Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci));
// Displays 07:27:15.018
```

```vb
Dim date1 As New Date(2008, 8, 29, 19, 27, 15, 018)
Dim ci As CultureInfo = CultureInfo.InvariantCulture

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci))
' Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci))
' Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci))
' Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci))
' Displays 07:27:15.018
```

## <a name="the-fff-custom-format-specifier"></a>Identificatore di formato personalizzato "fff"

L'identificatore di formato personalizzato "fff" rappresenta le tre cifre più significative della frazione di secondi, ovvero i millisecondi in un valore di data e ora. 

L'esempio seguente include l'identificatore di formato personalizzato "fff" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15, 18);
CultureInfo ci = CultureInfo.InvariantCulture;

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci));
// Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci));
// Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci));
// Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci));
// Displays 07:27:15.018
```

```vb
Dim date1 As New Date(2008, 8, 29, 19, 27, 15, 018)
Dim ci As CultureInfo = CultureInfo.InvariantCulture

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci))
' Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci))
' Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci))
' Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci))
' Displays 07:27:15.018
```

## <a name="the-ffff-custom-format-specifier"></a>Identificatore di formato personalizzato "ffff"

L'identificatore di formato personalizzato "ffff" rappresenta le quattro cifre più significative della frazione di secondi, ovvero i decimillesimi di secondo in un valore di data e ora.

Sebbene sia possibile visualizzare i decimillesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema.

## <a name="the-fffff-custom-format-specifier"></a>Identificatore di formato personalizzato "fffff"

L'identificatore di formato personalizzato "fffff" rappresenta le cinque cifre più significative della frazione di secondi, ovvero i centomillesimi di secondo in un valore di data e ora.

Sebbene sia possibile visualizzare i centomillesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema. 

## <a name="the-ffffff-custom-format-specifier"></a>Identificatore di formato personalizzato "ffffff"

L'identificatore di formato personalizzato "ffffff" rappresenta le sei cifre più significative della frazione di secondi, ovvero i milionesimi di secondo in un valore di data e ora.

Sebbene sia possibile visualizzare i milionesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema. 

## <a name="the-fffffff-custom-format-specifier"></a>Identificatore di formato personalizzato "fffffff"

L'identificatore di formato personalizzato "fffffff" rappresenta le sette cifre più significative della frazione di secondi, ovvero i decimilionesimi di secondo in un valore di data e ora.

Sebbene sia possibile visualizzare i decimilionesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema. 

## <a name="the-f-custom-format-specifier"></a>Identificatore di formato personalizzato "F"

L'identificatore di formato personalizzato "F" rappresenta la cifra più significativa della frazione di secondi, ovvero i decimi di secondo in un valore di data e ora. Se la cifra è zero, non viene prodotta alcuna visualizzazione. 

Se l'identificatore di formato "F" viene usato senza altri identificatori di formato, viene interpretato come l'identificatore di formato di data e ora standard "F". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#using-single-custom-format-specifiers) più avanti in questo argomento.

Il numero di identificatori di formato "F" usati con il metodo [DateTime.ParseExact](xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider)), [DateTime.TryParseExact](xref:System.DateTime.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles,System.DateTime@)), [DateTimeOffset.ParseExact](xref:System.DateTimeOffset.ParseExact(System.String,System.String,System.IFormatProvider)) o [DateTimeOffset.TryParseExact](xref:System.DateTimeOffset.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles,System.DateTimeOffset@)) indica il numero massimo di cifre più significative della frazione di secondi che possono essere presenti per analizzare correttamente la stringa.

L'esempio seguente include l'identificatore di formato personalizzato "F" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15, 18);
CultureInfo ci = CultureInfo.InvariantCulture;

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci));
// Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci));
// Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci));
// Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci));
// Displays 07:27:15.018
```

```vb
Dim date1 As New Date(2008, 8, 29, 19, 27, 15, 018)
Dim ci As CultureInfo = CultureInfo.InvariantCulture

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci))
' Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci))
' Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci))
' Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci))
' Displays 07:27:15.018
```

## <a name="the-ff-custom-format-specifier"></a>Identificatore di formato personalizzato "FF"

L'identificatore di formato personalizzato "FF" rappresenta le due cifre più significative della frazione di secondi, ovvero i centesimi di secondo in un valore di data e ora. Gli zeri finali o le cifre con due zeri non vengono tuttavia visualizzate. 

L'esempio seguente include l'identificatore di formato personalizzato "FF" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15, 18);
CultureInfo ci = CultureInfo.InvariantCulture;

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci));
// Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci));
// Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci));
// Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci));
// Displays 07:27:15.018
```

```vb
Dim date1 As New Date(2008, 8, 29, 19, 27, 15, 018)
Dim ci As CultureInfo = CultureInfo.InvariantCulture

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci))
' Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci))
' Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci))
' Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci))
' Displays 07:27:15.018
```

## <a name="the-fff-custom-format-specifier"></a>Identificatore di formato personalizzato "FFF"

L'identificatore di formato personalizzato "FFF" rappresenta le tre cifre più significative della frazione di secondi, ovvero i millisecondi in un valore di data e ora. Gli zeri finali o le cifre con tre zeri non vengono tuttavia visualizzate. 

L'esempio seguente include l'identificatore di formato personalizzato "FFF" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15, 18);
CultureInfo ci = CultureInfo.InvariantCulture;

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci));
// Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci));
// Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci));
// Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci));
// Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci));
// Displays 07:27:15.018
````

```vb
Dim date1 As New Date(2008, 8, 29, 19, 27, 15, 018)
Dim ci As CultureInfo = CultureInfo.InvariantCulture

Console.WriteLine(date1.ToString("hh:mm:ss.f", ci))
' Displays 07:27:15.0
Console.WriteLine(date1.ToString("hh:mm:ss.F", ci))
' Displays 07:27:15
Console.WriteLine(date1.ToString("hh:mm:ss.ff", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.FF", ci))
' Displays 07:27:15.01
Console.WriteLine(date1.ToString("hh:mm:ss.fff", ci))
' Displays 07:27:15.018
Console.WriteLine(date1.ToString("hh:mm:ss.FFF", ci))
' Displays 07:27:15.018
```

## <a name="the-ffff-custom-format-specifier"></a>Identificatore di formato personalizzato "FFFF"

L'identificatore di formato personalizzato "FFFF" rappresenta le quattro cifre più significative della frazione di secondi, ovvero i decimillesimi di secondo in un valore di data e ora. Gli zeri finali o le cifre con quattro zeri non vengono tuttavia visualizzate.

Sebbene sia possibile visualizzare i decimillesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema.

## <a name="the-fffff-custom-format-specifier"></a>Identificatore di formato personalizzato "FFFFF"

L'identificatore di formato personalizzato "FFFFF" rappresenta le cinque cifre più significative della frazione di secondi, ovvero i centomillesimi di secondo in un valore di data e ora. Gli zeri finali o le cifre con cinque zeri non vengono tuttavia visualizzate.

Sebbene sia possibile visualizzare i centomillesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema.

## <a name="the-ffffff-custom-format-specifier"></a>Identificatore di formato personalizzato "FFFFFF"

L'identificatore di formato personalizzato "FFFFFF" rappresenta le sei cifre più significative della frazione di secondi, ovvero i milionesimi di secondo in un valore di data e ora. Gli zeri finali o le cifre con sei zeri non vengono visualizzate.

Sebbene sia possibile visualizzare i milionesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema.

## <a name="the-fffffff-custom-format-specifier"></a>Identificatore di formato personalizzato "FFFFFFF"

L'identificatore di formato personalizzato "FFFFFFF" rappresenta le sette cifre più significative della frazione di secondi, ovvero i decimilionesimi di secondo in un valore di data e ora. Gli zeri finali o le cifre con sette zeri non vengono tuttavia visualizzate.

Sebbene sia possibile visualizzare i decimilionesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema.

## <a name="the-g-or-gg-custom-format-specifier"></a>Identificatore di formato personalizzato "g" o "gg"

Gli identificatori di formato personalizzati "g" o "gg" (più qualsiasi numero di identificatori "g" aggiuntivi) rappresentano il periodo o l'era, ad esempio D.C. Questo identificatore viene ignorato dall'operazione di formattazione se la data da formattare non è associata a una stringa di periodo o di era. 

Se l'identificatore di formato "g" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard "g". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#using-single-custom-format-specifiers) più avanti in questo argomento.

L'esempio seguente include l'identificatore di formato personalizzato "g" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(70, 08, 04);

Console.WriteLine(date1.ToString("MM/dd/yyyy g", 
                  CultureInfo.InvariantCulture));
// Displays 08/04/0070 A.D.                        
Console.WriteLine(date1.ToString("MM/dd/yyyy g", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));                         
// Displays 08/04/0070 ap. J.-C.
```

```vb
Dim date1 As Date = #08/04/0070#

Console.WriteLine(date1.ToString("MM/dd/yyyy g", _
                  CultureInfo.InvariantCulture))
' Displays 08/04/0070 A.D.                        
Console.WriteLine(date1.ToString("MM/dd/yyyy g", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))                         
' Displays 08/04/0070 ap. J.-C.
```

## <a name="the-h-custom-format-specifier"></a>Identificatore di formato personalizzato "h"

L'identificatore di formato personalizzato "h" rappresenta l'ora come numero compreso tra 1 e 12, ovvero l'ora rappresentata nell'orario in formato 12 ore in base al quale il conteggio riparte da mezzanotte o da mezzogiorno. Una particolare ora dopo mezzanotte non è distinguibile dalla stessa ora dopo mezzogiorno. L'ora non viene arrotondata e se è costituita da una singola cifra viene formattata senza zero iniziale. Se viene, ad esempio, specificata un'ora equivalente alle 5:43 della mattina o del pomeriggio, tramite questo identificatore di formato personalizzato viene visualizzato "5". 

Se l'identificatore di formato "h" viene usato senza altri identificatori di formato personalizzato, viene interpretato come l'identificatore di formato di data e ora standard e viene generato un evento [FormatException](xref:System.FormatException). Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#using-single-custom-format-specifiers) più avanti in questo argomento.

L'esempio seguente include l'identificatore di formato personalizzato "h" in una stringa di formato personalizzata.

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1 µ                        
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1.5 µ
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1 µ                        
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1.5 µ
```

## <a name="the-hh-custom-format-specifier"></a>Identificatore di formato personalizzato "hh"

L'identificatore di formato personalizzato "hh" (più qualsiasi numero di identificatori "h" aggiuntivi) rappresenta l'ora come numero compreso tra 01 e 12, ovvero l'ora rappresentata nell'orario in formato 12 ore in base al quale il conteggio riparte da mezzanotte o da mezzogiorno. Una particolare ora dopo mezzanotte non è distinguibile dalla stessa ora dopo mezzogiorno. L'ora non viene arrotondata e se è costituita da una singola cifra viene formattata con uno zero iniziale. Se viene, ad esempio, specificata un'ora equivalente alle 5:43 della mattina o del pomeriggio, tramite questo identificatore di formato viene visualizzato "05".

L'esempio seguente include l'identificatore di formato personalizzato "hh" in una stringa di formato personalizzata.

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01 du.
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01.50 du.
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01 du.
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01.50 du.
```

## <a name="the-h-custom-format-specifier"></a>Identificatore di formato personalizzato "H"

L'identificatore di formato personalizzato "H" rappresenta l'ora come numero compreso tra 0 e 23, ovvero l'ora rappresentata nell'orario in formato 24 ore a base zero in base al quale il conteggio riparte da mezzanotte. Un'ora costituita da una singola cifra viene formattata senza zero iniziale. 

Se l'identificatore di formato "H" viene usato senza altri identificatori di formato personalizzato, viene interpretato come l'identificatore di formato di data e ora standard e viene generato un evento [FormatException](xref:System.FormatException). Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#using-single-custom-format-specifiers) più avanti in questo argomento.

L'esempio seguente include l'identificatore di formato personalizzato "H" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(2008, 1, 1, 6, 9, 1);
Console.WriteLine(date1.ToString("H:mm:ss", 
                  CultureInfo.InvariantCulture));
// Displays 6:09:01 
```

```vb
Dim date1 As Date = #6:09:01AM#
Console.WriteLine(date1.ToString("H:mm:ss", _
                  CultureInfo.InvariantCulture))
' Displays 6:09:01 
```

## <a name="the-hh-custom-format-specifier"></a>Identificatore di formato personalizzato "HH"

L'identificatore di formato personalizzato "HH" (più qualsiasi numero di identificatori "H" aggiuntivi) rappresenta l'ora come numero compreso tra 00 e 23, ovvero l'ora rappresentata nell'orario in formato 24 ore a base zero in base al quale il conteggio riparte da mezzanotte. Un'ora costituita da una singola cifra viene formattata con uno zero iniziale. 

L'esempio seguente include l'identificatore di formato personalizzato "HH" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(2008, 1, 1, 6, 9, 1);
Console.WriteLine(date1.ToString("HH:mm:ss", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01                        
```

```vb
Dim date1 As Date = #6:09:01AM#
Console.WriteLine(date1.ToString("HH:mm:ss", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01
```

## <a name="the-k-custom-format-specifier"></a>Identificatore di formato personalizzato "K"

L'identificatore di formato personalizzato "K" rappresenta le informazioni sul fuso orario di un valore di data e ora. Quando questo identificatore di formato viene usato con valori [DateTime](xref:System.DateTime), la stringa di risultato viene definita dal valore della proprietà [DateTime.Kind](xref:System.DateTime.Kind): 
 
* Per il fuso orario locale (un valore della proprietà [DateTime.Kind](xref:System.DateTime.Kind) uguale a [DateTimeKind.Local](xref:System.DateTimeKind.Local)) questo identificatore è equivalente all'identificatore "zzz" e genera una stringa di risultato che contiene l'offset locale rispetto all'ora UTC (Coordinated Universal Time), ad esempio "-07.00". 

* Per un'ora UTC (un valore della proprietà [DateTime.Kind](xref:System.DateTime.Kind) uguale a [DateTimeKind.Utc](xref:System.DateTimeKind.Utc)) la stringa di risultato include un carattere "Z" per rappresentare una data UTC. 

* Per un'ora di un fuso orario non specificato (un'ora la cui proprietà [DateTime.Kind](xref:System.DateTime.Kind) è uguale a [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified)), il risultato è equivalente a [String.Empty](xref:System.String#System_String_Empty). 

Per i valori [DateTimeOffset](xref:System.DateTimeOffset), l'identificatore di formato "K" è equivalente all'identificatore di formato "zz" e genera una stringa di risultato che contiene l'offset del valore [DateTimeOffset](xref:System.DateTimeOffset) rispetto all'ora UTC. 

Se l'identificatore di formato "K" viene usato senza altri identificatori di formato personalizzato, viene interpretato come l'identificatore di formato di data e ora standard e viene generato un evento [FormatException](xref:System.FormatException). Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#using-single-custom-format-specifiers) più avanti in questo argomento.

L'esempio seguente illustra la stringa risultante dall'uso dell'identificatore di formato personalizzato "K" con vari valori [DateTime](xref:System.DateTime) e [DateTimeOffset](xref:System.DateTimeOffset) in un sistema nel fuso orario Pacifico (Stati Uniti).

```csharp
Console.WriteLine(DateTime.Now.ToString("%K"));
// Displays -07:00
Console.WriteLine(DateTime.UtcNow.ToString("%K"));
// Displays Z      
Console.WriteLine("'{0}'", 
                  DateTime.SpecifyKind(DateTime.Now, 
                       DateTimeKind.Unspecified).ToString("%K"));
// Displays ''      
Console.WriteLine(DateTimeOffset.Now.ToString("%K"));
// Displays -07:00
Console.WriteLine(DateTimeOffset.UtcNow.ToString("%K"));
// Displays +00:00
Console.WriteLine(new DateTimeOffset(2008, 5, 1, 6, 30, 0, 
                      new TimeSpan(5, 0, 0)).ToString("%K"));
// Displays +05:00  
```

```vb
Console.WriteLine(Date.Now.ToString("%K"))
' Displays -07:00
Console.WriteLine(Date.UtcNow.ToString("%K"))
' Displays Z      
Console.WriteLine("'{0}'", _
                  Date.SpecifyKind(Date.Now, _
                                   DateTimeKind.Unspecified). _
                  ToString("%K"))
' Displays ''      
Console.WriteLine(DateTimeOffset.Now.ToString("%K"))
' Displays -07:00
Console.WriteLine(DateTimeOffset.UtcNow.ToString("%K"))
' Displays +00:00
Console.WriteLine(New DateTimeOffset(2008, 5, 1, 6, 30, 0, _
                                     New TimeSpan(5, 0, 0)). _
                  ToString("%K"))
' Displays +05:00 
```

## <a name="the-m-custom-format-specifier"></a>Identificatore di formato personalizzato "m"

L'identificatore di formato personalizzato "m" rappresenta i minuti come numero compreso tra 0 e 59. Tali minuti rappresentano il numero intero di minuti passati dall'ultima ora. Un minuto costituito da una singola cifra viene formattato senza zero iniziale. 

Se l'identificatore di formato "m" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard "m". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#using-single-custom-format-specifiers) più avanti in questo argomento. 

L'esempio seguente include l'identificatore di formato personalizzato "m" in una stringa di formato personalizzata.

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1 µ                        
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1.5 µ
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1 µ                        
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1.5 µ
```

## <a name="the-mm-custom-format-specifier"></a>Identificatore di formato personalizzato "mm"

L'identificatore di formato personalizzato "mm" (più qualsiasi numero di identificatori "m" aggiuntivi) rappresenta i minuti come numero compreso tra 00 e 59. Tali minuti rappresentano il numero intero di minuti passati dall'ultima ora. Un minuto costituito da una singola cifra viene formattato con uno zero iniziale. 

L'esempio seguente include l'identificatore di formato personalizzato "mm" in una stringa di formato personalizzata.

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01 du.
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01.50 du.
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01 du.
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01.50 du.
```

## <a name="the-m-custom-format-specifier"></a>Identificatore di formato personalizzato "M"

L'identificatore di formato personalizzato "M" rappresenta il mese come numero compreso tra 1 e 12 (o tra 1 e 13 per i calendari con 13 mesi). Un mese a una sola cifra viene formattato senza uno zero iniziale. 

Se l'identificatore di formato "M" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard "M". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#using-single-custom-format-specifiers) più avanti in questo argomento.

L'esempio seguente include l'identificatore di formato personalizzato "M" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(2008, 8, 18);
Console.WriteLine(date1.ToString("(M) MMM, MMMM", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays (8) Aug, August
Console.WriteLine(date1.ToString("(M) MMM, MMMM", 
                  CultureInfo.CreateSpecificCulture("nl-NL")));                       
// Displays (8) aug, augustus
Console.WriteLine(date1.ToString("(M) MMM, MMMM", 
                  CultureInfo.CreateSpecificCulture("lv-LV")));                        
// Displays (8) Aug, augusts
```

```vb
Dim date1 As Date = #8/18/2008#
Console.WriteLine(date1.ToString("(M) MMM, MMMM", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays (8) Aug, August
Console.WriteLine(date1.ToString("(M) MMM, MMMM", _
                  CultureInfo.CreateSpecificCulture("nl-NL")))                        
' Displays (8) aug, augustus
Console.WriteLine(date1.ToString("(M) MMM, MMMM", _
                  CultureInfo.CreateSpecificCulture("lv-LV")))                        
' Displays (8) Aug, augusts 
```

## <a name="the-mm-custom-format-specifier"></a>Identificatore di formato personalizzato "MM"

L'identificatore di formato personalizzato "MM" rappresenta il mese come numero compreso tra 01 e 12 (o tra 1 e 13 per i calendari con 13 mesi). Un mese a una sola cifra viene formattato con uno zero iniziale. 

L'esempio seguente include l'identificatore di formato personalizzato "MM" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(2008, 1, 2, 6, 30, 15);

Console.WriteLine(date1.ToString("dd, MM", 
                  CultureInfo.InvariantCulture)); 
// 02, 01
```

```vb
Dim date1 As Date = #1/2/2008 6:30:15AM#

Console.WriteLine(date1.ToString("dd, MM", _
                  CultureInfo.InvariantCulture)) 
' 02, 01
```

## <a name="the-mmm-custom-format-specifier"></a>Identificatore di formato personalizzato "MMM"

L'identificatore di formato personalizzato "MMM" rappresenta il nome abbreviato del mese. Il nome abbreviato localizzato del mese viene recuperato dalla proprietà [DateTimeFormatInfo.AbbreviatedMonthNames](xref:System.Globalization.DateTimeFormatInfo.AbbreviatedMonthNames) delle impostazioni cultura correnti o specificate.

L'esempio seguente include l'identificatore di formato personalizzato "MMM" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15);

Console.WriteLine(date1.ToString("ddd d MMM", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Fri 29 Aug
Console.WriteLine(date1.ToString("ddd d MMM", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays ven. 29 août
```

```vb
Dim date1 As Date = #08/29/2008 7:27:15PM#

Console.WriteLine(date1.ToString("ddd d MMM", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays Fri 29 Aug
Console.WriteLine(date1.ToString("ddd d MMM", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays ven. 29 août
```

## <a name="the-mmmm-custom-format-specifier"></a>Identificatore di formato personalizzato "MMMM"

L'identificatore di formato personalizzato "MMMM" rappresenta il nome completo del mese. Il nome localizzato del mese viene recuperato dalla proprietà [DateTimeFormatInfo.MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames) delle impostazioni cultura correnti o specificate. 

L'esempio seguente include l'identificatore di formato personalizzato "MMMM" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(2008, 8, 29, 19, 27, 15);

Console.WriteLine(date1.ToString("dddd dd MMMM", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Friday 29 August
Console.WriteLine(date1.ToString("dddd dd MMMM", 
                  CultureInfo.CreateSpecificCulture("it-IT")));
// Displays venerdì 29 agosto 
```

```vb
Dim date1 As Date = #08/29/2008 7:27:15PM#

Console.WriteLine(date1.ToString("dddd dd MMMM", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays Friday 29 August
Console.WriteLine(date1.ToString("dddd dd MMMM", _
                  CultureInfo.CreateSpecificCulture("it-IT")))
' Displays venerdì 29 agosto  
```

## <a name="the-s-custom-format-specifier"></a>Identificatore di formato personalizzato "s"

L'identificatore di formato personalizzato "s" rappresenta i secondi come numero compreso tra 0 e 59. Il risultato rappresenta il numero intero di secondi passati dall'ultimo minuto. Un secondo costituito da una singola cifra viene formattato senza zero iniziale. 

Se l'identificatore di formato "s" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard "s". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#using-single-custom-format-specifiers) più avanti in questo argomento. 

L'esempio seguente include l'identificatore di formato personalizzato "s" in una stringa di formato personalizzata.

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1 µ                        
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1.5 µ
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1 µ                        
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1.5 µ
```

## <a name="the-ss-custom-format-specifier"></a>Identificatore di formato personalizzato "ss"

L'identificatore di formato personalizzato "ss" (più qualsiasi numero di identificatori "s" aggiuntivi) rappresenta i secondi come numero compreso tra 00 e 59. Il risultato rappresenta il numero intero di secondi passati dall'ultimo minuto. Un secondo costituito da una singola cifra viene formattato con uno zero iniziale. 

L'esempio seguente include l'identificatore di formato personalizzato "ss" in una stringa di formato personalizzata.

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01 du.
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01.50 du.
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01 du.
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01.50 du.
```

## <a name="the-t-custom-format-specifier"></a>Identificatore di formato personalizzato "t"

L'identificatore di formato personalizzato "t" rappresenta il primo carattere dell'indicatore AM/PM. L'indicatore localizzato appropriato viene recuperato dalla proprietà [DateTimeFormatInfo.AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) o [DateTimeFormatInfo.PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) delle impostazioni cultura correnti o specificate. L'indicatore AM viene usato per tutti gli orari da 0:00:00 (mezzanotte) a 11:59:59.999. L'indicatore PM viene usato per tutti gli orari da 12:00:00 (mezzogiorno) a 23:59:59.999. 

Se l'identificatore di formato "t" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato data e ora standard "t". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#using-single-custom-format-specifiers) più avanti in questo argomento.

L'esempio seguente include l'identificatore di formato personalizzato "t" in una stringa di formato personalizzata.

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1 µ                        
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.InvariantCulture));
// Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", 
                  CultureInfo.CreateSpecificCulture("el-GR")));
// Displays 6:9:1.5 µ
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1 µ                        
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.InvariantCulture))
' Displays 6:9:1.5 P
Console.WriteLine(date1.ToString("h:m:s.F t", _
                  CultureInfo.CreateSpecificCulture("el-GR")))
' Displays 6:9:1.5 µ
```

## <a name="the-tt-custom-format-specifier"></a>Identificatore di formato personalizzato "tt"

L'identificatore di formato personalizzato "tt" (più qualsiasi numero di identificatori "t" aggiuntivi) rappresenta l'indicatore AM/PM completo. L'indicatore localizzato appropriato viene recuperato dalla proprietà [DateTimeFormatInfo.AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) o [DateTimeFormatInfo.PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) delle impostazioni cultura correnti o specificate. L'indicatore AM viene usato per tutti gli orari da 0:00:00 (mezzanotte) a 11:59:59.999. L'indicatore PM viene usato per tutti gli orari da 12:00:00 (mezzogiorno) a 23:59:59.999.

Assicurarsi di usare l'identificatore "tt" per le lingue per le quali è necessario mantenere la distinzione tra AM e PM. Un esempio è la lingua giapponese per cui gli indicatori AM e PM differiscono in corrispondenza del secondo carattere anziché del primo.

L'esempio seguente include l'identificatore di formato personalizzato "tt" in una stringa di formato personalizzata.

```csharp
DateTime date1; 
date1 = new DateTime(2008, 1, 1, 18, 9, 1);
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01 du.
date1 = new DateTime(2008, 1, 1, 18, 9, 1, 500);
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.InvariantCulture));
// Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", 
                  CultureInfo.CreateSpecificCulture("hu-HU")));
// Displays 06:09:01.50 du.
```

```vb
Dim date1 As Date 
date1 = #6:09:01PM#
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01 du.
date1 = New Date(2008, 1, 1, 18, 9, 1, 500)
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.InvariantCulture))
' Displays 06:09:01.50 PM                        
Console.WriteLine(date1.ToString("hh:mm:ss.ff tt", _
                  CultureInfo.CreateSpecificCulture("hu-HU")))
' Displays 06:09:01.50 du.
```

## <a name="the-y-custom-format-specifier"></a>Identificatore di formato personalizzato "y"

L'identificatore di formato personalizzato "y" rappresenta l'anno come numero a una cifra o a due cifre. Se l'anno ha più di due cifre, nel risultato vengono visualizzate solo le due cifre di ordine inferiore. Se la prima cifra di un anno a due cifre inizia con zero (ad esempio, 2008), il numero viene formattato senza zero iniziale. 

Se l'identificatore di formato "y" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard "y". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#using-single-custom-format-specifiers) più avanti in questo argomento.

L'esempio seguente include l'identificatore di formato personalizzato "y" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(1, 12, 1);
DateTime date2 = new DateTime(2010, 1, 1);
Console.WriteLine(date1.ToString("%y"));
// Displays 1
Console.WriteLine(date1.ToString("yy"));
// Displays 01
Console.WriteLine(date1.ToString("yyy"));
// Displays 001
Console.WriteLine(date1.ToString("yyyy"));
// Displays 0001
Console.WriteLine(date1.ToString("yyyyy"));
// Displays 00001
Console.WriteLine(date2.ToString("%y"));
// Displays 10
Console.WriteLine(date2.ToString("yy"));
// Displays 10
Console.WriteLine(date2.ToString("yyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"));
// Displays 02010
```

```vb
Dim date1 As Date = #12/1/0001#
Dim date2 As Date = #1/1/2010#
Console.WriteLine(date1.ToString("%y"))
' Displays 1
Console.WriteLine(date1.ToString("yy"))
' Displays 01
Console.WriteLine(date1.ToString("yyy"))
' Displays 001
Console.WriteLine(date1.ToString("yyyy"))
' Displays 0001
Console.WriteLine(date1.ToString("yyyyy"))
' Displays 00001
Console.WriteLine(date2.ToString("%y"))
' Displays 10
Console.WriteLine(date2.ToString("yy"))
' Displays 10
Console.WriteLine(date2.ToString("yyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"))
' Displays 02010
```

## <a name="the-yy-custom-format-specifier"></a>Identificatore di formato personalizzato "yy"

L'identificatore di formato personalizzato "yy" rappresenta l'anno come numero a due cifre. Se l'anno ha più di due cifre, nel risultato vengono visualizzate solo le due cifre di ordine inferiore. Se l'anno a due cifre ha meno di due cifre significative, al numero vengono anteposti tanti zeri quanti sono necessari per ottenere due cifre.

In un'operazione di analisi, un anno a due cifre analizzato usando l'identificatore di formato personalizzato "yy" viene interpretato in base alla proprietà [Calendar.TwoDigitYearMax](xref:System.Globalization.Calendar.TwoDigitYearMax) del calendario corrente del provider di formato. Nell'esempio seguente viene analizzata la rappresentazione di stringa di una data con un anno a due cifre usando il calendario gregoriano predefinito delle impostazioni cultura en-US, che, in questo caso, sono le impostazioni cultura correnti. Modifica quindi l'oggetto [CultureInfo](xref:System.Globalization.CultureInfo) delle impostazioni cultura correnti in modo che usi un oggetto [GregorianCalendar](xref:System.Globalization.GregorianCalendar) la cui proprietà[TwoDigitYearMax](xref:System.Globalization.GregorianCalendar.TwoDigitYearMax) è stata modificata.

```csharp
using System;
using System.Globalization;
using System.Threading;

public class Example
{
   public static void Main()
   {
      string fmt = "dd-MMM-yy";
      string value = "24-Jan-49";

      Calendar cal = (Calendar) CultureInfo.CurrentCulture.Calendar.Clone();
      Console.WriteLine("Two Digit Year Range: {0} - {1}", 
                        cal.TwoDigitYearMax - 99, cal.TwoDigitYearMax);

      Console.WriteLine("{0:d}", DateTime.ParseExact(value, fmt, null));
      Console.WriteLine();

      cal.TwoDigitYearMax = 2099;
      CultureInfo culture = (CultureInfo) CultureInfo.CurrentCulture.Clone();
      culture.DateTimeFormat.Calendar = cal;
      Thread.CurrentThread.CurrentCulture = culture;

      Console.WriteLine("Two Digit Year Range: {0} - {1}", 
                        cal.TwoDigitYearMax - 99, cal.TwoDigitYearMax);
      Console.WriteLine("{0:d}", DateTime.ParseExact(value, fmt, null));
   }
}
// The example displays the following output:
//       Two Digit Year Range: 1930 - 2029
//       1/24/1949
//       
//       Two Digit Year Range: 2000 - 2099
//       1/24/2049
```

```vb
Imports System.Globalization
Imports System.Threading

Module Example
   Public Sub Main()
      Dim fmt As String = "dd-MMM-yy"
      Dim value As String = "24-Jan-49"

      Dim cal As Calendar = CType(CultureInfo.CurrentCulture.Calendar.Clone(), Calendar)
      Console.WriteLine("Two Digit Year Range: {0} - {1}", 
                        cal.TwoDigitYearMax - 99, cal.TwoDigitYearMax)

      Console.WriteLine("{0:d}", DateTime.ParseExact(value, fmt, Nothing))
      Console.WriteLine()

      cal.TwoDigitYearMax = 2099
      Dim culture As CultureInfo = CType(CultureInfo.CurrentCulture.Clone(), CultureInfo)
      culture.DateTimeFormat.Calendar = cal
      Thread.CurrentThread.CurrentCulture = culture

      Console.WriteLine("Two Digit Year Range: {0} - {1}", 
                        cal.TwoDigitYearMax - 99, cal.TwoDigitYearMax)
      Console.WriteLine("{0:d}", DateTime.ParseExact(value, fmt, Nothing))
   End Sub
End Module
' The example displays the following output:
'       Two Digit Year Range: 1930 - 2029
'       1/24/1949
'       
'       Two Digit Year Range: 2000 - 2099
'       1/24/2049
```

L'esempio seguente include l'identificatore di formato personalizzato "yy" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(1, 12, 1);
DateTime date2 = new DateTime(2010, 1, 1);
Console.WriteLine(date1.ToString("%y"));
// Displays 1
Console.WriteLine(date1.ToString("yy"));
// Displays 01
Console.WriteLine(date1.ToString("yyy"));
// Displays 001
Console.WriteLine(date1.ToString("yyyy"));
// Displays 0001
Console.WriteLine(date1.ToString("yyyyy"));
// Displays 00001
Console.WriteLine(date2.ToString("%y"));
// Displays 10
Console.WriteLine(date2.ToString("yy"));
// Displays 10
Console.WriteLine(date2.ToString("yyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"));
// Displays 02010
```

```vb
Dim date1 As Date = #12/1/0001#
Dim date2 As Date = #1/1/2010#
Console.WriteLine(date1.ToString("%y"))
' Displays 1
Console.WriteLine(date1.ToString("yy"))
' Displays 01
Console.WriteLine(date1.ToString("yyy"))
' Displays 001
Console.WriteLine(date1.ToString("yyyy"))
' Displays 0001
Console.WriteLine(date1.ToString("yyyyy"))
' Displays 00001
Console.WriteLine(date2.ToString("%y"))
' Displays 10
Console.WriteLine(date2.ToString("yy"))
' Displays 10
Console.WriteLine(date2.ToString("yyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"))
' Displays 02010
```

## <a name="the-yyy-custom-format-specifier"></a>Identificatore di formato personalizzato "yyy"

L'identificatore di formato personalizzato "yyy" rappresenta l'anno con un minimo di tre cifre. Se l'anno ha più di tre cifre significative, queste vengono incluse nella stringa di risultato. Se l'anno ha meno di tre cifre, al numero vengono anteposti tanti zeri quanti sono necessari per ottenere tre cifre.

> [!NOTE]
> Per il calendario buddista tailandese, in cui sono previsti anni di cinque cifre, questo identificatore di formato consente di visualizzare tutte le cifre significative.

L'esempio seguente include l'identificatore di formato personalizzato "yyy" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(1, 12, 1);
DateTime date2 = new DateTime(2010, 1, 1);
Console.WriteLine(date1.ToString("%y"));
// Displays 1
Console.WriteLine(date1.ToString("yy"));
// Displays 01
Console.WriteLine(date1.ToString("yyy"));
// Displays 001
Console.WriteLine(date1.ToString("yyyy"));
// Displays 0001
Console.WriteLine(date1.ToString("yyyyy"));
// Displays 00001
Console.WriteLine(date2.ToString("%y"));
// Displays 10
Console.WriteLine(date2.ToString("yy"));
// Displays 10
Console.WriteLine(date2.ToString("yyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"));
// Displays 02010      
```

```vb
Dim date1 As Date = #12/1/0001#
Dim date2 As Date = #1/1/2010#
Console.WriteLine(date1.ToString("%y"))
' Displays 1
Console.WriteLine(date1.ToString("yy"))
' Displays 01
Console.WriteLine(date1.ToString("yyy"))
' Displays 001
Console.WriteLine(date1.ToString("yyyy"))
' Displays 0001
Console.WriteLine(date1.ToString("yyyyy"))
' Displays 00001
Console.WriteLine(date2.ToString("%y"))
' Displays 10
Console.WriteLine(date2.ToString("yy"))
' Displays 10
Console.WriteLine(date2.ToString("yyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"))
' Displays 02010 
```

## <a name="the-yyyy-custom-format-specifier"></a>Identificatore di formato personalizzato "yyyy"

L'identificatore di formato personalizzato "yyyy" rappresenta l'anno con un minimo di quattro cifre. Se l'anno ha più di quattro cifre significative, queste vengono incluse nella stringa di risultato. Se l'anno ha meno di quattro cifre, al numero vengono anteposti tanti zeri quanti sono necessari per ottenere quattro cifre.

> [!NOTE]
> Per il calendario buddista tailandese, in cui sono previsti anni di cinque cifre, questo identificatore di formato consente di visualizzare tutte le cifre significative.

L'esempio seguente include l'identificatore di formato personalizzato "yyyy" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(1, 12, 1);
DateTime date2 = new DateTime(2010, 1, 1);
Console.WriteLine(date1.ToString("%y"));
// Displays 1
Console.WriteLine(date1.ToString("yy"));
// Displays 01
Console.WriteLine(date1.ToString("yyy"));
// Displays 001
Console.WriteLine(date1.ToString("yyyy"));
// Displays 0001
Console.WriteLine(date1.ToString("yyyyy"));
// Displays 00001
Console.WriteLine(date2.ToString("%y"));
// Displays 10
Console.WriteLine(date2.ToString("yy"));
// Displays 10
Console.WriteLine(date2.ToString("yyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"));
// Displays 02010 
```

```vb
Dim date1 As Date = #12/1/0001#
Dim date2 As Date = #1/1/2010#
Console.WriteLine(date1.ToString("%y"))
' Displays 1
Console.WriteLine(date1.ToString("yy"))
' Displays 01
Console.WriteLine(date1.ToString("yyy"))
' Displays 001
Console.WriteLine(date1.ToString("yyyy"))
' Displays 0001
Console.WriteLine(date1.ToString("yyyyy"))
' Displays 00001
Console.WriteLine(date2.ToString("%y"))
' Displays 10
Console.WriteLine(date2.ToString("yy"))
' Displays 10
Console.WriteLine(date2.ToString("yyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"))
' Displays 02010
```

## <a name="the-yyyyy-custom-format-specifier"></a>Identificatore di formato personalizzato "yyyyy"

L'identificatore di formato personalizzato "yyyyy" (più qualsiasi numero di identificatori "y" aggiuntivi) rappresenta l'anno con un minimo di cinque cifre. Se l'anno ha più di cinque cifre significative, queste vengono incluse nella stringa di risultato. Se l'anno ha meno di cinque cifre, al numero vengono anteposti tanti zeri quanto sono necessari per ottenere cinque cifre.

Se sono presenti identificatori "y" aggiuntivi, al numero vengono anteposti tanti zeri quanti sono necessari per ottenere il numero di identificatori "y". 

L'esempio seguente include l'identificatore di formato personalizzato "yyyyy" in una stringa di formato personalizzata.

```csharp
DateTime date1 = new DateTime(1, 12, 1);
DateTime date2 = new DateTime(2010, 1, 1);
Console.WriteLine(date1.ToString("%y"));
// Displays 1
Console.WriteLine(date1.ToString("yy"));
// Displays 01
Console.WriteLine(date1.ToString("yyy"));
// Displays 001
Console.WriteLine(date1.ToString("yyyy"));
// Displays 0001
Console.WriteLine(date1.ToString("yyyyy"));
// Displays 00001
Console.WriteLine(date2.ToString("%y"));
// Displays 10
Console.WriteLine(date2.ToString("yy"));
// Displays 10
Console.WriteLine(date2.ToString("yyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyy"));
// Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"));
// Displays 02010 
```

```vb
Dim date1 As Date = #12/1/0001#
Dim date2 As Date = #1/1/2010#
Console.WriteLine(date1.ToString("%y"))
' Displays 1
Console.WriteLine(date1.ToString("yy"))
' Displays 01
Console.WriteLine(date1.ToString("yyy"))
' Displays 001
Console.WriteLine(date1.ToString("yyyy"))
' Displays 0001
Console.WriteLine(date1.ToString("yyyyy"))
' Displays 00001
Console.WriteLine(date2.ToString("%y"))
' Displays 10
Console.WriteLine(date2.ToString("yy"))
' Displays 10
Console.WriteLine(date2.ToString("yyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyy"))
' Displays 2010      
Console.WriteLine(date2.ToString("yyyyy"))
' Displays 02010 
```

## <a name="the-z-custom-format-specifier"></a>Identificatore di formato personalizzato "z"

Con valori [DateTime](xref:System.DateTime), l'identificatore di formato personalizzato "z" rappresenta l'offset con segno del fuso orario del sistema operativo locale rispetto all'ora UTC (Coordinated Universal Time), misurato in ore. Non riflette il valore della proprietà [DateTime.Kind](xref:System.DateTime.Kind) di un'istanza. Per questo motivo non è consigliabile usare l'identificatore di formato "z" con valori [DateTime](xref:System.DateTime).

Con valori [DateTimeOffset](xref:System.DateTimeOffset), questo identificatore di formato rappresenta l'offset del valore [DateTimeOffset](xref:System.DateTimeOffset) rispetto all'ora UTC in ore. 

Lo scarto viene visualizzato sempre con un segno iniziale. Un segno più (+) indica le ore in più e un segno meno (-) le ore in meno rispetto all'ora UTC. Un valore di offset a una sola cifra viene formattato senza uno zero iniziale. 

Se l'identificatore di formato "z" viene usato senza altri identificatori di formato personalizzato, viene interpretato come l'identificatore di formato di data e ora standard e viene generato un evento [FormatException](xref:System.FormatException). Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#using-single-custom-format-specifiers) più avanti in questo argomento. 

L'esempio seguente include l'identificatore di formato personalizzato "z" in una stringa di formato personalizzata.

```csharp
DateTime date1 = DateTime.UtcNow;
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", 
                  date1));
// Displays -7, -07, -07:00                     

DateTimeOffset date2 = new DateTimeOffset(2008, 8, 1, 0, 0, 0, 
                                          new TimeSpan(6, 0, 0));
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", 
                  date2));
// Displays +6, +06, +06:00
```

```vb
Dim date1 As Date = Date.UtcNow
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", _
                  date1))
' Displays -7, -07, -07:00                     

Dim date2 As New DateTimeOffset(2008, 8, 1, 0, 0, 0, _
                                New Timespan(6, 0, 0))
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", _
                  date2))                                     
' Displays +6, +06, +06:00
```

## <a name="the-zz-custom-format-specifier"></a>Identificatore di formato personalizzato "zz"

Con valori [DateTime](xref:System.DateTime), l'identificatore di formato personalizzato "zz" rappresenta l'offset con segno del fuso orario del sistema operativo locale rispetto all'ora UTC (Coordinated Universal Time), misurato in ore. Non riflette il valore della proprietà [DateTime.Kind](xref:System.DateTime.Kind) di un'istanza. Per questo motivo non è consigliabile usare l'identificatore di formato "zz" con valori [DateTime](xref:System.DateTime).

Con valori [DateTimeOffset](xref:System.DateTimeOffset), questo identificatore di formato rappresenta l'offset del valore [DateTimeOffset](xref:System.DateTimeOffset) rispetto all'ora UTC in ore.

Lo scarto viene visualizzato sempre con un segno iniziale. Un segno più (+) indica le ore in più e un segno meno (-) le ore in meno rispetto all'ora UTC. Un valore di offset di una sola cifra viene formattato con uno zero iniziale. 

L'esempio seguente include l'identificatore di formato personalizzato "zz" in una stringa di formato personalizzata.

```csharp
DateTime date1 = DateTime.UtcNow;
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", 
                  date1));
// Displays -7, -07, -07:00                     

DateTimeOffset date2 = new DateTimeOffset(2008, 8, 1, 0, 0, 0, 
                                          new TimeSpan(6, 0, 0));
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", 
                  date2));
// Displays +6, +06, +06:00
```

```vb
Dim date1 As Date = Date.UtcNow
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", _
                  date1))
' Displays -7, -07, -07:00                     

Dim date2 As New DateTimeOffset(2008, 8, 1, 0, 0, 0, _
                                New Timespan(6, 0, 0))
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", _
                  date2))                                     
' Displays +6, +06, +06:00
```

## <a name="the-zzz-custom-format-specifier"></a>Identificatore di formato personalizzato "zzz"

Con valori [DateTime](xref:System.DateTime), l'identificatore di formato personalizzato "zzz" rappresenta l'offset con segno del fuso orario del sistema operativo locale rispetto all'ora UTC (Coordinated Universal Time), misurato in ore. Non riflette il valore della proprietà [DateTime.Kind](xref:System.DateTime.Kind) di un'istanza. Per questo motivo non è consigliabile usare l'identificatore di formato "zzz" con valori [DateTime](xref:System.DateTime).

Con valori [DateTimeOffset](xref:System.DateTimeOffset), questo identificatore di formato rappresenta l'offset del valore [DateTimeOffset](xref:System.DateTimeOffset) rispetto all'ora UTC in ore.

Lo scarto viene visualizzato sempre con un segno iniziale. Un segno più (+) indica le ore in più e un segno meno (-) le ore in meno rispetto all'ora UTC. Un valore di offset di una sola cifra viene formattato con uno zero iniziale. 

L'esempio seguente include l'identificatore di formato personalizzato "zzz" in una stringa di formato personalizzata.

```csharp
DateTime date1 = DateTime.UtcNow;
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", 
                  date1));
// Displays -7, -07, -07:00                     

DateTimeOffset date2 = new DateTimeOffset(2008, 8, 1, 0, 0, 0, 
                                          new TimeSpan(6, 0, 0));
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", 
                  date2));
// Displays +6, +06, +06:00
```

```vb
Dim date1 As Date = Date.UtcNow
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", _
                  date1))
' Displays -7, -07, -07:00                     

Dim date2 As New DateTimeOffset(2008, 8, 1, 0, 0, 0, _
                                New Timespan(6, 0, 0))
Console.WriteLine(String.Format("{0:%z}, {0:zz}, {0:zzz}", _
                  date2))                                     
' Displays +6, +06, +06:00
```

## <a name="the--custom-format-specifier"></a>Identificatore di formato personalizzato ":"

L'identificatore di formato personalizzato ":" rappresenta il separatore di ora che viene usato per distinguere ore, minuti e secondi. 

Se l'identificatore di formato ":" viene usato senza altri identificatori di formato personalizzato, viene interpretato come l'identificatore di formato di data e ora standard e viene generato un evento [FormatException](xref:System.FormatException). Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#using-single-custom-format-specifiers) più avanti in questo argomento.

## <a name="the--custom-format-specifier"></a>Identificatore di formato personalizzato "/"

L'identificatore di formato personalizzato "/" rappresenta il separatore di data usato per distinguere anni, mesi e giorni. 

Se l'identificatore di formato "/" viene usato senza altri identificatori di formato personalizzato, viene interpretato come l'identificatore di formato di data e ora standard e viene generato un evento [FormatException](xref:System.FormatException). Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#using-single-custom-format-specifiers) più avanti in questo argomento.

## <a name="character-literals"></a>Valori letterali carattere

I caratteri seguenti in una stringa di formato data e ora sono riservati e vengono sempre interpretati come caratteri di formattazione o, nel caso di ", ', / e \,, come caratteri speciali. 

  |   |   |   |      
- | - | - | - | -
F | H | K | M | d
f | V | h | m | s
s | s | l | % | :
/ | " | ' | \ |
  |   |   |   |
  
Tutti gli altri caratteri vengono sempre interpretati come valori letterali carattere e in un'operazione di formattazione vengono inclusi senza modifiche nella stringa di risultato. In un'operazione di analisi questi caratteri devono corrispondere esattamente ai caratteri nella stringa di input. Il confronto tiene conto di maiuscole e minuscole. 

Nell'esempio seguente i caratteri "PST" (abbreviazione di Pacific Standard Time, Ora solare Pacifico) e "PDT" (abbreviazione di Pacific Daylight Time, Ora legale Pacifico) rappresentano il fuso orario locale in una stringa di formato. Si noti che la stringa è inclusa nella stringa di risultato e che una stringa che include la stringa del fuso orario locale viene analizzata correttamente. 

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      String[] formats = { "dd MMM yyyy hh:mm tt PST", 
                           "dd MMM yyyy hh:mm tt PDT" };
      var dat = new DateTime(2016, 8, 18, 16, 50, 0);
      // Display the result string. 
      Console.WriteLine(dat.ToString(formats[1]));

      // Parse a string. 
      String value = "25 Dec 2016 12:00 pm PST";
      DateTime newDate;
      if (DateTime.TryParseExact(value, formats, null, 
                                 DateTimeStyles.None, out newDate)) 
         Console.WriteLine(newDate);
      else
         Console.WriteLine("Unable to parse '{0}'", value);
   }
}
// The example displays the following output:
//       18 Aug 2016 04:50 PM PDT
//       12/25/2016 12:00:00 PM
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim formats() As String = { "dd MMM yyyy hh:mm tt PST", 
                                  "dd MMM yyyy hh:mm tt PDT" }
      Dim dat As New Date(2016, 8, 18, 16, 50, 0)
      ' Display the result string. 
      Console.WriteLine(dat.ToString(formats(1)))

      ' Parse a string. 
      Dim value As String = "25 Dec 2016 12:00 pm PST"
      Dim newDate As Date
      If Date.TryParseExact(value, formats, Nothing, 
                            DateTimeStyles.None, newDate) Then 
         Console.WriteLine(newDate)
      Else
         Console.WriteLine("Unable to parse '{0}'", value)
      End If                               
   End Sub
End Module
' The example displays the following output:
'       18 Aug 2016 04:50 PM PDT
'       12/25/2016 12:00:00 PM
```

Esistono due modi per indicare che determinati caratteri devono essere interpretati come caratteri e non come caratteri riservati, per includerli in una stringa di risultato o eseguirne l'analisi in una stringa di input:

* Usando un carattere di escape per ogni carattere riservato. Per altre informazioni, vedere [Uso del carattere di escape](#using-the-escape-character). 
  
  Nell'esempio seguente i caratteri "pst" (abbreviazione di Pacific Standard Time, Ora solare Pacifico) rappresentano il fuso orario locale in una stringa di formato. Poiché sia "s" che "t" sono stringhe di formato personalizzato, perché siano interpretate come valori letterali carattere è necessario usare un carattere di escape per entrambe. 
  
```csharp
using System;
using System.Globalization;

public class Example
{
  public static void Main()
  {
      String format = "dd MMM yyyy hh:mm tt p\\s\\t";
      var dat = new DateTime(2016, 8, 18, 16, 50, 0);
      // Display the result string. 
      Console.WriteLine(dat.ToString(format));

      // Parse a string. 
      String value = "25 Dec 2016 12:00 pm pst";
      DateTime newDate;
      if (DateTime.TryParseExact(value, format, null, 
                                  DateTimeStyles.None, out newDate)) 
          Console.WriteLine(newDate);
      else
          Console.WriteLine("Unable to parse '{0}'", value);
  }
}
// The example displays the following output:
//       18 Aug 2016 04:50 PM PDT
//       12/25/2016 12:00:00 PM
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim fmt As String = "dd MMM yyyy hh:mm tt p\s\t" 
      Dim dat As New Date(2016, 8, 18, 16, 50, 0)
      ' Display the result string. 
      Console.WriteLine(dat.ToString(fmt))

      ' Parse a string. 
      Dim value As String = "25 Dec 2016 12:00 pm pst"
      Dim newDate As Date
      If Date.TryParseExact(value, fmt, Nothing, 
                            DateTimeStyles.None, newDate) Then 
         Console.WriteLine(newDate)
      Else
         Console.WriteLine("Unable to parse '{0}'", value)
      End If                               
   End Sub
End Module
' The example displays the following output:
'       18 Aug 2016 04:50 PM pst
'       12/25/2016 12:00:00 PM
```
  
* Racchiudendo l'intera stringa tra virgolette o apostrofi. L'esempio seguente è simile a quello precedente, ad eccezione del fatto che "pst" è racchiuso tra virgolette per indicare che l'intera stringa delimitata deve essere interpretata come insieme di valori letterali carattere. 

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      String format = "dd MMM yyyy hh:mm tt \"pst\"";
      var dat = new DateTime(2016, 8, 18, 16, 50, 0);
      // Display the result string. 
      Console.WriteLine(dat.ToString(format));

      // Parse a string. 
      String value = "25 Dec 2016 12:00 pm pst";
      DateTime newDate;
      if (DateTime.TryParseExact(value, format, null, 
                                 DateTimeStyles.None, out newDate)) 
         Console.WriteLine(newDate);
      else
         Console.WriteLine("Unable to parse '{0}'", value);
   }
}
// The example displays the following output:
//       18 Aug 2016 04:50 PM PDT
//       12/25/2016 12:00:00 PM
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim fmt As String = "dd MMM yyyy hh:mm tt ""pst"""  
      Dim dat As New Date(2016, 8, 18, 16, 50, 0)
      ' Display the result string. 
      Console.WriteLine(dat.ToString(fmt))

      ' Parse a string. 
      Dim value As String = "25 Dec 2016 12:00 pm pst"
      Dim newDate As Date
      If Date.TryParseExact(value, fmt, Nothing, 
                            DateTimeStyles.None, newDate) Then 
         Console.WriteLine(newDate)
      Else
         Console.WriteLine("Unable to parse '{0}'", value)
      End If                               
   End Sub
End Module
' The example displays the following output:
'       18 Aug 2016 04:50 PM pst
'       12/25/2016 12:00:00 PM
```

## <a name="notes"></a>Note


### <a name="using-single-custom-format-specifiers"></a>Uso di singoli identificatori di formato personalizzato

Una stringa di formato di data e ora personalizzata è costituita da due o più caratteri. I metodi di formattazione di data e ora interpretano qualsiasi stringa a carattere singolo come stringa di formato di data e ora standard. Se il carattere non viene riconosciuto come identificatore di formato valido, viene generato un evento [FormatException](xref:System.FormatException). Una stringa di formato costituita solo dall'identificatore "h" viene ad esempio interpretata come una stringa di formato di data e ora standard. In questo caso specifico, tuttavia, viene generata un'eccezione in quanto non esiste alcun identificatore di formato di data e ora standard "h". 

Per usare qualsiasi identificatore di formato di data e ora personalizzato come unico identificatore in una stringa di formato (ovvero, per usare l'identificatore di formato personalizzato "d", "f", "F", "g", "h", "H", "K", "m", "M", "s", "t", "y", "z", ":" o "/" da solo), includere uno spazio prima o dopo l'identificatore oppure includere un identificatore di formato percentuale ("%") prima del singolo identificatore di data e ora personalizzato.

La stringa "`%h`" viene ad esempio interpretata come stringa di formato di data e ora personalizzato che consente di visualizzare l'ora rappresentata dal valore di data e ora corrente. È anche possibile usare la stringa di formato " h" o "h ", sebbene, in questo caso, verrà incluso uno spazio nella stringa di risultato insieme all'ora. Nell'esempio seguente vengono illustrate queste tre stringhe di formato.


```csharp
DateTime dat1 = new DateTime(2009, 6, 15, 13, 45, 0);

Console.WriteLine("'{0:%h}'", dat1);
Console.WriteLine("'{0: h}'", dat1);
Console.WriteLine("'{0:h }'", dat1);
// The example displays the following output:
//       '1'
//       ' 1'
//       '1 '
```

```vb
Dim dat1 As Date = #6/15/2009 1:45PM#

Console.WriteLine("'{0:%h}'", dat1)
Console.WriteLine("'{0: h}'", dat1)
Console.WriteLine("'{0:h }'", dat1)
' The example displays the following output:
'       '1'
'       ' 1'
'       '1 '
```

### <a name="using-the-escape-character"></a>Uso del carattere di escape

I caratteri "d", "f", "F", "g", "h", "H", "K", "m", "M", "s", "t", "y", "z", ":" o "/" in una stringa di formato vengono interpretati come identificatori di formato personalizzati anziché come caratteri letterali. Per evitare che un carattere venga interpretato come un identificatore di formato, è possibile anteporvi una barra rovesciata (\), che rappresenta il carattere di escape. Il carattere di escape indica che il carattere seguente è un valore letterale carattere che deve essere incluso nella stringa di risultato senza modifiche.

Per includere una barra rovesciata in una stringa dei risultati, è necessario aggiungere un carattere di escape facendolo quindi precedere da un'altra barra rovesciata (`\\`).

> [!NOTE]
> Alcuni compilatori, ad esempio il compilatore C#, possono anche interpretare un singolo carattere barra rovesciata come carattere di escape. Per assicurarsi che una stringa venga interpretata correttamente quando viene eseguita la formattazione, è possibile usare il carattere letterale di stringa verbatim (carattere @) prima della stringa o aggiungere un altro carattere barra rovesciata prima di ogni barra rovesciata. Nell'esempio C# seguente vengono illustrati entrambi gli approcci.

Nell'esempio seguente viene usato il carattere di escape per impedire che durante l'operazione di formattazione i caratteri "h" e "m" vengano interpretati come identificatori di formato. 

```csharp
DateTime date = new DateTime(2009, 06, 15, 13, 45, 30, 90);
string fmt1 = "h \\h m \\m";
string fmt2 = @"h \h m \m";

Console.WriteLine("{0} ({1}) -> {2}", date, fmt1, date.ToString(fmt1));
Console.WriteLine("{0} ({1}) -> {2}", date, fmt2, date.ToString(fmt2));
// The example displays the following output:
//       6/15/2009 1:45:30 PM (h \h m \m) -> 1 h 45 m
//       6/15/2009 1:45:30 PM (h \h m \m) -> 1 h 45 m
```

```vb
Dim date1 As Date = #6/15/2009 13:45#
Dim fmt As String = "h \h m \m"

Console.WriteLine("{0} ({1}) -> {2}", date1, fmt, date1.ToString(fmt))
' The example displays the following output:
'       6/15/2009 1:45:00 PM (h \h m \m) -> 1 h 45 m 
```

### <a name="datetimeformatinfo-properties"></a>Proprietà DateTimeFormatInfo

La formattazione è influenzata dalle proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) corrente, che viene fornito in modo implicito dalle impostazioni cultura del thread corrente o in modo esplicito dal parametro [IFormatProvider](xref:System.IFormatProvider) del metodo che richiama la formattazione. Per il parametro [IFormatProvider](xref:System.IFormatProvider) è necessario specificare un oggetto [CultureInfo](xref:System.Globalization.CultureInfo), che rappresenta le impostazioni cultura, o un oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo). 

La stringa di risultato prodotta da molti degli identificatori di formato di data e ora personalizzato dipende anche dalle proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) corrente. Nell'applicazione può quindi essere modificato il risultato prodotto da alcuni identificatori di formato di data e ora personalizzato modificando la proprietà [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) corrispondente. L'identificatore di formato "ddd" aggiunge, ad esempio, un nome di giorno della settimana abbreviato trovato nella matrice di stringhe [AbbreviatedDayNames](xref:System.Globalization.DateTimeFormatInfo.AbbreviatedDayNames) alla stringa di risultato. In modo analogo, l'identificatore di formato "MMMM" aggiunge alla stringa di risultato un nome del mese completo trovato nella matrice di stringhe [MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames).

## <a name="see-also"></a>Vedere anche

[System.DateTime](xref:System.DateTime)

[System.IFormatProvider](xref:System.IFormatProvider)

[Formattazione di tipi](formatting-types.md)

[Stringhe di formato di data e ora standard](standard-datetime.md)


