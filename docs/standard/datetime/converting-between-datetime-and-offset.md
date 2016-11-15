---
title: Conversione tra DateTime e DateTimeOffset
description: Conversione tra DateTime e DateTimeOffset
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 08/15/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: fab3af5b-5d0f-4384-a40a-1b5d99b30dd1
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: 312ac8cb7e901c4ceeff2e428620c2c4c615ca3d

---

# <a name="converting-between-datetime-and-datetimeoffset"></a>Conversione tra DateTime e DateTimeOffset

Anche se la struttura [System.DateTimeOffset](xref:System.DateTimeOffset) offre una maggiore chiarezza sui fusi orari rispetto alla struttura [System.DateTime](xref:System.DateTime), i parametri [DateTime](xref:System.DateTime) sono usati più comunemente per le chiamate al metodo. Per questo motivo la possibilità di convertire valori [DateTimeOffset](xref:System.DateTimeOffset) in valori [DateTime](xref:System.DateTime) e viceversa è particolarmente importante. In questo articolo viene illustrato come eseguire tali conversioni in un modo che consenta di mantenere il maggior numero possibile di informazioni sul fuso orario.

> [!NOTE]
> I tipi [DateTime](xref:System.DateTime) e [DateTimeOffset](xref:System.DateTimeOffset) presentano alcune limitazioni in caso di rappresentazione delle ore nei fusi orari. Con la proprietà [Kind](xref:System.DateTime.Kind), [DateTime](xref:System.DateTime) è in grado di riflettere solo l'UTC (Coordinated Universal Time) e il fuso orario locale di sistema. [DateTimeOffset](xref:System.DateTimeOffset) riflette l'offset di un'ora rispetto all'UTC, ma non riflette il fuso orario effettivo al quale appartiene tale offset. Per dettagli sui valori orari e il supporto dei fusi orari, vedere [Scelta tra DateTime, DateTimeOffset, TimeSpan e TimeZoneInfo](choosing-between-datetime.md).

## <a name="conversions-from-datetime-to-datetimeoffset"></a>Conversioni da DateTime a DateTimeOffset

La struttura [DateTimeOffset](xref:System.DateTimeOffset) fornisce due modalità equivalenti per eseguire la conversione da [DateTime](xref:System.DateTime) a [DateTimeOffset](xref:System.DateTimeOffset) adatte per la maggior parte delle conversioni:

* Tramite il costruttore [DateTimeOffset(DateTime)](xref:System.DateTimeOffset), che crea un nuovo oggetto [DateTimeOffset](xref:System.DateTimeOffset) in base a un valore [DateTime](xref:System.DateTime).

* Tramite l'operatore di conversione implicito, che consente di assegnare un valore [DateTime](xref:System.DateTime) a un oggetto [DateTimeOffset](xref:System.DateTimeOffset).

Per i valori UTC e locali di [DateTime](xref:System.DateTime) la proprietà [DateTimeOffset.Offset](xref:System.DateTimeOffset.Offset) del valore risultante [DateTimeOffset](xref:System.DateTimeOffset) riflette accuratamente l'offset UTC o del fuso orario locale. Nel codice riportato di seguito, ad esempio, un'ora UTC viene convertito nel valore [DateTimeOffset](xref:System.DateTimeOffset) equivalente. 

```csharp
DateTime utcTime1 = new DateTime(2008, 6, 19, 7, 0, 0);
utcTime1 = DateTime.SpecifyKind(utcTime1, DateTimeKind.Utc);
DateTimeOffset utcTime2 = utcTime1;
Console.WriteLine("Converted {0} {1} to a DateTimeOffset value of {2}", 
                  utcTime1, 
                  utcTime1.Kind.ToString(), 
                  utcTime2);
// This example displays the following output to the console:
//    Converted 6/19/2008 7:00:00 AM Utc to a DateTimeOffset value of 6/19/2008 7:00:00 AM +00:00
```

