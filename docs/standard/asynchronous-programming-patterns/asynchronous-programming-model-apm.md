---
title: "Asynchronous Programming Model (APM) | Microsoft Docs"
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
  - "starting asynchronous operations"
  - "beginning asynchronous operations"
  - "asynchronous programming, ending operations"
  - "asynchronous programming"
  - "stopping asynchronous operations"
  - "asynchronous programming, beginning operations"
ms.assetid: c9b3501e-6bc6-40f9-8efd-4b6d9e39ccf0
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Asynchronous Programming Model (APM)
L'implementazione di un'operazione asincrona che usa lo schema progettuale <xref:System.IAsyncResult> avviene mediante due metodi, denominati **Begin** *OperationName* e **End** *OperationName*, che rispettivamente avviano e terminano l'operazione asincrona *OperationName*. La classe <xref:System.IO.FileStream> fornisce ad esempio i metodi <xref:System.IO.FileStream.BeginRead%2A> e <xref:System.IO.FileStream.EndRead%2A> per la lettura asincrona dei byte da un file. Tali metodi implementano la versione asincrona del metodo <xref:System.IO.FileStream.Read%2A>.  
  
> [!NOTE]
>  A partire da .NET Framework 4, Task Parallel Library fornisce un nuovo modello di programmazione asincrona e parallela. Per altre informazioni, vedere [Task Parallel Library \(TPL\)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md) e [Task\-based Asynchronous Pattern \(TAP\)](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md).  
  
 Dopo aver chiamato il metodo **Begin** *OperationName*, un'applicazione può continuare a eseguire le istruzioni sul thread chiamante mentre l'operazione asincrona viene eseguita su un altro thread. Per ogni chiamata a **Begin** *OperationName*, l'applicazione deve chiamare anche il metodo **End** *OperationName* per ottenere i risultati dell'operazione.  
  
## Avvio di un'operazione asincrona  
 Il metodo **Begin** *OperationName* avvia l'operazione asincrona *OperationName* e restituisce un oggetto che implementa l'interfaccia <xref:System.IAsyncResult>. Gli oggetti <xref:System.IAsyncResult> archiviano le informazioni sulle operazioni asincrone. La tabella seguente illustra le informazioni relative a un'operazione asincrona.  
  
|Membro|Descrizione|  
|------------|-----------------|  
|<xref:System.IAsyncResult.AsyncState%2A>|Oggetto facoltativo specifico dell'applicazione che contiene informazioni sull'operazione asincrona.|  
|<xref:System.IAsyncResult.AsyncWaitHandle%2A>|Oggetto <xref:System.Threading.WaitHandle> che può essere usato per bloccare l'esecuzione dell'applicazione fino al completamento dell'operazione asincrona.|  
|<xref:System.IAsyncResult.CompletedSynchronously%2A>|Valore che indica l'eventuale completamento dell'operazione asincrona sul thread usato per chiamare il metodo **Begin** *OperationName* anziché su un thread <xref:System.Threading.ThreadPool> diverso.|  
|<xref:System.IAsyncResult.IsCompleted%2A>|Valore che indica l'eventuale completamento dell'operazione asincrona.|  
  
 Un metodo **Begin** *OperationName* accetta tutti i parametri dichiarati nella firma della versione sincrona del metodo passati per valore o per riferimento. Nella firma del metodo **Begin** *OperationName* non sono inclusi parametri out. Sono invece inclusi due parametri aggiuntivi nella firma del metodo **Begin** *OperationName*. Il primo dei quali definisce un delegato <xref:System.AsyncCallback> che fa riferimento a un metodo chiamato al completamento dell'operazione asincrona. Il chiamante può specificare `null` \(`Nothing` in Visual Basic\) se non vuole richiamare un metodo al termine dell'operazione. Il secondo parametro aggiuntivo è un oggetto definito dall'utente che può essere usato per passare informazioni sullo stato specifiche dell'applicazione al metodo richiamato al completamento dell'operazione asincrona. Se un metodo **Begin** *OperationName* accetta altri parametri specifici dell'operazione, quale un array di byte per l'archiviazione dei byte letti da un file, l'oggetto <xref:System.AsyncCallback> e l'oggetto stato dell'applicazione saranno gli ultimi parametri nella firma del metodo **Begin** *OperationName*.  
  
 **Begin** *OperationName* restituisce immediatamente il controllo al thread chiamante. Se il metodo **Begin** *OperationName* genera eccezioni, la generazione delle eccezioni avviene prima dell'avvio dell'operazione asincrona. Se il metodo **Begin** *OperationName* genera eccezioni, il metodo di callback non viene richiamato.  
  
