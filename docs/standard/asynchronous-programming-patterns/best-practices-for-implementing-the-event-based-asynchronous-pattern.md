---
title: "Suggerimenti per l&#39;implementazione del modello asincrono basato su eventi | Microsoft Docs"
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
  - "modello asincrono basato su eventi"
  - "ProgressChangedEventArgs (classe)"
  - "BackgroundWorker (componente)"
  - "eventi [.NET Framework], asincroni"
  - "AsyncOperationManager (classe)"
  - "threading [.NET Framework], funzionalità asincrone"
  - "AsyncOperation (classe)"
  - "AsyncCompletedEventArgs (classe)"
ms.assetid: 4acd2094-4f46-4eff-9190-92d0d9ff47db
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Suggerimenti per l&#39;implementazione del modello asincrono basato su eventi
Il modello asincrono basato su eventi offre un sistema efficace per l'esposizione del comportamento asincrono nelle classi attraverso una semantica nota di eventi e delegati. Per implementare tale modello, è necessario soddisfare alcuni requisiti comportamentali specifici. Nelle sezioni riportate di seguito vengono illustrati i requisiti e le indicazioni da tenere presenti per l'implementazione di una classe che segue il modello asincrono basato su eventi.  
  
 Per informazioni generali, vedere [Implementing the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/implementing-the-event-based-asynchronous-pattern.md).  
  
## Garanzie comportamentali richieste  
 Se si implementa il modello asincrono basato su eventi, è necessario fornire garanzie sul comportamento della classe e sull'affidabilità di tale comportamento per i client.  
  
### Completamento  
 Richiamare sempre il gestore eventi *NomeMetodo*`Completed` in caso di completamento, errore o annullamento. È infatti consigliabile che le applicazioni non si trovino mai in una situazione permanente di inattività nella quale il completamento non si verifica mai. Fa eccezione a questa regola il caso in cui l'operazione asincrona stessa sia progettata per non essere mai completata.  
  
### Eventi Completed e classi EventArgs  
 Per ogni metodo *NomeMetodo*`Async` distinto, applicare i requisiti di progettazione seguenti:  
  
-   Definire un evento *NomeMetodo*`Completed` sulla stessa classe del metodo.  
  
-   Definire una classe <xref:System.EventArgs> e un delegato associato per l'evento *NomeMetodo*`Completed` che deriva dalla classe <xref:System.ComponentModel.AsyncCompletedEventArgs>. Il nome predefinito della classe deve avere il formato *NomeMetodo*`CompletedEventArgs`.  
  
-   Verificare che la classe <xref:System.EventArgs> sia specifica dei valori restituiti del metodo *NomeMetodo*. Quando si usa la classe <xref:System.EventArgs>, è consigliabile non richiedere mai agli sviluppatori di eseguire il cast del risultato.  
  
     Nell'esempio di codice seguente vengono illustrate rispettivamente un'implementazione valida e non valida del requisito di progettazione in questione.  
  
```csharp  
// Good design  
private void Form1_MethodNameCompleted(object sender, xxxCompletedEventArgs e)   
{   
    DemoType result = e.Result;  
}  
  
// Bad design  
private void Form1_MethodNameCompleted(object sender, MethodNameCompletedEventArgs e)   
{   
    DemoType result = (DemoType)(e.Result);  
}  
```  
  
-   Non definire una classe <xref:System.EventArgs> per restituire metodi che restituiscono `void`. Usare invece un'istanza della classe <xref:System.ComponentModel.AsyncCompletedEventArgs>.  
  
-   Assicurarsi di generare sempre l'evento *NomeMetodo*`Completed`. Questo evento deve essere generato in caso di corretto completamento, errore o annullamento. È infatti consigliabile che le applicazioni non si trovino mai in una situazione permanente di inattività nella quale il completamento non si verifica mai.  
  
-   Assicurarsi di intercettare le eccezioni che si verificano nell'operazione asincrona e assegnare l'eccezione intercettata alla proprietà <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A>.  
  
