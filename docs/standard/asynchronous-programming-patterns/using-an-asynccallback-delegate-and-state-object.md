---
title: "Using an AsyncCallback Delegate and State Object | Microsoft Docs"
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
  - "asynchronous programming, delegates"
  - "AsyncCallback delegate, samples"
  - "asynchronous programming, state objects"
  - "IAsyncResult interface, samples"
ms.assetid: e3e5475d-c5e9-43f0-928e-d18df8ca1f1d
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Using an AsyncCallback Delegate and State Object
Quando si utilizza un delegato di <xref:System.AsyncCallback> per elaborare in un thread separato i risultati dell'operazione asincrona, è possibile utilizzare un oggetto di stato per passare informazioni tra i callback e recuperare un risultato finale.  In questo argomento viene illustrata questa procedura espandendo l'esempio che si trova in [Using an AsyncCallback Delegate to End an Asynchronous Operation](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come utilizzare i metodi asincroni nella classe <xref:System.Net.Dns> per recuperare informazioni DNS \(Domain Name System\) relative ai computer specificati dall'utente.  Viene definita e utilizzata la classe `HostRequest` per memorizzare informazioni sullo stato.  Viene creato un oggetto `HostRequest` per ogni nome computer immesso dall'utente.  Questo oggetto viene passato al metodo <xref:System.Net.Dns.BeginGetHostByName%2A>.  Il metodo `ProcessDnsInformation` viene chiamato ogni volta che viene completata una richiesta.  L'oggetto `HostRequest` viene recuperato mediante la proprietà <xref:System.IAsyncResult.AsyncState%2A>.  Il metodo `ProcessDnsInformation` utilizza l'oggetto `HostRequest` per memorizzare l'oggetto <xref:System.Net.IPHostEntry> restituito dalla richiesta o una <xref:System.Net.Sockets.SocketException> generata dalla richiesta.  Al termine dell'esecuzione di tutte le richieste, l'applicazione scorre gli oggetti `HostRequest` e visualizza le informazioni DNS o il messaggio di errore <xref:System.Net.Sockets.SocketException>.  
  
 [!code-csharp[AsyncDesignPattern#5](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/AsyncDelegateWithStateObject.cs#5)]
 [!code-vb[AsyncDesignPattern#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/AsyncDelegateWithStateObject.vb#5)]  
  
## Vedere anche  
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)   
 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)   
 [Using an AsyncCallback Delegate to End an Asynchronous Operation](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md)