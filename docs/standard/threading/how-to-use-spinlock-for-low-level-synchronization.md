---
title: "How to: Use SpinLock for Low-Level Synchronization | Microsoft Docs"
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
  - "SpinLock, how to use"
ms.assetid: a9ed3e4e-4f29-4207-b730-ed0a51ecbc19
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# How to: Use SpinLock for Low-Level Synchronization
Nell'esempio seguente viene illustrato come utilizzare un oggetto <xref:System.Threading.SpinLock>.  
  
## Esempio  
 In questo esempio la sezione di importanza principale esegue una quantità minima di lavoro e pertanto risulta essere un ottimo candidato per <xref:System.Threading.SpinLock>.  Se si aumenta il lavoro di una piccola quantità si ottiene un aumento delle prestazioni di <xref:System.Threading.SpinLock> rispetto a un blocco standard.  Tuttavia, esiste un punto in cui SpinLock diventa più oneroso di un blocco standard.  È possibile utilizzare la nuova funzionalità di profilo della concorrenza, presente negli strumenti per la profilatura, per vedere quale tipo di blocco fornisce le prestazioni migliori nel programma.  Per ulteriori informazioni, vedere [Visualizzatore di concorrenze](../Topic/Concurrency%20Visualizer.md).  
  
 [!code-csharp[CDS_SpinLock#02](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinlock/cs/spinlockdemo.cs#02)]
 [!code-vb[CDS_SpinLock#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinlock/vb/spinlock_vb.vb#02)]  
  
 <xref:System.Threading.SpinLock> potrebbe essere utile quando un blocco su una risorsa condivisa non verrà mantenuto per molto tempo.  In questi casi, nei computer multicore uno spin di alcuni cicli del thread bloccato fino al rilascio del blocco può risultare efficiente.  Lo spin impedisce il blocco del thread, un processo che richiede un elevato consumo della CPU.  Per impedire l'esaurimento di risorse dei processori logici o l'inversione di priorità nei sistemi con Hyper\-Threading, <xref:System.Threading.SpinLock> interromperà lo spin in determinate condizioni.  
  
 In questo esempio viene utilizzata la classe <xref:System.Collections.Generic.Queue%601?displayProperty=fullName> che richiede la sincronizzazione dell'utente per l'accesso multithreading.  Nelle applicazioni destinate a .NET Framework versione 4, un'altra possibilità è utilizzare <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=fullName>, poiché non richiede blocchi utente.  
  
 Si noti l'utilizzo di `false` \(`False` in Visual Basic\) nella chiamata a <xref:System.Threading.SpinLock.Exit%2A>.  Ciò fornisce le migliori prestazioni.  Specificare `true` \(`True`\) nelle architetture IA64 per utilizzare il limite di memoria che scarica il buffer di scrittura per assicurarsi che il blocco sia ora disponibile per l'uscita di altri thread.  
  
## Vedere anche  
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)