---
title: 'Procedura: Usare fusi orari nell''aritmetica di data e ora'
description: Come usare i fusi orari nell&quot;aritmetica di data e ora
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 08/16/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 26870cdc-1709-4978-831b-ff2a2f24856f
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: da4c5aec6e02393c9e6201edd766eb7579a40b5e

---

# <a name="how-to-use-time-zones-in-date-and-time-arithmetic"></a>Procedura: Usare fusi orari nell'aritmetica di data e ora

In genere, quando si eseguono operazioni aritmetiche di data e ora con i valori [System.DateTimeOffset](xref:System.DateTimeOffset), il risultato non riflette nessuna regola di rettifica del fuso orario. Ciò resta vero anche quando il fuso orario del valore di data ora è chiaramente identificabile. In questo articolo viene illustrato come eseguire operazioni aritmetiche su valori di data e ora appartenenti a un determinato fuso orario. I risultati delle operazioni aritmetiche rifletteranno le regole di rettifica del fuso orario.

## <a name="to-apply-adjustment-rules-to-date-and-time-arithmetic"></a>Per applicare regole di rettifica ai calcoli aritmetici di data e ora

1. Implementare un metodo per vincolare un valore di data e ora al fuso orario al quale appartiene. Ad esempio, dichiarare una struttura che include sia il valore di data e ora sia il fuso orario al quale appartiene. Nell'esempio seguente viene usato questo approccio per collegare un valore [DateTimeOffset](xref:System.DateTimeOffset) al fuso orario di appartenenza.

    ```csharp
    // Define a structure for DateTime values for internal use only
    internal struct TimeWithTimeZone
    {
    TimeZoneInfo TimeZone;
    DateTimeOffset Time;
    }
    ```

    ```vb
    ' Define a structure for DateTime values for internal use only
    Friend Structure TimeWithTimeZone
       Dim TimeZone As TimeZoneInfo
       Dim Time As Date
    End Structure
    ```
    
2. Convertire un'ora nell'ora Coordinated Universal Time (UTC) chiamando il metodo [TimeZoneInfo.ConvertTime(DateTime, TimeZoneInfo)](xref:System.TimeZoneInfo.ConvertTime(System.DateTime,System.TimeZoneInfo)).

3. Eseguire l'operazione aritmetica sull'ora UTC.

4. Convertire l'ora da UTC al fuso orario associato all'ora originale, chiamando il metodo [TimeZoneInfo.ConvertTime(DateTime, TimeZoneInfo)](xref:System.TimeZoneInfo.ConvertTime(System.DateTime,System.TimeZoneInfo)). 

## <a name="example"></a>Esempio

L'esempio seguente aggiunge due ore e trenta minuti al 9 marzo 2008, alle 1.30 ora solare fuso centrale (CST). La transizione del fuso orario all'ora legale si verifica trenta minuti dopo, alle 2.00 del 9 marzo 2008. Poiché nell'esempio vengono seguiti i quattro passaggi elencati nella sezione precedente, l'orario corretto risultante corrisponderà alle 5.00 del 9 marzo 2008. 

```csharp
using System;

public struct TimeZoneTime
{
   public TimeZoneInfo TimeZone;
   public DateTimeOffset Time;

   public TimeZoneTime(TimeZoneInfo tz, DateTimeOffset time)
   {
      if (tz == null) 
         throw new ArgumentNullException("The time zone cannot be a null reference.");

      this.TimeZone = tz;
      this.Time = time;   
   }

   public TimeZoneTime AddTime(TimeSpan interval)
   {
      // Convert time to UTC
      DateTimeOffset utcTime = TimeZoneInfo.ConvertTime(this.Time, TimeZoneInfo.Utc);      
      // Add time interval to time
      utcTime = utcTime.Add(interval);
      // Convert time back to time in time zone
      return new TimeZoneTime(this.TimeZone, TimeZoneInfo.ConvertTime(utcTime, this.TimeZone));
   }
}

public class TimeArithmetic
{
   public const string tzName = "Central Standard Time";

   public static void Main()
   {
      try
      {
         TimeZoneTime cstTime1, cstTime2;

         TimeZoneInfo cst = TimeZoneInfo.FindSystemTimeZoneById(tzName);
         DateTime time1 = new DateTime(2008, 3, 9, 1, 30, 0);          
         TimeSpan twoAndAHalfHours = new TimeSpan(2, 30, 0);

         cstTime1 = new TimeZoneTime(cst, 
                        new DateTimeOffset(time1, cst.GetUtcOffset(time1)));
         cstTime2 = cstTime1.AddTime(twoAndAHalfHours);
         Console.WriteLine("{0} + {1} hours = {2}", cstTime1.Time, 
                                                    twoAndAHalfHours.ToString(),  
                                                    cstTime2.Time);
      }
      catch
      {
         Console.WriteLine("Unable to find {0}.", tzName);
      }
   }
}
```

