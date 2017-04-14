---
title: "Polling for the Status of an Asynchronous Operation | Microsoft Docs"
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
  - "asynchronous programming, status polling"
  - "polling asynchronous operation status"
  - "status information [.NET Framework], asynchronous operations"
ms.assetid: b541af31-dacb-4e20-8847-1b1ff7c35363
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Polling for the Status of an Asynchronous Operation
Si consiglia di non bloccare le applicazioni che consentono di eseguire altre attività in attesa dei risultati di un'operazione asincrona fino al completamento di quest'ultima.  Utilizzare una delle opzioni riportate di seguito per continuare l'esecuzione delle istruzioni durante l'attesa del completamento di un'operazione asincrona.  
  
-   Utilizzare la proprietà <xref:System.IAsyncResult.IsCompleted%2A> dell'oggetto <xref:System.IAsyncResult> restituito dal metodo *OperationName* dell'operazione asincrona **Begin** per determinare se l'operazione è stata completata.  Questo approccio è noto come polling e viene illustrato nel presente argomento.  
  
-   Utilizzare un delegato <xref:System.AsyncCallback> per elaborare i risultati dell'operazione asincrona in un thread diverso.  Per un esempio in cui venga illustrato questo approccio, vedere [Using an AsyncCallback Delegate to End an Asynchronous Operation](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come utilizzare i metodi asincroni nella classe <xref:System.Net.Dns> per recuperare informazioni DNS \(Domain Name System\) relative a un computer specificato dall'utente.  In questo esempio viene avviata un'operazione asincrona e quindi vengono stampati punti \("."\) nella console fino al completamento dell'operazione.  Per i parametri <xref:System.Net.Dns.BeginGetHostByName%2A> <xref:System.AsyncCallback> e <xref:System.Object> viene passata la parola chiave **null** \(**Nothing** in Visual Basic\) in quanto tali parametri non sono richiesti per l'utilizzo di questo approccio.  
  
 [!code-csharp[AsyncDesignPattern#3](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/Async_Poll.cs#3)]
 [!code-vb[AsyncDesignPattern#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/Async_Poll.vb#3)]  
  
## Vedere anche  
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)   
 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)