```vb
Dim utcTime1 As Date = Date.SpecifyKind(#06/19/2008 7:00AM#, _
                                        DateTimeKind.Utc)
Dim utcTime2 As DateTimeOffset = utcTime1
Console.WriteLine("Converted {0} {1} to a DateTimeOffset value of {2}", _
                  utcTime1, _
                  utcTime1.Kind.ToString(), _
                  utcTime2)
' This example displays the following output to the console:
'    Converted 6/19/2008 7:00:00 AM Utc to a DateTimeOffset value of 6/19/2008 7:00:00 AM  +00:00
```

In questo caso, l'offset della variabile `utcTime2` è 00:00. Analogamente, il codice riportato di seguito converte un'ora locale nel valore [DateTimeOffset](xref:System.DateTimeOffset) equivalente.

```csharp
DateTime localTime1 = new DateTime(2008, 6, 19, 7, 0, 0);
localTime1 = DateTime.SpecifyKind(localTime1, DateTimeKind.Local);
DateTimeOffset localTime2 = localTime1;
Console.WriteLine("Converted {0} {1} to a DateTimeOffset value of {2}", 
                  localTime1, 
                  localTime1.Kind.ToString(), 
                  localTime2);
// This example displays the following output to the console:
//    Converted 6/19/2008 7:00:00 AM Local to a DateTimeOffset value of 6/19/2008 7:00:00 AM -07:00
```

```vb
Dim localTime1 As Date = Date.SpecifyKind(#06/19/2008 7:00AM#, DateTimeKind.Local)
Dim localTime2 As DateTimeOffset = localTime1
Console.WriteLine("Converted {0} {1} to a DateTimeOffset value of {2}", _
                  localTime1, _
                  localTime1.Kind.ToString(), _
                  localTime2)
' This example displays the following output to the console:
'    Converted 6/19/2008 7:00:00 AM Local to a DateTimeOffset value of 6/19/2008 7:00:00 AM -07:00
```

Per valori [DateTime](xref:System.DateTime) la cui proprietà [Kind](xref:System.DateTime.Kind) è [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified), questi due metodi di conversione producono tuttavia un valore [DateTimeOffset](xref:System.DateTimeOffset) il cui offset è quello del fuso orario locale. Ciò viene illustrato nell'esempio seguente che viene eseguito nel fuso orario Ora solare del Pacifico (Stati Uniti).

```csharp
DateTime time1 = new DateTime(2008, 6, 19, 7, 0, 0);  // Kind is DateTimeKind.Unspecified
DateTimeOffset time2 = time1;
Console.WriteLine("Converted {0} {1} to a DateTimeOffset value of {2}", 
                  time1, 
                  time1.Kind.ToString(), 
                  time2);
// This example displays the following output to the console:
//    Converted 6/19/2008 7:00:00 AM Unspecified to a DateTimeOffset value of 6/19/2008 7:00:00 AM -07:00
```

```vb
Dim time1 As Date = #06/19/2008 7:00AM#      ' Kind is DateTimeKind.Unspecified
Dim time2 As DateTimeOffset = time1
Console.WriteLine("Converted {0} {1} to a DateTimeOffset value of {2}", _
                  time1, _
                  time1.Kind.ToString(), _
                  time2)
' This example displays the following output to the console:
'    Converted 6/19/2008 7:00:00 AM Unspecified to a DateTimeOffset value of 6/19/2008 7:00:00 AM -07:00
```

Se il valore [DateTime](xref:System.DateTime) riflette la data e l'ora in modo diverso dal fuso orario locale o UTC, è possibile convertirlo in un valore [DateTimeOffset](xref:System.DateTimeOffset) e mantenere le informazioni sul fuso orario chiamando il costruttore [DateTimeOffset(DateTime, TimeSpan)](xref:System.DateTimeOffset) di overload. Nell'esempio riportato di seguito viene creata un'istanza di un oggetto [DateTimeOffset](xref:System.DateTimeOffset) che riflette l'ora solare fuso centrale.

