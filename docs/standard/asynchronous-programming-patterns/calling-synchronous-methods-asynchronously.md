---
title: "Calling Synchronous Methods Asynchronously | Microsoft Docs"
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
  - "asynchronous delegates"
  - "AsyncWaitHandle property"
  - "callback methods"
  - "calling synchronous methods in asynchronous manner"
  - "WaitHandle class, code examples"
  - "asynchronous programming, status polling"
  - "polling asynchronous operation status"
  - "delegates [.NET Framework], asynchronous"
  - "synchronous calling in asynchronous manner"
  - "waiting for asynchronous calls"
  - "status information [.NET Framework], asynchronous operations"
ms.assetid: 41972034-92ed-450a-9664-ab93fcc6f1fb
caps.latest.revision: 24
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 24
---
# Calling Synchronous Methods Asynchronously
.NET Framework consente di chiamare qualsiasi metodo in modo asincrono. A questo scopo occorre definire un delegato con la stessa firma del metodo che si vuole chiamare. Common Language Runtime definisce automaticamente i metodi `BeginInvoke` e `EndInvoke` per il delegato, con le firme appropriate.  
  
> [!NOTE]
>  Le chiamate asincrone dei delegati, con particolare riferimento ai metodi `BeginInvoke` e `EndInvoke`, non sono supportate in .NET Compact Framework.  
  
 Il `BeginInvoke` metodo avvia la chiamata asincrona. Presenta gli stessi parametri del metodo da eseguire in modo asincrono, con due parametri aggiuntivi facoltativi. Il primo parametro è un delegato <xref:System.AsyncCallback> che fa riferimento a un metodo da chiamare al completamento della chiamata asincrona. Il secondo parametro è un oggetto definito dall'utente che passa informazioni al metodo di callback.`BeginInvoke` restituisce immediatamente un valore e non attende il completamento della chiamata asincrona.`BeginInvoke` restituisce un oggetto <xref:System.IAsyncResult> che può essere usato per monitorare lo stato di avanzamento della chiamata asincrona.  
  
 Il metodo `EndInvoke` recupera i risultati della chiamata asincrona. Può essere chiamato in qualsiasi momento dopo `BeginInvoke`. Se la chiamata asincrona non è stata completata, `EndInvoke` blocca il thread chiamante fino al suo completamento. Nei parametri di `EndInvoke` sono inclusi quelli di tipo `out` e `ref` \([\<Out\>](../Topic/OutAttribute%20Class.md) `ByRef` e `ByRef` in Visual Basic\) del metodo da eseguire in modo asincrono, oltre all'oggetto <xref:System.IAsyncResult> restituito da `BeginInvoke`.  
  
> [!NOTE]
>  La funzionalità IntelliSense in [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] visualizza i parametri di `BeginInvoke` e `EndInvoke`. Se non si usa Visual Studio o uno strumento analogo o se si usa C\# con [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)], vedere [Asynchronous Programming Model \(APM\)](../../../docs/standard/asynchronous-programming-patterns/asynchronous-programming-model-apm.md) per una descrizione dei parametri definiti per tali metodi.  
  
 Gli esempi di codice in questo argomento presentano quattro modi comuni per usare `BeginInvoke` e `EndInvoke` per effettuare chiamate asincrone. Dopo avere chiamato `BeginInvoke` è possibile procedere nel modo seguente:  
  
-   Eseguire alcune operazioni, quindi chiamare `EndInvoke` per bloccare l'esecuzione fino al completamento della chiamata.  
  
-   Ottenere un oggetto <xref:System.Threading.WaitHandle> mediante la proprietà <xref:System.IAsyncResult.AsyncWaitHandle%2A?displayProperty=fullName>, usare il relativo metodo <xref:System.Threading.WaitHandle.WaitOne%2A> per bloccare l'esecuzione fino a quando non viene segnalato <xref:System.Threading.WaitHandle>, quindi chiamare `EndInvoke`.  
  
-   Eseguire il polling dell'oggetto <xref:System.IAsyncResult> restituito da `BeginInvoke` per stabilire quando viene completata la chiamata, quindi chiamare `EndInvoke`.  
  
