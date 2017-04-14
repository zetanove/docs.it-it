---
title: "Using an AsyncCallback Delegate to End an Asynchronous Operation | Microsoft Docs"
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
  - "ending asynchronous operations"
  - "asynchronous programming, ending operations"
  - "AsyncCallback delegate"
  - "stopping asynchronous operations"
ms.assetid: 9d97206c-8917-406c-8961-7d0909d84eeb
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Using an AsyncCallback Delegate to End an Asynchronous Operation
Si consiglia di non bloccare le applicazioni che consentono di eseguire altre attività in attesa dei risultati di un'operazione asincrona fino al completamento di quest'ultima.  Utilizzare una delle opzioni riportate di seguito per continuare l'esecuzione delle istruzioni durante l'attesa del completamento di un'operazione asincrona.  
  
-   Utilizzare un delegato <xref:System.AsyncCallback> per elaborare i risultati dell'operazione asincrona in un thread diverso.  Tale approccio verrà descritto nel presente argomento.  
  
-   Utilizzare la proprietà <xref:System.IAsyncResult.IsCompleted%2A> dell'oggetto <xref:System.IAsyncResult> restituito dal metodo *OperationName* dell'operazione asincrona **Begin** per determinare se l'operazione è stata completata.  Per un esempio in cui venga illustrato questo approccio, vedere [Polling for the Status of an Asynchronous Operation](../../../docs/standard/asynchronous-programming-patterns/polling-for-the-status-of-an-asynchronous-operation.md).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come utilizzare i metodi asincroni nella classe <xref:System.Net.Dns> per recuperare informazioni DNS \(Domain Name System\) relative ai computer specificati dall'utente.  In questo esempio viene creato un delegato <xref:System.AsyncCallback> che fa riferimento al metodo `ProcessDnsInformation`.  Tale metodo viene chiamato per ogni richiesta asincrona di informazioni DNS.  
  
 L'host specificato dall'utente viene passato al parametro <xref:System.Net.Dns.BeginGetHostByName%2A> <xref:System.Object>.  Per un esempio in cui vengano illustrati la definizione e l'utilizzo di un oggetto stato più complesso, vedere [Using an AsyncCallback Delegate and State Object](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-and-state-object.md).  
  
 [!code-csharp[AsyncDesignPattern#4](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/AsyncDelegateNoStateObject.cs#4)]
 [!code-vb[AsyncDesignPattern#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/AsyncDelegateNoState.vb#4)]  
  
## Vedere anche  
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)   
 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)   
 [Calling Asynchronous Methods Using IAsyncResult](../../../docs/standard/asynchronous-programming-patterns/calling-asynchronous-methods-using-iasyncresult.md)   
 [Using an AsyncCallback Delegate and State Object](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-and-state-object.md)