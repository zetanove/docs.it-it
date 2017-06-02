---
title: "Scelta tra DateTime, DateTimeOffset, TimeSpan e TimeZoneInfo | Microsoft Docs"
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
  - "DateTimeOffset (struttura)"
  - "TimeZoneInfo (classe)"
  - "fusi orari [.NET Framework], usi comuni"
  - "data e ora (classi) [.NET Framework]"
  - "fusi orari [.NET Framework], opzioni di tipo"
  - "DateTime (struttura)"
ms.assetid: 07f17aad-3571-4014-9ef3-b695a86f3800
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Scelta tra DateTime, DateTimeOffset, TimeSpan e TimeZoneInfo
Le applicazioni [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] che usano informazioni su data e ora sono molto diversificate e possono usare tali informazioni in modi diversi. Gli utilizzi più comuni delle informazioni su data e ora includono uno o più dei seguenti:  
  
-   Indicare solo una data, perché le informazioni sull'ora non sono importanti.  
  
-   Indicare solo un'ora, perché le informazioni sulla data non sono importanti.  
  
-   Indicare una data e un'ora astratte e non associate a un momento e un luogo specifici. Ad esempio, la maggior parte dei negozi di una catena internazionale apre alle 9.00 di ogni giorno feriale.  
  
-   Recuperare informazioni su data e ora da origini esterne a [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], in genere quando tali informazioni sono archiviate in un tipo di dati semplice.  
  
-   Identificare in modo univoco e senza ambiguità un singolo momento. In alcune applicazioni è necessario che la data e l'ora siano non ambigue solo nel sistema host, in altre devono non esserlo in tutti i sistemi \(ovvero, una data serializzata in un sistema può essere deserializzata in modo significativo e usata in un altro sistema in qualsiasi parte del mondo\).  
  
-   Mantenere più ore correlate, ad esempio l'ora locale del richiedente e l'ora di ricezione di una richiesta Web nel server.  
  
-   Eseguire operazioni aritmetiche per date e ore, possibilmente con un risultato che identifichi in modo univoco e senza ambiguità una singolo momento.  
  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] include i tipi <xref:System.DateTime>, <xref:System.DateTimeOffset>, <xref:System.TimeSpan> e <xref:System.TimeZoneInfo>, che possono tutti essere usati per compilare applicazioni in grado di funzionare con date e ore.  
  
> [!NOTE]
>  Questo argomento non descrive un quarto tipo, <xref:System.TimeZone>, la cui funzionalità è quasi interamente integrata nella classe <xref:System.TimeZoneInfo>. Quando è possibile, gli sviluppatori devono usare la classe <xref:System.TimeZoneInfo> invece della classe <xref:System.TimeZone>.  
  
## Struttura DateTime  
 Un valore <xref:System.DateTime> definisce una data e un'ora specifiche. A partire dalla versione 2.0, [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] include la proprietà <xref:System.DateTime.Kind%2A> che fornisce informazioni limitate sul fuso orario cui appartengono la data e l'ora. Il valore <xref:System.DateTimeKind> restituito dalla proprietà <xref:System.DateTime.Kind%2A> indica se il valore <xref:System.DateTime> rappresenta l'ora locale \(<xref:System.DateTimeKind?displayProperty=fullName>\), l'ora UTC \(Coordinated Universal Time\) \(<xref:System.DateTimeKind?displayProperty=fullName>\) o un'ora non specificata \(<xref:System.DateTimeKind?displayProperty=fullName>\).  
  
 La struttura <xref:System.DateTime> è adatta per le applicazioni che hanno le caratteristiche seguenti:  
  
-   Usano solo date.  
  
-   Usano solo ore.  
  
-   Usano date e ore astratte.  
  
-   Usano date e ore per le quali mancano informazioni sul fuso orario.  
  
-   Usano solo date e ore UTC.  
  
-   Recuperano informazioni su data e ora da origini esterne a [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], come i database SQL. In genere, queste origini archiviano le informazioni su data e ora in un formato semplice, compatibile con la struttura <xref:System.DateTime>.  
  
