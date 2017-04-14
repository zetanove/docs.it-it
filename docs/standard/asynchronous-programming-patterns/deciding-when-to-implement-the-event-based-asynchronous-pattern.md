---
title: "Deciding When to Implement the Event-based Asynchronous Pattern | Microsoft Docs"
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
  - "Event-based Asynchronous Pattern"
  - "ProgressChangedEventArgs class"
  - "BackgroundWorker component"
  - "events [.NET Framework], asynchronous"
  - "AsyncOperationManager class"
  - "threading [.NET Framework], asynchronous features"
  - "AsyncOperation class"
  - "AsyncCompletedEventArgs class"
ms.assetid: a00046aa-785d-4f7f-a8e5-d06475ea50da
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Deciding When to Implement the Event-based Asynchronous Pattern
Il modello asincrono basato su eventi consente di esporre il comportamento asincrono di una classe.  Con l'introduzione di questo modello, in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] sono ora disponibili due modelli per l'esposizione del comportamento asincrono: il modello asincrono basato sull'interfaccia <xref:System.IAsyncResult?displayProperty=fullName> e il modello basato su eventi.  In questo argomento vengono illustrati i casi in cui è opportuno implementare entrambi i modelli.  
  
 Per ulteriori informazioni sulla programmazione asincrona con l'interfaccia <xref:System.IAsyncResult>, vedere [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md).  
  
## Principi generali  
 In genere, è sempre opportuno esporre le funzionalità asincrone utilizzando il modello asincrono basato su eventi, se possibile.  Esistono tuttavia alcuni requisiti che il modello basato su eventi non è in grado di soddisfare.  In questi casi, può essere necessario implementare il modello <xref:System.IAsyncResult>, oltre a quello basato su eventi.  
  
> [!NOTE]
>  È raro che il modello <xref:System.IAsyncResult> venga implementato senza che lo sia anche il modello basato su eventi.  
  
## Indicazioni  
 Di seguito vengono fornite alcune indicazioni in base alle quali stabilire quando è necessario implementare il modello asincrono basato su eventi.  
  
-   Utilizzare il modello basato su eventi come API predefinita per esporre il comportamento asincrono della classe.  
  
-   Non esporre il modello <xref:System.IAsyncResult> se la classe viene principalmente utilizzata in un'applicazione client, ad esempio Windows Form.  
  
-   Esporre il modello <xref:System.IAsyncResult> solo quando risulta necessario per soddisfare i requisiti.  È ad esempio possibile che il modello <xref:System.IAsyncResult> debba essere esposto per motivi di compatibilità con un'API esistente.  
  
-   Non esporre il modello <xref:System.IAsyncResult> senza esporre anche quello basato su eventi.  
  
-   Se è necessario esporre il modello <xref:System.IAsyncResult>, eseguire questa operazione come opzione avanzata.  Se ad esempio si genera un oggetto proxy, generare il modello basato su eventi per impostazione predefinita, inserendo un'opzione per la generazione del modello <xref:System.IAsyncResult>.  
  
-   Compilare l'implementazione del modello basato su eventi nell'implementazione del modello <xref:System.IAsyncResult>.  
  
