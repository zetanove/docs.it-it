---
title: Scelta tra DateTime, DateTimeOffset, TimeSpan e TimeZoneInfo
description: Scelta tra DateTime, DateTimeOffset, TimeSpan e TimeZoneInfo
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 08/11/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 2dd84ee8-9f0f-4054-9537-155857a460cd
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: f8a603bab32afd0b8e7d13c9c5755e3f14a9d2bd

---

# <a name="choosing-between-datetime-datetimeoffset-timespan-and-timezoneinfo"></a>Scelta tra DateTime, DateTimeOffset, TimeSpan e TimeZoneInfo

Le applicazioni .NET che usano informazioni su data e ora sono molto diversificate e possono usare tali informazioni in modi diversi. Gli utilizzi più comuni delle informazioni su data e ora includono uno o più dei seguenti:

* Indicare solo una data, perché le informazioni sull'ora non sono importanti.

* Indicare solo un'ora, perché le informazioni sulla data non sono importanti.

* Indicare una data e un'ora astratte e non associate a un momento e un luogo specifici. Ad esempio, la maggior parte dei negozi di una catena internazionale apre alle 9.00 di ogni giorno feriale.

* Recuperare informazioni su data e ora da origini esterne all'applicazione .NET, in genere quando tali informazioni sono archiviate in un tipo di dati semplice.

* Identificare in modo univoco e senza ambiguità un singolo momento. In alcune applicazioni è necessario che la data e l'ora siano non ambigue solo nel sistema host, in altre devono non esserlo in tutti i sistemi (ovvero, una data serializzata in un sistema può essere deserializzata in modo significativo e usata in un altro sistema in qualsiasi parte del mondo). 

* Mantenere più ore correlate, ad esempio l'ora locale del richiedente e l'ora di ricezione di una richiesta Web nel server.

* Eseguire operazioni aritmetiche per date e ore, possibilmente con un risultato che identifichi in modo univoco e senza ambiguità una singolo momento. 

.NET include i tipi [System.DateTime](xref:System.DateTime), [System.DateTimeOffset](xref:System.DateTimeOffset), [System.TimeSpan](xref:System.TimeSpan) e [System.TimeZoneInfo](xref:System.TimeZoneInfo). Tutti i tipi possono essere usati per compilare applicazioni che impiegano date e ore. 

> [!NOTE]
> Questo argomento non descrive `TimeZone`, un tipo mene recente la cui funzionalità è quasi interamente integrata nella classe [System.TimeZoneInfo](xref:System.TimeZoneInfo). Quando è possibile, gli sviluppatori devono usare la classe [System.TimeZoneInfo](xref:System.TimeZoneInfo) anziché la classe `TimeZone`.


## <a name="the-datetime-structure"></a>Struttura DateTime

Un valore [System.DateTime](xref:System.DateTime) definisce una data e un'ora specifiche. Include la proprietà [Kind](xref:System.DateTime.Kind) che contiene informazioni limitate sul fuso orario cui appartengono la data e l'ora. Il valore [DateTimeKind](xref:System.DateTimeKind) restituito dalla proprietà [Kind](xref:System.DateTime.Kind) indica se il valore [DateTime](xref:System.DateTime) si riferisce all'ora locale [DateTimeKind.Local](xref:System.DateTimeKind.Local)), Coordinated Universal Time (UTC) [DateTimeKind.Utc](xref:System.DateTimeKind.Utc) o a un'ora non specificata [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified).

La struttura [DateTime](xref:System.DateTime) è adatta per le applicazioni che hanno le caratteristiche seguenti: 

* Usano solo date.

* Usano solo ore.

* Usano date e ore astratte.

* Usano date e ore per le quali mancano informazioni sul fuso orario. 

* Usano solo date e ore UTC. 

* Recuperano informazioni sulla data e sull'ora da origini esterne a .NET Framework, come i database SQL. In genere, queste origini archiviano le informazioni su data e ora in un formato semplice, compatibile con la struttura [DateTime](xref:System.DateTime).

* Eseguono operazioni aritmetiche su date e ore, ma con particolare attenzione ai risultati generali. Ad esempio, in un'operazione di addizione che aggiunge sei mesi a una data e un'ora specifiche, spesso non è importante se il risultato viene adattato per l'ora legale.