```csharp
DateTime time1 = new DateTime(2008, 6, 19, 7, 0, 0);     // Kind is DateTimeKind.Unspecified
try
{
   DateTimeOffset time2 = new DateTimeOffset(time1, 
                  TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time").GetUtcOffset(time1)); 
   Console.WriteLine("Converted {0} {1} to a DateTime value of {2}", 
                     time1, 
                     time1.Kind.ToString(), 
                     time2);
}
// Handle exception if time zone is not defined in registry
catch (TimeZoneNotFoundException)
{
   Console.WriteLine("Unable to identify target time zone for conversion.");
}
// This example displays the following output to the console:
//    Converted 6/19/2008 7:00:00 AM Unspecified to a DateTime value of 6/19/2008 7:00:00 AM -05:00
```

```vb
Dim time1 As Date = #06/19/2008 7:00AM#      ' Kind is DateTimeKind.Unspecified
Try
   Dim time2 As New DateTimeOffset(time1, _
                    TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time").GetUtcOffset(time1)) 
   Console.WriteLine("Converted {0} {1} to a DateTime value of {2}", _
                     time1, _
                     time1.Kind.ToString(), _
                     time2)
' Handle exception if time zone is not defined in registry
Catch e As TimeZoneNotFoundException
   Console.WriteLine("Unable to identify target time zone for conversion.")
End Try
' This example displays the following output to the console:
'    Converted 6/19/2008 7:00:00 AM Unspecified to a DateTime value of 6/19/2008 7:00:00 AM -05:00
```

Il secondo parametro per questo overload del costruttore, un oggetto [System.TimeSpan](xref:System.TimeSpan)che rappresenta l'offset dell'ora rispetto all'ora UTC, deve essere recuperato chiamando il metodo [TimeZoneInfo.GetUtcOffset(DateTime)](xref:System.TimeZoneInfo) del fuso orario corrispondente all'ora. L'unico parametro del metodo è il valore [DateTime](xref:System.DateTime) che rappresenta la data e l'ora da convertire. Se il fuso orario supporta l'ora legale, questo parametro consente al metodo di determinare l'offset adatto per la data e l'ora specifici.

## <a name="conversions-from-datetimeoffset-to-datetime"></a>Conversioni da DateTimeOffset a DateTime

La proprietà [DateTime](xref:System.DateTime)è nella maggior parte dei casi usata per eseguire la conversione da [DateTimeOffset](xref:System.DateTimeOffset) a [DateTime](xref:System.DateTime). Tuttavia, restituisce un valore [DateTime](xref:System.DateTime) la cui proprietà [Kind](xref:System.DateTime.Kind) è [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified), come illustrato nell'esempio seguente. 

```csharp
DateTime baseTime = new DateTime(2008, 6, 19, 7, 0, 0);
DateTimeOffset sourceTime;
DateTime targetTime;

// Convert UTC to DateTime value
sourceTime = new DateTimeOffset(baseTime, TimeSpan.Zero);
targetTime = sourceTime.DateTime;
Console.WriteLine("{0} converts to {1} {2}", 
                  sourceTime, 
                  targetTime, 
                  targetTime.Kind.ToString());

// Convert local time to DateTime value
sourceTime = new DateTimeOffset(baseTime, 
                                TimeZoneInfo.Local.GetUtcOffset(baseTime));
targetTime = sourceTime.DateTime;
Console.WriteLine("{0} converts to {1} {2}", 
                  sourceTime, 
                  targetTime, 
                  targetTime.Kind.ToString());

// Convert Central Standard Time to a DateTime value
try
{
   TimeSpan offset = TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time").GetUtcOffset(baseTime);
   sourceTime = new DateTimeOffset(baseTime, offset);
   targetTime = sourceTime.DateTime;
   Console.WriteLine("{0} converts to {1} {2}", 
                     sourceTime, 
                     targetTime, 
                     targetTime.Kind.ToString());
}
catch (TimeZoneNotFoundException)
{
   Console.WriteLine("Unable to create DateTimeOffset based on U.S. Central Standard Time.");
} 
// This example displays the following output to the console:
//    6/19/2008 7:00:00 AM +00:00 converts to 6/19/2008 7:00:00 AM Unspecified
//    6/19/2008 7:00:00 AM -07:00 converts to 6/19/2008 7:00:00 AM Unspecified
//    6/19/2008 7:00:00 AM -05:00 converts to 6/19/2008 7:00:00 AM Unspecified 
```