-   Eseguono operazioni aritmetiche su date e ore, ma con particolare attenzione ai risultati generali. Ad esempio, in un'operazione di addizione che aggiunge sei mesi a una data e un'ora specifiche, spesso non è importante se il risultato viene adattato per l'ora legale.  
  
 A meno che un determinato valore <xref:System.DateTime> non rappresenti un'ora UTC, il valore di data e ora è spesso ambiguo e limitato in fatto di portabilità. Ad esempio, se un valore <xref:System.DateTime> rappresenta l'ora locale, è portabile solo all'interno del fuso orario locale. Di conseguenza, se il valore viene deserializzato in un altro sistema con lo stesso fuso orario, identifica comunque un singolo momento senza ambiguità. Al di fuori del fuso orario locale, tale valore <xref:System.DateTime> è soggetto a più interpretazioni. Se la proprietà <xref:System.DateTime.Kind%2A> del valore è <xref:System.DateTimeKind?displayProperty=fullName>, il valore è ancora meno portabile, in quanto è ora ambiguo all'interno dello stesso fuso orario e probabilmente anche nello stesso sistema in cui è stato inizialmente serializzato. Solo se un valore <xref:System.DateTime> rappresenta un'ora UTC, identifica senza ambiguità un singolo momento, indipendentemente dal sistema o dal fuso orario in cui viene usato.  
  
> [!IMPORTANT]
>  Quando si salvano o condividono dati <xref:System.DateTime>, è consigliabile usare UTC e la proprietà <xref:System.DateTime.Kind%2A> del valore <xref:System.DateTime> deve essere impostata su <xref:System.DateTimeKind?displayProperty=fullName>.  
  
## Struttura DateTimeOffset  
 La struttura <xref:System.DateTimeOffset> rappresenta un valore di data e ora, insieme a un offset che indica la differenza di tale valore rispetto all'ora UTC. In questo modo, il valore identifica sempre senza ambiguità un singolo momento.  
  
 Il tipo <xref:System.DateTimeOffset> include tutte le funzionalità del tipo <xref:System.DateTime> insieme alla compatibilità del fuso orario. Lo rende adatto per le applicazioni che hanno le caratteristiche seguenti:  
  
-   Identificano in modo univoco e non ambiguo un singolo momento. Il tipo <xref:System.DateTimeOffset> può essere usato per definire senza ambiguità il significato di "adesso", per registrare data e ora delle transazioni, del sistema o degli eventi delle applicazioni, nonché registrare data e ora di creazione e modifica dei file.  
  
-   Eseguono operazioni aritmetiche su data e ora.  
  
-   Mantengono più date e ore correlate, purché vengano archiviate come due valori separati o due membri di una struttura.  
  
