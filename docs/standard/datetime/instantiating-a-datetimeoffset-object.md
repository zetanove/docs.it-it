---
title: Creazione di un&quot;istanza di un oggetto DateTimeOffset
description: Creazione di un&quot;istanza di un oggetto DateTimeOffset
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 08/15/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 476fe67b-6be4-4435-88ab-ced37304f1d1
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: 330371397d0ec258597e4e4f109f3f1bb35df6b7

---

# <a name="instantiating-a-datetimeoffset-object"></a>Creazione di un'istanza di un oggetto DateTimeOffset

La struttura [System.DateTimeOffset](xref:System.DateTimeOffset) offre diverse opzioni per creare nuovi valori [DateTimeOffset](xref:System.DateTimeOffset). Molti corrispondono direttamente ai metodi disponibili per creare istanze dei nuovi valori [System.DateTime](xref:System.DateTime), con miglioramenti che consentono di specificare l'offset del valore di data e ora rispetto all'ora UTC. In particolare è possibile creare istanze di un valore [DateTimeOffset](xref:System.DateTimeOffset) nei modi seguenti:

* Chiamando il costruttore [DateTimeOffset](xref:System.DateTimeOffset).

* Convertendo in modo implicito un valore in un valore [DateTimeOffset](xref:System.DateTimeOffset).

* Analizzando la rappresentazione di stringa di una data e dell'ora.

## <a name="date-and-time-literals"></a>Valori letterali di data e ora

Per linguaggi che supportano questa opzione, uno dei modi più comuni per creare un'istanza di un valore [DateTime](xref:System.DateTime) consiste nello specificare la data e l'ora come valore letterale specificato hardcoded. Con il codice Visual Basic seguente viene, ad esempio, creato un oggetto [DateTime](xref:System.DateTime) il cui valore corrisponde al 1 gennaio 2008, alle 10:00.

```vb
Dim literalDate1 As Date = #05/01/2008 8:06:32 AM#
Console.WriteLine(literalDate1.ToString())
' Displays:
'              5/1/2008 8:06:32 AM
```

I valori [DateTimeOffset](xref:System.DateTimeOffset) possono essere inizializzati anche con valori letterali di data e ora, quando si usano linguaggi che supportano i valori letterali [DateTime](xref:System.DateTime). Il codice Visual Basic seguente, ad esempio, consente di creare un oggetto [DateTimeOffset](xref:System.DateTimeOffset).

```vb
Dim literalDate As DateTimeOffset = #05/01/2008 8:06:32 AM#
Console.WriteLine(literalDate.ToString())
' Displays:
'              5/1/2008 8:06:32 AM -07:00
```

Come mostrato nell'output della console, al valore [DateTimeOffset](xref:System.DateTimeOffset) così creato viene assegnato l'offset del fuso orario locale. Ciò significa che un valore [DateTimeOffset](xref:System.DateTimeOffset) assegnato usando un valore letterale del carattere non identifica un momento specifico se il codice viene eseguito su computer diversi.

## <a name="datetimeoffset-constructors"></a>Costruttori DateTimeOffset

Il tipo [System.DateTimeOffset](xref:System.DateTimeOffset) definisce cinque costruttori. Tre corrispondono direttamente a costruttori [DateTime](xref:System.DateTime), con un parametro aggiuntivo di tipo [System.TimeSpan](xref:System.TimeSpan) che definisce l'offset di data e ora rispetto all'ora UTC. Questi consentono di definire un valore [DateTimeOffset](xref:System.DateTimeOffset) in base al valore dei singoli componenti di data e ora. Nel codice seguente vengono, ad esempio, usati questi tre costruttori per creare istanze di oggetti [DateTimeOffset](xref:System.DateTimeOffset) con valori identici di 7/1/2008 00:05 +01:00.

```csharp
DateTimeOffset dateAndTime;

// Instantiate date and time using years, months, days, 
// hours, minutes, and seconds
dateAndTime = new DateTimeOffset(2008, 5, 1, 8, 6, 32, 
                                 new TimeSpan(1, 0, 0));
Console.WriteLine(dateAndTime);
// Instantiate date and time using years, months, days,
// hours, minutes, seconds, and milliseconds
dateAndTime = new DateTimeOffset(2008, 5, 1, 8, 6, 32, 545, 
                                 new TimeSpan(1, 0, 0));
Console.WriteLine("{0} {1}", dateAndTime.ToString("G"), 
                             dateAndTime.ToString("zzz"));

// Instantiate date and time using number of ticks
// 05/01/2008 8:06:32 AM is 633,452,259,920,000,000 ticks
dateAndTime = new DateTimeOffset(633452259920000000, new TimeSpan(1, 0, 0));  
Console.WriteLine(dateAndTime);
// The example displays the following output to the console:
//       5/1/2008 8:06:32 AM +01:00
//       5/1/2008 8:06:32 AM +01:00
//       5/1/2008 8:06:32 AM +01:00
```

