---
title: Analisi di stringhe di data e ora in .NET
description: Analisi di stringhe di data e ora in .NET
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: e61514cd-5329-4eb8-b122-482fffb54ab7
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: f0131baa0874880b6697458426da5ae9ce1705b7
ms.lasthandoff: 03/02/2017

---

# <a name="parsing-date-and-time-strings-in-net"></a>Analisi di stringhe di data e ora in .NET

I metodi di analisi consentono di convertire la rappresentazione di stringa di una data e un'ora in un oggetto [DateTime](xref:System.DateTime) equivalente. I metodi [Parse](xref:System.DateTime.Parse(System.String)) e [TryParse](xref:System.DateTime.TryParse(System.String,System.DateTime@)) convertono qualsiasi rappresentazione di data e ora tra quelle usate comunemente. I metodi [ParseExact](xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider)) e [TryParseExact](xref:System.DateTime.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles,System.DateTime@)) convertono una rappresentazione di stringa conforme al criterio specificato da una stringa di formato di data e ora. Vedere gli argomenti relativi alle [stringhe di formato di data e ora standard](standard-datetime.md) e alle [stringhe di formato di data e ora personalizzato](custom-datetime.md). 

L'analisi è influenzata dalle proprietà di un provider di formato che rende disponibili informazioni quali le stringhe usate per i separatori di data e ora e i nomi di mesi, giorni ed ere. Il provider di formato è l'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) corrente, che viene definito in modo implicito dalle impostazioni cultura del thread corrente o in modo esplicito dal parametro [IFormatProvider](xref:System.IFormatProvider) di un metodo di analisi. Per il parametro [IFormatProvider](xref:System.IFormatProvider) specificare un oggetto [CultureInfo](xref:System.Globalization.CultureInfo), che rappresenta le impostazioni cultura, o un oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo). 

La rappresentazione di stringa di una data da analizzare deve includere il mese e almeno un giorno o anno. La rappresentazione di stringa di un'ora deve includere l'ora e almeno i minuti o l'indicazione AM/PM. Se possibile, tuttavia, l'analisi indica i valori predefiniti per i componenti omessi. Per impostazione predefinita, per una data mancante viene indicata la data corrente, per un anno mancante viene indicato l'anno in corso, per un giorno del mese mancante viene indicato il primo giorno del mese e per un'ora mancante viene indicata la mezzanotte. 

Se la rappresentazione di stringa specifica solo l'ora, l'analisi restituisce un oggetto [DateTime](xref:System.DateTime) con le relative proprietà [Year](xref:System.DateTime.Year), [Month](xref:System.DateTime.Month) e [Day](xref:System.DateTime.Day) impostate sui valori corrispondenti della proprietà [Today](xref:System.DateTime.Today). Tuttavia, se viene specificata la costante [NoCurrentDateDefault](xref:System.Globalization.DateTimeStyles.NoCurrentDateDefault) nel metodo di analisi, le proprietà relative ad anno, mese e giorno vengono impostate sul valore 1.

Oltre a un componente di data e ora, la rappresentazione di stringa di una data e un'ora può includere un offset che indica in che misura l'ora differisce dall'ora UTC (Coordinated Universal Time). Ad esempio, la stringa "2/14/2007 5:32:00 -7:00" definisce un'ora che precede di sette ore l'ora UTC. Se viene omesso l'offset dalla rappresentazione di stringa di un'ora, l'analisi restituisce un oggetto [DateTime](xref:System.DateTime) con la relativa proprietà [Kind](xref:System.DateTime.Kind) impostata su [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified). Se viene specificato un offset, l'analisi restituisce un oggetto [DateTime](xref:System.DateTime) con la proprietà [Kind](xref:System.DateTime.Kind) impostata su [Local](xref:System.DateTimeKind.Local) e il relativo valore adeguato in base al fuso orario locale del computer. È possibile modificare questo comportamento usando una costante [DateTimeStyles](xref:System.Globalization.DateTimeStyles) con il metodo di analisi.

Il provider di formato viene usato anche per interpretare una data numerica ambigua. Ad esempio, non risulta chiaro quali componenti della data rappresentata dalla stringa "02/03/04" sono il mese, il giorno e l'anno. In questo caso i componenti vengono interpretati in base all'ordine dei formati di data simili nel provider di formato. 

## <a name="parse"></a>Parse

L'esempio di codice seguente illustra l'uso del metodo `Parse` per convertire una stringa in un oggetto `DateTime`. In questo esempio vengono usate le impostazioni cultura associate al thread corrente per eseguire l'analisi. Se l'oggetto [CultureInfo](xref:System.Globalization.CultureInfo) associato alle impostazioni cultura correnti non è in grado di analizzare la stringa di input, viene generata un'eccezione [FormatException](xref:System.FormatException).

```csharp
string MyString = "Jan 1, 2009";
DateTime MyDateTime = DateTime.Parse(MyString);
Console.WriteLine(MyDateTime);
// Displays the following output on a system whose culture is en-US:
//       1/1/2009 12:00:00 AM
```

```vb
Dim MyString As String = "Jan 1, 2009"
Dim MyDateTime As DateTime = DateTime.Parse(MyString)
Console.WriteLine(MyDateTime)
' Displays the following output on a system whose culture is en-US:
'       1/1/2009 12:00:00 AM
```

