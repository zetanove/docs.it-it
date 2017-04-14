---
title: "How to: Cancel a PLINQ Query | Microsoft Docs"
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
  - "PLINQ queries, how to cancel"
  - "cancellation, PLINQ"
ms.assetid: 80b14640-edfa-4153-be1b-3e003d3e9c1a
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# How to: Cancel a PLINQ Query
Negli esempi seguenti vengono mostrati due modi per annullare una query PLINQ.  Nel primo esempio viene mostrato come annullare una query che consiste principalmente nell'attraversamento di dati.  Nel secondo esempio viene mostrato come annullare una query che contiene una funzione utente dispendiosa in termini di calcolo.  
  
> [!NOTE]
>  Quando viene abilitato "Just My Code", Visual Studio si interromperà in corrispondenza della riga che genera l'eccezione e in cui viene visualizzato un messaggio di errore che indica che l'eccezione non è gestita dal codice utente. Questo errore è benigno.  È possibile premere F5 per continuare e visualizzare il comportamento di gestione delle eccezioni illustrato negli esempi riportati di seguito.  Per impedire l'interruzione di Visual Studio al primo errore, deselezionare semplicemente la casella di controllo "Just My Code" in **Strumenti, Opzioni, Debug, Generale**.  
>   
>  Lo scopo di questo esempio è dimostrare l'utilizzo e potrebbe non essere eseguito più velocemente dell'equivalente query LINQ to Objects sequenziale.  Per ulteriori informazioni sull'aumento di velocità, vedere [Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md).  
  
## Esempio  
 [!code-csharp[PLINQ#16](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#16)]
 [!code-vb[PLINQ#16](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#16)]  
  
 Il framework PLINQ non include alcun <xref:System.OperationCanceledException> in un oggetto <xref:System.AggregateException?displayProperty=fullName>. È necessario gestire <xref:System.OperationCanceledException> in un blocco catch a parte.  Se almeno un delegato dell'utente genera un oggetto OperationCanceledException\(externalCT\) tramite un oggetto <xref:System.Threading.CancellationToken?displayProperty=fullName> esterno senza tuttavia generare nessun'altra eccezione e la query è stata definita come `AsParallel().WithCancellation(externalCT)`, PLINQ genererà un solo oggetto <xref:System.OperationCanceledException>\(externalCT\) anziché un oggetto <xref:System.AggregateException?displayProperty=fullName>.  Tuttavia, se un determinato delegato dell'utente genera un oggetto <xref:System.OperationCanceledException> e un altro delegato genera un altro tipo di eccezione, entrambe le eccezioni verranno incluse in un oggetto <xref:System.AggregateException>.  
  
 La linea guida generale per quanto riguarda l'annullamento è:  
  
1.  Se si esegue l'annullamento tramite un delegato dell'utente è necessario segnalare a PLINQ l'oggetto <xref:System.Threading.CancellationToken> esterno e generare un oggetto <xref:System.OperationCanceledException>\(externalCT\).  
  
2.  Se si verifica l'annullamento e non vengono generate altre eccezioni è necessario gestire un oggetto <xref:System.OperationCanceledException> anziché un oggetto <xref:System.AggregateException>.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come gestire l'annullamento quando il codice utente contiene una funzione dispendiosa in termini di calcolo.  
  
 [!code-csharp[PLINQ#17](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#17)]
 [!code-vb[PLINQ#17](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#17)]  
  
 Quando si gestisce l'annullamento nel codice utente, non è necessario utilizzare <xref:System.Linq.ParallelEnumerable.WithCancellation%2A> nella definizione della query.  Tuttavia, poiché <xref:System.Linq.ParallelEnumerable.WithCancellation%2A> non influisce in alcun modo sulle prestazioni di esecuzione delle query e consente la gestione dell'annullamento tramite gli operatori di query e il codice utente, è consigliabile utilizzarlo.  
  
 Per garantire la capacità di risposta del sistema è consigliabile verificare l'annullamento con una frequenza di circa una volta al millisecondo. Tuttavia, qualsiasi periodo minore o uguale a 10 millisecondi è considerato accettabile.  Questa frequenza probabilmente non influirà negativamente sulle prestazioni del codice.  
  
 Quando un enumeratore viene eliminato, ad esempio quando il codice esce da un ciclo foreach \(For Each in Visual Basic\) che sta scorrendo i risultati della query, la query viene annullata automaticamente senza che venga generata alcuna eccezione.  
  
## Vedere anche  
 <xref:System.Linq.ParallelEnumerable>   
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)   
 [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)