A meno che un determinato valore [DateTime](xref:System.DateTime) non rappresenti un'ora UTC, il valore di data e ora è spesso ambiguo e limitato in termini di portabilità. Ad esempio, se un valore [DateTime](xref:System.DateTime) rappresenta l'ora locale, è portabile all'interno del fuso orario locale. Di conseguenza, se il valore viene deserializzato in un altro sistema con lo stesso fuso orario, identifica comunque un singolo momento senza ambiguità. Al di fuori del fuso orario locale, tale valore [DateTime](xref:System.DateTime) è soggetto a più interpretazioni. Se la proprietà [Kind](xref:System.DateTime.Kind) del valore è [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified), il valore è ancora meno portabile, in quanto è ora ambiguo all'interno dello stesso fuso orario e probabilmente anche nello stesso sistema in cui è stato inizialmente serializzato. Solo se un valore [DateTime](xref:System.DateTime) rappresenta un'ora UTC, identifica senza ambiguità un singolo momento, indipendentemente dal sistema o dal fuso orario in cui viene usato.

> [!IMPORTANT]
> Quando si salvano o condividono dati [DateTime](xref:System.DateTime), è consigliabile usare l'ora UTC e la proprietà [Kind](xref:System.DateTime) del valore [DateTime](xref:System.DateTime.Kind) deve essere impostata su [DateTimeKind.Utc](xref:System.DateTimeKind.Utc).

## <a name="the-datetimeoffset-structure"></a>Struttura DateTimeOffset

La struttura [System.DateTimeOffset](xref:System.DateTimeOffset) rappresenta un valore di data e ora, insieme a un offset che indica la differenza di tale valore rispetto all'ora UTC. In questo modo, il valore identifica sempre senza ambiguità un singolo momento. 

Il tipo [DateTimeOffset](xref:System.DateTimeOffset) include tutte le funzionalità del tipo [DateTime](xref:System.DateTime) insieme alla compatibilità del fuso orario. Lo rende adatto per le applicazioni che hanno le caratteristiche seguenti: 

* Identificano in modo univoco e non ambiguo un singolo momento. Il tipo [DateTimeOffset](xref:System.DateTimeOffset) può essere usato per definire senza ambiguità il significato di "adesso", per registrare data e ora delle transazioni, del sistema o degli eventi delle applicazioni, nonché registrare data e ora di creazione e modifica dei file. 

* Eseguono operazioni aritmetiche su data e ora.

* Mantengono più date e ore correlate, purché vengano archiviate come due valori separati o due membri di una struttura.

> [!NOTE]
> Questi usi per i valori [DateTimeOffset](xref:System.DateTimeOffset) sono molto più comuni di quelli per i valori [DateTime](xref:System.DateTime). Di conseguenza, [DateTimeOffset](xref:System.DateTimeOffset) deve essere considerato il tipo di data e ora predefinito per lo sviluppo di applicazioni.

Un valore [DateTimeOffset](xref:System.DateTimeOffset) non è associato a un determinato fuso orario, ma può derivare da svariati fusi orari. Per illustrare questo concetto, l'esempio seguente elenca i fusi orari cui può appartenere un certo numero di valori [DateTimeOffset](xref:System.DateTimeOffset), incluso un valore con ora solare Pacifico locale.

