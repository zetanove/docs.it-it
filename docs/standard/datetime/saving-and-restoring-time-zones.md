---
title: "Salvataggio e ripristino dei fusi orari | Microsoft Docs"
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
  - "deserializzazione [.NET Framework], fusi orari"
  - "ripristino di fusi orari"
  - "salvataggio di fusi orari"
  - "serializzazione [.NET Framework], fusi orari"
  - "fusi orari (oggetti) [.NET Framework], deserializzazione"
  - "fusi orari (oggetti) [.NET Framework], ripristino"
  - "fusi orari (oggetti) [.NET Framework], salvataggio"
  - "fusi orari (oggetti) [.NET Framework], serializzazione"
  - "fusi orari [.NET Framework], ripristino"
  - "fusi orari [.NET Framework], salvataggio"
ms.assetid: 4028b310-e7ce-49d4-a646-1e83bfaf6f9d
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Salvataggio e ripristino dei fusi orari
La classe <xref:System.TimeZoneInfo> si basa sul Registro di sistema per recuperare i dati predefiniti del fuso orario,  sebbene il Registro di sistema sia una struttura dinamica.  Inoltre, le informazioni del fuso orario contenute nel Registro di sistema vengono utilizzate dal sistema operativo principalmente per gestire le regolazioni e le conversioni di fusi orari per l'anno corrente.  Ciò comporta due principali implicazioni per le applicazioni che si basano su dati del fuso orario accurati:  
  
-   È possibile che un fuso orario richiesto da un'applicazione non sia definito nel Registro di sistema o che sia stato rinominato o rimosso dal Registro di sistema.  
  
-   È possibile che un fuso orario definito nel Registro di sistema non contenga le informazioni su determinate regole di regolazione necessarie per le conversioni di fusi orari storici.  
  
 La classe <xref:System.TimeZoneInfo> risolve tali limitazioni grazie al supporto della serializzazione \(salvataggio\) e della deserializzazione \(ripristino\) dei dati del fuso orario.  
  
## Serializzazione e deserializzazione del fuso orario  
 Il salvataggio e il ripristino di un fuso orario serializzando e deserializzando i dati del fuso orario comportano solo due chiamate al metodo:  
  
-   È possibile serializzare un oggetto <xref:System.TimeZoneInfo> chiamando il metodo <xref:System.TimeZoneInfo.ToSerializedString%2A> di tale oggetto.  Il metodo non accetta alcun parametro e restituisce una stringa che contiene le informazioni del fuso orario.  
  
-   È possibile deserializzare un oggetto <xref:System.TimeZoneInfo> da una stringa serializzata passando tale stringa al metodo `static` \(`Shared` in Visual Basic\) <xref:System.TimeZoneInfo.FromSerializedString%2A?displayProperty=fullName>.  
  
## Scenari di serializzazione e deserializzazione  
 La possibilità di salvare \(o serializzare\) un oggetto <xref:System.TimeZoneInfo> in una stringa e di ripristinarlo \(o deserializzarlo\) per un uso successivo aumenta l'utilità e la flessibilità della classe <xref:System.TimeZoneInfo>.  In questa sezione vengono esaminate alcune situazioni in cui la serializzazione e la deserializzazione sono molto utili.  
  
