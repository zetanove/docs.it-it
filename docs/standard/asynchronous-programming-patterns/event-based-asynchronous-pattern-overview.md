---
title: "Event-based Asynchronous Pattern Overview | Microsoft Docs"
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
  - "Asynchronous Pattern"
  - "AsyncOperationManager class"
  - "threading [.NET Framework], asynchronous features"
  - "AsyncOperation class"
  - "AsyncCompletedEventArgs class"
ms.assetid: 792aa8da-918b-458e-b154-9836b97735f3
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Event-based Asynchronous Pattern Overview
Le applicazioni che eseguono più attività contemporaneamente, pur rimanendo disponibili all'utente, richiedono spesso una progettazione che preveda l'uso di più thread.  Lo spazio dei nomi <xref:System.Threading> offre tutti gli strumenti necessari per creare applicazioni multithreading a elevate prestazioni, per l'uso dei quali è necessaria tuttavia una notevole esperienza nel campo della progettazione di software multithreading.  Per applicazioni multithreading relativamente semplici, il componente <xref:System.ComponentModel.BackgroundWorker> rappresenta una soluzione adeguata.  Per applicazioni asincrone più complesse, si consiglia di implementare una classe che segua il modello asincrono basato su eventi.  
  
 Tale modello consente di usufruire dei vantaggi offerti dalle applicazioni multithreading nascondendo al contempo gran parte degli aspetti complessi inerenti la progettazione multithreading.  L'uso di una classe che supporta questo modello consente di:  
  
-   Eseguire in background attività che richiedono una quantità eccessiva di tempo, come download e operazioni di database, senza interrompere l'applicazione.  
  
-   Eseguire più operazioni contemporaneamente, ricevendo notifiche relative al completamento di ognuna.  
  
-   Attendere la disponibilità delle risorse senza interrompere o sospendere l'esecuzione dell'applicazione.  
  
-   Comunicare con operazioni asincrone in sospeso mediante un modello noto di eventi e delegati.  Per altre informazioni sull'uso di gestori eventi e delegati, vedere [Eventi](../../../docs/standard/events/index.md).  
  
 Una classe che supporta il modello asincrono basato su eventi avrà uno o più metodi denominati *MethodName*`Async`.  Tali metodi possono eseguire il mirroring delle versioni sincrone che eseguono la stessa operazione sul thread corrente.  La classe potrebbe anche avere un evento *MethodName*`Completed` e un metodo *MethodName*`AsyncCancel` \(o semplicemente `CancelAsync`\).  
  
 <xref:System.Windows.Forms.PictureBox> è un componente tipico che supporta il modello asincrono basato su eventi.  Per scaricare un'immagine in modo sincrono è possibile chiamare il relativo metodo <xref:System.Windows.Forms.PictureBox.Load%2A>, ma qualora le dimensioni dell'immagine fossero eccessive o la connessione di rete troppo lenta, l'esecuzione dell'applicazione verrà interrotta o sospesa fino al completamento dell'operazione di download e alla restituzione della chiamata a <xref:System.Windows.Forms.PictureBox.Load%2A>.  
  
 Per lasciare che l'applicazione continui a essere eseguita durante il caricamento dell'immagine, è possibile chiamare il metodo <xref:System.Windows.Forms.PictureBox.LoadAsync%2A> e gestire l'evento <xref:System.Windows.Forms.PictureBox.LoadCompleted> analogamente a qualsiasi altro evento.  Quando si chiama il metodo <xref:System.Windows.Forms.PictureBox.LoadAsync%2A> l'esecuzione dell'applicazione procede mentre l'operazione di download continua su un altro thread, in background.  Al termine dell'operazione di caricamento dell'immagine verrà chiamato il gestore eventi che potrà esaminare il parametro <xref:System.ComponentModel.AsyncCompletedEventArgs> per determinare se il download è stato eseguito.  
  
 Il modello asincrono basato su eventi richiede la possibilità di annullare un'operazione asincrona, requisito supportato dal controllo <xref:System.Windows.Forms.PictureBox> per mezzo del relativo metodo <xref:System.Windows.Forms.PictureBox.CancelAsync%2A>.  La chiamata del metodo <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> determina l'invio di una richiesta di interruzione del download in sospeso. Quando l'attività viene annullata, viene generato l'evento <xref:System.Windows.Forms.PictureBox.LoadCompleted>.  
  