```vb
Const baseTime As Date = #06/19/2008 7:00AM#
Dim sourceTime As DateTimeOffset
Dim targetTime As Date

' Convert UTC to DateTime value
sourceTime = New DateTimeOffset(baseTime, TimeSpan.Zero)
targetTime = sourceTime.DateTime
Console.WriteLine("{0} converts to {1} {2}", _
                  sourceTime, _
                  targetTime, _
                  targetTime.Kind.ToString())

' Convert local time to DateTime value
sourceTime = New DateTimeOffset(baseTime, _
                                TimeZoneInfo.Local.GetUtcOffset(baseTime))
targetTime = sourceTime.DateTime
Console.WriteLine("{0} converts to {1} {2}", _
                  sourceTime, _
                  targetTime, _
                  targetTime.Kind.ToString())

' Convert Central Standard Time to a DateTime value
Try
   Dim offset As TimeSpan = TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time").GetUtcOffset(baseTime)
   sourceTime = New DateTimeOffset(baseTime, offset)
   targetTime = sourceTime.DateTime
Console.WriteLine("{0} converts to {1} {2}", _
                  sourceTime, _
                  targetTime, _
                  targetTime.Kind.ToString())
Catch e As TimeZoneNotFoundException
   Console.WriteLine("Unable to create DateTimeOffset based on U.S. Central Standard Time.")
End Try 
' This example displays the following output to the console:
'    6/19/2008 7:00:00 AM +00:00 converts to 6/19/2008 7:00:00 AM Unspecified
'    6/19/2008 7:00:00 AM -07:00 converts to 6/19/2008 7:00:00 AM Unspecified
'    6/19/2008 7:00:00 AM -05:00 converts to 6/19/2008 7:00:00 AM Unspecified 
```

Qualsiasi informazione sulla relazione tra il valore [DateTimeOffset](xref:System.DateTimeOffset) e UTC viene persa durante la conversione quando viene usata la proprietà [DateTime](xref:System.DateTime). Ciò influisce sui valori [DateTimeOffset](xref:System.DateTimeOffset) che corrispondono all'ora UTC o all'ora locale del sistema perché la struttura [DateTime](xref:System.DateTime) riflette solo questi due fusi orari nella proprietà [Kind](xref:System.DateTime.Kind).

Per mantenere il maggior numero possibile di informazioni sul fuso orario durante la conversione di [DateTimeOffset](xref:System.DateTimeOffset) in un valore [DateTime](xref:System.DateTime), è possibile usare le proprietà [DateTimeOffset.UtcDateTime](xref:System.DateTimeOffset.UtcDateTime) e [DateTimeOffset.LocalDateTime](xref:System.DateTimeOffset.LocalDateTime). 

## <a name="converting-a-utc-time"></a>Conversione di un'ora UTC

Per indicare che un valore [DateTime](xref:System.DateTime) convertito corrisponde all'ora UTC, è possibile recuperare il valore della proprietà [DateTimeOffset.UtcDateTime](xref:System.DateTimeOffset.UtcDateTime). Tale proprietà è diversa dalla proprietà [DateTimeOffset.DateTime](xref:System.DateTimeOffset.DateTime) per due motivi:

* Restituisce un valore [DateTime](xref:System.DateTime) la cui proprietà [Kind](xref:System.DateTime.Kind) è [DateTimeKind.Utc](xref:System.DateTimeKind.Utc).

* Se il valore della proprietà [DateTimeOffset.Offset](xref:System.DateTimeOffset.Offset) non è uguale a [TimeSpan.Zero](xref:System.TimeSpan.Zero), l'ora viene convertita in UTC.

> [!NOTE]
> Se l'applicazione richiede che i valori [DateTime](xref:System.DateTime) convertiti identifichino in modo non ambiguo un singolo momento, è necessario usare la proprietà [DateTimeOffset.UtcDateTime](xref:System.DateTimeOffset.UtcDateTime) per gestire tutte le conversioni da [DateTimeOffset](xref:System.DateTimeOffset) a [DateTime](xref:System.DateTime).