```vb
Public Structure TimeZoneTime
   Public TimeZone As TimeZoneInfo
   Public Time As Date

   Public Sub New(tz As TimeZoneInfo, time As Date)
      If tz Is Nothing Then _
         Throw New ArgumentNullException("The time zone cannot be a null reference.")

      Me.TimeZone = tz
      Me.Time = time
   End Sub

   Public Function AddTime(interval As TimeSpan) As TimeZoneTime
      ' Convert time to UTC
      Dim utcTime As DateTime = TimeZoneInfo.ConvertTimeToUtc(Me.Time, _
                                                              Me.TimeZone)      
      ' Add time interval to time
      utcTime = utcTime.Add(interval)
      ' Convert time back to time in time zone
      Return New TimeZoneTime(Me.TimeZone, TimeZoneInfo.ConvertTime(utcTime, _
                              TimeZoneInfo.Utc, Me.TimeZone))
   End Function
End Structure

Module TimeArithmetic
   Public Const tzName As String = "Central Standard Time"

   Public Sub Main()
      Try
         Dim cstTime1, cstTime2 As TimeZoneTime

         Dim cst As TimeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById(tzName)
         Dim time1 As Date = #03/09/2008 1:30AM#
         Dim twoAndAHalfHours As New TimeSpan(2, 30, 0)

         cstTime1 = New TimeZoneTime(cst, time1)
         cstTime2 = cstTime1.AddTime(twoAndAHalfHours)

         Console.WriteLine("{0} + {1} hours = {2}", cstTime1.Time, _
                                                    twoAndAHalfHours.ToString(), _ 
                                                    cstTime2.Time)  
      Catch
         Console.WriteLine("Unable to find {0}.", tzName)
      End Try   
   End Sub   
End Module
```

Se questa aggiunta viene eseguita semplicemente al valore [DateTimeOffset](xref:System.DateTimeOffset) senza prima convertirlo a UTC, il risultato riflette l'orario corretto, ma il suo offset non riflette quello del fuso orario designato per l'orario. 

I valori [DateTimeOffset](xref:System.DateTimeOffset) sono dissociati da qualsiasi fuso orario al quale appartengono. Per eseguire operazioni aritmetiche di data ora con una modalità che applica automaticamente le regole di rettifica del fuso orario, il fuso orario di appartenenza di qualsiasi valore di data e ora deve essere immediatamente identificabile. Ciò significa che una data e ora e il fuso orario associato devono essere strettamente collegati. Esistono diversi modi per ottenere questo risultato, tra cui i seguenti:

* Presupporre che tutti gli orari usati in un'applicazione appartengano a un determinato fuso orario. Pur essendo appropriato in alcuni casi, questo approccio offre una flessibilità limitata e potenzialmente anche una portabilità limitata.

* Definire un tipo che vincoli in modo stretto una data e ora con il fuso orario associato, includendo entrambi come campi del tipo. Questo approccio viene usato nell'esempio di codice, che definisce una struttura per l'archiviazione della data e ora e del fuso orario in due campi membro.

## <a name="see-also"></a>Vedere anche

[Date, ore e fusi orari](index.md)

[Esecuzione di operazioni aritmetiche con date e ore](performing-arithmetic-operations.md)



<!--HONumber=Nov16_HO3-->


