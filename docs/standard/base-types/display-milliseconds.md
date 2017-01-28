---
title: 'Procedura: Visualizzare i millisecondi nei valori di data e ora'
description: Come visualizzare i millisecondi nei valori di data e ora
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 78599e33-1c3f-4335-b320-751e35906338
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 9bcec8a610ed0fd47d168e23fb1454067e2d3fac

---

# <a name="how-to-display-milliseconds-in-date-and-time-values"></a>Procedura: Visualizzare i millisecondi nei valori di data e ora

I metodi di formattazione di data e ora predefiniti, ad esempio [DateTime.ToString()](xref:System.DateTime.ToString), includono le ore, i minuti e i secondi di un valore di ora ma ne escludono il componente millisecondi. Questo argomento descrive come includere un componente millisecondi di una data e un'ora nelle stringhe di data e ora formattate.

## <a name="to-display-the-millisecond-component-of-a-datetime-value"></a>Per visualizzare il componente millisecondi di un valore DateTime

1. Se si sta lavorando alla rappresentazione di stringa di una data, convertirla in un valore [DateTime](xref:System.DateTime) o in un valore [DateTimeOffset](xref:System.DateTimeOffset) usando il metodo statico [DateTime.Parse(String)](xref:System.DateTime.Parse(System.String)) o [DateTimeOffset.Parse(String)](xref:System.DateTimeOffset.Parse(System.String)).

2. Per estrarre la rappresentazione di stringa del componente millisecondi di un'ora, chiamare il metodo [DateTime.ToString(String)](xref:System.DateTime.ToString(System.String)) o [DateTimeOffset.ToString](xref:System.DateTimeOffset.ToString(System.String)) del valore di data e ora e passare il modello di formato personalizzato `fff` o `FFF` da solo o con altri identificatori di formato personalizzato come parametro.

## <a name="example"></a>Esempio

Nell'esempio il componente millisecondi di un valore [DateTime](xref:System.DateTime) e [DateTimeOffset](xref:System.DateTimeOffset) viene visualizzato nella console, sia da solo che incluso in una stringa di data e ora più lunga. 

```csharp
using System;
using System.Globalization;
using System.Text.RegularExpressions;

public class MillisecondDisplay
{
   public static void Main()
   {
      string dateString = "7/16/2008 8:32:45.126 AM";

      try
      {
         DateTime dateValue = DateTime.Parse(dateString);
         DateTimeOffset dateOffsetValue = DateTimeOffset.Parse(dateString);

         // Display Millisecond component alone.
         Console.WriteLine("Millisecond component only: {0}", 
                           dateValue.ToString("fff"));
         Console.WriteLine("Millisecond component only: {0}", 
                           dateOffsetValue.ToString("fff"));

         // Display Millisecond component with full date and time.
         Console.WriteLine("Date and Time with Milliseconds: {0}", 
                           dateValue.ToString("MM/dd/yyyy hh:mm:ss.fff tt"));                        
         Console.WriteLine("Date and Time with Milliseconds: {0}", 
                           dateOffsetValue.ToString("MM/dd/yyyy hh:mm:ss.fff tt"));

         // Append millisecond pattern to current culture's full date time pattern
         string fullPattern = DateTimeFormatInfo.CurrentInfo.FullDateTimePattern;
         fullPattern = Regex.Replace(fullPattern, "(:ss|:s)", "$1.fff");

         // Display Millisecond component with modified full date and time pattern.
         Console.WriteLine("Modified full date time pattern: {0}", 
                           dateValue.ToString(fullPattern));
         Console.WriteLine("Modified full date time pattern: {0}",
                           dateOffsetValue.ToString(fullPattern));
      }
      catch (FormatException)
      {
         Console.WriteLine("Unable to convert {0} to a date.", dateString);
      }
   }
}
// The example displays the following output if the current culture is en-US:
//    Millisecond component only: 126
//    Millisecond component only: 126
//    Date and Time with Milliseconds: 07/16/2008 08:32:45.126 AM
//    Date and Time with Milliseconds: 07/16/2008 08:32:45.126 AM
//    Modified full date time pattern: Wednesday, July 16, 2008 8:32:45.126 AM
//    Modified full date time pattern: Wednesday, July 16, 2008 8:32:45.126 AM
```