È anche possibile specificare un oggetto `CultureInfo` impostato su una delle impostazioni cultura definite da tale oggetto oppure specificare uno degli oggetti [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) standard restituiti dalla proprietà [CultureInfo.DateTimeFormat](xref:System.Globalization.CultureInfo.DateTimeFormat). L'esempio di codice seguente usa un provider di formato per analizzare una stringa in lingua tedesca in un `DateTime`. Un oggetto `CultureInfo` che rappresenta le impostazioni cultura de-DE viene definito e passato con la stringa da analizzare per garantire che tale stringa venga analizzata correttamente. Questo preclude qualsiasi impostazione in `CurrentCulture` di `CurrentThread`.

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      CultureInfo MyCultureInfo = new CultureInfo("de-DE");
      string MyString = "12 Juni 2008";
      DateTime MyDateTime = DateTime.Parse(MyString, MyCultureInfo);
      Console.WriteLine(MyDateTime);
   }
}
// The example displays the following output:
//       6/12/2008 12:00:00 AM
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim MyCultureInfo As CultureInfo = new CultureInfo("de-DE")
      Dim MyString As String = "12 Juni 2008"
      Dim MyDateTime As DateTime = DateTime.Parse(MyString, MyCultureInfo)
      Console.WriteLine(MyDateTime)
   End Sub
End Module
' The example displays the following output:
'       6/12/2008 12:00:00 AM
```

Tuttavia, sebbene sia possibile usare overload del metodo [Parse](xref:System.DateTime.Parse(System.String)) per specificare provider di formato personalizzati, il metodo non supporta l'uso di provider di formato non standard. Per analizzare una data e un'ora espresse in un formato non standard, usare il metodo [ParseExact](xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider)).

Nell'esempio di codice seguente viene usata l'enumerazione [DateTimeStyles](xref:System.Globalization.DateTimeStyles) per specificare che la data e l'ora correnti non devono essere aggiunte a `DateTime` per i campi che la stringa non definisce.

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      CultureInfo MyCultureInfo = new CultureInfo("de-DE");
      string MyString = "12 Juni 2008";
      DateTime MyDateTime = DateTime.Parse(MyString, MyCultureInfo, 
                                           DateTimeStyles.NoCurrentDateDefault);
      Console.WriteLine(MyDateTime);
   }
}
// The example displays the following output if the current culture is en-US:
//      6/12/2008 12:00:00 AM
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim MyCultureInfo As CultureInfo = new CultureInfo("de-DE")
      Dim MyString As String = "12 Juni 2008"
      Dim MyDateTime As DateTime = DateTime.Parse(MyString, MyCultureInfo)
      Console.WriteLine(MyDateTime)
   End Sub
End Module
' The example displays the following output:
'       6/12/2008 12:00:00 AM
```

## <a name="parseexact"></a>ParseExact

Il metodo [DateTime.ParseExact]((xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider)) converte una stringa conforme a un modello di stringa specificato in un oggetto `DateTime`. Quando una stringa che non è nel formato specificato viene passata a questo metodo, viene generata un'eccezione [FormatException](xref:System.FormatException). È possibile specificare uno degli identificatori di formato di data e ora standard o una combinazione limitata degli identificatori di formato di data e ora personalizzato. Usando gli identificatori di formato personalizzato è possibile costruire una stringa di riconoscimento personalizzata. Per una spiegazione degli identificatori, vedere gli argomenti relativi alle [stringhe di formato di data e ora standard](standard-datetime.md) e alle [stringhe di formato di data e ora personalizzato](custom-datetime.md). 

Ogni overload del metodo [ParseExact](xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider)) usa anche un parametro [IFormatProvider](xref:System.IFormatProvider) che in genere indica informazioni specifiche delle impostazioni cultura sulla formattazione della stringa. In genere, questo oggetto [IFormatProvider](xref:System.IFormatProvider) è un oggetto [CultureInfo](xref:System.Globalization.CultureInfo) che rappresenta le impostazioni cultura standard o un oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) restituito dalla proprietà [DateTimeFormat](xref:System.Globalization.CultureInfo.DateTimeFormat). Tuttavia, a differenza di altre funzioni di analisi di data e ora, questo metodo supporta anche un oggetto [IFormatProvider](xref:System.IFormatProvider) che definisce un formato di data e ora non standard. 

Nell'esempio di codice seguente, al metodo `ParseExact` viene passato un oggetto stringa da analizzare, seguito da un identificatore di formato, seguito da un oggetto `CultureInfo`. Questo metodo `ParseExact` consente di analizzare solo le stringhe con il modello di data estesa nelle impostazioni cultura en-US.

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      CultureInfo MyCultureInfo = new CultureInfo("en-US");
      string[] MyString = {" Friday, April 10, 2009", "Friday, April 10, 2009"};
      foreach (string dateString in MyString)
      {
         try {
            DateTime MyDateTime = DateTime.ParseExact(dateString, "D", MyCultureInfo);
            Console.WriteLine(MyDateTime);
         }
         catch (FormatException) {
            Console.WriteLine("Unable to parse '{0}'", dateString);
         }
      }
   }
}
// The example displays the following output:
//       Unable to parse ' Friday, April 10, 2009'
//       4/10/2009 12:00:00 AM
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim MyCultureInfo As CultureInfo = new CultureInfo("en-US")
      Dim MyString() As String = {" Friday, April 10, 2009", "Friday, April 10, 2009"}
      For Each dateString As String In MyString
         Try
            Dim MyDateTime As DateTime = DateTime.ParseExact(dateString, "D", _
                                                             MyCultureInfo)
            Console.WriteLine(MyDateTime)
         Catch e As FormatException
            Console.WriteLine("Unable to parse '{0}'", dateString)
         End Try
      Next
   End Sub
End Module
' The example displays the following output:
'       Unable to parse ' Friday, April 10, 2009'
'       4/10/2009 12:00:00 AM
```

## <a name="see-also"></a>Vedere anche

[Analisi di stringhe in .NET](parsing-strings.md)

[Formattazione di tipi in .NET](formatting-types.md)

[Conversione di tipi in .NET](type-conversion.md)