```csharp
using System;
using System.Collections.ObjectModel;

public class TimeOffsets
{
   public static void Main()
   {
      DateTime thisDate = new DateTime(2007, 3, 10, 0, 0, 0);
      DateTime dstDate = new DateTime(2007, 6, 10, 0, 0, 0);
      DateTimeOffset thisTime;

      thisTime = new DateTimeOffset(dstDate, new TimeSpan(-7, 0, 0));
      ShowPossibleTimeZones(thisTime);

      thisTime = new DateTimeOffset(thisDate, new TimeSpan(-6, 0, 0));  
      ShowPossibleTimeZones(thisTime);

      thisTime = new DateTimeOffset(thisDate, new TimeSpan(+1, 0, 0));
      ShowPossibleTimeZones(thisTime);
   }

   private static void ShowPossibleTimeZones(DateTimeOffset offsetTime)
   {
      TimeSpan offset = offsetTime.Offset;
      ReadOnlyCollection<TimeZoneInfo> timeZones;

      Console.WriteLine("{0} could belong to the following time zones:", 
                        offsetTime.ToString());
      // Get all time zones defined on local system
      timeZones = TimeZoneInfo.GetSystemTimeZones();     
      // Iterate time zones 
      foreach (TimeZoneInfo timeZone in timeZones)
      {
         // Compare offset with offset for that date in that time zone
         if (timeZone.GetUtcOffset(offsetTime.DateTime).Equals(offset))
            Console.WriteLine("   {0}", timeZone.DisplayName);
      }
      Console.WriteLine();
   } 
}
// This example displays the following output to the console:
//       6/10/2007 12:00:00 AM -07:00 could belong to the following time zones:
//          (GMT-07:00) Arizona
//          (GMT-08:00) Pacific Time (US & Canada)
//          (GMT-08:00) Tijuana, Baja California
//       
//       3/10/2007 12:00:00 AM -06:00 could belong to the following time zones:
//          (GMT-06:00) Central America
//          (GMT-06:00) Central Time (US & Canada)
//          (GMT-06:00) Guadalajara, Mexico City, Monterrey - New
//          (GMT-06:00) Guadalajara, Mexico City, Monterrey - Old
//          (GMT-06:00) Saskatchewan
//       
//       3/10/2007 12:00:00 AM +01:00 could belong to the following time zones:
//          (GMT+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna
//          (GMT+01:00) Belgrade, Bratislava, Budapest, Ljubljana, Prague
//          (GMT+01:00) Brussels, Copenhagen, Madrid, Paris
//          (GMT+01:00) Sarajevo, Skopje, Warsaw, Zagreb
//          (GMT+01:00) West Central Africa
```

```vb
Imports System.Collections.ObjectModel

Module TimeOffsets
   Public Sub Main()
      Dim thisTime As DateTimeOffset 

      thisTime = New DateTimeOffset(#06/10/2007#, New TimeSpan(-7, 0, 0))
      ShowPossibleTimeZones(thisTime) 

      thisTime = New DateTimeOffset(#03/10/2007#, New TimeSpan(-6, 0, 0))  
      ShowPossibleTimeZones(thisTime)

      thisTime = New DateTimeOffset(#03/10/2007#, New TimeSpan(+1, 0, 0))
      ShowPossibleTimeZones(thisTime)
   End Sub

   Private Sub ShowPossibleTimeZones(offsetTime As DateTimeOffset)
      Dim offset As TimeSpan = offsetTime.Offset
      Dim timeZones As ReadOnlyCollection(Of TimeZoneInfo)

      Console.WriteLine("{0} could belong to the following time zones:", _
                        offsetTime.ToString())
      ' Get all time zones defined on local system
      timeZones = TimeZoneInfo.GetSystemTimeZones()     
      ' Iterate time zones
      For Each timeZone As TimeZoneInfo In timeZones
         ' Compare offset with offset for that date in that time zone
         If timeZone.GetUtcOffset(offsetTime.DateTime).Equals(offset) Then
            Console.WriteLine("   {0}", timeZone.DisplayName)
         End If   
      Next
      Console.WriteLine()
   End Sub
End Module
' This example displays the following output to the console:
'       6/10/2007 12:00:00 AM -07:00 could belong to the following time zones:
'          (GMT-07:00) Arizona
'          (GMT-08:00) Pacific Time (US & Canada)
'          (GMT-08:00) Tijuana, Baja California
'       
'       3/10/2007 12:00:00 AM -06:00 could belong to the following time zones:
'          (GMT-06:00) Central America
'          (GMT-06:00) Central Time (US & Canada)
'          (GMT-06:00) Guadalajara, Mexico City, Monterrey - New
'          (GMT-06:00) Guadalajara, Mexico City, Monterrey - Old
'          (GMT-06:00) Saskatchewan
'       
'       3/10/2007 12:00:00 AM +01:00 could belong to the following time zones:
'          (GMT+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna
'          (GMT+01:00) Belgrade, Bratislava, Budapest, Ljubljana, Prague
'          (GMT+01:00) Brussels, Copenhagen, Madrid, Paris
'          (GMT+01:00) Sarajevo, Skopje, Warsaw, Zagreb
'          (GMT+01:00) West Central Africa
```