Nell'esempio di codice riportato di seguito viene usata la proprietà [UtcDateTime](xref:System.DateTimeOffset.UtcDateTime) per convertire un valore [DateTimeOffset](xref:System.DateTimeOffset) il cui offset equivale a [TimeSpan.Zero](xref:System.TimeSpan.Zero) in un valore [DateTime](xref:System.DateTime).

```csharp
DateTimeOffset utcTime1 = new DateTimeOffset(2008, 6, 19, 7, 0, 0, TimeSpan.Zero);
DateTime utcTime2 = utcTime1.UtcDateTime;
Console.WriteLine("{0} converted to {1} {2}", 
                  utcTime1, 
                  utcTime2, 
                  utcTime2.Kind.ToString());
// The example displays the following output to the console:
//   6/19/2008 7:00:00 AM +00:00 converted to 6/19/2008 7:00:00 AM Utc
```

```vb
Dim utcTime1 As New DateTimeOffset(#06/19/2008 7:00AM#, TimeSpan.Zero)
Dim utcTime2 As Date = utcTime1.UtcDateTime
Console.WriteLine("{0} converted to {1} {2}", _
                  utcTime1, _
                  utcTime2, _
                  utcTime2.Kind.ToString())
' The example displays the following output to the console:
'   6/19/2008 7:00:00 AM +00:00 converted to 6/19/2008 7:00:00 AM Utc
```

Nel codice seguente viene usata la proprietà UtcDateTime per eseguire una conversione del fuso orario e del tipo su un valore [DateTimeOffset](xref:System.DateTimeOffset).

```csharp
DateTimeOffset originalTime = new DateTimeOffset(2008, 6, 19, 7, 0, 0, new TimeSpan(5, 0, 0));
DateTime utcTime = originalTime.UtcDateTime;
Console.WriteLine("{0} converted to {1} {2}", 
                  originalTime, 
                  utcTime, 
                  utcTime.Kind.ToString());
// The example displays the following output to the console:
//       6/19/2008 7:00:00 AM +05:00 converted to 6/19/2008 2:00:00 AM Utc
```

```vb
Dim originalTime As New DateTimeOffset(#6/19/2008 7:00AM#, _
                                       New TimeSpan(5, 0, 0))
Dim utcTime As Date = originalTime.UtcDateTime
Console.WriteLine("{0} converted to {1} {2}", _ 
                  originalTime, _
                  utcTime, _
                  utcTime.Kind.ToString())
' The example displays the following output to the console:
'       6/19/2008 7:00:00 AM +05:00 converted to 6/19/2008 2:00:00 AM Utc
```

## <a name="converting-a-local-time"></a>Conversione dell'ora locale

Per indicare che un valore [DateTimeOffset](xref:System.DateTimeOffset) rappresenta l'ora locale, è possibile passare il valore [DateTime](xref:System.DateTime) restituito dalla proprietà [DateTimeOffset.DateTime](xref:System.DateTimeOffset.DateTime) al metodo statico [DateTime.SpecifyKind(DateTime, DateTimeKind)](xref:System.DateTime.SpecifyKind(System.DateTime,System.DateTimeKind)). Il metodo restituisce la data e l'ora passate come primo parametro, ma imposta la proprietà [Kind](xref:System.DateTime.Kind) sul valore specificato dal secondo parametro. Nel codice seguente viene usato il metodo [SpecifyKind(DateTime, DateTimeKind)](xref:System.DateTime.SpecifyKind(System.DateTime,System.DateTimeKind)) in caso di conversione di un valore [DateTimeOffset](xref:System.DateTimeOffset) il cui offset corrisponde a quello del fuso orario locale.

```csharp
DateTime sourceDate = new DateTime(2008, 6, 19, 7, 0, 0);
DateTimeOffset utcTime1 = new DateTimeOffset(sourceDate, 
                          TimeZoneInfo.Local.GetUtcOffset(sourceDate));
DateTime utcTime2 = utcTime1.DateTime;
if (utcTime1.Offset.Equals(TimeZoneInfo.Local.GetUtcOffset(utcTime1.DateTime))) 
   utcTime2 = DateTime.SpecifyKind(utcTime2, DateTimeKind.Local);

Console.WriteLine("{0} converted to {1} {2}", 
                  utcTime1, 
                  utcTime2, 
                  utcTime2.Kind.ToString());
// The example displays the following output to the console:
//   6/19/2008 7:00:00 AM -07:00 converted to 6/19/2008 7:00:00 AM Local
```