-   Se si è verificato un errore durante il completamento dell'attività, è possibile che i risultati non siano accessibili. Quando la proprietà <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A> non è `null`, assicurarsi che l'accesso a qualsiasi proprietà nella struttura <xref:System.EventArgs> generi un'eccezione. Usare il metodo <xref:System.ComponentModel.AsyncCompletedEventArgs.RaiseExceptionIfNecessary%2A> per eseguire questa verifica.  
  
-   Modellare un timeout come errore. Quando si verifica un timeout, generare l'evento *NomeMetodo*`Completed` e assegnare un oggetto <xref:System.TimeoutException> alla proprietà <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A>.  
  
-   Se la classe supporta più chiamate simultanee, assicurarsi che l'evento *NomeMetodo*`Completed` contenga l'oggetto `userSuppliedState` appropriato.  
  
-   Assicurarsi che l'evento *NomeMetodo*`Completed` venga generato nel thread appropriato e nel momento adeguato del ciclo di vita dell'applicazione. Per altre informazioni, vedere la sezione Thread e contesti.  
  
### Esecuzione simultanea di operazioni  
  
-   Se la classe supporta più chiamate simultanee, consentire allo sviluppatore di tenere traccia di ogni chiamata separatamente definendo l'overload di *NomeMetodo*`Async` che accetta un parametro di stato con valori di oggetto, o un ID attività, denominato `userSuppliedState`. Questo parametro deve essere sempre l'ultimo nella firma del metodo *NomeMetodo*`Async`.  
  
-   Se la classe definisce l'overload di *NomeMetodo*`Async` che accetta un parametro di stato con valori di oggetto, o un ID attività, tenere traccia del ciclo di vita dell'operazione con tale ID e specificarlo nuovamente nel gestore del completamento. Per l'esecuzione di tali operazioni sono disponibili classi di supporto specifiche. Per altre informazioni sulla gestione della concorrenza, vedere [Walkthrough: Implementing a Component That Supports the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md).  
  
-   Se la classe definisce il metodo *NomeMetodo*`Async` senza il parametro di stato e non supporta più chiamate simultanee, assicurarsi che qualsiasi tentativo di richiamare *NomeMetodo*`Async` prima del completamento della chiamata *NomeMetodo*`Async` precedente generi un'eccezione di tipo <xref:System.InvalidOperationException>.  
  
-   Di norma, non generare un'eccezione se il metodo *NomeMetodo*`Async` senza il parametro `userSuppliedState` viene richiamato più volte determinando la presenza di più operazioni in attesa. È possibile generare un'eccezione quando la classe non può gestire questa situazione, ma si presuppone che gli sviluppatori possano gestire i diversi callback indistinguibili in corso.  
  
### Accesso ai risultati  
  
-   Se durante l'esecuzione dell'operazione asincrona si è verificato un errore, è possibile che i risultati non siano accessibili. Verificare che l'accesso a qualsiasi proprietà in <xref:System.ComponentModel.AsyncCompletedEventArgs> quando <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A> non è `null` generi l'eccezione a cui fa riferimento <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A>. La classe <xref:System.ComponentModel.AsyncCompletedEventArgs> fornisce il metodo <xref:System.ComponentModel.AsyncCompletedEventArgs.RaiseExceptionIfNecessary%2A> a questo scopo.  
  
-   Assicurarsi che i tentativi di accesso al risultato generino un'eccezione di tipo <xref:System.InvalidOperationException> che segnala l'avvenuto annullamento dell'operazione. Usare il metodo <xref:System.ComponentModel.AsyncCompletedEventArgs.RaiseExceptionIfNecessary%2A?displayProperty=fullName> per eseguire questa verifica.  
  
### Generazione di report sullo stato di avanzamento  
  
-   Garantire il supporto della generazione di report sullo stato di avanzamento, se possibile, per consentire agli sviluppatori di offrire prestazioni ottimali dell'applicazione durante l'utilizzo della classe.  
  