L'output mostra che ogni valore di data e ora nell'esempio può appartenere almeno a tre fusi orari diversi. Il valore [DateTimeOffset](xref:System.DateTimeOffset) 6/10/2007 indica che se un valore di data e ora rappresenta un orario con ora legale, la sua differenza dall'ora UTC non corrisponde necessariamente alla differenza dall'ora UTC di base del fuso orario di origine o alla differenza dall'ora UTC indicata nel nome visualizzato. Questo significa che poiché un singolo valore [DateTimeOffset](xref:System.DateTimeOffset) non è strettamente collegato al proprio fuso orario, non può indicare la transizione di un fuso orario da e verso l'ora legale. Questo comportamento può rivelarsi particolarmente problematico quando vengono usate operazioni aritmetiche per date e ore per modificare un valore [DateTimeOffset](xref:System.DateTimeOffset). Per informazioni su come eseguire operazioni aritmetiche per date e ore che tengano conto delle regole di adeguamento del fuso orario, vedere [Performing arithmetic operations with dates and times](performing-arithmetic-operations.md) (Esecuzione di operazioni aritmetiche con date e ore).

## <a name="the-timespan-structure"></a>Struttura TimeSpan

La struttura [System.TimeSpan](xref:System.TimeSpan) rappresenta un intervallo di tempo. Ecco i due utilizzi tipici: 

* Indicare l'intervallo di tempo tra due valori di data e ora. Ad esempio, la sottrazione di un valore [DateTime](xref:System.DateTime) da un altro restituisce un valore [TimeSpan](xref:System.TimeSpan). 

* Misurare il tempo trascorso. Ad esempio, la proprietà [Stopwatch.Elapsed](xref:System.Diagnostics.Stopwatch.Elapsed) restituisce un valore [TimeSpan](xref:System.TimeSpan) che indica l'intervallo di tempo trascorso dalla chiamata a uno dei metodi [System.Diagnostics.Stopwatch](xref:System.Diagnostics.Stopwatch) che inizia a misurare il tempo trascorso.

Un valore [TimeSpan](xref:System.TimeSpan) può essere usato anche come sostituzione di un valore [DateTime](xref:System.DateTime) quando tale valore indica un momento senza riferimento a una determinata ora del giorno. Questo uso è simile alle proprietà [DateTime.TimeOfDay](xref:System.DateTime.TimeOfDay) e [DateTimeOffset.TimeOfDay](xref:System.DateTimeOffset.TimeOfDay), che restituiscono un valore [TimeSpan](xref:System.TimeSpan) che rappresenta l'ora senza riferimento a una data. Ad esempio, la struttura [TimeSpan](xref:System.TimeSpan) può essere usata per indicare l'ora di apertura o di chiusura di un negozio oppure per rappresentare l'ora in cui si verifica un evento regolare.

L'esempio seguente definisce una struttura `StoreInfo` che include oggetti [TimeSpan](xref:System.TimeSpan) per le ore di apertura e di chiusura di un negozio, nonché un oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) che rappresenta il fuso orario del negozio. La struttura include anche due metodi, `IsOpenNow` e `IsOpenAt`, che indicano se il negozio è aperto a un'ora specificata dall'utente, che si suppone si trovi nel fuso orario locale.  

```csharp
using System;

public struct StoreInfo
{
   public String store;
   public TimeZoneInfo tz;
   public TimeSpan open;
   public TimeSpan close;

   public bool IsOpenNow()
   {
      return IsOpenAt(DateTime.TimeOfDay);
   }

   public bool IsOpenAt(TimeSpan time)
   {
      TimeZoneInfo local = TimeZoneInfo.Local;
      TimeSpan offset = TimeZoneInfo.BaseUtcOffset;

      // Is the store in the same time zone?
      if (tz.Equals(local)) {
         return time >= open & time <= close;
      }
   }
}
```

```vb
Public Structure StoreInfo
   Dim store As String
   Dim tz As TimeZoneInfo
   Dim open As TimeSpan
   Dim close As TimeSpan

   Public Function IsOpenNow() As Boolean
      Return IsOpenAt(Date.Now.TimeOfDay)
   End Function

   Public Function IsOpenAt(time As TimeSpan) As Boolean
      Dim local As TimeZoneInfo = TimeZoneInfo.Local
      Dim offset As TimeSpan = TimeZoneInfo.Local.BaseUtcOffset

      ' Is the store in the same time zone?
      If tz.Equals(local) Then
         Return time >= open And time <= close
      Else
         Dim delta As TimeSpan = TimeSpan.Zero
         Dim storeDelta As TimeSpan = TimeSpan.Zero

         ' Is it daylight saving time in either time zone?
         If local.IsDaylightSavingTime(Date.Now.Date + time) Then
            delta = local.GetAdjustmentRules(local.GetAdjustmentRules().Length - 1).DaylightDelta
         End If
         If tz.IsDaylightSavingTime(TimeZoneInfo.ConvertTime(Date.Now.Date + time, local, tz))
            storeDelta = tz.GetAdjustmentRules(local.GetAdjustmentRules().Length - 1).DaylightDelta
         End If
         Dim comparisonTime As TimeSpan = time + (offset - tz.BaseUtcOffset).Negate() + (delta - storeDelta).Negate
         Return (comparisonTime >= open And comparisonTime <= close)
      End If
   End Function
End Structure
```