-   Evitare di esporre il modello basato su eventi e il modello <xref:System.IAsyncResult> nella stessa classe.  Esporre il modello basato su eventi in classi di livello superiore e il modello <xref:System.IAsyncResult> in classi di livello inferiore.  Ad esempio, confrontare il modello basato su eventi nel componente <xref:System.Net.WebClient> con il modello <xref:System.IAsyncResult> nella classe <xref:System.Web.HttpRequest>.  
  
    -   Esporre il modello basato su eventi e il modello <xref:System.IAsyncResult> nella stessa classe quando necessario per motivi di compatibilità.  Se ad esempio è stata già rilasciata un'API che utilizza il modello <xref:System.IAsyncResult>, sarà necessario mantenere il modello <xref:System.IAsyncResult> per compatibilità con le versioni precedenti.  
  
    -   Esporre il modello basato su eventi e il modello <xref:System.IAsyncResult> nella stessa classe se la complessità del modello a oggetti risultante è superiore al vantaggio offerto da implementazioni separate.  È preferibile esporre entrambi i modelli in una singola classe anziché evitare di esporre il modello basato su eventi.  
  
    -   Se è necessario esporre sia il modello basato su eventi che il modello <xref:System.IAsyncResult> in una singola classe, utilizzare <xref:System.ComponentModel.EditorBrowsableAttribute> impostato su <xref:System.ComponentModel.EditorBrowsableState> per contrassegnare l'implementazione del modello <xref:System.IAsyncResult> come funzionalità avanzata.  In questo modo verrà indicato agli ambienti di sviluppo, ad esempio IntelliSense di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], di non visualizzare i metodi o le proprietà di <xref:System.IAsyncResult>.  Tali metodi e proprietà potranno comunque essere utilizzati in modo completo, ma lo sviluppatore che opera mediante IntelliSense avrà una visualizzazione più chiara dell'API.  
  
## Criteri per esporre il modello IAsyncResult insieme al modello basato su eventi  
 Il modello asincrono basato su eventi offre numerosi vantaggi negli scenari descritti in precedenza, ma presenta anche alcuni inconvenienti, di cui è necessario essere a conoscenza se le prestazioni rappresentano un requisito fondamentale.  
  
 Esistono tre scenari in cui il modello basato su eventi offre vantaggi minori rispetto al modello <xref:System.IAsyncResult>:  
  
-   Attesa bloccante su un singolo oggetto <xref:System.IAsyncResult>  
  
-   Attesa bloccante su numerosi oggetti <xref:System.IAsyncResult>  
  
-   Polling per il completamento sull'oggetto <xref:System.IAsyncResult>  
  
 È possibile operare in questi scenari utilizzando il modello basato su eventi, anche se il modello <xref:System.IAsyncResult> risulterebbe meno complicato.  
  
 Gli sviluppatori spesso utilizzano il modello <xref:System.IAsyncResult> per servizi che presentano in genere requisiti di prestazioni molto elevati.  Il polling per lo scenario di completamento è ad esempio un tecnica per server ad alte prestazioni.  
  
 Inoltre, il modello basato su eventi è meno efficiente del modello <xref:System.IAsyncResult> perché crea più oggetti, in particolare <xref:System.EventArgs>, ed esegue la sincronizzazione attraverso i thread.  
  
 Nell'elenco riportato di seguito vengono fornite alcune indicazioni a cui attenersi se si sceglie di utilizzare il modello <xref:System.IAsyncResult>:  
  
-   Esporre il modello <xref:System.IAsyncResult> solo quando è necessario disporre del supporto per l'oggetto <xref:System.Threading.WaitHandle> o <xref:System.IAsyncResult>.  
  
-   Esporre il modello <xref:System.IAsyncResult> solo quando è disponibile un'API esistente che utilizza il modello <xref:System.IAsyncResult>.  
  
-   Se si dispone di un'API esistente basata sul modello <xref:System.IAsyncResult>, può essere opportuno esporre anche il modello basato su eventi nel rilascio successivo.  
  
-   Esporre il modello <xref:System.IAsyncResult> solo se esistono requisiti di prestazioni elevate già verificati che non possono essere soddisfatti dal modello basato su eventi, ma dal modello <xref:System.IAsyncResult>.  
  
## Vedere anche  
 [Walkthrough: Implementing a Component That Supports the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)   
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)   
 [Multithreaded Programming with the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/multithreaded-programming-with-the-event-based-asynchronous-pattern.md)   
 [Implementing the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/implementing-the-event-based-asynchronous-pattern.md)   
 [Suggerimenti per l'implementazione del modello asincrono basato su eventi](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)   
 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)