```vb
Dim dateAndTime As DateTimeOffset

' Instantiate date and time using years, months, days, 
' hours, minutes, and seconds
dateAndTime = New DateTimeOffset(2008, 5, 1, 8, 6, 32, _
                                 New TimeSpan(1, 0, 0))
Console.WriteLine(dateAndTime)
' Instantiate date and time using years, months, days,
' hours, minutes, seconds, and milliseconds
dateAndTime = New DateTimeOffset(2008, 5, 1, 8, 6, 32, 545, _
                                 New TimeSpan(1, 0, 0))
Console.WriteLine("{0} {1}", dateAndTime.ToString("G"), _
                             dateAndTime.ToString("zzz"))

' Instantiate date and time using Persian calendar with years,
' months, days, hours, minutes, seconds, and milliseconds
dateAndTime = New DateTimeOffset(1387, 2, 12, 8, 6, 32, 545, New PersianCalendar, New TimeSpan(1, 0, 0))
' Note that the console output displays the date in the Gregorian
' calendar, not the Persian calendar. 
Console.WriteLine("{0} {1}", dateAndTime.ToString("G"), _
                             dateAndTime.ToString("zzz"))

' Instantiate date and time using number of ticks
' 05/01/2008 8:06:32 AM is 633,452,259,920,000,000 ticks
dateAndTime = New DateTimeOffset(633452259920000000, New TimeSpan(1, 0, 0))  
Console.WriteLine(dateAndTime)
' The example displays the following output to the console:
'       5/1/2008 8:06:32 AM +01:00
'       5/1/2008 8:06:32 AM +01:00
'       5/1/2008 8:06:32 AM +01:00
'       5/1/2008 8:06:32 AM +01:00
```

Si noti che, quando il valore dell'oggetto [DateTimeOffset](xref:System.DateTimeOffset) di cui si è creata un'istanza usando un oggetto [PersianCalendar](xref:System.Globalization.PersianCalendar) come uno degli argomenti per il relativo costruttore viene visualizzato sulla console, viene espresso come data del calendario gregoriano anziché persiano. 

Gli altri due costruttori creano un oggetto [DateTimeOffset](xref:System.DateTimeOffset) da un valore DateTime. Il primo ha un solo parametro, il valore [DateTime](xref:System.DateTime) da convertire in un valore [DateTimeOffset](xref:System.DateTimeOffset). L'offset del valore [DateTimeOffset](xref:System.DateTimeOffset) risultante dipende dalla proprietà [Kind](xref:System.DateTime.Kind) del solo parametro [DateTime](xref:System.DateTime) del costruttore. Se il valore è [DateTimeKind.Utc](xref:System.DateTimeKind.Utc), l'offset viene impostato su un valore uguale a [TimeSpan.Zero](xref:System.TimeSpan.Zero). In caso contrario, l'offset viene impostato su un valore uguale a quello del fuso orario locale. L'esempio seguente illustra l'uso di questo costruttore per creare istanze di oggetti [DateTimeOffset](xref:System.DateTimeOffset) che rappresentano l'ora UTC e il fuso orario locale:

