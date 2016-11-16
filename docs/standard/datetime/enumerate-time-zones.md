---
title: 'Procedura: Enumerare i fusi orari presenti in un computer'
description: Come enumerare i fusi orari presenti in un computer
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 08/15/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: c5ae4a6c-1790-4355-b5b1-879aaf956129
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: 417a421f443f90e5f4ccd48bcabb3735dc5bc981

---

# <a name="how-to-enumerate-time-zones-present-on-a-computer"></a>Procedura: Enumerare i fusi orari presenti in un computer

Per poter usare correttamente un determinato fuso orario è necessario che nel sistema siano disponibili le informazioni sul fuso orario. Nel sistema operativo Windows, ad esempio, le informazioni sono archiviate nel Registro di sistema. Sebbene nel mondo esistano molti fusi orari, le informazioni presenti nel Registro di sistema sono relative solo a una parte di essi. Inoltre, il Registro di sistema è una struttura dinamica il cui contenuto è soggetto a modifiche intenzionali e accidentali. Di conseguenza, un'applicazione non può sempre presupporre che un determinato fuso orario sia definito e disponibile in un sistema. Il primo passaggio per molte applicazioni che si basano sulle informazioni del fuso orario è determinare se i fusi orari richiesti sono disponibili nel sistema locale o offrire all'utente un elenco di fusi orari da selezionare. A tale scopo, è necessario che un'applicazione sia in grado di enumerare i fusi orari definiti in un sistema locale. 

## <a name="to-enumerate-the-time-zones-present-on-the-local-system"></a>Per enumerare i fusi orari presenti nel sistema locale

1. Chiamare il metodo [TimeZoneInfo.GetSystemTimeZones](xref:System.TimeZoneInfo.GetSystemTimeZones). Il metodo restituisce una raccolta [ReadOnlyCollection&lt;T&gt;](xref:System.Collections.ObjectModel.ReadOnlyCollection%601) generica di oggetti [TimeZoneInfo](xref:System.TimeZoneInfo). Le voci della raccolta sono ordinate in base alla relativa proprietà [DisplayName](xref:System.TimeZoneInfo.DisplayName). Ad esempio:

    ```csharp
    ReadOnlyCollection<TimeZoneInfo> tzCollection;
    tzCollection = TimeZoneInfo.GetSystemTimeZones();
    ```

    ```vb
    Dim tzCollection As ReadOnlyCollection(Of TimeZoneInfo) = TimeZoneInfo.GetSystemTimeZones
    ```

2. Enumerare i singoli oggetti [TimeZoneInfo](xref:System.TimeZoneInfo) della raccolta usando un ciclo `foreach` (in C#) o un ciclo `For Each…Next` (in Visual Basic) ed eseguire tutte le elaborazioni necessarie su ogni oggetto. Nel codice seguente, ad esempio, viene enumerata la raccolta [ReadOnlyCollection&lt;T&gt;](xref:System.Collections.ObjectModel.ReadOnlyCollection%601) degli oggetti [TimeZoneInfo](xref:System.TimeZoneInfo) restituiti nel passaggio 1 ed elencato il nome visualizzato di ogni fuso orario nella console.

    ```csharp
    foreach (TimeZoneInfo timeZone in tzCollection)
    Console.WriteLine("   {0}: {1}", timeZone.Id, timeZone.DisplayName);
    ```

    ```vb
    For Each timeZone As TimeZoneInfo In tzCollection
        Console.WriteLine("   {0}: {1}", timeZone.Id, timeZone.DisplayName)
    Next
    ```

## <a name="see-also"></a>Vedere anche

[Date, ore e fusi orari](index.md)

[Ricerca dei fusi orari definiti in un sistema locale](finding-the-time-zones-on-local-system.md)




<!--HONumber=Nov16_HO1-->


