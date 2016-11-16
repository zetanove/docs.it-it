---
title: Date, ore e fusi orari
description: Date, ore e fusi orari
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/22/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 76e6cacc-1c0c-4a71-8cb8-018c112385ba
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: a4d0a68ac32c3d722a1479ca2b067892fd88bf52

---

# <a name="dates-times-and-time-zones"></a>Date, ore e fusi orari

Oltre alla struttura di base [System.DateTime](xref:System.DateTime), .NET fornisce le classi seguenti che supportano l'uso dei fusi orari:

* [System.TimeZoneInfo](xref:System.TimeZoneInfo)
    
  Usare questa classe con il fuso orario locale del sistema e il fuso UTC (Coordinated Universal Time).
  
* [System.DateTimeOffset](xref:System.DateTimeOffset)  

  Usare questa struttura con le date e le ore il cui offset (o differenza) rispetto all'ora UTC è noto. La struttura [DateTimeOffset](xref:System.DateTimeOffset)] combina un valore di data e ora con l'offset di quell'ora rispetto all'ora UTC. Per via della relazione con l'ora UTC, un singolo valore di data e ora identifica un momento specifico senza ambiguità. Un valore [DateTimeOffset](xref:System.DateTimeOffset)] risulta pertanto più portabile da un computer a un altro rispetto a un valore [DateTime](xref:System.DateTime)]. 
  
Questa sezione della documentazione include le informazioni necessarie per usare i fusi orari e per creare applicazioni in grado di riconoscere i fusi orari e convertire date e ore da un fuso orario a un altro.

## <a name="in-this-section"></a>Contenuto della sezione

[Panoramica sul fuso orario](time-zone-overview.md): illustra concetti, terminologia e problemi relativi alla creazione di applicazioni che dipendono dal fuso orario.
    
[Scelta tra DateTime, DateTimeOffset, TimeSpan e TimeZoneInfo](choosing-between-datetime.md): illustra quando usare i tipi [System.DateTime](xref:System.DateTime), [System.DateTimeOffset](xref:System.DateTimeOffset) e [System.TimeZoneInfo](xref:System.TimeZoneInfo) con i dati relativi a data e ora.
    
[Ricerca dei fusi orari definiti in un sistema locale](finding-the-time-zones-on-local-system.md): descrive come enumerare i fusi orari che si trovano in un sistema locale.

[Creazione di un'istanza di un oggetto DateTimeOffse](instantiating-a-datetimeoffset-object.md): illustra i modi per creare un'istanza di un oggetto [System.DateTimeOffset](xref:System.DateTimeOffset) e i modi per convertire un valore [System.DateTime](xref:System.DateTime) in un valore [System.DateTimeOffset](xref:System.DateTimeOffset).

[Esecuzione di operazioni aritmetiche con date e ore](performing-arithmetic-operations.md): descrive i problemi relativi ad aggiunta, sottrazione e confronto dei valori [System.DateTime](xref:System.DateTime) e [System.DateTimeOffset](xref:System.DateTimeOffset).

[Conversione tra DateTime e DateTimeOffset](converting-between-datetime-and-offset.md): descrive come eseguire la conversione tra i valori [System.DateTime](xref:System.DateTime) e [System.DateTimeOffset](xref:System.DateTimeOffset).

[Conversione degli orari tra fusi orari](converting-between-time-zones.md): descrive come eseguire la conversione di ore tra un fuso orario e un altro.

[Procedura: enumerare i fusi orari presenti in un computer](enumerate-time-zones.md): include esempi che enumerano i fusi orari definiti nel Registro di sistema di un computer e che consentono agli utenti di selezionare un fuso orario predefinito da un elenco.

[Procedura: accedere agli oggetti predefiniti dell'ora UTC e del fuso orario locale](access-utc-and-local.md): descrive come accedere all'ora UTC e al fuso orario locale.

[Procedura: creare un'istanza di un oggetto TimeZoneInfo](instantiate-time-zone-info.md): descrive come creare un'istanza di un oggetto [System.TimeZoneInfo](xref:System.TimeZoneInfo) dal Registro di sistema locale.

[Procedura: utilizzare fusi orari nell'aritmetica di data e ora](use-time-zones-in-arithmetic.md): illustra come eseguire operazioni aritmetiche di data e ora che riflettano le regole di adeguamento di un fuso orario.

[Procedura: risolvere orari ambigui](resolve-ambiguous-times.md): descrive come risolvere un orario ambiguo eseguendone il mapping all'ora solare del fuso orario.

[Procedura: consentire agli utenti di risolvere orari ambigui](let-users-resolve-ambiguous-times.md): descrive come consentire agli utenti di determinare il mapping tra un'ora locale ambigua e l'ora UTC.

## <a name="reference"></a>Riferimento

[System.TimeZoneInfo](xref:System.TimeZoneInfo)

[System.DateTimeOffset](xref:System.DateTimeOffset)

[System.DateTime](xref:System.DateTime)



<!--HONumber=Nov16_HO3-->