```vb
Dim sourceDate As Date = #06/19/2008 7:00AM#
Dim utcTime1 As New DateTimeOffset(sourceDate, _
                                   TimeZoneInfo.Local.GetUtcOffset(sourceDate))
Dim utcTime2 As Date = utcTime1.DateTime
If utcTime1.Offset.Equals(TimeZoneInfo.Local.GetUtcOffset(utcTime1.DateTime)) Then
   utcTime2 = DateTime.SpecifyKind(utcTime2, DateTimeKind.Local)
End If   
Console.WriteLine("{0} converted to {1} {2}", _
                  utcTime1, _
                  utcTime2, _
                  utcTime2.Kind.ToString())
' The example displays the following output to the console:
'   6/19/2008 7:00:00 AM -07:00 converted to 6/19/2008 7:00:00 AM Local
```

È anche possibile usare la proprietà [DateTimeOffset.LocalDateTime](xref:System.DateTimeOffset.LocalDateTime) per convertire un valore [DateTimeOffset](xref:System.DateTimeOffset) in un valore [DateTime](xref:System.DateTime) locale. La proprietà [Kind](xref:System.DateTime.Kind) del valore [DateTime](xref:System.DateTime) restituito è [DateTimeKind.Local](xref:System.DateTimeKind.Local). Nel codice seguente viene usata la proprietà [DateTimeOffset.LocalDateTime](xref:System.DateTimeOffset.LocalDateTime) in caso di conversione di un valore [DateTimeOffset](xref:System.DateTimeOffset) il cui offset corrisponde a quello del fuso orario locale.

```csharp
DateTime sourceDate = new DateTime(2008, 6, 19, 7, 0, 0);
DateTimeOffset localTime1 = new DateTimeOffset(sourceDate, 
                          TimeZoneInfo.Local.GetUtcOffset(sourceDate));
DateTime localTime2 = localTime1.LocalDateTime;

Console.WriteLine("{0} converted to {1} {2}", 
                  localTime1, 
                  localTime2, 
                  localTime2.Kind.ToString());
// The example displays the following output to the console:
//   6/19/2008 7:00:00 AM -07:00 converted to 6/19/2008 7:00:00 AM Local
```

```vb
Dim sourceDate As Date = #06/19/2008 7:00AM#
Dim localTime1 As New DateTimeOffset(sourceDate, _
                                   TimeZoneInfo.Local.GetUtcOffset(sourceDate))
Dim localTime2 As Date = localTime1.LocalDateTime
Console.WriteLine("{0} converted to {1} {2}", _
                  localTime1, _
                  localTime2, _
                  localTime2.Kind.ToString())
' The example displays the following output to the console:
'   6/19/2008 7:00:00 AM -07:00 converted to 6/19/2008 7:00:00 AM Local 
```

Quando si recupera un valore [DateTime](xref:System.DateTime) usando la proprietà [DateTimeOffset.LocalDateTime](xref:System.DateTimeOffset.LocalDateTime), la funzione di accesso della proprietà `get` converte dapprima il valore [DateTimeOffset](xref:System.DateTimeOffset) in UTC, quindi lo converte in ora locale chiamando il metodo [DateTimeOffset.ToLocalTime](xref:System.DateTimeOffset). È pertanto possibile recuperare un valore dalla proprietà [DateTimeOffset.LocalDateTime](xref:System.DateTimeOffset.LocalDateTime) per eseguire una conversione del fuso orario contemporaneamente all'esecuzione della conversione di un tipo. Nell'esecuzione della conversione vengono anche applicate le regole di rettifica del fuso orario. Nel codice seguente viene illustrato l'uso della proprietà [DateTimeOffset.LocalDateTime](xref:System.DateTimeOffset.LocalDateTime) per eseguire una conversione del fuso orario e del tipo.