```vb
Imports System.Globalization
Imports System.Text.REgularExpressions

Module MillisecondDisplay
   Public Sub Main()

      Dim dateString As String = "7/16/2008 8:32:45.126 AM"

      Try
         Dim dateValue As Date = Date.Parse(dateString)
         Dim dateOffsetValue As DateTimeOffset = DateTimeOffset.Parse(dateString)

         ' Display Millisecond component alone.
         Console.WriteLine("Millisecond component only: {0}", _
                           dateValue.ToString("fff"))
         Console.WriteLine("Millisecond component only: {0}", _
                           dateOffsetValue.ToString("fff"))

         ' Display Millisecond component with full date and time.
         Console.WriteLine("Date and Time with Milliseconds: {0}", _
                           dateValue.ToString("MM/dd/yyyy hh:mm:ss.fff tt"))                        
         Console.WriteLine("Date and Time with Milliseconds: {0}", _
                           dateOffsetValue.ToString("MM/dd/yyyy hh:mm:ss.fff tt"))

         ' Append millisecond pattern to current culture's full date time pattern
         Dim fullPattern As String = DateTimeFormatInfo.CurrentInfo.FullDateTimePattern
         fullPattern = Regex.Replace(fullPattern, "(:ss|:s)", "$1.fff")

         ' Display Millisecond component with modified full date and time pattern.
         Console.WriteLine("Modified full date time pattern: {0}", _
                           dateValue.ToString(fullPattern))                        
         Console.WriteLine("Modified full date time pattern: {0}", _
                           dateOffsetValue.ToString(fullPattern))
      Catch e As FormatException
         Console.WriteLine("Unable to convert {0} to a date.", dateString)      
      End Try
   End Sub
End Module
' The example displays the following output if the current culture is en-US:
'    Millisecond component only: 126
'    Millisecond component only: 126
'    Date and Time with Milliseconds: 07/16/2008 08:32:45.126 AM
'    Date and Time with Milliseconds: 07/16/2008 08:32:45.126 AM
'    Modified full date time pattern: Wednesday, July 16, 2008 8:32:45.126 AM
'    Modified full date time pattern: Wednesday, July 16, 2008 8:32:45.126 AM
```

Il modello di formato `fff` include gli zeri finali nei millisecondi. Il modello di formato `FFF` li elimina. Nell'esempio seguente è illustrata questa differenza.

```csharp
DateTime dateValue = new DateTime(2008, 7, 16, 8, 32, 45, 180); 
Console.WriteLine(dateValue.ToString("fff"));    
Console.WriteLine(dateValue.ToString("FFF"));
// The example displays the following output to the console:
//    180
//    18 
```

```vb
Dim dateValue As New Date(2008, 7, 16, 8, 32, 45, 180) 
Console.WriteLIne(dateValue.ToString("fff"))    
Console.WriteLine(dateValue.ToString("FFF"))
' The example displays the following output to the console:
'    180
'    18
```

Uno dei problemi della definizione di un identificatore di formato personalizzato completo che include il componente millisecondi di una data e ora è rappresentato dal fatto che l'identificatore definisce un formato hardcoded che potrebbe non corrispondere alla disposizione degli elementi relativi all'ora delle impostazioni cultura correnti dell'applicazione. Un'alternativa migliore consiste nel recuperare uno dei modelli di visualizzazione della data/ora definiti dall'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) delle impostazioni cultura correnti e modificarlo in modo da includere i millisecondi. L'esempio illustra anche questo approccio. Viene recuperato il modello di data e ora completo delle impostazioni cultura correnti dalla proprietà [DateTimeFormatInfo.FullDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern) e viene quindi inserito il modello personalizzato `.ffff` dopo il modello dei secondi. Si noti che nell'esempio viene usata un'espressione regolare per eseguire questa operazione in una sola chiamata al metodo.

È anche possibile usare un identificatore di formato personalizzato per visualizzare una parte frazionaria di secondi diversa dai millisecondi. Ad esempio, l'identificatore di formato personalizzato `f` o `F` visualizza i decimi di secondo, l'identificatore di formato personalizzato `ff` o `FF` i centesimi di secondo e l'identificatore di formato personalizzato `ffff` o `FFFF` i decimillesimi di secondo. Le parti frazionarie di un millisecondo vengono troncate anziché arrotondate nella stringa restituita. Questi identificatori di formato vengono usati nell'esempio seguente.

```csharp
DateTime dateValue = new DateTime(2008, 7, 16, 8, 32, 45, 180); 
Console.WriteLine("{0} seconds", dateValue.ToString("s.f"));
Console.WriteLine("{0} seconds", dateValue.ToString("s.ff"));      
Console.WriteLine("{0} seconds", dateValue.ToString("s.ffff"));
// The example displays the following output to the console:
//    45.1 seconds
//    45.18 seconds
//    45.1800 seconds
```

```vb
Dim dateValue As New DateTime(2008, 7, 16, 8, 32, 45, 180) 
Console.WriteLine("{0} seconds", dateValue.ToString("s.f"))
Console.WriteLine("{0} seconds", dateValue.ToString("s.ff"))      
Console.WriteLine("{0} seconds", dateValue.ToString("s.ffff"))
' The example displays the following output to the console:
'    45.1 seconds
'    45.18 seconds
'    45.1800 seconds
```

> [!NOTE]
> È possibile visualizzare piccolissime unità di secondo frazionarie, come decimillesimi di secondo o centomillesimi di secondo. Questi valori tuttavia potrebbero non essere significativi. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema.

## <a name="see-also"></a>Vedere anche

[System.Globalization.DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo)

[Stringhe di formato di data e ora personalizzato](custom-datetime.md)




<!--HONumber=Nov16_HO3-->


