---
title: Esecuzione di operazioni aritmetiche con date e ore
description: Esecuzione di operazioni aritmetiche con date e ore
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 08/16/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 589ac5ec-8365-4a0d-bc38-72183718110c
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: b872cc4c2b799ddafc9df263795d860754d1ec17
ms.lasthandoff: 03/02/2017

---

# <a name="performing-arithmetic-operations-with-dates-and-times"></a>Esecuzione di operazioni aritmetiche con date e ore

Sebbene le strutture [System.DateTime](xref:System.DateTime) e [System.DateTimeOffset](xref:System.DateTimeOffset) contengano entrambe membri che eseguono operazioni aritmetiche sui propri valori, i risultati delle operazioni aritmetiche sono molto diversi. In questo articolo vengono esaminate tali differenze, in relazione alla presenza del fuso orario nei dati di data e ora, e viene descritto come eseguire operazioni completamente compatibili con il fuso orario usando i dati di data e ora.

## <a name="comparisons-and-arithmetic-operations-with-datetime-values"></a>Confronti e operazioni aritmetiche con i valori DateTime

I valori [System.DateTime](xref:System.DateTime) sono caratterizzati da un livello limitato di riferimenti al fuso orario. La proprietà [DateTime.Kind](xref:System.DateTime.Kind) consente di assegnare un valore [System.DateTimeKind](xref:System.DateTimeKind) a data e ora per indicare se rappresenta l'ora locale, l'ora UTC (Coordinated Universal Time) o l'ora in un fuso orario non specificato. Queste informazioni limitate sul fuso orario vengono tuttavia ignorate durante il confronto o l'esecuzione di operazioni aritmetiche con data e ora per i valori [DateTime](xref:System.DateTime). Questa condizione è illustrata nell'esempio seguente, in cui si confronta l'ora locale corrente con l'ora UTC corrente.

```csharp
using System;

public enum TimeComparison
{
   EarlierThan = -1,
   TheSameAs = 0,
   LaterThan = 1
}

public class DateManipulation
{
   public static void Main()
   {
      DateTime localTime = DateTime.Now;
      DateTime utcTime = DateTime.UtcNow;

      Console.WriteLine("Difference between {0} and {1} time: {2}:{3} hours", 
                        localTime.Kind.ToString(), 
                        utcTime.Kind.ToString(), 
                        (localTime - utcTime).Hours, 
                        (localTime - utcTime).Minutes);
      Console.WriteLine("The {0} time is {1} the {2} time.", 
                        localTime.Kind.ToString(), 
                        Enum.GetName(typeof(TimeComparison), localTime.CompareTo(utcTime)), 
                        utcTime.Kind.ToString());  
   }
}
// If run in the U.S. Pacific Standard Time zone, the example displays 
// the following output to the console:
//    Difference between Local and Utc time: -7:0 hours
//    The Local time is EarlierThan the Utc time.
```

```vb
Public Enum TimeComparison As Integer
   EarlierThan = -1
   TheSameAs = 0
   LaterThan = 1
End Enum

Module DateManipulation
   Public Sub Main()
      Dim localTime As Date = Date.Now
      Dim utcTime As Date = Date.UtcNow

      Console.WriteLine("Difference between {0} and {1} time: {2}:{3} hours", _
                        localTime.Kind.ToString(), _
                        utcTime.Kind.ToString(), _
                        (localTime - utcTime).Hours, _
                        (localTime - utcTime).Minutes)
      Console.WriteLine("The {0} time is {1} the {2} time.", _
                        localTime.Kind.ToString(), _ 
                        [Enum].GetName(GetType(TimeComparison), localTime.CompareTo(utcTime)), _
                        utcTime.Kind.ToString())  
      ' If run in the U.S. Pacific Standard Time zone, the example displays 
      ' the following output to the console:
      '    Difference between Local and Utc time: -7:0 hours
      '    The Local time is EarlierThan the Utc time.                                                    
   End Sub
End Module
```

Il metodo [DateTime.CompareTo(DateTime, DateTime)](xref:System.DateTime.Compare(System.DateTime,System.DateTime)) indica che l'ora locale è più indietro rispetto all'ora UTC e l'operazione di sottrazione indica che la differenza tra l'ora UTC e l'ora locale per un sistema nel fuso orario standard del Pacifico (Stati Uniti) è sette ore. Ma poiché questi due valori indicano rappresentazioni diverse di un singolo momento, è chiaro in questo caso che l'intervallo di tempo è completamente attribuibile all'offset del fuso orario locale rispetto all'ora UTC. 