> [!CAUTION]
>  Il download potrebbe terminare non appena viene effettuata la richiesta di <xref:System.Windows.Forms.PictureBox.CancelAsync%2A>. In tal caso, la proprietà <xref:System.ComponentModel.AsyncCompletedEventArgs.Cancelled%2A> potrebbe non riflettere la richiesta di annullamento.  Si tratta di una *race condition*, ovvero di un problema riscontrato comunemente nella programmazione multithreading.  Per altre informazioni sui problemi inerenti la programmazione multithreading, vedere [Managed Threading Best Practices](../../../docs/standard/threading/managed-threading-best-practices.md).  
  
## Caratteristiche del modello asincrono basato su eventi  
 Sono disponibili diversi tipi di modello asincrono basato su eventi, a seconda della complessità delle operazioni supportate da una determinata classe.  Le classi più semplici possono presentare un solo metodo *MethodName*`Async` e un evento *MethodName*`Completed` corrispondente.  Le classi più complesse possono invece avere diversi metodi *MethodName*`Async` ognuno dei quali con un evento *MethodName*`Completed` associato, nonché versioni sincrone di tali metodi.  Per ogni metodo asincrono le classi possono supportare funzionalità di annullamento e creazione di rapporti sullo stato di avanzamento, nonché risultati incrementali.  
  
 Un metodo asincrono può anche supportare più chiamate in sospeso, ovvero più richiami concorrenti, consentendo al codice di chiamarlo un numero indeterminato di volte prima del completamento di altre operazioni in sospeso.  Una gestione efficace di questa situazione può richiedere che l'applicazione tenga traccia del completamento di ogni operazione.  
  
### Esempi del modello asincrono basato su eventi  
 I componenti <xref:System.Media.SoundPlayer> e <xref:System.Windows.Forms.PictureBox> rappresentano implementazioni semplici del modello asincrono basato su eventi.  I componenti <xref:System.Net.WebClient> e <xref:System.ComponentModel.BackgroundWorker> rappresentano implementazioni più complesse del modello in questione.  
  
 Di seguito viene riportata una dichiarazione di classe di esempio conforme al modello:  
  
```vb  
Public Class AsyncExample  
    ' Synchronous methods.  
    Public Function Method1(ByVal param As String) As Integer   
    Public Sub Method2(ByVal param As Double)   
  
    ' Asynchronous methods.  
    Overloads Public Sub Method1Async(ByVal param As String)   
    Overloads Public Sub Method1Async(ByVal param As String, ByVal userState As Object)   
    Public Event Method1Completed As Method1CompletedEventHandler  
  
    Overloads Public Sub Method2Async(ByVal param As Double)   
    Overloads Public Sub Method2Async(ByVal param As Double, ByVal userState As Object)   
    Public Event Method2Completed As Method2CompletedEventHandler  
  
    Public Sub CancelAsync(ByVal userState As Object)   
  
    Public ReadOnly Property IsBusy () As Boolean  
  
    ' Class implementation not shown.  
End Class  
```  
  
```csharp  
public class AsyncExample  
{  
    // Synchronous methods.  
    public int Method1(string param);  
    public void Method2(double param);  
  
    // Asynchronous methods.  
    public void Method1Async(string param);  
    public void Method1Async(string param, object userState);  
    public event Method1CompletedEventHandler Method1Completed;  
  
    public void Method2Async(double param);  
    public void Method2Async(double param, object userState);  
    public event Method2CompletedEventHandler Method2Completed;  
  
    public void CancelAsync(object userState);  
  
    public bool IsBusy { get; }  
  
    // Class implementation not shown.  
}  
```  
  
 La classe `AsyncExample` fittizia presenta due metodi che supportano entrambi i richiami sincroni e asincroni.  Gli overload sincroni si comportano come qualsiasi chiamata di metodo ed eseguono le operazioni sul thread chiamante. Se l'operazione eseguita richiede tempo, potrebbe verificarsi un ritardo notevole nella restituzione della chiamata.  Gli overload asincroni avviano l'operazione su un altro thread e vengono restituiti immediatamente consentendo al thread chiamante di continuare mentre l'operazione viene eseguita in background.  
  
### Overload di metodi asincroni  
 Esistono potenzialmente due overload per le operazioni asincrone: a richiamo singolo e a più richiami.  È possibile distinguere i due tipi di overload dalle firme dei relativi metodi. Il tipo a più richiami presenta un parametro supplementare denominato `userState` e consente al codice di chiamare più volte `Method1Async(string param, object userState)` senza attendere il completamento di eventuali operazioni asincrone in sospeso.  Se, invece, si prova a chiamare `Method1Async(string param)` prima del completamento di un richiamo precedente, il metodo genera una <xref:System.InvalidOperationException>.  
  
 Il parametro `userState` degli overload a più richiami consente di distinguere le diverse operazioni asincrone.  Specificare un valore univoco, ad esempio un GUID o un codice hash, per ogni chiamata al metodo  `Method1Async(string param, object userState)`. Al termine di ogni operazione, il gestore eventi potrà individuare l'istanza dell'operazione che ha generato l'evento di completamento.  
  
