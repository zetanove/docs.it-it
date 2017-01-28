---
title: 'Procedura: Accedere agli oggetti predefiniti dell&quot;ora UTC e del fuso orario locale'
description: Come accedere agli oggetti predefiniti dell&quot;ora UTC e del fuso orario locale
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 08/11/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 13454d47-d957-421b-9ecd-940058b8835e
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: ab419cf365b61399ea41e99c15e276584ad0db31

---

# <a name="how-to-access-the-predefined-utc-and-local-time-zone-objects"></a>Procedura: Accedere agli oggetti predefiniti dell'ora UTC e del fuso orario locale

Due proprietà della classe [System.TimeZoneInfo](xref:System.TimeZoneInfo), `Utc` e `Local`, consentono di usare un codice di accesso per gli oggetti predefiniti del fuso orario. In questo argomento viene illustrato come accedere agli oggetti `TimeZoneInfo` restituiti da tali proprietà.

## <a name="to-access-the-coordinated-universal-time-utc-timezoneinfo-object"></a>Per accedere all'oggetto TimeZoneInfo dell'ora UTC (Coordinated Universal Time)

1. Usare la proprietà **static** (**Shared** in Visual Basic) [TimeZoneInfo.Utc](xref:System.TimeZoneInfo.Utc) per accedere all'ora UTC.

2. Anziché assegnare l'oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) restituito dalla proprietà a una variabile oggetto, continuare ad accedere all'ora UTC usando la proprietà [TimeZoneInfo.Utc](xref:System.TimeZoneInfo.Utc).


## <a name="to-access-the-local-time-zone"></a>Per accedere al fuso orario locale

1. Usare la proprietà **static** (**Shared** in Visual Basic) [TimeZoneInfo.Local](xref:System.TimeZoneInfo.Local) per accedere al fuso orario locale.

2. Anziché assegnare l'oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) restituito dalla proprietà a una variabile oggetto, continuare ad accedere al fuso orario locale usando la proprietà [TimeZoneInfo.Local](xref:System.TimeZoneInfo.Local).

## <a name="example"></a>Esempio

Nel codice seguente vengono usate le proprietà [TimeZoneInfo.Local](xref:System.TimeZoneInfo.Local) e [TimeZoneInfo.Utc](xref:System.TimeZoneInfo.Utc) per convertire un orario del fuso orario standard degli Stati Uniti e Canada orientale, nonché per visualizzare il nome del fuso orario nella console.

```csharp
// Create Eastern Standard Time value and TimeZoneInfo object      
DateTime estTime = new DateTime(2007, 1, 1, 00, 00, 00);
string timeZoneName = "Eastern Standard Time";
try
{
   TimeZoneInfo est = TimeZoneInfo.FindSystemTimeZoneById(timeZoneName);

   // Convert EST to local time
   DateTime localTime = TimeZoneInfo.ConvertTime(estTime, est, TimeZoneInfo.Local);
   Console.WriteLine("At {0} {1}, the local time is {2} {3}.", 
           estTime, 
           est, 
           localTime, 
           TimeZoneInfo.Local.IsDaylightSavingTime(localTime) ?
                     TimeZoneInfo.Local.DaylightName : 
                     TimeZoneInfo.Local.StandardName);

   // Convert EST to UTC
   DateTime utcTime = TimeZoneInfo.ConvertTime(estTime, est, TimeZoneInfo.Utc);
   Console.WriteLine("At {0} {1}, the time is {2} {3}.", 
           estTime, 
           est, 
           utcTime, 
           TimeZoneInfo.Utc.StandardName);
}
catch (TimeZoneNotFoundException)
{
   Console.WriteLine("The {0} zone cannot be found in the registry.", 
                     timeZoneName);
}
catch (InvalidTimeZoneException)
{
   Console.WriteLine("The registry contains invalid data for the {0} zone.", 
                     timeZoneName);
}
```

```vb
' Create Eastern Standard Time value and TimeZoneInfo object      
Dim estTime As Date = #01/01/2007 00:00:00#
Dim timeZoneName As String = "Eastern Standard Time"
Try
   Dim est As TimeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById(timeZoneName)

   ' Convert EST to local time
   Dim localTime As Date = TimeZoneInfo.ConvertTime(estTime, est, TimeZoneInfo.Local)
   Console.WriteLine("At {0} {1}, the local time is {2} {3}.", _
           estTime, _
           est, _
           localTime, _
           IIf(TimeZoneInfo.Local.IsDaylightSavingTime(localTime), _
               TimeZoneInfo.Local.DaylightName, _
               TimeZoneInfo.Local.StandardName))

   ' Convert EST to UTC
   Dim utcTime As Date = TimeZoneInfo.ConvertTime(estTime, est, TimeZoneInfo.Utc)
   Console.WriteLine("At {0} {1}, the time is {2} {3}.", _
           estTime, _
           est, _
           utcTime, _
           TimeZoneInfo.Utc.StandardName)
Catch e As TimeZoneNotFoundException
   Console.WriteLine("The {0} zone cannot be found in the registry.", _
                     timeZoneName)
Catch e As InvalidTimeZoneException
   Console.WriteLine("The registry contains invalid data for the {0} zone.", _
                     timeZoneName)
End Try
```

Accedere sempre al fuso orario locale usando la proprietà [TimeZoneInfo.Local](xref:System.TimeZoneInfo.Local) anziché assegnare il fuso orario locale a una variabile oggetto [TimeZoneInfo](xref:System.TimeZoneInfo). Analogamente, accedere sempre all'ora UTC usando la proprietà [TimeZoneInfo.Utc](xref:System.TimeZoneInfo.Utc) anziché assegnare l'ora UTC a una variabile oggetto [TimeZoneInfo](xref:System.TimeZoneInfo). Ciò impedisce che la variabile oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) venga invalidata da un metodo esterno.


## <a name="see-also"></a>Vedere anche

[Date, ore e fusi orari](index.md)

[Ricerca dei fusi orari definiti in un sistema locale](finding-the-time-zones-on-local-system.md)



<!--HONumber=Nov16_HO3-->


