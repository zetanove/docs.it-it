---
title: Panoramica sui fusi orari
description: Panoramica sui fusi orari
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 08/16/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: e3a10f62-d403-4441-8621-adc964e32c07
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: 67d77b80c2517da1c553094689eaf08c0c29078b

---

# <a name="time-zone-overview"></a>Panoramica sui fusi orari

La classe [System.TimeZoneInfo](xref:System.TimeZoneInfo) semplifica la creazione di applicazioni che rilevano il fuso orario. La classe [TimeZoneInfo](xref:System.TimeZoneInfo) supporta l'uso del fuso orario locale e dell'ora Coordinated Universal Time (UTC), nonché di qualsiasi fuso orario per il quale esistono informazioni predefinite nel Registro di sistema. È anche possibile usare [TimeZoneInfo](xref:System.TimeZoneInfo) per definire fusi orari personalizzati le cui informazioni non sono presenti nel sistema.

## <a name="time-zone-essentials"></a>Informazioni essenziali sui fusi orari

Un fuso orario è un'area geografica nella quale si usa la stessa ora. In genere, ma non sempre, i fusi orari adiacenti hanno un'ora di differenza. L'ora in un qualsiasi fuso orario del mondo può essere espressa come scostamento rispetto all'ora Coordinated Universal Time (UTC).

Molti fusi orari del mondo supportano l'ora legale. L'ora legale ha lo scopo di massimizzare le ore di luce diurna, con uno spostamento in avanti di un'ora in primavera o a inizio estate e con il ripristino dell'ora normale o solare a fine estate o inizio autunno. Queste modifiche rispetto all'ora solare sono note come regole di rettifica.

La transizione alla e dall'ora legale in un determinato fuso orario può essere definita da una regola di rettifica fissa o mobile. Una regola di rettifica fissa imposta una determinata data in cui si verifica ogni anno la transizione alla o dall'ora legale. Ad esempio, una transizione dall'ora legale all'ora solare che si verifica ogni anno il 25 ottobre segue una regola di rettifica fissa. Le regole di rettifica mobili, molto più comuni, impostano un determinato giorno di una determinata settimana di un determinato mese per la transizione alla o dall'ora legale. Ad esempio, una transizione dall'ora solare all'ora legale che si verifica la terza domenica del mese di marzo segue una regola di rettifica mobile.

Per i fusi orari che supportano le regole di rettifica, la transizione alla e dall'ora legale crea due tipi di ore anomale: le ore non valide e le ore ambigue. Un'ora non valida è un'ora inesistente creata dalla transizione dall'ora solare all'ora legale. Se ad esempio questa transizione ha luogo in un determinato giorno alle 2.00 e l'ora diventa le 3.00, ogni intervallo di tempo tra le 2.00 e le 2.59.99 non è valido. Un'ora ambigua è un'ora che può essere mappata su due ore diverse in un singolo fuso orario. Viene creata con la transizione dall'ora legale all'ora solare. Se ad esempio questa transizione ha luogo in un determinato giorno alle 2.00 e l'ora diventa le 1.00, ogni intervallo di tempo tra le 1.00 e le 1.59.99 può essere interpretato come ora solare o ora legale. 

## <a name="time-zone-terminology"></a>Terminologia dei fusi orari

Nella tabella seguente sono definiti termini usati comunemente quando si lavora con i fusi orari e si sviluppano applicazioni che rilevano il fuso orario.

