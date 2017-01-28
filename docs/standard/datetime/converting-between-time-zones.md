---
title: Conversione degli orari tra fusi orari
description: Conversione degli orari tra fusi orari
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 08/15/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: bf8f74e6-e7f2-4c2a-a04c-57db0e28dd36
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: c2baa48c3b79dfbc5d39652cc57fe015a2313d6e

---

# <a name="converting-times-between-time-zones"></a>Conversione degli orari tra fusi orari

La gestione delle differenze tra fusi orari sta divenendo sempre più importante per le applicazioni che usano date e ore. Non è più possibile presupporre che tutti gli orari possano essere espressi su base locale, ovvero in base all'orario disponibile dalla struttura [System.DateTime](xref:System.DateTime). Ad esempio, una pagina Web che visualizza l'orario corrente della parte orientale degli Stati Uniti risulterà non attendibile per un cliente dell'Asia orientale. In questo argomento viene illustrato come convertire gli orari da un fuso orario all'altro, nonché come convertire i valori [System.DateTimeOffset](xref:System.DateTimeOffset) che dipendono in parte dal fuso orario.

## <a name="converting-to-coordinated-universal-time"></a>Conversione nel formato UTC

UTC (Coordinated Universal Time) è uno standard di alta precisione basato sul tempo atomico. I fusi orari del mondo sono espressi come offset positivi o negativi dall'ora UTC. L'ora espressa in UTC è quindi indipendente dal fuso orario. L'uso dell'ora UTC è consigliato quando la portabilità di data e ora tra i computer è importante. La conversione di singoli fusi orari in ore UTC semplifica i confronti tra gli orari.

> [!NOTE]
> È anche possibile serializzare una struttura [DateTimeOffset](xref:System.DateTimeOffset) per rappresentare in modo non ambiguo un momento preciso. Poiché gli oggetti [DateTimeOffset](xref:System.DateTimeOffset) archiviano un valore di data e ora insieme all'offset dall'ora UTC, rappresentano sempre un momento preciso in relazione all'ora UTC.