Più in generale, la proprietà [DateTimeKind](xref:System.DateTimeKind) non influisce sui risultati restituiti dai metodi di confronto e aritmetici [DateTime](xref:System.DateTime) (come indica il confronto tra due identici momenti), anche se può influire sull'interpretazione dei risultati. Ad esempio:

* Il risultato di qualsiasi operazione aritmetica eseguita su due valori di data e ora le cui proprietà [DateTimeKind](xref:System.DateTimeKind) sono entrambe uguali a [DateTimeKind.Utc](xref:System.DateTimeKind.Utc) riflette l'intervallo di tempo effettivo tra i due valori. Analogamente, il confronto di due valori di data e ora di questo tipo riflette esattamente la relazione tra le ore.

* Il risultato di qualsiasi operazione aritmetica o di confronto eseguita su due valori di data e ora le cui proprietà [DateTimeKind](xref:System.DateTimeKind) sono entrambe uguali a [DateTimeKind.Local](xref:System.DateTimeKind.Local) su due valori di data e ora con valori della proprietà [DateTimeKind](xref:System.DateTimeKind) diversi riflette la differenza di ora tra i due valori. 

* Le operazioni aritmetiche o di confronto sui valori locali di data e ora non considerano se un particolare valore è ambiguo o non valido e non tengono conto dell'effetto di eventuali regole di regolazione risultanti dalla transizione del fuso orario locale a o dall'ora legale.

* Qualsiasi operazione che confronta o calcola la differenza tra ora UTC e ora locale include un intervallo di tempo uguale all'offset del fuso orario locale rispetto all'ora UTC nel risultato. 

* Qualsiasi operazione che confronta o calcola la differenza tra un'ora non specificata e l'ora UTC o l'ora locale riflette l'ora dell'orologio. Le differenze di fuso orario non vengono considerate e il risultato non riflette l'applicazione delle regole di regolazione del fuso orario. 

* Qualsiasi operazione che confronta o calcola la differenza tra due ore non specificate può includere un intervallo sconosciuto che riflette la differenza di orario in due fusi orari diversi.

Esistono molti scenari in cui le differenze di fuso orario non influiscono sui calcoli di data e ora o in cui il contesto dei dati di data e ora definisce il significato delle operazioni aritmetiche o di confronto. Per una discussione su alcuni di questi elementi, vedere [Scelta tra DateTime, DateTimeOffset, TimeSpan e TimeZoneInfo](choosing-between-datetime.md).

## <a name="comparisons-and-arithmetic-operations-with-datetimeoffset-values"></a>Confronti e operazioni aritmetiche con i valori DateTimeOffset

Un valore [System.DateTimeOffset](xref:System.DateTimeOffset) include non solo una data e un'ora, ma anche un offset che definisce in modo univoco tale data e ora rispetto all'ora UTC. In questo modo è possibile definire l'uguaglianza in modo diverso rispetto ai valori [System.DateTime](xref:System.DateTime). Mentre i valori [DateTime](xref:System.DateTime) sono uguali se hanno lo stesso valore di data e ora, i valori [DateTimeOffset](xref:System.DateTimeOffset) sono uguali se si riferiscono entrambi allo stesso momento. Un valore [DateTimeOffset](xref:System.DateTimeOffset) è quindi più preciso e meno soggetto a interpretazione quando viene usato nei confronti e nella maggior parte delle operazioni aritmetiche che determinano l'intervallo tra due date e ore. L'esempio seguente, identico a quello precedente in cui si confrontano i valori DateTime locali e UTC ma con [DateTimeOffset](xref:System.DateTimeOffset), illustra questa differenza di comportamento.

```csharp
using System;

public enum TimeComparison
{
   EarlierThan = -1,
   TheSameAs = 0,
   LaterThan = 1
}

public class DateTimeOffsetManipulation
{
   public static void Main()
   {
      DateTimeOffset localTime = DateTimeOffset.Now;
      DateTimeOffset utcTime = DateTimeOffset.UtcNow;

      Console.WriteLine("Difference between local time and UTC: {0}:{1:D2} hours", 
                        (localTime - utcTime).Hours, 
                        (localTime - utcTime).Minutes);
      Console.WriteLine("The local time is {0} UTC.", 
                        Enum.GetName(typeof(TimeComparison), localTime.CompareTo(utcTime)));  
   }
}
// Regardless of the local time zone, the example displays 
// the following output to the console:
//    Difference between local time and UTC: 0:00 hours.
//    The local time is TheSameAs UTC.
```

