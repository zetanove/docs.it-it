---
title: "Pausing and Resuming Threads | Microsoft Docs"
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
  - "resuming threads"
  - "threading [.NET Framework], pausing"
  - "pausing threads"
ms.assetid: 9fce4859-a19d-4506-b082-7dd0792688ca
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Pausing and Resuming Threads
Le tecniche più comuni per sincronizzare le attività dei thread consistono nel blocco e nel rilascio dei thread oppure nel blocco di oggetti o aree di codice.  Per altre informazioni su questi meccanismi di blocco, vedere [Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md).  
  
 È anche possibile fare in modo che i thread vengano sospesi automaticamente.  Quando i thread sono bloccati o sospesi, è possibile usare un'eccezione <xref:System.Threading.ThreadInterruptedException> per interromperne lo stato di attesa.  
  
## Metodo Thread.Sleep  
 Se si chiama il metodo <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName>, il thread corrente viene bloccato immediatamente per il numero di millisecondi passati a <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName>, cedendo il resto della porzione di tempo a un altro thread.  Un thread non può chiamare <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName> su un altro thread.  
  
 Se si chiama <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName> con <xref:System.Threading.Timeout.Infinite?displayProperty=fullName>, un thread rimarrà sospeso finché non verrà interrotto da un altro thread tramite una chiamata al metodo <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName> o finché non verrà terminato da <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName>.  
  
## Interruzione di thread  
 È possibile interrompere un thread in attesa chiamando il metodo <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName> sul thread bloccato per generare un'eccezione <xref:System.Threading.ThreadInterruptedException>, che fa uscire il thread dalla chiamata che lo blocca.  Il thread dovrebbe intercettare l'eccezione <xref:System.Threading.ThreadInterruptedException> ed eseguire le operazioni appropriate per continuare a funzionare.  Se il thread ignora l'eccezione, l'ambiente di esecuzione la intercetta e interrompe il thread.  
  
> [!NOTE]
>  Se il thread di destinazione non è bloccato al momento della chiamata del metodo <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName>, il thread non subisce interruzioni finché non viene bloccato.  Se il thread non si blocca, verrà completato senza subire alcuna interruzione.  
  
 Se un'attesa è di tipo gestito, sia <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName> che <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName> riporteranno immediatamente il thread allo stato di attività.  Nel caso di un'attesa non gestita, ad esempio un platform invoke alla funzione Win32 `WaitForSingleObject`, né <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName> né <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName> potrà assumere il controllo del thread fino alla restituzione o alla chiamata nel codice gestito.  Di seguito è descritto il comportamento nel codice gestito.  
  
-   <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName> fa uscire un thread da qualsiasi attesa e genera un'eccezione <xref:System.Threading.ThreadInterruptedException> nel thread di destinazione.  
  
-   <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName> è simile a <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName>, con la differenza che il primo determina la generazione di un'eccezione <xref:System.Threading.ThreadAbortException> sul thread.  Per informazioni dettagliate, vedere [Distruzione di thread](../../../docs/standard/threading/destroying-threads.md).  
  
## Metodi obsoleti Suspend e Resume  
 La classe <xref:System.Threading.Thread> include due metodi, <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> e <xref:System.Threading.Thread.Resume%2A?displayProperty=fullName>, per la sospensione e la ripresa di un thread.  Tuttavia, l'uso di questi metodi non è consigliabile.  
  
> [!IMPORTANT]
>  A partire da .NET Framework versione 2.0, i metodi <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> e <xref:System.Threading.Thread.Resume%2A?displayProperty=fullName> saranno contrassegnati come obsoleti e rimossi nelle versioni future.  
>   
>  I metodi <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> e <xref:System.Threading.Thread.Resume%2A?displayProperty=fullName> generalmente non sono utili per le applicazioni e non devono essere confusi con i meccanismi di sincronizzazione.  Poiché i metodi <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> e <xref:System.Threading.Thread.Resume%2A?displayProperty=fullName> non si basano sulla cooperazione del thread che viene controllato, sono estremamente intrusivi e possono causare alle applicazioni seri problemi come i deadlock, che si verificano ad esempio se si sospende un thread che contiene una risorsa richiesta da un altro thread.  
  
 Per alcune applicazioni è effettivamente necessario controllare la priorità dei thread per ottenere prestazioni migliori.  A tale scopo, si consiglia di usare la proprietà <xref:System.Threading.Thread.Priority%2A?displayProperty=fullName> anziché il metodo <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Threading.Thread>   
 <xref:System.Threading.ThreadInterruptedException>   
 <xref:System.Threading.ThreadAbortException>   
 [Threading](../../../docs/standard/threading/index.md)   
 [Using Threads and Threading](../../../docs/standard/threading/using-threads-and-threading.md)   
 [Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md)