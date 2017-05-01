---
title: Date, ore e fusi orari | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework-4.6
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time zone objects [.NET Framework]
- date and time data [.NET Framework]
- time zones [.NET Framework]
- times [.NET Framework], time zones
- time [.NET Framework], time zones
ms.assetid: 295c16e0-641b-4771-94b3-39c1ffa98c13
caps.latest.revision: 22
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: c50b3e328998b65ec47efe6d7457b36116813c77
ms.openlocfilehash: 2445188fda029ddc0f673d4c81f99f7f46edb89b
ms.lasthandoff: 04/08/2017

---
# <a name="dates-times-and-time-zones"></a>Date, ora e fusi orari
Oltre alla struttura di base <xref:System.DateTime>, [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] fornisce le classi seguenti che supportano l'uso dei fusi orari:  
  
-   <xref:System.TimeZone>  
  
     Usare questa classe con il fuso orario locale del sistema e il fuso UTC (Coordinated Universal Time).  La funzionalità della classe <xref:System.TimeZone> è ampiamente sostituita dalla classe <xref:System.TimeZoneInfo>.  
  
-   <xref:System.TimeZoneInfo>  
  
     Utilizzare questa classe per utilizzare qualsiasi fuso orario predefinito in un sistema, per creare nuovi fusi orari e per convertire facilmente date e ore da un fuso orario a un altro. Per i nuovi sviluppi, usare la classe <xref:System.TimeZoneInfo> anziché la classe <xref:System.TimeZone>.  
  
-   <xref:System.DateTimeOffset>  
  
     Usare questa struttura con le date e le ore il cui offset (o differenza) rispetto all'ora UTC è noto. La struttura <xref:System.DateTimeOffset> combina un valore di data e ora con l'offset di quell'ora rispetto all'ora UTC. Per via della relazione con l'ora UTC, un singolo valore di data e ora identifica un momento specifico senza ambiguità. Un valore <xref:System.DateTimeOffset> risulta pertanto più portabile da un computer a un altro rispetto a un valore <xref:System.DateTime>.  
  
 Questa sezione della documentazione include le informazioni necessarie per usare i fusi orari e per creare applicazioni in grado di riconoscere i fusi orari e convertire date e ore da un fuso orario a un altro.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Panoramica sui fusi orari](../../../docs/standard/datetime/time-zone-overview.md)  
 Illustra concetti, terminologia e problemi relativi alla creazione di applicazioni che dipendono dal fuso orario.  
  
 [Scelta tra DateTime, DateTimeOffset, TimeSpan e TimeZoneInfo](../../../docs/standard/datetime/choosing-between-datetime.md)  
 Illustra quando usare i tipi <xref:System.DateTime>, <xref:System.DateTimeOffset> e <xref:System.TimeZoneInfo> con i dati relativi a data e ora.  
  
 [Ricerca dei fusi orari definiti in un sistema locale](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md)  
 Descrive come enumerare i fusi orari che si trovano in un sistema locale.  
  
 [Procedura: Enumerare i fusi orari presenti in un computer](../../../docs/standard/datetime/enumerate-time-zones.md)  
 Include esempi che enumerano i fusi orari definiti nel Registro di sistema di un computer e che consentono agli utenti di selezionare un fuso orario predefinito da un elenco.  
  
 [Procedura: Accedere agli oggetti predefiniti dell'ora UTC e del fuso orario locale](../../../docs/standard/datetime/access-utc-and-local.md)  
 Descrive come accedere all'ora UTC e al fuso orario locale.  
  
 [Procedura: Creare un'istanza di un oggetto TimeZoneInfo](../../../docs/standard/datetime/instantiate-time-zone-info.md)  
 Questo argomento illustra come creare un'istanza di un oggetto <xref:System.TimeZoneInfo> dal Registro di sistema locale.  
  
 [Creazione di un'istanza di un oggetto DateTimeOffset](../../../docs/standard/datetime/instantiating-a-datetimeoffset-object.md)  
 Illustra i modi per creare un'istanza di un oggetto <xref:System.DateTimeOffset> e i modi per convertire un valore <xref:System.DateTime> in un valore <xref:System.DateTimeOffset>.  
  
 [Procedura: Creare fusi orari senza regole di regolazione](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md)  
 Descrive come creare un fuso orario personalizzato che non supporta la transizione da e verso l'ora legale.  
  
 [Procedura: Creare fusi orari con regole di regolazione](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md)  
 Descrive come creare un fuso orario personalizzato che supporta una o più transizioni da e verso l'ora legale.  
  
 [Salvataggio e ripristino dei fusi orari](../../../docs/standard/datetime/saving-and-restoring-time-zones.md)  
 Descrive il supporto <xref:System.TimeZoneInfo> per la serializzazione e deserializzazione dei dati del fuso orario e illustra alcuni degli scenari in cui è possibile usare tali funzionalità.  
  
 [Procedura: Salvare fusi orari in una risorsa incorporata](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)  
 Descrive come creare un fuso orario personalizzato e salvare le informazioni in un file di risorse.  
  
 [Procedura: Ripristinare i fusi orari da una risorsa incorporata](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)  
 Descrive come creare un'istanza di fusi orari personalizzati che sono stati salvati in un file di risorsa incorporata.  
  
 [Esecuzione di operazioni aritmetiche con date e ore](../../../docs/standard/datetime/performing-arithmetic-operations.md)  
 Descrive i problemi relativi ad aggiunta, sottrazione e confronto dei valori <xref:System.DateTime> e <xref:System.DateTimeOffset>.  
  
 [Procedura: Usare fusi orari nell'aritmetica di data e ora](../../../docs/standard/datetime/use-time-zones-in-arithmetic.md)  
 Illustra come eseguire operazioni aritmetiche di data e ora che riflettano le regole di adeguamento di un fuso orario.  
  
 [Conversione tra DateTime e DateTimeOffset](../../../docs/standard/datetime/converting-between-datetime-and-offset.md)  
 Descrive come eseguire la conversione tra i valori <xref:System.DateTime> e <xref:System.DateTimeOffset>.  
  
 [Conversione degli orari tra fusi orari](../../../docs/standard/datetime/converting-between-time-zones.md)  
 Descrive come eseguire la conversione di ore tra un fuso orario e un altro.  
  
 [Procedura: Risolvere orari ambigui](../../../docs/standard/datetime/resolve-ambiguous-times.md)  
 Descrive come risolvere un orario ambiguo eseguendone il mapping all'ora solare del fuso orario.  
  
 [Procedura: Consentire agli utenti di risolvere orari ambigui](../../../docs/standard/datetime/let-users-resolve-ambiguous-times.md)  
 Descrive come consentire agli utenti di determinare il mapping tra un'ora locale ambigua e l'ora UTC.  
  
## <a name="reference"></a>Riferimento  
 <xref:System.TimeZoneInfo?displayProperty=fullName>
