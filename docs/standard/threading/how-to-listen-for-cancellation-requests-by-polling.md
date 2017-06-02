---
title: "How to: Listen for Cancellation Requests by Polling | Microsoft Docs"
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
  - "cancellation, how to poll for requests"
ms.assetid: c7f2f022-d08e-4e00-b4eb-ae84844cb1bc
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# How to: Listen for Cancellation Requests by Polling
Nell'esempio seguente viene illustrato un modo in cui il codice utente può eseguire il polling di un token di annullamento a intervalli regolari per verificare se l'annullamento è stato richiesto dal thread chiamante.  In questo esempio viene utilizzato il tipo <xref:System.Threading.Tasks.Task?displayProperty=fullName>, ma lo stesso modello è valido per le operazioni asincrone create direttamente dal tipo <xref:System.Threading.ThreadPool?displayProperty=fullName> o dal tipo <xref:System.Threading.Thread?displayProperty=fullName>.  
  
## Esempio  
 Il polling richiede un tipo di codice di ciclo o ricorsivo in grado di leggere periodicamente il valore della proprietà <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> booleana.  Se si utilizza il tipo <xref:System.Threading.Tasks.Task?displayProperty=fullName> e si attende il completamento dell'attività nel thread chiamante, è possibile utilizzare il metodo <xref:System.Threading.CancellationToken.ThrowIfCancellationRequested%2A> per controllare la proprietà e generare l'eccezione.  Utilizzando questo metodo, si garantisce che venga generata l'eccezione corretta in risposta a una richiesta.  Se si utilizza un oggetto <xref:System.Threading.Tasks.Task>, la chiamata a questo metodo è pertanto preferibile rispetto alla generazione manuale di un evento <xref:System.OperationCanceledException>.  Se non è necessario generare l'eccezione, è quindi sufficiente controllare la proprietà e ottenere un risultato dal metodo se la proprietà è `true`.  
  
 [!code-csharp[Cancellation#11](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex11.cs#11)]
 [!code-vb[Cancellation#11](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex11.vb#11)]  
  
 La chiamata a <xref:System.Threading.CancellationToken.ThrowIfCancellationRequested%2A> è estremamente veloce e non comporta un sovraccarico significativo nei cicli.  
  
 Se si chiama <xref:System.Threading.CancellationToken.ThrowIfCancellationRequested%2A> è solo necessario controllare in modo esplicito la proprietà <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> se sono presenti altre attività da eseguire in risposta all'annullamento oltre alla generazione dell'eccezione.  In questo esempio è possibile vedere come il codice in effetti acceda alla proprietà due volte: una volta tramite accesso esplicito e di nuovo nel metodo <xref:System.Threading.CancellationToken.ThrowIfCancellationRequested%2A>.  Poiché tuttavia l'operazione di lettura della proprietà <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> comporta solo un'istruzione di lettura volatile per accesso, il doppio accesso non è significativo dal punto di vista prestazionale.  È comunque preferibile chiamare il metodo anziché generare manualmente l'evento <xref:System.OperationCanceledException>.  
  
## Vedere anche  
 [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)