La struttura `StoreInfo` può quindi essere usata da codice client simile al seguente. 

```csharp
public class Example
{
   public static void Main()
   {
      // Instantiate a StoreInfo object.
      var store103 = new StoreInfo();
      store103.store = "Store #103";
      store103.tz = TimeZoneInfo.FindSystemTimeZoneById("Eastern Standard Time");
      // Store opens at 8:00.
      store103.open = new TimeSpan(8, 0, 0);
      // Store closes at 9:30.
      store103.close = new TimeSpan(21, 30, 0);

      Console.WriteLine("Store is open now at {0}: {1}",
                        DateTime.TimeOfDay, store103.IsOpenNow());
      TimeSpan[] times = { new TimeSpan(8, 0, 0), new TimeSpan(21, 0, 0),
                           new TimeSpan(4, 59, 0), new TimeSpan(18, 31, 0) };
      foreach (var time in times)
         Console.WriteLine("Store is open at {0}: {1}",
                           time, store103.IsOpenAt(time));
   }
}
// The example displays the following output:
//       Store is open now at 15:29:01.6129911: True
//       Store is open at 08:00:00: True
//       Store is open at 21:00:00: False
//       Store is open at 04:59:00: False
//       Store is open at 18:31:00: False
```

```vb
Module Example
   Public Sub Main()
      ' Instantiate a StoreInfo object.
      Dim store103 As New StoreInfo()
      store103.store = "Store #103"
      store103.tz = TimeZoneInfo.FindSystemTimeZoneById("Eastern Standard Time")
      ' Store opens at 8:00.
      store103.open = new TimeSpan(8, 0, 0)
      ' Store closes at 9:30.
      store103.close = new TimeSpan(21, 30, 0)

      Console.WriteLine("Store is open now at {0}: {1}",
                        Date.Now.TimeOfDay, store103.IsOpenNow())
      Dim times() As TimeSpan = { New TimeSpan(8, 0, 0),
                                  New TimeSpan(21, 0, 0),
                                  New TimeSpan(4, 59, 0),
                                  New TimeSpan(18, 31, 0) }
      For Each time In times
         Console.WriteLine("Store is open at {0}: {1}",
                           time, store103.IsOpenAt(time))
      Next
   End Sub
End Module
' The example displays the following output:
'       Store is open now at 15:29:01.6129911: True
'       Store is open at 08:00:00: True
'       Store is open at 21:00:00: False
'       Store is open at 04:59:00: False
'       Store is open at 18:31:00: False
```

## <a name="the-timezoneinfo-class"></a>Classe TimeZoneInfo

La classe [System.TimeZoneInfo](xref:System.TimeZoneInfo) rappresenta uno dei fusi orari della terra e consente la conversione di qualsiasi data e ora di un fuso orario negli equivalenti di un altro fuso orario. La classe [TimeZoneInfo](xref:System.TimeZoneInfo) consente di usare date e ore in modo che qualsiasi valore di data e ora identifichi un singolo momento senza ambiguità.

In alcuni casi, per sfruttare tutti i vantaggi della classe [TimeZoneInfo](xref:System.TimeZoneInfo) possono essere necessarie attività aggiuntive di sviluppo. I valori di data e ora non sono strettamente collegati ai fusi orari cui appartengono. Di conseguenza, a meno che l'applicazione non fornisca un meccanismo per collegare una data e un'ora al fuso orario associato, è facile che una data e un'ora specifiche non risultino associate al rispettivo fuso orario. Un metodo per collegare queste informazioni consiste nel definire una classe o una struttura che contiene sia i valori di data e ora sia l'oggetto fuso orario associato.

L'uso del supporto per i fusi orari in .NET è possibile solo se il fuso orario cui appartengono la data e l'ora è noto quando viene creata un'istanza dell'oggetto data e ora. Questo è un caso piuttosto raro, in particolare nelle applicazioni Web o di rete.

## <a name="see-also"></a>Vedere anche

[Date, ore e fusi orari](index.md)


<!--HONumber=Nov16_HO3-->