Il modo più semplice per convertire un orario in ora UTC è chiamare il metodo `static` (`Shared` in Visual Basic) [TimeZoneInfo.ConvertTimeToUtc(DateTime)](https://msdn.microsoft.com/en-us/library/bb381744(v=vs.110).aspx). 

> [!IMPORTANT]
> Il metodo `TimeZoneInfo.ConvertTimeToUtc(DateTime)` non è attualmente disponibile in .NET Core. 

Il tipo specifico di conversione eseguita dal metodo dipende dal valore della proprietà [Kind](xref:System.DateTime.Kind) del parametro `DateTime`, come illustrato nella tabella seguente.

Proprietà [DateTime.Kind](xref:System.DateTimeKind) | Conversione
---------------------------------------------------------------------------------------------- | ----------
[DateTimeKind.Local](xref:System.DateTimeKind.Local) | Converte l'ora locale in ora UTC.
[DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified) | Presuppone che il parametro `DateTime` sia l'ora locale e converte l'ora locale in ora UTC.
[DateTimeKind.Utc](xref:System.DateTimeKind.Utc) | Restituisce il parametro `DateTime` invariato.

Il codice seguente converte l'ora locale corrente in ora UTC e visualizza il risultato nella console.

```csharp
DateTime dateNow = DateTime.Now;
Console.WriteLine("The date and time are {0} UTC.", 
                   TimeZoneInfo.ConvertTimeToUtc(dateNow));
```

```vb
Dim dateNow As Date = Date.Now      
Console.WriteLine("The date and time are {0} UTC.", _
                  TimeZoneInfo.ConvertTimeToUtc(dateNow))
```

> [!NOTE]
>Il metodo [TimeZoneInfo.ConvertTimeToUtc(DateTime)](https://msdn.microsoft.com/en-us/library/bb381744(v=vs.110).aspx) non comporta necessariamente risultati identici a quelli forniti dai metodi [TimeZone.ToUniversalTime](https://msdn.microsoft.com/en-us/library/System.TimeZone.ToUniversalTime(v=vs.110).aspx) e [DateTime.ToUniversalTime](xref:System.DateTime.ToUniversalTime). Se il fuso orario locale del sistema host prevede più regole di modifica, il metodo, [TimeZoneInfo.ConvertTimeToUtc(DateTime)](https://msdn.microsoft.com/en-us/library/System.TimeZone.ConvertTimeToUtc(v=vs.110).aspx) applica la regola appropriata a una data e a un'ora specifiche. Gli altri due metodi vengono sempre applicati alla regola di modifica più recente.

Se il valore di data e ora non rappresenta l'ora locale o l'ora UTC, il metodo [ToUniversalTime](https://msdn.microsoft.com/en-us/library/System.TimeZone.ToUniversalTime(v=vs.110).aspx) restituirà probabilmente un risultato errato. È tuttavia possibile usare il metodo [TimeZoneInfo.ConvertTimeToUtc](https://msdn.microsoft.com/en-us/library/bb381744(v=vs.110).aspx) per convertire la data e l'ora da un fuso orario specifico. Per informazioni dettagliate sul recupero di un oggetto TimeZoneInfo che rappresenta il fuso orario di destinazione, vedere [Ricerca dei fusi orari definiti in un sistema locale](finding-the-time-zones-on-local-system.md). Nel codice seguente viene usato il metodo [TimeZoneInfo.ConvertTimeToUtc](https://msdn.microsoft.com/en-us/library/bb381744(v=vs.110).aspx) per convertire l'ora solare fuso orientale in ora UTC.

```csharp
DateTime easternTime = new DateTime(2007, 01, 02, 12, 16, 00);
string easternZoneId = "Eastern Standard Time";
try
{
   TimeZoneInfo easternZone = TimeZoneInfo.FindSystemTimeZoneById(easternZoneId);
   Console.WriteLine("The date and time are {0} UTC.", 
                     TimeZoneInfo.ConvertTimeToUtc(easternTime, easternZone));
}
catch (TimeZoneNotFoundException)
{
   Console.WriteLine("Unable to find the {0} zone in the registry.", 
                     easternZoneId);
}                           
catch (InvalidTimeZoneException)
{
   Console.WriteLine("Registry data on the {0} zone has been corrupted.", 
                     easternZoneId);
}
```

```vb
Dim easternTime As New Date(2007, 01, 02, 12, 16, 00)
Dim easternZoneId As String = "Eastern Standard Time"
Try
   Dim easternZone As TimeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById(easternZoneId)
   Console.WriteLine("The date and time are {0} UTC.", _ 
                     TimeZoneInfo.ConvertTimeToUtc(easternTime, easternZone))
Catch e As TimeZoneNotFoundException
   Console.WriteLine("Unable to find the {0} zone in the registry.", _
                     easternZoneId)
Catch e As InvalidTimeZoneException
   Console.WriteLine("Registry data on the {0} zone has been corrupted.", _ 
                     easternZoneId)
End Try    
```

Si noti che questo metodo genera un'eccezione [ArgumentException](xref:System.ArgumentException) se la proprietà [Kind](xref:System.DateTimeKind) dell'oggetto [DateTime](xref:System.DateTime) e il fuso orario non corrispondono. Una mancata corrispondenza viene rilevata se la proprietà Kind è [DateTimeKind.Local](xref:System.DateTimeKind.Local) ma l'oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) non rappresenta il fuso orario locale oppure se la proprietà Kind è [DateTimeKind.Utc](xref:System.DateTimeKind.Utc) ma l'oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) non è uguale a [DateTimeKind.Utc](xref:System.DateTimeKind.Utc).

Tutti questi metodi accettano valori [DateTime](xref:System.DateTime) come parametri e restituiscono un valore [DateTime](xref:System.DateTime). Per i valori [DateTimeOffset](xref:System.DateTimeOffset) la struttura [DateTimeOffset](xref:System.DateTimeOffset) presenta un metodo di istanza [ToUniversalTime](xref:System.DateTimeOffset.ToUniversalTime) che converte la data e ora dell'istanza corrente in ora UTC. Nell'esempio seguente viene chiamato il metodo [ToUniversalTime](xref:System.DateTimeOffset.ToUniversalTime) per convertire l'ora locale e diversi altri orari nell'ora UTC (Coordinated Universal Time).

```csharp
DateTimeOffset localTime, otherTime, universalTime;

// Define local time in local time zone
localTime = new DateTimeOffset(new DateTime(2007, 6, 15, 12, 0, 0));
Console.WriteLine("Local time: {0}", localTime);
Console.WriteLine();

// Convert local time to offset 0 and assign to otherTime
otherTime = localTime.ToOffset(TimeSpan.Zero);
Console.WriteLine("Other time: {0}", otherTime);
Console.WriteLine("{0} = {1}: {2}", 
                  localTime, otherTime, 
                  localTime.Equals(otherTime));
Console.WriteLine("{0} exactly equals {1}: {2}", 
                  localTime, otherTime, 
                  localTime.EqualsExact(otherTime));
Console.WriteLine();

// Convert other time to UTC
universalTime = localTime.ToUniversalTime(); 
Console.WriteLine("Universal time: {0}", universalTime);
Console.WriteLine("{0} = {1}: {2}", 
                  otherTime, universalTime, 
                  universalTime.Equals(otherTime));
Console.WriteLine("{0} exactly equals {1}: {2}", 
                  otherTime, universalTime, 
                  universalTime.EqualsExact(otherTime));
Console.WriteLine();
// The example produces the following output to the console:
//    Local time: 6/15/2007 12:00:00 PM -07:00
//    
//    Other time: 6/15/2007 7:00:00 PM +00:00
//    6/15/2007 12:00:00 PM -07:00 = 6/15/2007 7:00:00 PM +00:00: True
//    6/15/2007 12:00:00 PM -07:00 exactly equals 6/15/2007 7:00:00 PM +00:00: False
//    
//    Universal time: 6/15/2007 7:00:00 PM +00:00
//    6/15/2007 7:00:00 PM +00:00 = 6/15/2007 7:00:00 PM +00:00: True
//    6/15/2007 7:00:00 PM +00:00 exactly equals 6/15/2007 7:00:00 PM +00:00: True 
```

```vb
Dim localTime, otherTime, universalTime As DateTimeOffset

' Define local time in local time zone
localTime = New DateTimeOffset(#6/15/2007 12:00:00PM#)
Console.WriteLine("Local time: {0}", localTime)
Console.WriteLine()

' Convert local time to offset 0 and assign to otherTime
otherTime = localTime.ToOffset(TimeSpan.Zero)
Console.WriteLine("Other time: {0}", otherTime)
Console.WriteLine("{0} = {1}: {2}", _
                  localTime, otherTime, _
                  localTime.Equals(otherTime))
Console.WriteLine("{0} exactly equals {1}: {2}", _ 
                  localTime, otherTime, _
                  localTime.EqualsExact(otherTime))
Console.WriteLine()

' Convert other time to UTC
universalTime = localTime.ToUniversalTime() 
Console.WriteLine("Universal time: {0}", universalTime)
Console.WriteLine("{0} = {1}: {2}", _
                  otherTime, universalTime, _ 
                  universalTime.Equals(otherTime))
Console.WriteLine("{0} exactly equals {1}: {2}", _ 
                  otherTime, universalTime, _
                  universalTime.EqualsExact(otherTime))
Console.WriteLine()
' The example produces the following output to the console:
'    Local time: 6/15/2007 12:00:00 PM -07:00
'    
'    Other time: 6/15/2007 7:00:00 PM +00:00
'    6/15/2007 12:00:00 PM -07:00 = 6/15/2007 7:00:00 PM +00:00: True
'    6/15/2007 12:00:00 PM -07:00 exactly equals 6/15/2007 7:00:00 PM +00:00: False
'    
'    Universal time: 6/15/2007 7:00:00 PM +00:00
'    6/15/2007 7:00:00 PM +00:00 = 6/15/2007 7:00:00 PM +00:00: True
'    6/15/2007 7:00:00 PM +00:00 exactly equals 6/15/2007 7:00:00 PM +00:00: True 
```

## <a name="converting-utc-to-a-designated-time-zone"></a>Conversione dell'ora UTC in un determinato fuso orario

Per convertire l'ora UTC nell'ora locale, vedere la sezione seguente [Conversione dell'ora UTC nell'ora locale](#converting-utc-to-local-time). 

Per convertire l'ora UTC nell'ora di un determinato fuso orario, chiamare il metodo [ConvertTimeFromUtc](https://msdn.microsoft.com/en-us/library/System.TimeZoneInfo.converttimefromutc(v=vs.110).aspx). 

> [!IMPORTANT]
> Il metodo 'TimeZoneInfo.ConvertTimeFromUtc' non è attualmente disponibile in .NET Core. 

Questo metodo accetta due parametri:

* L'ora UTC da convertire. Deve essere un valore [DateTime](xref:System.DateTime) la cui proprietà [Kind](xref:System.DateTime.Kind) è impostata su [DateTimeKind](xref:System.DateTimeKind.Utc) o [DateTimeKind](xref:System.DateTimeKind.Unspecified). 

* Il fuso orario nel quale convertire l'ora UTC. 

Nel codice seguente l'ora UTC viene convertita nell'ora solare fuso centrale.

```csharp
DateTime timeUtc = DateTime.UtcNow;
try
{
   TimeZoneInfo cstZone = TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time");
   DateTime cstTime = TimeZoneInfo.ConvertTimeFromUtc(timeUtc, cstZone);
   Console.WriteLine("The date and time are {0} {1}.", 
                     cstTime, 
                     cstZone.IsDaylightSavingTime(cstTime) ?
                             cstZone.DaylightName : cstZone.StandardName);
}
catch (TimeZoneNotFoundException)
{
   Console.WriteLine("The registry does not define the Central Standard Time zone.");
}                           
catch (InvalidTimeZoneException)
{
   Console.WriteLine("Registry data on the Central Standard Time zone has been corrupted.");
}
```

```vb
Dim timeUtc As Date = Date.UtcNow
Try
   Dim cstZone As TimeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time")
   Dim cstTime As Date = TimeZoneInfo.ConvertTimeFromUtc(timeUtc, cstZone)
   Console.WriteLine("The date and time are {0} {1}.", _
                     cstTime, _
                     IIf(cstZone.IsDaylightSavingTime(cstTime), _
                         cstZone.DaylightName, cstZone.StandardName))
Catch e As TimeZoneNotFoundException
   Console.WriteLine("The registry does not define the Central Standard Time zone.")
Catch e As InvalidTimeZoneException
   Console.WriteLine("Registry data on the Central Standard Time zone has been corrupted.")
End Try
``` 

## <a name="converting-utc-to-local-time"></a>Conversione dell'ora UTC nell'ora locale

Per convertire l'ora UTC nell'ora locale, chiamare il metodo [DateTime.ToLocalTime](xref:System.DateTime) dell'oggetto [DateTime](xref:System.DateTime) di cui si vuole convertire l'orario. Il comportamento del metodo dipende dal valore della proprietà [Kind](xref:System.DateTime.Kind) dell'oggetto, come illustrato nella tabella seguente.

Proprietà [DateTime.Kind](xref:System.DateTimeKind) | Conversione
---------------------------------------------------------------------------------------------- | ----------
[DateTimeKind.Local](xref:System.DateTimeKind.Local) | Restituisce il valore [DateTime](xref:System.DateTime) invariato.
[DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified) | Presuppone che il valore [DateTime](xref:System.DateTime) sia UTC e converte l'ora UTC nell'ora locale.
[DateTimeKind.Utc](xref:System.DateTimeKind.Utc) | Converte il valore [DateTime](xref:System.DateTime) nell'ora locale.

## <a name="converting-between-any-two-time-zones"></a>Conversione tra due fusi orari

È possibile eseguire una conversione tra due fusi orari usando il metodo statico [TimeZoneInfo.ConvertTime](xref:System.TimeZoneInfo.ConvertTime(System.DateTime,System.TimeZoneInfo)). I parametri di questo metodo sono il valore [DateTime](xref:System.DateTime) da convertire, un oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) che rappresenta il fuso orario del valore di data e ora e un oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) che rappresenta il fuso orario in cui convertire il valore di data e ora.

Questo metodo richiede che la proprietà [Kind](xref:System.DateTime.Kind) del valore di data e ora da convertire e l'oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) o l'identificatore del fuso orario che rappresenta il relativo fuso orario corrispondano tra loro. In caso contrario, viene generata un'eccezione [ArgumentException](xref:System.ArgumentException). Se, ad esempio, la proprietà [Kind](xref:System.DateTime.Kind)del valore di data e ora è [DateTimeKind.Local](xref:System.DateTimeKind.Local), viene generata un'eccezione se l'oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) passato come parametro al metodo non è uguale a [TimeZoneInfo.Local](xref:System.TimeZoneInfo.Local). Un'eccezione viene generata anche se l'identificatore passato come parametro al metodo non è uguale a [TimeZoneInfo.Id](xref:System.TimeZoneInfo.Id).

Nell'esempio seguente viene usato il metodo [ConvertTime](xref:System.TimeZoneInfo.ConvertTime(System.DateTime,System.TimeZoneInfo)) per eseguire la conversione dall'ora solare Hawaii all'ora locale.

```csharp
DateTime hwTime = new DateTime(2007, 02, 01, 08, 00, 00);
try
{
   TimeZoneInfo hwZone = TimeZoneInfo.FindSystemTimeZoneById("Hawaiian Standard Time");
   Console.WriteLine("{0} {1} is {2} local time.", 
           hwTime, 
           hwZone.IsDaylightSavingTime(hwTime) ? hwZone.DaylightName : hwZone.StandardName, 
           TimeZoneInfo.ConvertTime(hwTime, hwZone, TimeZoneInfo.Local));
}
catch (TimeZoneNotFoundException)
{
   Console.WriteLine("The registry does not define the Hawaiian Standard Time zone.");
}                           
catch (InvalidTimeZoneException)
{
   Console.WriteLine("Registry data on the Hawaiian STandard Time zone has been corrupted.");
}
```

```vb
Dim hwTime As Date = #2/01/2007 8:00:00 AM#
Try
   Dim hwZone As TimeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById("Hawaiian Standard Time")
   Console.WriteLine("{0} {1} is {2} local time.", _
                     hwTime, _
                     IIf(hwZone.IsDaylightSavingTime(hwTime), hwZone.DaylightName, hwZone.StandardName), _
                     TimeZoneInfo.ConvertTime(hwTime, hwZone, TimeZoneInfo.Local))
Catch e As TimeZoneNotFoundException
   Console.WriteLine("The registry does not define the Hawaiian Standard Time zone.")
Catch e As InvalidTimeZoneException
   Console.WriteLine("Registry data on the Hawaiian Standard Time zone has been corrupted.")
End Try
```

## <a name="converting-datetimeoffset-values"></a>Conversione dei valori DateTimeOffset

I valori di data e ora rappresentati dagli oggetti [System.DateTimeOffset](xref:System.DateTimeOffset) non dipendono completamente dal fuso orario poiché è stata annullata l'associazione dell'oggetto al relativo fuso orario al momento della creazione dell'istanza di tale oggetto. In molti casi è tuttavia necessario convertire semplicemente una data e un'ora in base a due offset dall'ora UTC diversi anziché in base all'ora di determinati fusi orari. Per eseguire questa conversione, è possibile chiamare il metodo [ToOffset](xref:System.DateTimeOffset.ToOffset(System.TimeSpan)) dell'istanza corrente. L'unico parametro del metodo è [TimeSpan](xref:System.TimeSpan), che rappresenta l'offset del nuovo valore di data e ora restituito dal metodo.  

Se, ad esempio, la data e l'ora della richiesta di una pagina Web da parte di un utente sono note e serializzate sotto forma di stringa nel formato MM/gg/aaaa hh:mm:ss zzzz, il metodo `ReturnTimeOnServer` seguente converte questo valore di data e ora nella data e nell'ora del server Web.

```csharp
public DateTimeOffset ReturnTimeOnServer(string clientString)
{
   string format = @"M/d/yyyy H:m:s zzz";
   TimeSpan serverOffset = TimeZoneInfo.Local.GetUtcOffset(DateTimeOffset.Now);

   try
   {      
      DateTimeOffset clientTime = DateTimeOffset.ParseExact(clientString, format, CultureInfo.InvariantCulture);
      DateTimeOffset serverTime = clientTime.ToOffset(serverOffset);
      return serverTime;
   }
   catch (FormatException)
   {
      return DateTimeOffset.MinValue;
   }
}
```

```vb
Public Function ReturnTimeOnServer(clientString As String) As DateTimeOffset
   Dim format As String = "M/d/yyyy H:m:s zzz"
   Dim serverOffset As TimeSpan = TimeZoneInfo.Local.GetUtcOffset(DateTimeOffset.Now)

   Try      
      Dim clientTime As DateTimeOffset = DateTimeOffset.ParseExact(clientString, format, CultureInfo.InvariantCulture)
      Dim serverTime As DateTimeOffset = clientTime.ToOffset(serverOffset)
      Return serverTime
   Catch e As FormatException
      Return DateTimeOffset.MinValue
   End Try    
End Function
```

Se al metodo viene passata la stringa "9/1/2007 5:32:07 -05:00" che rappresenta la data e l'ora in un fuso orario indietro di cinque ore rispetto all'ora UTC, viene restituito 9/1/2007 3:32:07 AM -07:00 per un server situato nel fuso orario Ora solare del Pacifico (Stati Uniti).

La classe [TimeZoneInfo](xref:System.TimeZoneInfo) include anche un overload del metodo [TimeZoneInfo.ConvertTime(DateTimeOffset, TimeZoneInfo)](xref:System.TimeZoneInfo.ConvertTime(System.DateTimeOffset,System.TimeZoneInfo)) che esegue le conversioni del fuso orario con i valori [System.DateTimeOffset](xref:System.DateTimeOffset). I parametri del metodo sono un valore [System.DateTimeOffset](xref:System.DateTimeOffset) e un riferimento al fuso orario in cui convertire l'ora. La chiamata al metodo restituisce un valore [System.DateTimeOffset](xref:System.DateTimeOffset). Ad esempio, il metodo `ReturnTimeOnServer` dell'esempio precedente potrebbe essere riscritto come segue per chiamare il metodo [ConvertTime(DateTimeOffset, TimeZoneInfo)](xref:System.TimeZoneInfo.ConvertTime(System.DateTimeOffset,System.TimeZoneInfo)).

```csharp
public DateTimeOffset ReturnTimeOnServer(string clientString)
{
   string format = @"M/d/yyyy H:m:s zzz";

   try
   {      
      DateTimeOffset clientTime = DateTimeOffset.ParseExact(clientString, format, 
                                  CultureInfo.InvariantCulture);
      DateTimeOffset serverTime = TimeZoneInfo.ConvertTime(clientTime, 
                                  TimeZoneInfo.Local);
      return serverTime;
   }
   catch (FormatException)
   {
      return DateTimeOffset.MinValue;
   }
}
```

```vb
Public Function ReturnTimeOnServer(clientString As String) As DateTimeOffset
   Dim format As String = "M/d/yyyy H:m:s zzz"

   Try      
      Dim clientTime As DateTimeOffset = DateTimeOffset.ParseExact(clientString, format, CultureInfo.InvariantCulture)
      Dim serverTime As DateTimeOffset = TimeZoneInfo.ConvertTime(clientTime, TimeZoneInfo.Local)
      Return serverTime
   Catch e As FormatException
      Return DateTimeOffset.MinValue
   End Try    
End Function
```

## <a name="see-also"></a>Vedere anche

[TimeZoneInfo](xref:System.TimeZoneInfo)

[Date, ore e fusi orari](index.md)

[Ricerca dei fusi orari definiti in un sistema locale](finding-the-time-zones-on-local-system.md)





<!--HONumber=Nov16_HO3-->


