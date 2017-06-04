---
title: "SpinWait | Microsoft Docs"
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
  - "synchronization primitives, SpinWait"
ms.assetid: 36012f42-34e5-4f86-adf4-973f433ed6c6
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# SpinWait
<xref:System.Threading.SpinWait?displayProperty=fullName> è un tipo di sincronizzazione leggero che è possibile utilizzare in scenari di basso livello per evitare le transizioni del kernel e i cambi di contesto dispendiosi necessari per gli eventi del kernel.  Nei computer multicore, quando una risorsa non è destinata a essere conservata per lunghi periodi di tempo, può risultare più efficiente per un thread in attesa eseguire uno spin in modalità utente per alcune decine o centinaia di cicli, quindi ritentare di acquisire la risorsa.  Se la risorsa è disponibile dopo lo spin, saranno state risparmiate diverse migliaia di cicli.  Se la risorsa continua a non essere disponibile, sono stati utilizzati solo pochi cicli ed è ancora possibile accedere a un'attesa basata sul kernel.  Questa combinazione di spin e attesa viene talvolta definita *operazione di attesa a due fasi*.  
  
 <xref:System.Threading.SpinWait> è pensato per essere utilizzato con i tipi di .NET Framework che eseguono il wrapping di eventi del kernel quale ad esempio <xref:System.Threading.ManualResetEvent>.  <xref:System.Threading.SpinWait> può inoltre essere utilizzato da solo per la funzionalità di spin di base in un unico programma.  
  
 <xref:System.Threading.SpinWait> è più di un semplice ciclo vuoto.  Viene implementato con cautela per fornire un comportamento di spin corretto per i casi generici e inizializza esso stesso cambi di contesto se lo spin è sufficientemente lungo \(all'incirca la durata richiesta per una transizione del kernel\).  Nei computer singlecore, ad esempio, <xref:System.Threading.SpinWait> restituisce immediatamente la porzione di tempo del thread poiché lo spin blocca l'avanzamento in tutti i thread.  <xref:System.Threading.SpinWait> restituisce inoltre, anche nei computer multicore, per impedire che il thread in attesa blocchi i thread con priorità più alta o il Garbage Collector.  Pertanto, se si utilizza <xref:System.Threading.SpinWait> in un'operazione di attesa a due fasi, è consigliabile richiamare l'attesa del kernel prima che <xref:System.Threading.SpinWait> stesso avvii un cambio di contesto.  <xref:System.Threading.SpinWait> fornisce la proprietà <xref:System.Threading.SpinWait.NextSpinWillYield%2A>, che è possibile controllare prima di ogni chiamata a <xref:System.Threading.SpinWait.SpinOnce%2A>.  Se la proprietà restituisce `true`, avviare l'operazione Wait personalizzata.  Per un esempio, vedere [How to: Use SpinWait to Implement a Two\-Phase Wait Operation](../../../docs/standard/threading/how-to-use-spinwait-to-implement-a-two-phase-wait-operation.md).  
  
 Se non si esegue un'operazione di attesa a due fasi bensì solo uno spin finché non si verifica una condizione, è possibile abilitare <xref:System.Threading.SpinWait> per eseguirne i cambi di contesto in modo che sia un elemento positivo nell'ambiente del sistema operativo Windows.  Nell'esempio di base seguente viene illustrato un oggetto <xref:System.Threading.SpinWait> in un stack privo di blocchi.  Se occorre uno stack thread\-safe ad elevate prestazioni, utilizzare <xref:System.Collections.Concurrent.ConcurrentStack%601?displayProperty=fullName>.  
  
 [!code-csharp[CDS_SpinWait#05](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinwait/cs/spinwait.cs#05)]
 [!code-vb[CDS_SpinWait#05](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinwait/vb/cds_spinwait1.vb#05)]  
  
## Vedere anche  
 <xref:System.Threading.Thread.SpinWait%2A>   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)