### Verifica delle operazioni in sospeso  
 Se si usano gli overload a più richiami, il codice deve tenere traccia degli oggetti `userState` \(o ID attività\) relativi alle attività in sospeso.  Per ogni chiamata al metodo  `Method1Async(string param, object userState)`, di solito viene generato un nuovo oggetto `userState` univoco che viene aggiunto a una raccolta.  Quando l'attività corrispondente a tale oggetto `userState` genera l'evento di completamento, l'implementazione del metodo di completamento esamina <xref:System.ComponentModel.AsyncCompletedEventArgs.UserState%2A?displayProperty=fullName> e la rimuove dalla raccolta.  Se usato in questo modo, il parametro `userState` funge da ID attività.  
  
> [!NOTE]
>  È necessario specificare un valore univoco per il parametro `userState` nelle chiamate a overload a più richiami.  La specifica di ID attività non univoci determina la generazione di una <xref:System.ArgumentException> da parte della classe asincrona.  
  
### Annullamento delle operazioni in sospeso  
 È importante che sia possibile annullare le operazioni asincrone in qualsiasi momento prima che vengano completate.  Le classi che implementano il modello asincrono basato su eventi avranno un metodo `CancelAsync` o *MethodName*`AsyncCancel` \(se sono presenti rispettivamente un solo metodo asincrono o più metodi asincroni\).  
  
 I metodi che consentono più chiamate accettano un parametro `userState` che può essere usato per tenere traccia della durata di ogni attività.  `CancelAsync` accetta un parametro `userState` che consente di annullare attività specifiche in sospeso.  
  
 I metodi che supportano una sola operazione in sospeso alla volta, come `Method1Async(string param)`, non sono annullabili.  
  
### Ricezione di aggiornamenti sullo stato di avanzamento e di risultati incrementali  
 Per tenere traccia dello stato di avanzamento e dei risultati incrementali, una classe conforme al modello asincrono basato su eventi può facoltativamente fornire un evento,  in genere è denominato `ProgressChanged` o *MethodName*`ProgressChanged`, il cui gestore eventi accetta un parametro <xref:System.ComponentModel.ProgressChangedEventArgs>.  
  
 Il gestore eventi relativo all'evento `ProgressChanged` può esaminare la proprietà <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A?displayProperty=fullName> per determinare la percentuale di completamento di un'attività asincrona.  Questa proprietà ha il valore compreso tra 0 e 100 e può essere usata per aggiornare la proprietà <xref:System.Windows.Forms.ProgressBar.Value%2A> di un oggetto <xref:System.Windows.Forms.ProgressBar>.  Se sono in sospeso più operazioni asincrone, è possibile usare la proprietà <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A?displayProperty=fullName> per identificare l'operazione per la quale viene generato il rapporto sullo stato di avanzamento.  
  
 Alcune classi possono generare un rapporto sui risultati incrementali mano a mano che procede l'esecuzione delle operazioni asincrone.  I risultati verranno memorizzati in una classe derivata da <xref:System.ComponentModel.ProgressChangedEventArgs> e verranno visualizzati come proprietà nella classe derivata.  È possibile accedere ai risultati nel gestore eventi dell'evento `ProgressChanged` usando la stessa procedura valida per la proprietà <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A>.  Se sono in sospeso più operazioni asincrone, è possibile usare la proprietà <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A> per identificare l'operazione per la quale viene generato il rapporto sui risultati incrementali.  
  
## Vedere anche  
 <xref:System.ComponentModel.ProgressChangedEventArgs>   
 <xref:System.ComponentModel.BackgroundWorker>   
 <xref:System.ComponentModel.AsyncCompletedEventArgs>   
 [How to: Use Components That Support the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/how-to-use-components-that-support-the-event-based-asynchronous-pattern.md)   
 [Procedura: eseguire un'operazione in background](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)   
 [Procedura: implementare un form che utilizza un'operazione in background](../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)   
 [Multithreaded Programming with the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/multithreaded-programming-with-the-event-based-asynchronous-pattern.md)   
 [Suggerimenti per l'implementazione del modello asincrono basato su eventi](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)   
 [Deciding When to Implement the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md)