```csharp
// Declare date; Kind property is DateTimeKind.Unspecified
DateTime sourceDate = new DateTime(2008, 5, 1, 8, 30, 0);
DateTimeOffset targetTime;

// Instantiate a DateTimeOffset value from a UTC time 
DateTime utcTime = DateTime.SpecifyKind(sourceDate, DateTimeKind.Utc);
targetTime = new DateTimeOffset(utcTime);
Console.WriteLine(targetTime);
// Displays 5/1/2008 8:30:00 AM +00:00
// Because the Kind property is DateTimeKind.Utc, 
// the offset is TimeSpan.Zero.

// Instantiate a DateTimeOffset value from a UTC time with a zero offset
targetTime = new DateTimeOffset(utcTime, TimeSpan.Zero);
Console.WriteLine(targetTime);
// Displays 5/1/2008 8:30:00 AM +00:00
// Because the Kind property is DateTimeKind.Utc, 
// the call to the constructor succeeds

// Instantiate a DateTimeOffset value from a UTC time with a negative offset
try
{
   targetTime = new DateTimeOffset(utcTime, new TimeSpan(-2, 0, 0));
   Console.WriteLine(targetTime);
}
catch (ArgumentException)
{
   Console.WriteLine("Attempt to create DateTimeOffset value from {0} failed.", 
                      targetTime);
}   
// Throws exception and displays the following to the console:
//   Attempt to create DateTimeOffset value from 5/1/2008 8:30:00 AM +00:00 failed.

// Instantiate a DateTimeOffset value from a local time
DateTime localTime = DateTime.SpecifyKind(sourceDate, DateTimeKind.Local);
targetTime = new DateTimeOffset(localTime);
Console.WriteLine(targetTime);
// Displays 5/1/2008 8:30:00 AM -07:00
// Because the Kind property is DateTimeKind.Local, 
// the offset is that of the local time zone.

// Instantiate a DateTimeOffset value from an unspecified time
targetTime = new DateTimeOffset(sourceDate);
Console.WriteLine(targetTime);
// Displays 5/1/2008 8:30:00 AM -07:00
// Because the Kind property is DateTimeKind.Unspecified, 
// the offset is that of the local time zone.
```

```vb
' Declare date; Kind property is DateTimeKind.Unspecified
Dim sourceDate As Date = #5/1/2008 8:30 AM#
Dim targetTime As DateTimeOffset

' Instantiate a DateTimeOffset value from a UTC time 
Dim utcTime As Date = Date.SpecifyKind(sourceDate, DateTimeKind.Utc)
targetTime = New DateTimeOffset(utcTime)
Console.WriteLine(targetTime)
' Displays 5/1/2008 8:30:00 AM +00:00
' Because the Kind property is DateTimeKind.Utc, 
' the offset is TimeSpan.Zero.


' Instantiate a DateTimeOffset value from a local time
Dim localTime As Date = Date.SpecifyKind(sourceDate, DateTimeKind.Local)
targetTime = New DateTimeOffset(localTime)
Console.WriteLine(targetTime)
' Displays 5/1/2008 8:30:00 AM -07:00
' Because the Kind property is DateTimeKind.Local, 
' the offset is that of the local time zone.

' Instantiate a DateTimeOffset value from an unspecified time
targetTime = New DateTimeOffset(sourceDate)
Console.WriteLine(targetTime)
' Displays 5/1/2008 8:30:00 AM -07:00
' Because the Kind property is DateTimeKind.Unspecified, 
' the offset is that of the local time zone.
```

> [!NOTE]
> La chiamata dell'overload del costruttore [DateTimeOffset](xref:System.DateTimeOffset) che ha un solo parametro [DateTime](xref:System.DateTime) equivale all'esecuzione di una conversione implicita di un valore [DateTime](xref:System.DateTime) in un valore [DateTimeOffset](xref:System.DateTimeOffset).

Il secondo costruttore che crea un oggetto [DateTimeOffset](xref:System.DateTimeOffset) da un valore [DateTime](xref:System.DateTime) ha due parametri: il valore [DateTime](xref:System.DateTime) da convertire e un valore [TimeSpan](xref:System.TimeSpan) che rappresenta l'offset di data e ora rispetto all'ora UTC. Tale valore dell'offset deve corrispondere alla proprietà [Kind](xref:System.DateTime.Kind) del primo parametro del costruttore oppure viene generata un'eccezione [System.ArgumentException](xref:System.ArgumentException). Se la proprietà [Kind](xref:System.DateTime.Kind) del primo parametro è [DateTimeKind.Utc](xref:System.DateTimeKind.Utc), il valore del secondo parametro deve essere [TimeSpan.Zero](xref:System.TimeSpan.Zero). Se la proprietà [Kind](xref:System.DateTime.Kind) del primo parametro è [DateTimeKind.Local](xref:System.DateTimeKind.Local), il valore del secondo parametro deve essere l'offset del fuso orario del sistema locale. Se la proprietà [Kind](xref:System.DateTime.Kind) del primo parametro è [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified), l'offset può essere qualsiasi valore valido. Il codice seguente illustra le chiamate a questo costruttore per convertire [DateTime](xref:System.DateTime) in valori [DateTimeOffset](xref:System.DateTimeOffset).

