---
title: "Interop with Other Asynchronous Patterns and Types | Microsoft Docs"
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
  - ".NET Framework, and TAP"
  - "asynchronous design patterns, .NET Framework"
  - "TAP, .NET Framework support for"
  - "Task-based Asynchronous Pattern, .NET Framework support for"
  - ".NET Framework, asynchronous design patterns"
ms.assetid: f120a5d9-933b-4d1d-acb6-f034a57c3749
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Interop with Other Asynchronous Patterns and Types
In .NET Framework 1.0 è stato introdotto il modello <xref:System.IAsyncResult>, altrimenti noto come [Asynchronous Programming Model \(APM\)](../../../docs/standard/asynchronous-programming-patterns/asynchronous-programming-model-apm.md) o modello `Begin/End`.  In .NET Framework 2.0 è stato aggiunto [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md).  A partire da .NET Framework 4, [Task\-based Asynchronous Pattern \(TAP\)](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md) sostituisce sia APM che EAP, ma consente di compilare facilmente le routine di migrazione dai modelli precedenti.  
  
 Contenuto dell'argomento:  
  
-   [Attività e APM](#APM) \([da APM a TAP](#ApmToTap) o [da TAP ad APM](#TapToApm)\)  
  
-   [Attività e EAP](#EAP)  
  
-   [Attività e handle di attesa](#WaitHandles) \([da handle di attesa a TAP](#WHToTap) o [da TAP a handle di attesa](#TapToWH)\)  
  
<a name="APM"></a>   
## Attività e modelli di programmazione asincrona \(APM\)  
  
<a name="ApmToTap"></a>   
### Da APM a TAP  
 Poiché il modello [Asynchronous Programming Model \(APM\)](../../../docs/standard/asynchronous-programming-patterns/asynchronous-programming-model-apm.md) è molto strutturato, è piuttosto facile compilare un wrapper per esporre l'implementazione APM come implementazione di TAP. Di fatto, .NET Framework, a partire da [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], include le routine di supporto sotto forma di overload del metodo <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A> per fornire questa conversione.  
  
 Si consideri la classe <xref:System.IO.Stream> e i relativi metodi <xref:System.IO.Stream.BeginRead%2A> e <xref:System.IO.Stream.EndRead%2A>, che rappresentano l'equivalente di APM del metodo sincrono <xref:System.IO.Stream.Read%2A>:  
  
 [!code-csharp[Conceptual.AsyncInterop#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Stream1.cs#1)]
 [!code-vb[Conceptual.AsyncInterop#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/stream1.vb#1)]  
[!code-csharp[Conceptual.AsyncInterop#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Stream1.cs#2)]
[!code-vb[Conceptual.AsyncInterop#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/stream1.vb#2)]  
[!code-csharp[Conceptual.AsyncInterop#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Stream1.cs#3)]
[!code-vb[Conceptual.AsyncInterop#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/stream1.vb#3)]  
  
 È possibile usare il metodo <xref:System.Threading.Tasks.TaskFactory%601.FromAsync%2A?displayProperty=fullName> per implementare un wrapper di TAP per questa operazione come segue:  
  
 [!code-csharp[Conceptual.AsyncInterop#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wrap1.cs#4)]
 [!code-vb[Conceptual.AsyncInterop#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wrap1.vb#4)]  
  
 Questa implementazione è simile alla seguente:  
  
 [!code-csharp[Conceptual.AsyncInterop#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wrap2.cs#5)]
 [!code-vb[Conceptual.AsyncInterop#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wrap2.vb#5)]  
  
<a name="TapToApm"></a>   
### Da TAP ad APM  
 Se l'infrastruttura esistente prevede il modello APM, sarà anche possibile creare un'implementazione di TAP e usarla dove è prevista un'implementazione APM.  Poiché le attività possono essere composte e tramite la classe <xref:System.Threading.Tasks.Task> viene implementato l'oggetto <xref:System.IAsyncResult>, a tal fine è possibile utilizzare una semplice funzione di supporto. Il codice seguente usa un'estensione della classe <xref:System.Threading.Tasks.Task%601>, ma è possibile usare una funzione quasi identica per le attività non generiche.  
  
 [!code-csharp[Conceptual.AsyncInterop#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM1.cs#6)]
 [!code-vb[Conceptual.AsyncInterop#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM1.vb#6)]  
  
 Ora, si consideri il caso in cui si dispone dell'implementazione di TAP:  
  
 [!code-csharp[Conceptual.AsyncInterop#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#7)]
 [!code-vb[Conceptual.AsyncInterop#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#7)]  
  
 e si desidera fornire questa implementazione APM:  
  
 [!code-csharp[Conceptual.AsyncInterop#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#8)]
 [!code-vb[Conceptual.AsyncInterop#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#8)]  
[!code-csharp[Conceptual.AsyncInterop#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#9)]
[!code-vb[Conceptual.AsyncInterop#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#9)]  
  
 Nell'esempio seguente viene illustrata una migrazione ad APM:  
  
 [!code-csharp[Conceptual.AsyncInterop#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#10)]
 [!code-vb[Conceptual.AsyncInterop#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#10)]  
  
<a name="EAP"></a>   
## Attività e modello asincrono basato su eventi \(EAP\)  
 Eseguire il wrapping di un'implementazione di [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md) è un'operazione più complessa dell'esecuzione del wrapping di un modello APM, perché il modello EAP è più variabile e meno strutturato del modello APM.  A dimostrazione di quanto detto, il codice seguente esegue il wrapping del metodo `DownloadStringAsync`.`DownloadStringAsync` accetta un URI, genera l'evento `DownloadProgressChanged` durante il download per comunicare diverse statistiche sullo stato di avanzamento e genera l'evento `DownloadStringCompleted` quando ha terminato.  Il risultato finale è una stringa che contiene il contenuto della pagina all'URI specificato.  
  
 [!code-csharp[Conceptual.AsyncInterop#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/EAP1.cs#11)]
 [!code-vb[Conceptual.AsyncInterop#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/EAP1.vb#11)]  
  
<a name="WaitHandles"></a>   
## Attività e handle di attesa  
  
<a name="WHToTap"></a>   
### Da handle di attesa a TAP  
 Sebbene gli handle di attesa non implementino un modello asincrono, gli sviluppatori avanzati possono usare la classe <xref:System.Threading.WaitHandle> e il metodo <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A?displayProperty=fullName> per le notifiche asincrone quando è impostato un handle di attesa.  È possibile eseguire il wrapping del metodo <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A> per abilitare un'alternativa basata su attività a qualsiasi attesa sincrona su un handle di attesa:  
  
 [!code-csharp[Conceptual.AsyncInterop#12](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wait1.cs#12)]
 [!code-vb[Conceptual.AsyncInterop#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wait1.vb#12)]  
  
 Con questo metodo, è possibile usare le implementazioni di <xref:System.Threading.WaitHandle> esistenti nei metodi asincroni.  Ad esempio, se si desidera limitare il numero di operazioni asincrone eseguite in un momento specifico, è possibile usare un semaforo \(oggetto <xref:System.Threading.SemaphoreSlim?displayProperty=fullName>\).  È possibile limitare a *N* il numero di operazioni eseguite contemporaneamente inizializzando il conteggio del semaforo a *N*, rimanendo in attesa del semaforo ogni volta che si desidera eseguire un'operazione e rilasciando il semaforo quando l'operazione è terminata:  
  
 [!code-csharp[Conceptual.AsyncInterop#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Semaphore1.cs#13)]
 [!code-vb[Conceptual.AsyncInterop#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Semaphore1.vb#13)]  
  
 È anche possibile creare un semaforo asincrono che non si basa sugli handle di attesa ma interagisce completamente con le attività. A questo scopo, è possibile usare tecniche quali quelle descritte in [Consuming the Task\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md) per basare le strutture dei dati su <xref:System.Threading.Tasks.Task>.  
  
<a name="TapToWH"></a>   
### Da TAP a handle di attesa  
 Come accennato in precedenza, la classe <xref:System.Threading.Tasks.Task> implementa <xref:System.IAsyncResult> e tale implementazione espone una proprietà <xref:System.Threading.Tasks.Task.System%23IAsyncResult%23AsyncWaitHandle%2A> che restituisce un handle di attesa che verrà impostato al completamento di <xref:System.Threading.Tasks.Task>.  È possibile ottenere un <xref:System.Threading.WaitHandle> per <xref:System.Threading.Tasks.Task> come segue:  
  
 [!code-csharp[Conceptual.AsyncInterop#14](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wait1.cs#14)]
 [!code-vb[Conceptual.AsyncInterop#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wait1.vb#14)]  
  
## Vedere anche  
 [Task\-based Asynchronous Pattern \(TAP\)](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)   
 [Implementing the Task\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/implementing-the-task-based-asynchronous-pattern.md)   
 [Consuming the Task\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md)