```csharp
DateTimeOffset originalDate;
DateTime localDate;

// Convert time originating in a different time zone
originalDate = new DateTimeOffset(2008, 6, 18, 7, 0, 0, 
                                  new TimeSpan(-5, 0, 0));
localDate = originalDate.LocalDateTime;
Console.WriteLine("{0} converted to {1} {2}", 
                  originalDate, 
                  localDate, 
                  localDate.Kind.ToString());
// Convert time originating in a different time zone 
// so local time zone's adjustment rules are applied
originalDate = new DateTimeOffset(2007, 11, 4, 4, 0, 0, 
                                  new TimeSpan(-5, 0, 0));
localDate = originalDate.LocalDateTime;
Console.WriteLine("{0} converted to {1} {2}", 
                  originalDate, 
                  localDate, 
                  localDate.Kind.ToString());
// The example displays the following output to the console:
//       6/19/2008 7:00:00 AM -05:00 converted to 6/19/2008 5:00:00 AM Local
//       11/4/2007 4:00:00 AM -05:00 converted to 11/4/2007 1:00:00 AM Local
```

```vb
Dim originalDate As DateTimeOffset
Dim localDate As Date

' Convert time originating in a different time zone
originalDate = New DateTimeOffset(#06/19/2008 7:00AM#, _
                                  New TimeSpan(-5, 0, 0))
localDate = originalDate.LocalDateTime
Console.WriteLine("{0} converted to {1} {2}", _
                  originalDate, _
                  localDate, _
                  localDate.Kind.ToString())
' Convert time originating in a different time zone 
' so local time zone's adjustment rules are applied
originalDate = New DateTimeOffset(#11/04/2007 4:00AM#, _
                                  New TimeSpan(-5, 0, 0))
localDate = originalDate.LocalDateTime
Console.WriteLine("{0} converted to {1} {2}", _
                  originalDate, _
                  localDate, _
                  localDate.Kind.ToString())
' The example displays the following output to the console:
'       6/19/2008 7:00:00 AM -05:00 converted to 6/19/2008 5:00:00 AM Local
'       11/4/2007 4:00:00 AM -05:00 converted to 11/4/2007 1:00:00 AM Local
```

## <a name="a-generalpurpose-conversion-method"></a>Metodo di conversione generale

Nell'esempio riportato di seguito viene definito un metodo denominato `ConvertFromDateTimeOffset` che converte valori [DateTimeOffset](xref:System.DateTimeOffset) in valori [DateTime](xref:System.DateTime). In base all'offset, determina se il valore [DateTimeOffset](xref:System.DateTimeOffset) si riferisce a un'ora UTC, a un'ora locale o ad altro e definisce di conseguenza la proprietà [Kind](xref:System.DateTime.Kind)del valore di data e ora restituito. 

```csharp
static DateTime ConvertFromDateTimeOffset(DateTimeOffset dateTime)
{
   if (dateTime.Offset.Equals(TimeSpan.Zero))
      return dateTime.UtcDateTime;
   else if (dateTime.Offset.Equals(TimeZoneInfo.Local.GetUtcOffset(dateTime.DateTime)))
      return DateTime.SpecifyKind(dateTime.DateTime, DateTimeKind.Local);
   else
      return dateTime.DateTime;   
}
```

```vb
Function ConvertFromDateTimeOffset(dateTime As DateTimeOffset) As Date
   If dateTime.Offset.Equals(TimeSpan.Zero) Then
      Return dateTime.UtcDateTime
   ElseIf dateTime.Offset.Equals(TimeZoneInfo.Local.GetUtcOffset(dateTime.DateTime))
      Return Date.SpecifyKind(dateTime.DateTime, DateTimeKind.Local)
   Else
      Return dateTime.DateTime   
   End If
```

Nell'esempio seguente viene chiamato il metodo `ConvertFromDateTimeOffset` per convertire i valori [DateTimeOffset](xref:System.DateTimeOffset) che rappresentano un'ora UTC, un'ora locale e un'ora solare fuso centrale degli Stati Uniti.