```csharp
DateTime sourceDate = new DateTime(2008, 5, 1, 8, 30, 0);
DateTimeOffset targetTime;

// Instantiate a DateTimeOffset value from a UTC time with a zero offset.
DateTime utcTime = DateTime.SpecifyKind(sourceDate, DateTimeKind.Utc);
targetTime = new DateTimeOffset(utcTime, TimeSpan.Zero);
Console.WriteLine(targetTime);
// Displays 5/1/2008 8:30:00 AM +00:00
// Because the Kind property is DateTimeKind.Utc,  
// the call to the constructor succeeds

// Instantiate a DateTimeOffset value from a UTC time with a non-zero offset.
try
{
   targetTime = new DateTimeOffset(utcTime, new TimeSpan(-2, 0, 0));
   Console.WriteLine(targetTime);
}
catch (ArgumentException)
{
   Console.WriteLine("Attempt to create DateTimeOffset value from {0} failed.", 
                      utcTime);
}   
// Throws exception and displays the following to the console:
//   Attempt to create DateTimeOffset value from 5/1/2008 8:30:00 AM failed.

// Instantiate a DateTimeOffset value from a local time with 
// the offset of the local time zone
DateTime localTime = DateTime.SpecifyKind(sourceDate, DateTimeKind.Local);
targetTime = new DateTimeOffset(localTime, 
                                TimeZoneInfo.Local.GetUtcOffset(localTime));
Console.WriteLine(targetTime);
// Displays 5/1/2008 8:30:00 AM -07:00
// Because the Kind property is DateTimeKind.Local and the offset matches
// that of the local time zone, the call to the constructor succeeds.

// Instantiate a DateTimeOffset value from a local time with a zero offset.
try
{
   targetTime = new DateTimeOffset(localTime, TimeSpan.Zero);
   Console.WriteLine(targetTime);
}
catch (ArgumentException)
{
   Console.WriteLine("Attempt to create DateTimeOffset value from {0} failed.", 
                      localTime);
}   
// Throws exception and displays the following to the console:
//   Attempt to create DateTimeOffset value from 5/1/2008 8:30:00 AM failed.

// Instantiate a DateTimeOffset value with an arbitary time zone. 
string timeZoneName = "Central Standard Time";
TimeSpan offset = TimeZoneInfo.FindSystemTimeZoneById(timeZoneName). 
                         GetUtcOffset(sourceDate); 
targetTime = new DateTimeOffset(sourceDate, offset);
Console.WriteLine(targetTime);
// Displays 5/1/2008 8:30:00 AM -05:00
```

```vb
Dim sourceDate As Date = #5/1/2008 8:30 AM#
Dim targetTime As DateTimeOffset

' Instantiate a DateTimeOffset value from a UTC time with a zero offset.
Dim utcTime As Date = Date.SpecifyKind(sourceDate, DateTimeKind.Utc)
targetTime = New DateTimeOffset(utcTime, TimeSpan.Zero)
Console.WriteLine(targetTime)
' Displays 5/1/2008 8:30:00 AM +00:00
' Because the Kind property is DateTimeKind.Utc,  
' the call to the constructor succeeds.

' Instantiate a DateTimeOffset value from a UTC time with a non-zero offset.
Try
   targetTime = New DateTimeOffset(utcTime, New TimeSpan(-2, 0, 0))
   Console.WriteLine(targetTime)
Catch e As ArgumentException
   Console.WriteLine("Attempt to create DateTimeOffset value from {0} failed.", _
                      utcTime)
End Try   
' Throws exception and displays the following to the console:
'   Attempt to create DateTimeOffset value from 5/1/2008 8:30:00 AM failed.

' Instantiate a DateTimeOffset value from a local time with 
' the offset of the local time zone.
Dim localTime As Date = Date.SpecifyKind(sourceDate, DateTimeKind.Local)
targetTime = New DateTimeOffset(localTime, _
                                TimeZoneInfo.Local.GetUtcOffset(localTime))
Console.WriteLine(targetTime)
' Because the Kind property is DateTimeKind.Local and the offset matches
' that of the local time zone, the call to the constructor succeeds.

' Instantiate a DateTimeOffset value from a local time with a zero offset.
Try
   targetTime = New DateTimeOffset(localTime, TimeSpan.Zero)
   Console.WriteLine(targetTime)
Catch e As ArgumentException
   Console.WriteLine("Attempt to create DateTimeOffset value from {0} failed.", _
                      localTime)
End Try   
' Throws exception and displays the following to the console:
'   Attempt to create DateTimeOffset value from 5/1/2008 8:30:00 AM failed.

' Instantiate a DateTimeOffset value with an arbitary time zone. 
Dim timeZoneName As String = "Central Standard Time"
Dim offset As TimeSpan = TimeZoneInfo.FindSystemTimeZoneById(timeZoneName). _
                         GetUtcOffset(sourceDate) 
targetTime = New DateTimeOffset(sourceDate, offset)
Console.WriteLine(targetTime)
' Displays 5/1/2008 8:30:00 AM -05:00
```