> [!NOTE]
>  Questi utilizzi per i valori <xref:System.DateTimeOffset> sono molto più comuni di quelli per i valori <xref:System.DateTime>. Di conseguenza, <xref:System.DateTimeOffset> deve essere considerato il tipo di data e ora predefinito per lo sviluppo di applicazioni.  
  
 Un valore <xref:System.DateTimeOffset> non è associato a un determinato fuso orario, ma può derivare da svariati fusi orari diversi. Per illustrare questo concetto, l'esempio seguente elenca i fusi orari cui può appartenere un certo numero di valori <xref:System.DateTimeOffset> \(incluso un valore con ora solare Pacifico locale\).  
  
 [!code-csharp[System.DateTimeOffset.Conceptual#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual1.cs#1)]
 [!code-vb[System.DateTimeOffset.Conceptual#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual1.vb#1)]  
  
 L'output mostra che ogni valore di data e ora nell'esempio può appartenere almeno a tre fusi orari diversi. Il valore <xref:System.DateTimeOffset> 6\/10\/2007 mostra che se un valore di data e ora rappresenta un orario con ora legale, il suo offset dall'ora UTC non corrisponde necessariamente all'offset UTC di base del fuso orario di origine o all'offset dall'ora UTC indicato nel nome visualizzato. Questo significa che poiché un singolo valore <xref:System.DateTimeOffset> non è strettamente collegato al proprio fuso orario, non può indicare la transizione di un fuso orario da e verso l'ora legale. Questo comportamento può rivelarsi particolarmente problematico quando vengono usate operazioni aritmetiche per date e ore per modificare un valore <xref:System.DateTimeOffset>. Per informazioni su come eseguire operazioni aritmetiche per date e ore che tengano conto delle regole di adeguamento del fuso orario, vedere [Esecuzione di operazioni aritmetiche con date e ore](../../../docs/standard/datetime/performing-arithmetic-operations.md).  
  
## Struttura TimeSpan  
 La struttura <xref:System.TimeSpan> rappresenta un intervallo di tempo. Ecco i due utilizzi tipici:  
  
-   Indicare l'intervallo di tempo tra due valori di data e ora. Ad esempio, la sottrazione di un valore <xref:System.DateTime> da un altro restituisce un valore <xref:System.TimeSpan>.  
  
-   Misurare il tempo trascorso. Ad esempio, la proprietà <xref:System.Diagnostics.Stopwatch.Elapsed%2A?displayProperty=fullName> restituisce un valore <xref:System.TimeSpan> che indica l'intervallo di tempo trascorso dalla chiamata a uno dei metodi <xref:System.Diagnostics.Stopwatch> che inizia a misurare il tempo trascorso.  
  
 Un valore <xref:System.TimeSpan> può essere usato anche come sostituzione per un valore <xref:System.DateTime> quando tale valore indica un momento senza riferimento a una determinata ora del giorno. Questo utilizzo è simile alle proprietà <xref:System.DateTime.TimeOfDay%2A?displayProperty=fullName> e <xref:System.DateTimeOffset.TimeOfDay%2A?displayProperty=fullName>, che restituiscono un valore <xref:System.TimeSpan> che rappresenta l'ora senza riferimento a una data. Ad esempio, la struttura <xref:System.TimeSpan> può essere usata per indicare l'ora di apertura o di chiusura di un negozio oppure per rappresentare l'ora a cui si verifica un evento regolare.  
  
 L'esempio seguente definisce una struttura `StoreInfo` che include oggetti <xref:System.TimeSpan> per le ore di apertura e di chiusura di un negozio, nonché un oggetto <xref:System.TimeZoneInfo> che rappresenta il fuso orario del negozio. La struttura include anche due metodi, `IsOpenNow` e `IsOpenAt`, che indicano se il negozio è aperto a un'ora specificata dall'utente, che si suppone si trovi nel fuso orario locale.  
  
 [!code-csharp[Conceptual.ChoosingDates#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.choosingdates/cs/datetimereplacement1.cs#1)]
 [!code-vb[Conceptual.ChoosingDates#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.choosingdates/vb/datetimereplacement1.vb#1)]  
  
 La struttura `StoreInfo` può quindi essere usata da codice client simile al seguente.  
  
 [!code-csharp[Conceptual.ChoosingDates#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.choosingdates/cs/datetimereplacement1.cs#2)]
 [!code-vb[Conceptual.ChoosingDates#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.choosingdates/vb/datetimereplacement1.vb#2)]  
  
## Classe TimeZoneInfo  
 La classe <xref:System.TimeZoneInfo> rappresenta uno dei fusi orari della terra e permette la conversione di qualsiasi data e ora di un fuso orario negli equivalenti di un altro fuso orario. La classe <xref:System.TimeZoneInfo> permette di usare date e ore in modo che qualsiasi valore di data e ora identifichi un singolo momento senza ambiguità. La classe <xref:System.TimeZoneInfo> può anche essere estesa. Benché dipenda dalle informazioni sul fuso orario fornite per i sistemi Windows e definite nel Registro di sistema, questa classe supporta la creazione di fusi orari personalizzati. Supporta anche la serializzazione e la deserializzazione delle informazioni sul fuso orario.  
  
 In alcuni casi, per sfruttare tutti i vantaggi della classe <xref:System.TimeZoneInfo> possono essere necessarie attività aggiuntive di sviluppo. Innanzitutto, i valori di data e ora non sono strettamente collegati ai fusi orari cui appartengono. Di conseguenza, a meno che l'applicazione non fornisca un meccanismo per collegare una data e un'ora al fuso orario associato, è facile che una data e un'ora specifiche non risultino associate al rispettivo fuso orario. Un metodo per collegare queste informazioni consiste nel definire una classe o una struttura che contiene sia i valori di data e ora sia l'oggetto fuso orario associato. In secondo luogo, in Windows XP e nelle versioni precedenti di Windows non è disponibile supporto effettivo per le informazioni cronologiche sul fuso orario, mentre [!INCLUDE[windowsver](../../../includes/windowsver-md.md)] offre solo supporto limitato. Le applicazioni progettate per gestire informazioni cronologiche su date e ore devono usare in modo esteso fusi orari personalizzati.  
  
 L'uso del supporto per i fusi orari in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] è possibile solo se il fuso orario cui appartengono la data e l'ora è noto quando viene creata un'istanza dell'oggetto data e ora. Questo è un caso piuttosto raro, in particolare nelle applicazioni Web o di rete.  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)