Termine | Definizione
---- | ----------
Regola di rettifica | Regola che definisce quando si verifica la transizione dall'ora solare all'ora legale e viceversa. Ogni regola di rettifica ha una data di inizio e una data di fine che definiscono quando la regola è attiva (ad esempio la regola può essere attiva dal 1 gennaio 1986 al 31 dicembre 2020), un valore delta (la variazione oraria risultante dall'applicazione della regola di rettifica) e informazioni sulla data e ora specifica in cui le transizioni avranno luogo durante il periodo di rettifica. Le transizioni possono seguire una regola fissa o una regola mobile.
Ora ambigua | Ora che può essere mappata su due ore diverse in un singolo fuso orario. Si verifica quando l'orologio viene riportato indietro, ad esempio durante la transizione dall'ora legale all'ora solare di un determinato fuso orario. Se ad esempio questa transizione ha luogo in un determinato giorno alle 2.00 e l'ora diventa le 1.00, ogni intervallo di tempo tra le 1.00 e le 1.59.99 può essere interpretato come ora solare o ora legale. 
Regola fissa | Regola di rettifica che imposta una determinata data per la transizione alla o dall'ora legale. Ad esempio, una transizione dall'ora legale all'ora solare che si verifica ogni anno il 25 ottobre segue una regola di rettifica fissa.
Regola mobile | Regola di rettifica che imposta un determinato giorno di una determinata settimana di un determinato mese per la transizione alla o dall'ora legale. Ad esempio, una transizione dall'ora solare all'ora legale che si verifica la terza domenica del mese di marzo segue una regola di rettifica mobile.
Ora non valida | Ora inesistente creata dalla transizione dall'ora solare all'ora legale. Si verifica quando l'orologio viene portato avanti, ad esempio durante la transizione dall'ora solare all'ora legale di un determinato fuso orario. Se ad esempio questa transizione ha luogo in un determinato giorno alle 2.00 e l'ora diventa le 3.00, ogni intervallo di tempo tra le 2.00 e le 2.59.99 non è valido.
Ora transizione | Informazioni su una modifica di ora specifica, ad esempio la modifica dall'ora legale all'ora solare o viceversa, in un particolare fuso orario.

## <a name="time-zones-and-the-timezoneinfo-class"></a>Fusi orari e classe TimeZoneInfo

In .NET un oggetto [System.TimeZoneInfo](xref:System.TimeZoneInfo) rappresenta un fuso orario, in base alle informazioni specificate dal sistema operativo. La dipendenza della classe [TimeZoneInfo](xref:System.TimeZoneInfo) dal sistema operativo significa che un'applicazione con rilevamento del fuso orario non può garantire che un determinato fuso orario sia definito in tutti sistemi operativi. Di conseguenza, se si prevede di creare un'istanza di un fuso orario specifico (diverso dal fuso orario locale o da quello che rappresenta l'ora UTC) è consigliabile usare la gestione delle eccezioni. Il codice dovrà anche includere un metodo che consenta all'applicazione di continuare l'esecuzione se non è possibile creare un'istanza dell'oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) necessario.

Dato che ogni fuso orario è caratterizzato da un offset di base rispetto al fuso orario UTC, nonché da un offset da UTC che riflette eventuali regole di rettifica, un'ora in un fuso orario può essere convertita facilmente nell'ora corrispondente in un altro fuso orario. A questo scopo, l'oggetto [TimeZoneInfo](xref:System.TimeZoneInfo) include diversi metodi di conversione, tra cui:

* [ConvertTime(DateTime, TimeZoneInfo)](xref:System.TimeZoneInfo.ConvertTime(System.DateTime,System.TimeZoneInfo)), che converte un valore [System. DateTime](xref:System.DateTime) all'ora in un determinato fuso orario.

* [ConvertTime(DateTime, TimeZoneInfo, TimeZoneInfo)](xref:System.TimeZoneInfo.ConvertTime(System.DateTime,System.TimeZoneInfo,System.TimeZoneInfo)), che converte un valore [DateTime](xref:System.DateTime) da un fuso orario a un altro.

* [ConvertTime(DateTimeOffset, TimeZoneInfo)](xref:System.TimeZoneInfo.ConvertTime(System.DateTimeOffset,System.TimeZoneInfo)), che converte un valore [System.DateTimeOffset](xref:System.DateTimeOffset) all'ora in un determinato fuso orario. 

Per informazioni dettagliate sulla conversione degli orari tra fusi orari, vedere [Conversione degli orari tra fusi orari](converting-between-time-zones.md).

## <a name="see-also"></a>Vedere anche

[Date, ore e fusi orari](index.md)


<!--HONumber=Nov16_HO3-->