### Serializzazione e deserializzazione dei dati del fuso orario in un'applicazione  
 Un fuso orario serializzato può essere ripristinato da una stringa quando necessario.  Tale operazione potrebbe risultare necessaria quando il fuso orario recuperato dal Registro di sistema non è in grado di convertire correttamente una data e ora all'interno di un determinato intervallo di date.  Ad esempio, i dati del fuso orario nel Registro di sistema di Windows XP supportano una sola regola di regolazione, mentre i fusi orari definiti nel Registro di sistema di Windows Vista forniscono generalmente informazioni su due regole di regolazione.  Ciò significa che le conversioni di fusi orari storici potrebbero essere imprecise.  La serializzazione e la deserializzazione dei dati del fuso orario possono gestire tale limitazione.  
  
 Nell'esempio seguente, una classe personalizzata <xref:System.TimeZoneInfo> senza regole di regolazione viene definita per rappresentare il fuso orario standard degli Stati Uniti orientali dal 1883 al 1917, prima dell'introduzione dell'ora legale Stati Uniti.  Il fuso orario personalizzato viene serializzato in una variabile con ambito globale.  L'ora UTC viene passata al metodo di conversione del fuso orario, `ConvertUtcTime`, per essere convertita.  Se la data e l'ora rientrano nel 1917 o in un anno precedente, il fuso Ora solare orientale personalizzato viene ripristinato da una stringa serializzata e sostituisce il fuso orario recuperato dal Registro di sistema.  
  
 [!code-csharp[System.TimeZone2.Serialization.1#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Serialization.1/cs/Serialization.cs#1)]
 [!code-vb[System.TimeZone2.Serialization.1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Serialization.1/vb/Serialization.vb#1)]  
  
### Gestione delle eccezioni del fuso orario  
 Poiché il Registro di sistema è una struttura dinamica, il contenuto è soggetto a modifiche accidentali o intenzionali,  ovvero è possibile che un fuso orario, che dovrebbe essere definito nel Registro di sistema e necessario per la corretta esecuzione di un'applicazione, sia assente.  Senza il supporto della serializzazione e della deserializzazione del fuso orario non si ha altra scelta che terminare l'applicazione per gestire l'eccezione <xref:System.TimeZoneNotFoundException>.  Grazie alla serializzazione e alla deserializzazione del fuso orario è, tuttavia, possibile gestire un'eccezione <xref:System.TimeZoneNotFoundException> imprevista ripristinando il fuso orario necessario da una stringa serializzata in modo da poter continuare l'esecuzione dell'applicazione.  
  
 Nell'esempio seguente viene creato e serializzato un fuso Ora solare fuso centrale personalizzato.  Viene poi effettuato un tentativo di recuperare il fuso Ora solare fuso centrale dal Registro di sistema.  Se l'operazione di recupero genera un'eccezione <xref:System.TimeZoneNotFoundException> o un'eccezione <xref:System.InvalidTimeZoneException>, il gestore di eccezioni deserializza il fuso orario.  
  
 [!code-csharp[System.TimeZone2.Serialization.2#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Serialization.2/cs/Serialization2.cs#1)]
 [!code-vb[System.TimeZone2.Serialization.2#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Serialization.2/vb/Serialization2.vb#1)]  
  
### Archiviazione e ripristino di una stringa serializzata quando necessario  
 Negli esempi precedenti le informazioni del fuso orario sono state archiviate in una variabile di stringa e ripristinate quando necessario.  La stringa che contiene le informazioni del fuso orario serializzato può a sua volta essere archiviata in un supporto di archiviazione, ad esempio un file esterno, un file di risorse incorporato nell'applicazione o il Registro di sistema. Notare che le informazioni sui fusi orari personalizzati devono essere archiviate separatamente dalle chiavi del fuso orario del Registro di sistema.  
  
 Se si archivia la stringa del fuso orario serializzato in questo modo, si separa anche la routine di creazione del fuso orario dall'applicazione stessa.  Ad esempio, una routine di creazione del fuso orario può eseguire e creare un file di dati che contiene le informazioni sui fusi orari storici utilizzate da un'applicazione.  Il file di dati può quindi essere installato con l'applicazione ed essere aperto deserializzando uno o più fusi orari quando richiesto dall'applicazione.  
  
 Per un esempio che utilizza una risorsa incorporata per archiviare i dati dei fusi orari serializzati, vedere [Procedura: salvare fusi orari in una risorsa incorporata](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md) e [Procedura: ripristinare i fusi orari da una risorsa incorporata](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md).  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)