-   Se si implementa un evento `ProgressChanged`\/*NomeMetodo*`ProgressChanged`, assicurarsi che non siano stati generati eventi di questo tipo per una determinata operazione asincrona dopo la generazione dell'evento *NomeMetodo*`Completed` dell'operazione.  
  
-   In caso di popolamento della classe <xref:System.ComponentModel.ProgressChangedEventArgs> standard, accertarsi che la proprietà <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A> possa essere sempre interpretata come percentuale. Non è necessario che il valore di percentuale sia preciso, purché si tratti di un valore di percentuale. Se l'unità di misura dei report sullo stato di avanzamento deve essere diversa da una percentuale, derivare una classe dalla classe <xref:System.ComponentModel.ProgressChangedEventArgs> e lasciare impostato su 0 il valore di <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A>. Evitare di usare unità di misura dei report diverse dalla percentuale.  
  
-   Verificare che l'evento `ProgressChanged` venga generato sul thread appropriato nel momento adeguato del ciclo di vita dell'applicazione. Per altre informazioni, vedere la sezione Thread e contesti.  
  
### Implementazione della proprietà IsBusy  
  
-   Non esporre una proprietà `IsBusy` se la classe supporta più chiamate simultanee. I proxy dei servizi Web XML, ad esempio, non espongono una proprietà `IsBusy` in quanto supportano più chiamate simultanee dei metodi asincroni.  
  
-   La proprietà `IsBusy` deve restituire `true` dopo la chiamata al metodo *NomeMetodo*`Async` e prima della generazione dell'evento *NomeMetodo*`Completed`. In caso contrario, deve restituire `false`. I componenti <xref:System.ComponentModel.BackgroundWorker> e <xref:System.Net.WebClient> sono esempi di classi che espongono una proprietà `IsBusy`.  
  
### Annullamento  
  
-   Garantire il supporto dell'annullamento, se possibile, per consentire agli sviluppatori di offrire prestazioni ottimali dell'applicazione durante l'utilizzo della classe.  
  
-   In caso di annullamento, impostare il flag <xref:System.ComponentModel.AsyncCompletedEventArgs.Cancelled%2A> nell'oggetto <xref:System.ComponentModel.AsyncCompletedEventArgs>.  
  
-   Assicurarsi che i tentativi di accesso al risultato generino un'eccezione di tipo <xref:System.InvalidOperationException> che segnala l'avvenuto annullamento dell'operazione. Usare il metodo <xref:System.ComponentModel.AsyncCompletedEventArgs.RaiseExceptionIfNecessary%2A?displayProperty=fullName> per eseguire questa verifica.  
  
-   Verificare che le chiamate a un metodo di annullamento vengano eseguite correttamente senza mai generare un'eccezione. Generalmente, a un client viene notificato se un'operazione è realmente annullabile in qualsiasi momento mentre non viene notificato se un annullamento già avviato ha avuto esito positivo. All'applicazione viene invece sempre notificato l'avvenuto annullamento, poiché lo stato di completamento dipende anche dall'applicazione.  
  
-   Generare l'evento *NomeMetodo*`Completed` quando l'operazione è annullata.  
  
### Errori ed eccezioni  
  
-   Intercettare le eccezioni che si verificano nell'operazione asincrona e impostare il valore della proprietà <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A?displayProperty=fullName> su tali eccezioni.  
  
### Thread e contesti  
 Per un corretto funzionamento della classe, è fondamentale che i gestori eventi del client siano richiamati sul thread o sul contesto appropriato per il modello di applicazione specifico, incluse le applicazioni [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] e Windows Form. Per garantire il comportamento corretto della classe asincrona con qualsiasi modello di applicazione sono disponibili due classi di supporto, <xref:System.ComponentModel.AsyncOperation> e <xref:System.ComponentModel.AsyncOperationManager>.  
  
 <xref:System.ComponentModel.AsyncOperationManager> fornisce un metodo, <xref:System.ComponentModel.AsyncOperationManager.CreateOperation%2A>, che restituisce un oggetto <xref:System.ComponentModel.AsyncOperation>. Il metodo *NomeMetodo*`Async` chiama <xref:System.ComponentModel.AsyncOperationManager.CreateOperation%2A> e la classe usa l'oggetto <xref:System.ComponentModel.AsyncOperation> restituito per tenere traccia del ciclo di vita dell'attività asincrona.  
  
 Per generare report destinati al client sullo stato di avanzamento, sui risultati incrementali e sul completamento, chiamare i metodi <xref:System.ComponentModel.AsyncOperation.Post%2A> e <xref:System.ComponentModel.AsyncOperation.OperationCompleted%2A> sull'oggetto <xref:System.ComponentModel.AsyncOperation>.<xref:System.ComponentModel.AsyncOperation> è responsabile del marshalling delle chiamate sui gestori eventi del client al thread o al contesto appropriato.  
  
> [!NOTE]
>  È possibile aggirare queste regole se si vuole esplicitamente evitare l'uso dei criteri del modello di applicazione, pur usufruendo degli altri vantaggi derivanti dal modello asincrono basato su eventi. È ad esempio possibile creare una classe threading Free operante in Windows Form, purché agli sviluppatori siano chiare le restrizioni implicate. Le applicazioni console non sincronizzano l'esecuzione delle chiamate del metodo <xref:System.ComponentModel.AsyncOperation.Post%2A>. L'ordine di generazione degli eventi `ProgressChanged` potrebbe quindi non essere corretto. Se si vuole l'esecuzione serializzata delle chiamate al metodo <xref:System.ComponentModel.AsyncOperation.Post%2A>, implementare e installare una classe <xref:System.Threading.SynchronizationContext?displayProperty=fullName>.  
  
 Per altre informazioni sull'uso di <xref:System.ComponentModel.AsyncOperation> e <xref:System.ComponentModel.AsyncOperationManager> per consentire operazioni asincrone, vedere [Walkthrough: Implementing a Component That Supports the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md).  
  
## Indicazioni  
  
-   È preferibile che ogni chiamata a un metodo sia indipendente dalle altre. Si consiglia di evitare di associare chiamate a risorse condivise. Se le risorse devono essere condivise tra le chiamate, è necessario fornire un meccanismo di sincronizzazione adeguato nell'implementazione.  
  
-   Non sono consigliati progetti in cui al client sia richiesta l'implementazione della funzionalità di sincronizzazione. Si supponga il caso di un metodo asincrono che riceve un oggetto statico globale come parametro. Più chiamate simultanee a tale metodo potrebbero determinare il danneggiamento dei dati o deadlock.  
  
-   Se si implementa un metodo con l'overload a più chiamate \(`userState` nella firma\), la classe dovrà gestire un insieme di stati utente, o ID attività, e le relative operazioni in sospeso. Questa raccolta deve essere protetta con aree `lock`, in quanto le varie chiamate aggiungono e rimuovono gli oggetti `userState` presenti al suo interno.  
  
-   Riutilizzare le classi `CompletedEventArgs`, quando possibile e appropriato. In tal caso, la denominazione non sarà coerente con il nome del metodo, poiché un determinato delegato e il tipo <xref:System.EventArgs> non saranno collegati a un unico metodo. Non è tuttavia accettabile imporre agli sviluppatori di eseguire il cast del valore recuperato da una proprietà sull'oggetto <xref:System.EventArgs>.  
  
-   Se si sta creando una classe che deriva da <xref:System.ComponentModel.Component>, non implementare e installare la propria classe <xref:System.Threading.SynchronizationContext>. Sono i modelli di applicazione e non i componenti a controllare l'oggetto <xref:System.Threading.SynchronizationContext> usato.  
  
-   L'uso di qualsiasi tipo di multithreading determina la potenziale esposizione a bug seri e complessi. Pertanto, prima di implementare una soluzione che preveda l'uso del multithreading, vedere [Managed Threading Best Practices](../../../docs/standard/threading/managed-threading-best-practices.md).  
  
## Vedere anche  
 <xref:System.ComponentModel.AsyncOperation>   
 <xref:System.ComponentModel.AsyncOperationManager>   
 <xref:System.ComponentModel.AsyncCompletedEventArgs>   
 <xref:System.ComponentModel.ProgressChangedEventArgs>   
 <xref:System.ComponentModel.BackgroundWorker>   
 [Implementing the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/implementing-the-event-based-asynchronous-pattern.md)   
 [Multithreaded Programming with the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/multithreaded-programming-with-the-event-based-asynchronous-pattern.md)   
 [Deciding When to Implement the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md)   
 [Best Practices for Implementing the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)   
 [How to: Use Components That Support the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/how-to-use-components-that-support-the-event-based-asynchronous-pattern.md)   
 [Walkthrough: Implementing a Component That Supports the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)