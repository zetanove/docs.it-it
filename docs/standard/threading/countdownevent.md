---
title: "CountdownEvent | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "synchronization primitives, CountdownEvent"
ms.assetid: eec3812a-e20f-4ecd-bfef-6921d508b708
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# CountdownEvent
<xref:System.Threading.CountdownEvent?displayProperty=fullName> è una primitiva di sincronizzazione che sblocca i thread in attesa dopo essere stata segnalata un determinato numero di volte.  <xref:System.Threading.CountdownEvent> è progettato per scenari nei quali si dovrebbe altrimenti utilizzare un oggetto <xref:System.Threading.ManualResetEvent> o <xref:System.Threading.ManualResetEventSlim> e diminuire manualmente una variabile prima di segnalare l'evento.  Ad esempio, in uno scenario di divisione\/unione, è possibile creare un oggetto <xref:System.Threading.CountdownEvent> con un conteggio segnali pari a 5, quindi avviare cinque elementi di lavoro nel pool di thread e fare in modo che ogni elemento di lavoro chiami <xref:System.Threading.CountdownEvent.Signal%2A> quando viene completato.  Ogni chiamata a <xref:System.Threading.CountdownEvent.Signal%2A> diminuisce di 1 il conteggio segnali.  Nel thread principale, la chiamata a <xref:System.Threading.CountdownEvent.Wait%2A> si bloccherà fino a che il conteggio segnali non sarà zero.  
  
> [!NOTE]
>  Nel caso di codice che non deve interagire con le API di sincronizzazione di .NET Framework legacy, considerare l'utilizzo di oggetti <xref:System.Threading.Tasks.Task?displayProperty=fullName> e\/o del metodo <xref:System.Threading.Tasks.Parallel.Invoke%2A> per un approccio ancora più semplice all'espressione del parallelismo di divisione\-unione.  
  
 <xref:System.Threading.CountdownEvent> presenta le seguenti funzionalità aggiuntive:  
  
-   L'operazione di attesa può essere annullata tramite token di annullamento.  
  
-   Il conteggio segnali può essere incrementato dopo la creazione dell'istanza.  
  
-   Una volta che <xref:System.Threading.CountdownEvent.Wait%2A> è stato restituito mediante la chiamata al metodo <xref:System.Threading.CountdownEvent.Reset%2A>, le istanze possono essere riutilizzate.  
  
-   Le istanze espongono un oggetto <xref:System.Threading.WaitHandle> per l'integrazione con altre API di sincronizzazione di .NET Framework, ad esempio <xref:System.Threading.WaitHandle.WaitAll%2A>.  
  
## Utilizzo di base  
 Nell'esempio seguente viene illustrato come utilizzare un oggetto <xref:System.Threading.CountdownEvent> con elementi di lavoro <xref:System.Threading.ThreadPool>.  
  
 [!code-csharp[CDS_CountdownEvent#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_countdownevent/cs/countdownevent.cs#01)]
 [!code-vb[CDS_CountdownEvent#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_countdownevent/vb/module1.vb#01)]  
  
## CountdownEvent con annullamento  
 Nell'esempio seguente viene illustrato come annullare l'operazione di attesa su <xref:System.Threading.CountdownEvent> tramite un token di annullamento.  Il modello di base segue il modello dell'annullamento unificato, introdotto in [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)].  Per ulteriori informazioni, vedere [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md).  
  
 [!code-csharp[CDS_CountdownEvent#02](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_countdownevent/cs/countdownevent.cs#02)]
 [!code-vb[CDS_CountdownEvent#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_countdownevent/vb/canceleventwait.vb#02)]  
  
 L'operazione di attesa non annulla i thread di segnalazione.  In genere, l'annullamento è applicato a un'operazione logica e ciò può includere l'attesa nell'evento e tutti gli elementi di lavoro che l'attesa sta sincronizzando.  In questo esempio, a ogni elemento di lavoro viene passata una copia dello stesso token di annullamento in modo che possa rispondere alla richiesta di annullamento.  
  
## Vedere anche  
 [EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent](../../../docs/standard/threading/eventwaithandle-autoresetevent-countdownevent-manualresetevent.md)