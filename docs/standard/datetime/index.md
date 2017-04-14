---
title: "Date, ora e fusi orari | Microsoft Docs"
ms.custom: ""
ms.date: "04/10/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "data e ora (dati) [.NET Framework]"
  - "ora [.NET Framework], fusi orari"
  - "fusi orari (oggetti) [.NET Framework]"
  - "fusi orari [.NET Framework]"
  - "ore [.NET Framework], fusi orari"
ms.assetid: 295c16e0-641b-4771-94b3-39c1ffa98c13
caps.latest.revision: 22
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 22
---
# Date, ora e fusi orari
Oltre alla struttura <xref:System.DateTime> di base, [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] include le classi seguenti che supportano l'utilizzo dei fusi orari:  
  
-   <xref:System.TimeZone>  
  
     Utilizzare questa classe per lavorare con il fuso orario locale del sistema e l'ora UTC \(Coordinated Universal Time\).  La funzionalità della classe <xref:System.TimeZone> è ampiamente sostituita dalla classe <xref:System.TimeZoneInfo>.  
  
-   <xref:System.TimeZoneInfo>  
  
     Utilizzare questa classe per lavorare con qualsiasi fuso orario predefinito di un sistema, per creare fusi orari nuovi e per convertire facilmente date e ore da un fuso orario all'altro.  Per lo sviluppo di nuovo codice, utilizzare la classe <xref:System.TimeZoneInfo> invece della classe <xref:System.TimeZone>.  
  
-   <xref:System.DateTimeOffset>  
  
     Utilizzare questa struttura per lavorare con date e ore il cui offset \(o differenza\) dall'ora UTC è conosciuto.  La struttura <xref:System.DateTimeOffset> combina un valore di data e ora con il relativo offset rispetto all'ora UTC.  A causa della relazione con UTC, un singolo valore di data e ora identifica uno specifico momento in modo inequivocabile.  Ciò migliora la portabilità di un valore <xref:System.DateTimeOffset> da un computer all'altro rispetto a un valore <xref:System.DateTime>.  
  
 In questa sezione della documentazione sono contenute le informazioni necessarie per utilizzare i fusi orari e per creare applicazioni in grado di riconoscere il fuso orario e convertire date e ore da uno fuso orario all'altro.  
  
## In questa sezione  
 [Panoramica sul fuso orario](../../../docs/standard/datetime/time-zone-overview.md)  
 Vengono illustrati la terminologia, i concetti e i problemi relativi alla creazione di applicazioni che dipendono dal fuso orario.  
  
 [Scelta tra DateTime, DateTimeOffset, TimeSpan e TimeZoneInfo](../../../docs/standard/datetime/choosing-between-datetime.md)  
 Viene illustrato quando utilizzare i tipi <xref:System.DateTime>, <xref:System.DateTimeOffset> e <xref:System.TimeZoneInfo> con i valori di data e ora.  
  
 [Ricerca dei fusi orari definiti in un sistema locale](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md)  
 Viene descritto come enumerare i fusi orari individuati in un sistema locale.  
  
 [Procedura: enumerare i fusi orari presenti in un computer](../../../docs/standard/datetime/enumerate-time-zones.md)  
 Vengono forniti esempi che enumerano i fusi orari definiti nel Registro di sistema di un computer e che consentono agli utenti di selezionare un fuso orario predefinito in un elenco.  
  
 [Procedura: accedere agli oggetti predefiniti dell'ora UTC e del fuso orario locale](../../../docs/standard/datetime/access-utc-and-local.md)  
 Viene descritto come accedere all'ora UCT \(Coordinated Universal Time\) e al fuso orario locale.  
  
 [Procedura: creare un'istanza di un oggetto TimeZoneInfo](../../../docs/standard/datetime/instantiate-time-zone-info.md)  
 Viene descritto come creare un'istanza di un oggetto <xref:System.TimeZoneInfo> dal Registro di sistema locale.  
  
 [Creazione di un'istanza di un oggetto DateTimeOffset](../../../docs/standard/datetime/instantiating-a-datetimeoffset-object.md)  
 Vengono illustrate le modalità per la creazione di un'istanza di un oggetto <xref:System.DateTimeOffset>, nonché quelle per la conversione di un valore <xref:System.DateTime> in un valore <xref:System.DateTimeOffset>.  
  
 [Procedura: creare fusi orari senza regole di regolazione](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md)  
 Viene descritto come creare un fuso orario personalizzato che non supporta la transizione da e verso l'ora legale.  
  
 [Procedura: creare fusi orari con regole di regolazione](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md)  
 Viene descritto come creare un fuso orario personalizzato che supporta una o più transizioni da e verso l'ora legale.  
  
 [Salvataggio e ripristino dei fusi orari](../../../docs/standard/datetime/saving-and-restoring-time-zones.md)  
 Viene descritto il supporto di <xref:System.TimeZoneInfo> per la serializzazione e la deserializzazione dei dati relativi al fuso orario e vengono illustrati alcuni scenari in cui è possibile utilizzare queste funzionalità.  
  
 [Procedura: salvare fusi orari in una risorsa incorporata](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)  
 Viene descritto come creare un fuso orario personalizzato e salvarne le informazioni in un file di risorse.  
  
 [Procedura: ripristinare i fusi orari da una risorsa incorporata](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)  
 Viene descritto come creare un'istanza dei fusi orari personalizzati salvati in un file di risorse incorporato.  
  
 [Esecuzione di operazioni aritmetiche con date e ore](../../../docs/standard/datetime/performing-arithmetic-operations.md)  
 Vengono descritti i problemi relativi all'aggiunta, alla sottrazione e al confronto dei valori <xref:System.DateTime> e <xref:System.DateTimeOffset>.  
  
 [Procedura: utilizzare fusi orari nell'aritmetica di data e ora](../../../docs/standard/datetime/use-time-zones-in-arithmetic.md)  
 Viene descritto come eseguire operazioni aritmetiche con date e ore che riflettono le regole di rettifica di un fuso orario.  
  
 [Conversione tra DateTime e DateTimeOffset](../../../docs/standard/datetime/converting-between-datetime-and-offset.md)  
 Viene descritto come eseguire la conversione tra valori <xref:System.DateTime> e <xref:System.DateTimeOffset>.  
  
 [Conversione degli orari tra fusi orari](../../../docs/standard/datetime/converting-between-time-zones.md)  
 Viene descritto come convertire gli orari da un fuso orario all'altro.  
  
 [Procedura: risolvere orari ambigui](../../../docs/standard/datetime/resolve-ambiguous-times.md)  
 Viene descritto come risolvere un'ora ambigua eseguendone il mapping all'ora standard del fuso orario.  
  
 [Procedura: consentire agli utenti di risolvere orari ambigui](../../../docs/standard/datetime/let-users-resolve-ambiguous-times.md)  
 Viene descritto come consentire a un utente di determinare il mapping tra un'ora locale ambigua e un'ora UCT \(Coordinated Universal Time\).  
  
## Riferimenti  
 <xref:System.TimeZoneInfo?displayProperty=fullName>