---
title: Ricerca dei fusi orari definiti in un sistema locale
description: Ricerca dei fusi orari definiti in un sistema locale
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 08/15/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 3a6ee323-f3cf-486d-aa0c-103931f1eba9
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: e7f07a1f86ca31a24e25d98de2f8918ff098db24

---

# <a name="finding-the-time-zones-defined-on-a-local-system"></a>Ricerca dei fusi orari definiti in un sistema locale

La classe [System.TimeZoneInfo](xref:System.TimeZoneInfo) non espone un costruttore pubblico. Di conseguenza, non è possibile usare la parola chiave `new` per creare un nuovo oggetto [TimeZoneInfo](xref:System.TimeZoneInfo). Le istanze degli oggetti [TimeZoneInfo](xref:System.TimeZoneInfo) vengono invece create recuperando le informazioni sui fusi orari predefiniti dal sistema operativo. Questo argomento descrive la creazione dell'istanza di un fuso orario da dati archiviati dal sistema operativo. Inoltre, le proprietà `static` (`Shared` in Visual Basic) della classe [TimeZoneInfo](xref:System.TimeZoneInfo) consentono l'accesso all'ora Coordinated Universal Time (UTC) e al fuso orario locale.

## <a name="accessing-individual-time-zones"></a>Accesso a singoli fusi orari

La classe [TimeZoneInfo](xref:System.TimeZoneInfo) offre due oggetti fuso orario predefiniti che rappresentano l'ora UTC e il fuso orario locale. Gli oggetti sono disponibili rispettivamente dalle proprietà [TimeZoneInfo.Utc](xref:System.TimeZoneInfo.Utc) e [TimeZoneInfo.Local](xref:System.TimeZoneInfo.Local). Per istruzioni sull'accesso all'ora UTC o ai fusi orari locali, vedere [Procedura: Accedere agli oggetti predefiniti dell'ora UTC e del fuso orario locale](access-utc-and-local.md). 

È anche possibile creare l'istanza di un oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) che rappresenta qualsiasi fuso orario definito dal sistema operativo. Per istruzioni sulla creazione dell'istanza di un oggetto fuso orario specifico, vedere [Procedura: Creare un'istanza di un oggetto TimeZoneInfo](instantiate-time-zone-info.md).

## <a name="time-zone-identifiers"></a>Identificatori del fuso orario

L'identificatore del fuso orario è un campo chiave che identifica in modo univoco il fuso orario. Benché la maggior parte delle chiavi sia relativamente breve, in confronto l'identificatore del fuso orario è piuttosto lungo. Nella maggior parte dei casi, il suo valore corrisponde alla proprietà [TimeZoneInfo.StandardName](xref:System.TimeZoneInfo.StandardName), che viene usata per specificare il nome dell'ora solare del fuso orario. Esistono tuttavia alcune eccezioni. Il modo migliore per assicurarsi di specificare un identificatore univoco consiste nell'enumerare i fusi orari disponibili nel sistema e annotare gli identificatori associati. Per istruzioni sull'enumerazione dei fusi orari, vedere [Procedura: Enumerare i fusi orari presenti in un computer](enumerate-time-zones.md).

## <a name="see-also"></a>Vedere anche

[Date, ore e fusi orari](index.md)

[Procedura: Accedere agli oggetti predefiniti dell'ora UTC e del fuso orario locale](access-utc-and-local.md)

[Procedura: Creare un'istanza di un oggetto TimeZoneInfo](instantiate-time-zone-info.md)

[Procedura: Enumerare i fusi orari presenti in un computer](enumerate-time-zones.md)

[Conversione degli orari tra fusi orari](converting-between-time-zones.md)


<!--HONumber=Nov16_HO3-->