## Fine di un'operazione asincrona  
 Il metodo **End** *OperationName* termina l'operazione asincrona *OperationName*. Il valore restituito dal metodo **End** *OperationName* è dello stesso tipo restituito dalla controparte sincrona ed è specifico dell'operazione asincrona. Il metodo <xref:System.IO.FileStream.EndRead%2A> restituisce ad esempio il numero di byte letti da un oggetto <xref:System.IO.FileStream> mentre il metodo <xref:System.Net.Dns.EndGetHostByName%2A> restituisce un oggetto <xref:System.Net.IPHostEntry> contenente le informazioni relative a un computer host. Il metodo **End** *OperationName* accetta tutti i parametri out o ref dichiarati nella firma della versione sincrona del metodo. Oltre ai parametri provenienti dal metodo sincrono, il metodo **End** *OperationName* comprende anche un parametro <xref:System.IAsyncResult>. I chiamanti devono passare l'istanza restituita dalla chiamata corrispondente al metodo **Begin** *OperationName*.  
  
 Se l'operazione asincrona rappresentata dall'oggetto <xref:System.IAsyncResult> non è stata completata quando viene chiamato il metodo **End** *OperationName*, il metodo **End** *OperationName* blocca il thread chiamante fino al completamento dell'operazione. Le eccezioni generate dall'operazione asincrona vengono generate dal metodo **End** *OperationName*. Non è definito l'effetto della chiamata ripetuta del metodo **End** *OperationName* con lo stesso oggetto <xref:System.IAsyncResult>. Analogamente, anche la chiamata del metodo **End** *OperationName* con un oggetto <xref:System.IAsyncResult> non restituito dal metodo Begin correlato risulta non essere definita.  
  
> [!NOTE]
>  In questi due scenari non definiti ai responsabili dell'implementazione è consigliata la generazione di <xref:System.InvalidOperationException>.  
  
> [!NOTE]
>  I responsabili dell'implementazione di questo schema progettuale devono notificare al chiamante il completamento dell'operazione asincrona impostando <xref:System.IAsyncResult.IsCompleted%2A> su true, chiamando il metodo di callback asincrono, se specificato, e segnalando l'oggetto <xref:System.IAsyncResult.AsyncWaitHandle%2A>.  
  
 Gli sviluppatori di applicazioni dispongono di diverse scelte di progettazione per accedere ai risultati dell'operazione asincrona. La scelta adeguata dipende dall'eventuale presenza nell'applicazione di istruzioni che possono essere eseguite durante il completamento dell'operazione. Se l'applicazione non consente di eseguire altre attività fino alla ricezione dei risultati dell'operazione asincrona, deve essere bloccata fino a quel momento. A tale scopo, sono disponibili i due approcci illustrati di seguito:  
  
-   Chiamare il metodo **End** *OperationName* dal thread principale dell'applicazione, bloccando l'esecuzione dell'applicazione fino al completamento dell'operazione. Per un esempio relativo all'uso di questa tecnica, vedere [Blocking Application Execution by Ending an Async Operation](../../../docs/standard/asynchronous-programming-patterns/blocking-application-execution-by-ending-an-async-operation.md).  
  
-   Usare <xref:System.IAsyncResult.AsyncWaitHandle%2A> per bloccare l'esecuzione dell'applicazione fino al completamento di una o più operazioni. Per un esempio relativo all'uso di questa tecnica, vedere [Blocking Application Execution Using an AsyncWaitHandle](../../../docs/standard/asynchronous-programming-patterns/blocking-application-execution-using-an-asyncwaithandle.md).  
  
 Per le applicazioni che non è necessario bloccare durante il completamento dell'operazione asincrona, è possibile usare uno degli approcci seguenti:  
  
-   Effettuare il polling dello stato di completamento dell'operazione verificando periodicamente la proprietà <xref:System.IAsyncResult.IsCompleted%2A> e chiamando il metodo **End** *OperationName* al completamento dell'operazione. Per un esempio relativo all'uso di questa tecnica, vedere [Polling for the Status of an Asynchronous Operation](../../../docs/standard/asynchronous-programming-patterns/polling-for-the-status-of-an-asynchronous-operation.md).  
  
-   Usare un delegato <xref:System.AsyncCallback> per specificare il metodo da richiamare quando l'operazione viene completata. Per un esempio relativo all'uso di questa tecnica, vedere [Using an AsyncCallback Delegate to End an Asynchronous Operation](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md).  
  
## Vedere anche  
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)   
 [Calling Synchronous Methods Asynchronously](../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)   
 [Using an AsyncCallback Delegate and State Object](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-and-state-object.md)