## <a name="implicit-type-conversion"></a>Conversione implicita di tipi
 
Il tipo [System.DateTimeOffset](xref:System.DateTimeOffset) supporta una conversione implicita di tipi: da un valore [System.DateTime](xref:System.DateTime) in un valore [DateTimeOffset](xref:System.DateTimeOffset). Una conversione implicita di tipi è una conversione da un tipo in un altro che non richiede un cast esplicito (in C#) o una conversione esplicita (in Visual Basic) e nella quale non vengono perse informazioni. Rende possibile la scrittura di codice come il seguente.

```csharp
DateTimeOffset targetTime;

// The Kind property of sourceDate is DateTimeKind.Unspecified
DateTime sourceDate = new DateTime(2008, 5, 1, 8, 30, 0);
targetTime = sourceDate;
Console.WriteLine(targetTime);   
// Displays 5/1/2008 8:30:00 AM -07:00

// define a UTC time (Kind property is DateTimeKind.Utc)
DateTime utcTime = DateTime.SpecifyKind(sourceDate, DateTimeKind.Utc);
targetTime = utcTime;
Console.WriteLine(targetTime);   
// Displays 5/1/2008 8:30:00 AM +00:00

// Define a local time (Kind property is DateTimeKind.Local)
DateTime localTime = DateTime.SpecifyKind(sourceDate, DateTimeKind.Local);
targetTime = localTime;
Console.WriteLine(targetTime);      
// Displays 5/1/2008 8:30:00 AM -07:00
```

```vb
Dim targetTime As DateTimeOffset

' The Kind property of sourceDate is DateTimeKind.Unspecified
Dim sourceDate As Date = #5/1/2008 8:30 AM#
targetTime = sourceDate
Console.WriteLine(targetTime)   
' Displays 5/1/2008 8:30:00 AM -07:00

' define a UTC time (Kind property is DateTimeKind.Utc)
Dim utcTime As Date = Date.SpecifyKind(sourceDate, DateTimeKind.Utc)
targetTime = utcTime
Console.WriteLine(targetTime)   
' Displays 5/1/2008 8:30:00 AM +00:00

' Define a local time (Kind property is DateTimeKind.Local)
Dim localTime As Date = Date.SpecifyKind(sourceDate, DateTimeKind.Local)
targetTime = localTime
Console.WriteLine(targetTime)      
' Displays 5/1/2008 8:30:00 AM -07:00
```

L'offset del valore [DateTimeOffset](xref:System.DateTimeOffset) risultante dipende dal valore della proprietà DateTime.Kind](xref:System.DateTime.Kind). Se il valore è [DateTimeKind.Utc](xref:System.DateTimeKind.Utc), l'offset viene impostato su un valore uguale a [TimeSpan.Zero](xref:System.TimeSpan.Zero). Se il valore è [DateTimeKind.Local](xref:System.DateTimeKind.Local) o [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified), l'offset viene impostato su un valore uguale a quello del fuso orario locale.

## <a name="parsing-the-string-representation-of-a-date-and-time"></a>Analisi della rappresentazione di stringa di data e ora

Il tipo [System.DateTimeOffset](xref:System.DateTimeOffset) supporta quattro metodi che consentono di convertire la rappresentazione di stringa di data e ora in un valore [DateTimeOffset](xref:System.DateTimeOffset):

* [Parse](xref:System.DateTimeOffset.Parse(System.String)), che tenta di convertire la rappresentazione di stringa di una data e dell'ora in un valore [DateTimeOffset](xref:System.DateTimeOffset) e genera un'eccezione se la conversione non riesce.

* [TryParse](xref:System.DateTimeOffset.TryParse(System.String,System.DateTimeOffset@)), che tenta di convertire la rappresentazione di stringa di una data e dell'ora in un valore [DateTimeOffset](xref:System.DateTimeOffset) e restituisce `false` se la conversione non riesce.

* [ParseExact](xref:System.DateTimeOffset.ParseExact(System.String,System.String,System.IFormatProvider)), che tenta di convertire la rappresentazione di stringa di una data e dell'ora in un formato specifico in un valore [DateTimeOffset](xref:System.DateTimeOffset). Il metodo genera un'eccezione se la conversione non riesce.

* [TryParseExact](xref:System.DateTimeOffset.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles,System.DateTimeOffset@)), che tenta di convertire la rappresentazione di stringa di una data e dell'ora in un formato specifico in un valore [DateTimeOffset](xref:System.DateTimeOffset). Il metodo restituisce `false` se la conversione non riesce.

