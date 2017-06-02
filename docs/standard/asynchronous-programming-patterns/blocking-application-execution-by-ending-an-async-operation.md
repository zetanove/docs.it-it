---
title: "Blocking Application Execution by Ending an Async Operation | Microsoft Docs"
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
  - "blocks, asynchronous operations"
  - "AsyncWaitHandle property"
  - "asynchronous programming, blocking applications"
  - "blocking application execution"
ms.assetid: cc5e2834-a65b-4df8-b750-7bdb79997fee
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Blocking Application Execution by Ending an Async Operation
È necessario bloccare le applicazioni che non consentono di eseguire altre attività in attesa dei risultati di un'operazione asincrona fino al completamento di quest'ultima.  Utilizzare una delle opzioni indicate di seguito per bloccare il thread principale dell'applicazione durante l'attesa del completamento di un'operazione asincrona.  
  
-   Chiamare il metodo **End** *OperationName* dell'operazione asincrona.  Tale approccio verrà descritto nel presente argomento.  
  
-   Utilizzare la proprietà <xref:System.IAsyncResult.AsyncWaitHandle%2A> dell'oggetto <xref:System.IAsyncResult> restituito dal metodo *OperationName* dell'operazione asincrona **Begin**.  Per un esempio in cui venga illustrato questo approccio, vedere [Blocking Application Execution Using an AsyncWaitHandle](../../../docs/standard/asynchronous-programming-patterns/blocking-application-execution-using-an-asyncwaithandle.md).  
  
 Le applicazioni che utilizzano il metodo **End** *OperationName* per eseguire il blocco fino al completamento di un'operazione asincrona generalmente chiamano il metodo **Begin** *OperationName*, eseguono le attività eseguibili senza i risultati dell'operazione e quindi chiamano **End** *OperationName*.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come utilizzare i metodi asincroni nella classe <xref:System.Net.Dns> per recuperare informazioni DNS \(Domain Name System\) relative a un computer specificato dall'utente.  Per i parametri `requestCallback` e `stateObject` del metodo <xref:System.Net.Dns.BeginGetHostByName%2A> viene passata la parola chiave `null` \(`Nothing` in Visual Basic\) in quanto tali argomenti non sono richiesti per l'utilizzo di questo approccio.  
  
 [!code-csharp[AsyncDesignPattern#1](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/Async_EndBlock.cs#1)]
 [!code-vb[AsyncDesignPattern#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/Async_EndBlock.vb#1)]  
  
## Vedere anche  
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)   
 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)