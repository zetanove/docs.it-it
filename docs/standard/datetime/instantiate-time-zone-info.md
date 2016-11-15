---
title: 'Procedura: Creare un''istanza di un oggetto TimeZoneInfo'
description: Come creare un&quot;istanza di un oggetto TimeZoneInfo
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 08/15/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: bff137e5-d550-44c3-b460-b3f2dabd4035
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: 5af479c40bb5db3213f45c0472dbdea99bbd5c21

---

# <a name="how-to-instantiate-a-timezoneinfo-object"></a>Procedura: Creare un'istanza di un oggetto TimeZoneInfo

Il modo più comune per creare un'istanza di un oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) è recuperare le relative informazioni dal sistema operativo. Questo argomento illustra come creare un'istanza di un oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) dal sistema locale.

## <a name="to-instantiate-a-timezoneinfo-object"></a>Per creare un'istanza di un oggetto TimeZoneInfo

1. Dichiarare un oggetto [TimeZoneInfo](xref:System.TimeZoneInfo).

2. Chiamare il metodo `static` (`Shared` in Visual Basic) [TimeZoneInfo.FindSystemTimeZoneById](xref:System.TimeZoneInfo.FindSystemTimeZoneById(System.String)).

3. Gestire le eccezioni generate dal metodo.

## <a name="example"></a>Esempio

Il codice seguente consente di recuperare un oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) che rappresenta il l'ora solare fuso orientale e di visualizzare l'ora solare fuso orientale corrispondente all'ora locale.

```csharp
DateTime timeNow = DateTime.Now;
try
{
   TimeZoneInfo easternZone = TimeZoneInfo.FindSystemTimeZoneById("Eastern Standard Time");
   DateTime easternTimeNow = TimeZoneInfo.ConvertTime(timeNow, TimeZoneInfo.Local, 
                                                   easternZone);
   Console.WriteLine("{0} {1} corresponds to {2} {3}.",
                     timeNow, 
                     TimeZoneInfo.Local.IsDaylightSavingTime(timeNow) ?
                               TimeZoneInfo.Local.DaylightName : 
                               TimeZoneInfo.Local.StandardName,
                     easternTimeNow, 
                     easternZone.IsDaylightSavingTime(easternTimeNow) ?
                                 easternZone.DaylightName : 
                                 easternZone.StandardName);
}
// Handle exception
//
// As an alternative to simply displaying an error message, an alternate Eastern
// Standard Time TimeZoneInfo object could be instantiated here either by restoring
// it from a serialized string or by providing the necessary data to the
// CreateCustomTimeZone method.
catch (InvalidTimeZoneException)
{
   Console.WriteLine("The Eastern Standard Time Zone contains invalid or missing data.");
}
catch (SecurityException)
{
   Console.WriteLine("The application lacks permission to read time zone information from the registry.");
}
catch (OutOfMemoryException)
{
   Console.WriteLine("Not enough memory is available to load information on the Eastern Standard Time zone.");
}
// If we weren't passing FindSystemTimeZoneById a literal string, we also 
// would handle an ArgumentNullException.
```

```vb
Dim timeNow As Date = Date.Now
Try
   Dim easternZone As TimeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById("Eastern Standard Time")
   Dim easternTimeNow As Date = TimeZoneInfo.ConvertTime(timeNow, TimeZoneInfo.Local, easternZone)
   Console.WriteLine("{0} {1} corresponds to {2} {3}.", _
                     timeNow, _
                     IIf(TimeZoneInfo.Local.IsDaylightSavingTime(timeNow), _
                         TimeZoneInfo.Local.DaylightName, TimeZoneInfo.Local.StandardName), _
                     easternTimeNow, _
                     IIf(easternZone.IsDaylightSavingTime(easternTimeNow), _
                         easternZone.DaylightName, easternZone.StandardName))
' Handle exception
'
' As an alternative to simply displaying an error message, an alternate Eastern
' Standard Time TimeZoneInfo object could be instantiated here either by restoring
' it from a serialized string or by providing the necessary data to the
' CreateCustomTimeZone method.
Catch e As InvalidTimeZoneException
   Console.WriteLine("The Eastern Standard Time Zone contains invalid or missing data.")   
Catch e As SecurityException
   Console.WriteLine("The application lacks permission to read time zone information from the registry.")
Catch e As OutOfMemoryException
   Console.WriteLine("Not enough memory is available to load information on the Eastern Standard Time zone.")
' If we weren't passing FindSystemTimeZoneById a literal string, we also 
' would handle an ArgumentNullException.
End
``` 

L'unico parametro del metodo [TimeZoneInfo.FindSystemTimeZoneById](xref:System.TimeZoneInfo.FindSystemTimeZoneById(System.String)) è l'identificatore del fuso orario da recuperare, che corrisponde alla proprietà [TimeZoneInfo.Id](xref:System.TimeZoneInfo.Id) dell'oggetto. L'identificatore del fuso orario è un campo chiave che identifica in modo univoco il fuso orario. Benché la maggior parte delle chiavi sia relativamente breve, in confronto l'identificatore del fuso orario è piuttosto lungo. Nella maggior parte dei casi il suo valore corrisponde alla proprietà [StandardName](xref:System.TimeZoneInfo.StandardName) di un oggetto [TimeZoneInfo](xref:System.TimeZoneInfo), che viene usata per specificare il nome dell'ora solare del fuso orario. Esistono tuttavia alcune eccezioni. Il modo migliore per verificare che venga fornito un identificatore valido consiste nell'enumerare i fusi orari disponibili nel sistema e annotare i relativi identificatori dei fusi orari. Per un'illustrazione, vedere [Procedura: enumerare i fusi orari presenti in un computer](enumerate-time-zones.md). L'argomento [Ricerca dei fusi orari definiti in un sistema locale](finding-the-time-zones-on-local-system.md) include anche l'elenco degli identificatori dei fusi orari selezionati.

Se il fuso orario viene trovato, il metodo restituisce l'oggetto [TimeZoneInfo](xref:System.TimeZoneInfo). Se invece il fuso orario viene trovato, ma i dati sono danneggiati o incompleti, il metodo genera un'eccezione [InvalidTimeZoneException](xref:System.InvalidTimeZoneException). 

## <a name="see-also"></a>Vedere anche

[Date, ore e fusi orari](index.md)

[Ricerca dei fusi orari definiti in un sistema locale](finding-the-time-zones-on-local-system.md)


<!--HONumber=Nov16_HO1-->