```vb
Public Enum TimeComparison As Integer
   EarlierThan = -1
   TheSameAs = 0
   LaterThan = 1
End Enum

Module DateTimeOffsetManipulation
   Public Sub Main()
      Dim localTime As DateTimeOffset = DateTimeOffset.Now
      Dim utcTime As DateTimeOffset = DateTimeOffset.UtcNow

      Console.WriteLine("Difference between local time and UTC: {0}:{1:D2} hours.", _
                        (localTime - utcTime).Hours, _
                        (localTime - utcTime).Minutes)
      Console.WriteLine("The local time is {0} UTC.", _
                        [Enum].GetName(GetType(TimeComparison), localTime.CompareTo(utcTime)))  
   End Sub
End Module
' Regardless of the local time zone, the example displays 
' the following output to the console:
'    Difference between local time and UTC: 0:00 hours.
'    The local time is TheSameAs UTC.
'          Console.WriteLine(e.GetType().Name)
```

In questo esempio il metodo [DateTimeOffset.CompareTo](xref:System.DateTimeOffset.CompareTo(System.DateTimeOffset)) indica che l'ora locale corrente e l'ora UTC corrente sono uguali e la sottrazione dei valori [DateTimeOffset](xref:System.DateTimeOffset) indica che la differenza tra i due orari è [TimeSpan.Zero](xref:System.TimeSpan.Zero). 

La limitazione principale dell'uso dei valori [DateTimeOffset](xref:System.DateTimeOffset) nelle operazioni aritmetiche con data e ora è che il fuso orario non è completamente rappresentato, benché i valori [DateTimeOffset](xref:System.DateTimeOffset) contengano riferimenti al fuso orario. Sebbene il valore [DateTimeOffset](xref:System.DateTimeOffset) rifletta l'offset del fuso orario rispetto all'ora UTC quando a una variabile [DateTimeOffset](xref:System.DateTimeOffset) viene assegnato per la prima volta un valore, in un secondo tempo l'associazione al fuso orario viene annullata. Poiché non è più associato direttamente a un'ora identificabile, l'aggiunta e la sottrazione degli intervalli di data e ora non considerano le regole di regolazione del fuso orario. 

A titolo esemplificativo, la transizione all'ora legale negli Stati Uniti, ora solare fuso centrale, avviene alle 2.00 del 9 marzo 2008. Ciò significa che l'aggiunta di un intervallo di due ore e mezzo all'1.30 del 9 marzo 2008 nel fuso orario standard centrale deve generare una data e un'ora equivalente alle 5.00 del 9 marzo 2008. Tuttavia, come mostrato nell'esempio seguente, il risultato dell'addizione è 4.00 del 9 marzo 2008. Si noti che il risultato di questa operazione rappresenta il momento corretto, sebbene non sia l'ora nel fuso orario che interessa (ovvero, non presenta l'offset previsto per il fuso orario).

```csharp
using System;

public class IntervalArithmetic
{
   public static void Main()
   {
      DateTime generalTime = new DateTime(2008, 3, 9, 1, 30, 0);
      const string tzName = "Central Standard Time";
      TimeSpan twoAndAHalfHours = new TimeSpan(2, 30, 0);

      // Instantiate DateTimeOffset value to have correct CST offset
      try
      {
         DateTimeOffset centralTime1 = new DateTimeOffset(generalTime, 
                    TimeZoneInfo.FindSystemTimeZoneById(tzName).GetUtcOffset(generalTime));

         // Add two and a half hours      
         DateTimeOffset centralTime2 = centralTime1.Add(twoAndAHalfHours);
         // Display result
         Console.WriteLine("{0} + {1} hours = {2}", centralTime1, 
                                                    twoAndAHalfHours.ToString(), 
                                                    centralTime2);  
      }
      catch (TimeZoneNotFoundException)
      {
         Console.WriteLine("Unable to retrieve Central Standard Time zone information.");
      }
   }
}
// The example displays the following output to the console:
//    3/9/2008 1:30:00 AM -06:00 + 02:30:00 hours = 3/9/2008 4:00:00 AM -06:00
```

```vb
Module IntervalArithmetic
   Public Sub Main()
      Dim generalTime As Date = #03/09/2008 1:30AM#
      Const tzName As String = "Central Standard Time"
      Dim twoAndAHalfHours As New TimeSpan(2, 30, 0)

      ' Instantiate DateTimeOffset value to have correct CST offset
      Try
         Dim centralTime1 As New DateTimeOffset(generalTime, _
                    TimeZoneInfo.FindSystemTimeZoneById(tzName).GetUtcOffset(generalTime))

         ' Add two and a half hours      
         Dim centralTime2 As DateTimeOffset = centralTime1.Add(twoAndAHalfHours)
         ' Display result
         Console.WriteLine("{0} + {1} hours = {2}", centralTime1, _
                                                    twoAndAHalfHours.ToString(), _
                                                    centralTime2)   
      Catch e As TimeZoneNotFoundException
         Console.WriteLine("Unable to retrieve Central Standard Time zone information.")
      End Try
   End Sub
End Module
' The example displays the following output to the console:
'    3/9/2008 1:30:00 AM -06:00 + 02:30:00 hours = 3/9/2008 4:00:00 AM -06:00
```