L'esempio seguente illustra le chiamate a ognuno di questi quattro metodi di conversione di stringhe per la creazione di un'istanza di un valore [DateTimeOffset](xref:System.DateTimeOffset).

```csharp
string timeString; 
DateTimeOffset targetTime;

timeString = "05/01/2008 8:30 AM +01:00";
try
{
   targetTime = DateTimeOffset.Parse(timeString);
   Console.WriteLine(targetTime);
}
catch (FormatException)
{
   Console.WriteLine("Unable to parse {0}.", timeString);   
}   

timeString = "05/01/2008 8:30 AM";
if (DateTimeOffset.TryParse(timeString, out targetTime))
   Console.WriteLine(targetTime);
else
   Console.WriteLine("Unable to parse {0}.", timeString);   

timeString = "Thursday, 01 May 2008 08:30";
try
{
   targetTime = DateTimeOffset.ParseExact(timeString, "f", 
                CultureInfo.InvariantCulture);
   Console.WriteLine(targetTime);
}
catch (FormatException)
{
   Console.WriteLine("Unable to parse {0}.", timeString);   
}   

timeString = "Thursday, 01 May 2008 08:30 +02:00";
string formatString; 
formatString = CultureInfo.InvariantCulture.DateTimeFormat.LongDatePattern +
                " " +
                CultureInfo.InvariantCulture.DateTimeFormat.ShortTimePattern +
                " zzz"; 
if (DateTimeOffset.TryParseExact(timeString, 
                                formatString, 
                                CultureInfo.InvariantCulture, 
                                DateTimeStyles.AllowLeadingWhite, 
                                out targetTime))
   Console.WriteLine(targetTime);
else
   Console.WriteLine("Unable to parse {0}.", timeString);
// The example displays the following output to the console:
//    5/1/2008 8:30:00 AM +01:00
//    5/1/2008 8:30:00 AM -07:00
//    5/1/2008 8:30:00 AM -07:00
//    5/1/2008 8:30:00 AM +02:00
```

```vb
Dim timeString As String 
Dim targetTime As DateTimeOffset

timeString = "05/01/2008 8:30 AM +01:00"
Try
   targetTime = DateTimeOffset.Parse(timeString)
   Console.WriteLine(targetTime)
Catch e As FormatException
   Console.WriteLine("Unable to parse {0}.", timeString)   
End Try   

timeString = "05/01/2008 8:30 AM"
If DateTimeOffset.TryParse(timeString, targetTime) Then
   Console.WriteLine(targetTime)
Else
   Console.WriteLine("Unable to parse {0}.", timeString)   
End If

timeString = "Thursday, 01 May 2008 08:30"
Try
   targetTime = DateTimeOffset.ParseExact(timeString, "f", _
                CultureInfo.InvariantCulture)
   Console.WriteLine(targetTime)
Catch e As FormatException
   Console.WriteLine("Unable to parse {0}.", timeString)   
End Try   

timeString = "Thursday, 01 May 2008 08:30 +02:00"
Dim formatString As String 
formatString = CultureInfo.InvariantCulture.DateTimeFormat.LongDatePattern & _
                " " & _
                CultureInfo.InvariantCulture.DateTimeFormat.ShortTimePattern & _
                " zzz" 
If DateTimeOffset.TryParseExact(timeString, _
                                formatString, _
                                CultureInfo.InvariantCulture, _
                                DateTimeStyles.AllowLeadingWhite, _
                                targetTime) Then
   Console.WriteLine(targetTime)
Else
   Console.WriteLine("Unable to parse {0}.", timeString)
End If      
' The example displays the following output to the console:
'    5/1/2008 8:30:00 AM +01:00
'    5/1/2008 8:30:00 AM -07:00
'    5/1/2008 8:30:00 AM -07:00
'    5/1/2008 8:30:00 AM +02:00
```

## <a name="see-also"></a>Vedere anche

[Date, ore e fusi orari](index.md)




<!--HONumber=Nov16_HO1-->


