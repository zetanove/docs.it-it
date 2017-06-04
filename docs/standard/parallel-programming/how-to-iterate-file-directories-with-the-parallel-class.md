---
title: "Procedura: scorrere le directory dei file con la classe Parallel | Microsoft Docs"
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
  - "cicli paralleli, come scorrere le directory"
ms.assetid: 555e9f48-f53d-4774-9bcf-3e965c732ec5
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: scorrere le directory dei file con la classe Parallel
In molti casi, l'iterazione di file è un'operazione che può essere facilmente parallelizzata.  Nell'argomento [How to: Iterate File Directories with PLINQ](../../../docs/standard/parallel-programming/how-to-iterate-file-directories-with-plinq.md) viene illustrato il modo più semplice per eseguire questa attività per molti scenari.  Quando tuttavia il codice deve gestire i molti tipi di eccezioni che possono essere generate durante l'accesso al file system, è possibile che si verifichino alcuni problemi.  Nell'esempio seguente viene illustrato un possibile approccio al problema.  Per l'attraversamento di tutti i file e tutte le cartelle in una directory specifica viene utilizzata un'iterazione basata su stack, consentendo al codice di intercettare e gestire diverse eccezioni.  Naturalmente, la modalità di gestione delle eccezioni compete all'utente.  
  
## Esempio  
 Nell'esempio seguente le directory vengono iterate in modo sequenziale, ma i file vengono processati in parallelo.  Questo è probabilmente il migliore approccio nel caso di un rapporto elevato tra file e directory.  È inoltre possibile parallelizzare l'iterazione delle directory e accedere a ogni file in sequenza.  La parallelizzazione di entrambi i cicli non è probabilmente una scelta efficiente se la destinazione non è un computer specifico con un numero elevato di processori.  Come sempre, è tuttavia consigliabile testare l'applicazione completamente per determinare quale sia l'approccio migliore.  
  
 [!code-csharp[TPL_Parallel#08](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/parallel_file.cs#08)]
 [!code-vb[TPL_Parallel#08](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/fileiteration08.vb#08)]  
  
 In questo esempio le operazioni di I\/O dei file vengono eseguite in modo sincrono.  Nel caso di file di grandi dimensioni o di connessioni di rete lente, potrebbe essere preferibile accedere ai file in modo asincrono.  L'iterazione parallela può essere combinata con tecniche di I\/O asincrono.  Per ulteriori informazioni, vedere [TPL and Traditional .NET Framework Asynchronous Programming](../../../docs/standard/parallel-programming/tpl-and-traditional-async-programming.md).  
  
 Nell'esempio viene utilizzata la variabile locale `fileCount` per gestire il conteggio del numero totale di file elaborati.  Poiché la variabile può essere acceduta contemporaneamente da più attività, l'accesso è sincronizzato chiamando il metodo <xref:System.Threading.Interlocked.Add%2A?displayProperty=fullName>.  
  
 Si noti che, se viene generata un'eccezione nel thread principale, i thread avviati dal metodo <xref:System.Threading.Tasks.Parallel.ForEach%2A> possono rimanere in esecuzione.  Per arrestare tali thread, è possibile impostare una variabile booleana nei gestori di eccezioni e verificarne il valore in ogni iterazione del ciclo parallelo.  Se il valore indica che è stata generata un'eccezione, utilizzare la variabile <xref:System.Threading.Tasks.ParallelLoopState> per uscire dal ciclo o arrestarlo.  Per ulteriori informazioni, vedere [How to: Stop or Break from a Parallel.For Loop](http://msdn.microsoft.com/it-it/de52e4f1-9346-4ad5-b582-1a4d54dc7f7e).  
  
## Vedere anche  
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)