## <a name="arithmetic-operations-with-times-in-time-zones"></a>Operazioni aritmetiche con ore in fusi orari

La classe [System.TimeZoneInfo](xref:System.TimeZoneInfo) non offre metodi che applicano automaticamente regole di regolazione quando si eseguono operazioni aritmetiche con data e ora. Tuttavia, è possibile convertire l'ora in un fuso orario in ora UTC, eseguendo l'operazione aritmetica, e quindi convertirla di nuovo da ora UTC a ora nel fuso orario. Per i dettagli, vedere [Procedura: Usare fusi orari nell'aritmetica di data e ora](use-time-zones-in-arithmetic.md).

Ad esempio, il codice seguente è simile al codice precedente che ha aggiunto due ore e mezzo alle 2.00 del 9 marzo 2008. Tuttavia, perché il codice converte un'ora solare nel fuso orario centrale in ora UTC prima di eseguire un'operazione aritmetica con data e ora e quindi converte di nuovo il risultato da ora UTC in ora solare nel fuso orario centrale, l'ora risultante riflette la transizione dell'ora solare nel fuso orario centrale all'ora legale.

```csharp
using System;

public class TimeZoneAwareArithmetic
{
   public static void Main()
   {
      const string tzName = "Central Standard Time";

      DateTime generalTime = new DateTime(2008, 3, 9, 1, 30, 0);
      TimeZoneInfo cst = TimeZoneInfo.FindSystemTimeZoneById(tzName);
      TimeSpan twoAndAHalfHours = new TimeSpan(2, 30, 0);

      // Instantiate DateTimeOffset value to have correct CST offset
      try
      {
         DateTimeOffset centralTime1 = new DateTimeOffset(generalTime, 
                                       cst.GetUtcOffset(generalTime));

         // Add two and a half hours
         DateTimeOffset utcTime = centralTime1.ToUniversalTime();
         utcTime += twoAndAHalfHours;

         DateTimeOffset centralTime2 = TimeZoneInfo.ConvertTime(utcTime, cst);
         // Display result
         Console.WriteLine("{0} + {1} hours = {2}", centralTime1, 
                                                    twoAndAHalfHours.ToString(), 
                                                    centralTime2);  
      }
      catch (TimeZoneNotFoundException)
      {
         Console.WriteLine("Unable to retrieve Central Standard Time zone information.");
      }
   }
}
// The example displays the following output to the console:
//    3/9/2008 1:30:00 AM -06:00 + 02:30:00 hours = 3/9/2008 5:00:00 AM -05:00
```

```vb
Module TimeZoneAwareArithmetic
   Public Sub Main()
      Const tzName As String = "Central Standard Time"

      Dim generalTime As Date = #03/09/2008 1:30AM#
      Dim cst As TimeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById(tzName) 
      Dim twoAndAHalfHours As New TimeSpan(2, 30, 0)

      ' Instantiate DateTimeOffset value to have correct CST offset
      Try
         Dim centralTime1 As New DateTimeOffset(generalTime, _
                    cst.GetUtcOffset(generalTime))

         ' Add two and a half hours 
         Dim utcTime As DateTimeOffset = centralTime1.ToUniversalTime()
         utcTime += twoAndAHalfHours

         Dim centralTime2 As DateTimeOffset = TimeZoneInfo.ConvertTime(utcTime, cst)
         ' Display result
         Console.WriteLine("{0} + {1} hours = {2}", centralTime1, _
                                                    twoAndAHalfHours.ToString(), _
                                                    centralTime2)   
      Catch e As TimeZoneNotFoundException
         Console.WriteLine("Unable to retrieve Central Standard Time zone information.")
      End Try
   End Sub
End Module
' The example displays the following output to the console:
'    3/9/2008 1:30:00 AM -06:00 + 02:30:00 hours = 3/9/2008 5:00:00 AM -05:00
```

## <a name="see-also"></a>Vedere anche

[Date, ore e fusi orari](index.md)

[Procedura: Usare fusi orari nell'aritmetica di data e ora](use-time-zones-in-arithmetic.md)