```csharp
DateTime timeComponent = new DateTime(2008, 6, 19, 7, 0, 0);
DateTime returnedDate; 

// Convert UTC time
DateTimeOffset utcTime = new DateTimeOffset(timeComponent, TimeSpan.Zero);
returnedDate = ConvertFromDateTimeOffset(utcTime); 
Console.WriteLine("{0} converted to {1} {2}", 
                  utcTime, 
                  returnedDate, 
                  returnedDate.Kind.ToString());

// Convert local time
DateTimeOffset localTime = new DateTimeOffset(timeComponent, 
                           TimeZoneInfo.Local.GetUtcOffset(timeComponent)); 
returnedDate = ConvertFromDateTimeOffset(localTime);                                          
Console.WriteLine("{0} converted to {1} {2}", 
                  localTime, 
                  returnedDate, 
                  returnedDate.Kind.ToString());

// Convert Central Standard Time
DateTimeOffset cstTime = new DateTimeOffset(timeComponent, 
               TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time").GetUtcOffset(timeComponent));
returnedDate = ConvertFromDateTimeOffset(cstTime);
Console.WriteLine("{0} converted to {1} {2}", 
                  cstTime, 
                  returnedDate, 
                  returnedDate.Kind.ToString());
// The example displays the following output to the console:
//    6/19/2008 7:00:00 AM +00:00 converted to 6/19/2008 7:00:00 AM Utc
//    6/19/2008 7:00:00 AM -07:00 converted to 6/19/2008 7:00:00 AM Local
//    6/19/2008 7:00:00 AM -05:00 converted to 6/19/2008 7:00:00 AM Unspecified
```

```vb
Dim timeComponent As Date = #06/19/2008 7:00AM#
Dim returnedDate As Date 

' Convert UTC time
Dim utcTime As New DateTimeOffset(timeComponent, TimeSpan.Zero)
returnedDate = ConvertFromDateTimeOffset(utcTime) 
Console.WriteLine("{0} converted to {1} {2}", _
                  utcTime, _
                  returnedDate, _
                  returnedDate.Kind.ToString())

' Convert local time
Dim localTime As New DateTimeOffset(timeComponent, _
                                    TimeZoneInfo.Local.GetUtcOffset(timeComponent)) 
returnedDate = ConvertFromDateTimeOffset(localTime)                                                                  
Console.WriteLine("{0} converted to {1} {2}", _
                  localTime, _
                  returnedDate, _
                  returnedDate.Kind.ToString())

' Convert Central Standard Time
Dim cstTime As New DateTimeOffset(timeComponent, _
               TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time").GetUtcOffset(timeComponent))
returnedDate = ConvertFromDateTimeOffset(cstTime)                                                                  
Console.WriteLine("{0} converted to {1} {2}", _
                  cstTime, _
                  returnedDate, _
                  returnedDate.Kind.ToString())
' The example displays the following output to the console:
'    6/19/2008 7:00:00 AM +00:00 converted to 6/19/2008 7:00:00 AM Utc
'    6/19/2008 7:00:00 AM -07:00 converted to 6/19/2008 7:00:00 AM Local
'    6/19/2008 7:00:00 AM -05:00 converted to 6/19/2008 7:00:00 AM Unspecified
```

Questo codice si basa su due presupposti che, a seconda dell'applicazione e dell'origine dei valori di data e ora, potrebbero non essere sempre validi:

* Il presupposto che un valore di data e ora il cui offset è [TimeSpan.Zero](xref:System.TimeSpan.Zero) rappresenti il fuso orario UTC. Infatti UTC non rappresenta un'ora in un particolare fuso orario, ma l'ora in relazione alla quale vengono normalizzati i fusi orari di tutto il mondo. I fusi orari possono presentare anche un offset pari a [Zero](xref:System.TimeSpan.Zero).

* Il presupposto è che valori di data e ora il cui offset è uguale a quelli del fuso orario locale rappresentino il fuso orario locale. Poiché l'associazione dei valori di data e ora al fuso orario originale è annullata, potrebbe non essere questo il caso; la data e l'ora potrebbero essere state originate in un altro fuso orario con lo stesso offset.

## <a name="see-also"></a>Vedere anche

[Date, ore e fusi orari](index.md)







<!--HONumber=Nov16_HO1-->