-   Passare un delegato per un metodo di callback a `BeginInvoke`. Il metodo viene eseguito su un thread <xref:System.Threading.ThreadPool> al completamento della chiamata asincrona. Il metodo di callback chiama `EndInvoke`.  
  
> [!IMPORTANT]
>  Indipendentemente dalla tecnica usata, chiamare sempre `EndInvoke` per completare la chiamata asincrona.  
  
## Definizione del metodo di test e del delegato asincrono  
 Gli esempi di codice seguenti illustrano diversi modi per chiamare lo stesso metodo di lunga durata, `TestMethod`, in modo asincrono. Il metodo `TestMethod` visualizza un messaggio di console per indicare che ha iniziato l'elaborazione, si disattiva per alcuni secondi e quindi termina.`TestMethod` include un parametro `out` per dimostrare in che modo tali parametri vengono aggiunti alle firme di `BeginInvoke` e `EndInvoke`. I parametri `ref` possono essere gestiti in modo analogo.  
  
 L'esempio di codice seguente illustra la definizione di `TestMethod` e il delegato denominato `AsyncMethodCaller` che può essere usato per chiamare `TestMethod` in modo asincrono. Per compilare gli esempi di codice, è necessario includere le definizioni per `TestMethod` e il delegato `AsyncMethodCaller`.  
  
 [!code-cpp[AsyncDelegateExamples#1](../../../samples/snippets/cpp/VS_Snippets_CLR/AsyncDelegateExamples/cpp/TestMethod.cpp#1)]
 [!code-csharp[AsyncDelegateExamples#1](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDelegateExamples/CS/TestMethod.cs#1)]
 [!code-vb[AsyncDelegateExamples#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDelegateExamples/VB/TestMethod.vb#1)]  
  
## Attesa di una chiamata asincrona con EndInvoke  
 Il modo più semplice per eseguire un metodo in modo asincrono consiste nell'avviare l'esecuzione del metodo chiamando il metodo `BeginInvoke` del delegato, eseguire alcune operazioni sul thread principale e quindi chiamare il metodo `EndInvoke` del delegato.`EndInvoke` potrebbe bloccare il thread chiamante perché non restituisce un valore fino al completamento della chiamata asincrona. Si tratta di una tecnica valida per le operazioni su file o rete.  
  
> [!IMPORTANT]
>  Poiché `EndInvoke` potrebbe bloccarsi, non deve mai essere chiamato dai thread che servono l'interfaccia utente.  
  
 [!code-cpp[AsyncDelegateExamples#2](../../../samples/snippets/cpp/VS_Snippets_CLR/AsyncDelegateExamples/cpp/EndInvoke.cpp#2)]
 [!code-csharp[AsyncDelegateExamples#2](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDelegateExamples/CS/EndInvoke.cs#2)]
 [!code-vb[AsyncDelegateExamples#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDelegateExamples/VB/EndInvoke.vb#2)]  
  
## Attesa di una chiamata asincrona con WaitHandle  
 È possibile ottenere un oggetto <xref:System.Threading.WaitHandle> usando la proprietà <xref:System.IAsyncResult.AsyncWaitHandle%2A> dell'oggetto <xref:System.IAsyncResult> restituito da `BeginInvoke`. L'oggetto <xref:System.Threading.WaitHandle> viene segnalato al completamento della chiamata asincrona ed è possibile attenderlo chiamando il metodo <xref:System.Threading.WaitHandle.WaitOne%2A>.  
  
 Se si usa un <xref:System.Threading.WaitHandle>, è possibile eseguire altre operazioni prima o dopo il completamento della chiamata asincrona, ma prima di chiamare `EndInvoke` per recuperare i risultati.  
  
> [!NOTE]
>  L'handle di attesa non viene chiuso automaticamente quando si chiama `EndInvoke`. Se si rilasciano tutti i riferimenti all'handle di attesa, le risorse di sistema vengono liberate quando Garbage Collection recupera l'handle di attesa. Per liberare le risorse di sistema non appena si ha finito di usare l'handle di attesa, eliminarlo chiamando il metodo <xref:System.Threading.WaitHandle.Close%2A?displayProperty=fullName>. Garbage Collection opera in modo più efficiente quando gli oggetti eliminabili vengono eliminati in modo esplicito.  
  
 [!code-cpp[AsyncDelegateExamples#3](../../../samples/snippets/cpp/VS_Snippets_CLR/AsyncDelegateExamples/cpp/waithandle.cpp#3)]
 [!code-csharp[AsyncDelegateExamples#3](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDelegateExamples/CS/waithandle.cs#3)]
 [!code-vb[AsyncDelegateExamples#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDelegateExamples/VB/WaitHandle.vb#3)]  
  
## Polling del completamento della chiamata asincrona  
 È possibile usare la proprietà <xref:System.IAsyncResult.IsCompleted%2A> dell'oggetto <xref:System.IAsyncResult> restituito da `BeginInvoke` per rilevare il completamento della chiamata asincrona. Questa operazione può essere eseguita quando si effettua la chiamata asincrona da un thread che serve l'interfaccia utente. Il polling del completamento consente al thread chiamante di continuare l'esecuzione mentre viene eseguita la chiamata asincrona su un thread <xref:System.Threading.ThreadPool>.  
  
 [!code-cpp[AsyncDelegateExamples#4](../../../samples/snippets/cpp/VS_Snippets_CLR/AsyncDelegateExamples/cpp/polling.cpp#4)]
 [!code-csharp[AsyncDelegateExamples#4](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDelegateExamples/CS/polling.cs#4)]
 [!code-vb[AsyncDelegateExamples#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDelegateExamples/VB/polling.vb#4)]  
  
## Esecuzione di un metodo di callback al completamento di una chiamata asincrona  
 Se il thread che avvia la chiamata asincrona non deve necessariamente essere il thread che elabora i risultati, è possibile eseguire un metodo di callback al completamento della chiamata. Il metodo di callback viene eseguito su un thread <xref:System.Threading.ThreadPool>.  
  
 Per usare un metodo di callback, è necessario passare a `BeginInvoke` un delegato <xref:System.AsyncCallback> che rappresenta il metodo di callback. È possibile passare anche un oggetto contenente informazioni che devono essere usate dal metodo di callback. Nel metodo di callback è possibile eseguire il cast di <xref:System.IAsyncResult>, che è l'unico parametro del metodo di callback, a un oggetto <xref:System.Runtime.Remoting.Messaging.AsyncResult>. È quindi possibile usare la proprietà <xref:System.Runtime.Remoting.Messaging.AsyncResult.AsyncDelegate%2A?displayProperty=fullName> per ottenere il delegato usato per avviare la chiamata in modo che sia possibile chiamare `EndInvoke`.  
  
 Note sull'esempio:  
  
-   Il parametro `threadId` di `TestMethod` è un parametro `out` \([\<Out\>](../Topic/OutAttribute%20Class.md) `ByRef` in Visual Basic\), pertanto il valore di input non viene mai utilizzato da `TestMethod`. Viene passata una variabile fittizia alla chiamata `BeginInvoke`. Se il parametro `threadId` fosse un parametro `ref` \(`ByRef` in Visual Basic\), la variabile dovrebbe essere un campo a livello di classe perché possa essere passata sia a `BeginInvoke` che a `EndInvoke`.  
  
-   Le informazioni sullo stato che vengono passate a `BeginInvoke` sono costituite da una stringa di formato, che viene usata dal metodo di callback per formattare un messaggio di output. Dato che le informazioni sullo stato vengono passate come tipo <xref:System.Object>, è necessario eseguirne il cast al tipo appropriato prima di poterle usare.  
  
-   Il callback viene eseguito su un thread <xref:System.Threading.ThreadPool>. I thread <xref:System.Threading.ThreadPool> sono thread in background, che non mantengono l'applicazione in esecuzione se il thread principale termina, quindi il thread principale dell'esempio deve rimanere sospeso per un tempo sufficiente al completamento del callback.  
  
 [!code-cpp[AsyncDelegateExamples#5](../../../samples/snippets/cpp/VS_Snippets_CLR/AsyncDelegateExamples/cpp/callback.cpp#5)]
 [!code-csharp[AsyncDelegateExamples#5](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDelegateExamples/CS/callback.cs#5)]
 [!code-vb[AsyncDelegateExamples#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDelegateExamples/VB/callback.vb#5)]  
  
## Vedere anche  
 <xref:System.Delegate>   
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)