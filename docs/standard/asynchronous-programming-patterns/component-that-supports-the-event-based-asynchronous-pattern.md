---
title: "Walkthrough: Implementing a Component That Supports the Event-based Asynchronous Pattern | Microsoft Docs"
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
  - "components [.NET Framework], asynchronous"
  - "AsyncOperation class"
  - "threading [Windows Forms], asynchronous features"
  - "AsyncCompletedEventArgs class"
ms.assetid: 61f676b5-936f-40f6-83ce-f22805ec9c2f
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Walkthrough: Implementing a Component That Supports the Event-based Asynchronous Pattern
Se la scrittura di una classe implica operazioni che possono causare ritardi notevoli, è possibile assegnare alla classe la funzionalità asincrona implementando [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md).  
  
 In questa procedura dettagliata viene illustrato come creare un componente che implementa il modello asincrono basato su eventi.  L'implementazione viene eseguita mediante le classi di supporto dello spazio dei nomi <xref:System.ComponentModel?displayProperty=fullName>. In questo modo è garantito il funzionamento del componente in qualsiasi modello di applicazione, incluse le applicazioni [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)], console e Windows Form.  Questo componente può anche essere progettato con un controllo <xref:System.Windows.Forms.PropertyGrid> e con strumenti di progettazione personalizzati.  
  
 Nel corso della procedura si disporrà di un'applicazione che consente di calcolare in modo asincrono i numeri primi.  L'applicazione in questione contiene un thread dell'interfaccia utente principale e un thread per ogni calcolo eseguito sui numeri primi.  Sebbene il test eseguito per verificare se un numero grande è un numero primo possa richiedere una notevole quantità di tempo, il thread dell'interfaccia utente principale non verrà interrotto da questo ritardo e il form sarà reattivo nel corso dei calcoli.  Sarà possibile eseguire il numero desiderato di calcoli concorrenti e annullare in modo selettivo i calcoli in sospeso.  
  
 Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Creazione del componente  
  
-   Definizione di eventi e delegati asincroni pubblici  
  
-   Definizione di delegati privati  
  
-   Implementazione di eventi pubblici  
  
-   Implementazione del metodo di completamento  
  
-   Implementazione dei metodi di lavoro  
  
-   Implementazione dei metodi di avvio e annullamento  
  
 Per copiare il codice nell'argomento corrente come un elenco singolo, vedere [How to: Implement a Component That Supports the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md).  
  
## Creazione del componente  
 Il primo passaggio consiste nella creazione del componente che implementerà il modello asincrono basato su eventi.  
  
#### Per creare un componente  
  
-   Creare una classe denominata `PrimeNumberCalculator` che eredita da <xref:System.ComponentModel.Component>.  
  
## Definizione di eventi e delegati asincroni pubblici  
 Il componente comunica con i client per mezzo degli eventi.  L'evento *MethodName*`Completed` avvisa i client del completamento di un'attività asincrona, mentre l'evento *NomeMetodo*`ProgressChanged` li informa dello stato di avanzamento di tale attività.  
  
#### Per definire eventi asincroni per i client del componente:  
  
1.  Importare gli spazi dei nomi <xref:System.Threading?displayProperty=fullName> e <xref:System.Collections.Specialized?displayProperty=fullName> nella parte superiore del file.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#11](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#11)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#11](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#11)]  
  
2.  Prima della definizione della classe `PrimeNumberCalculator` , dichiarare i delegati per gli eventi di avanzamento e completamento.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#7](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#7)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#7](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#7)]  
  
3.  Prima della definizione della classe `PrimeNumberCalculator` , dichiarare gli eventi per la generazione di report sullo stato di avanzamento e sul completamento destinati ai client.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#8](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#8)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#8](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#8)]  
  
4.  Dopo la definizione della classe `PrimeNumberCalculator` , derivare la classe  `CalculatePrimeCompletedEventArgs` per la generazione del report sul risultato di ogni calcolo destinato al gestore eventi del client relativo all'evento `CalculatePrimeCompleted`.  Oltre alle proprietà `AsyncCompletedEventArgs`, questa classe consente al client di determinare il numero sottoposto a test, se si tratta di un numero primo e il valore del primo divisore, se non è numero primo.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#6](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#6)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#6](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#6)]  
  
## Verifica  
 A questo punto, è possibile compilare il componente.  
  
#### Per eseguire il test del componente  
  
-   Compilare il componente.  
  
     Verranno visualizzati due messaggi di avviso del compilatore:  
  
    ```  
    warning CS0067: The event 'AsynchronousPatternExample.PrimeNumberCalculator.ProgressChanged' is never used  
    warning CS0067: The event 'AsynchronousPatternExample.PrimeNumberCalculator.CalculatePrimeCompleted' is never used  
    ```  
  
     Questi messaggi verranno eliminati nella sezione successiva.  
  
## Definizione di delegati privati  
 Le caratteristiche asincrone del componente `PrimeNumberCalculator` vengono implementate internamente con un delegato speciale noto come <xref:System.Threading.SendOrPostCallback> Un <xref:System.Threading.SendOrPostCallback> che rappresenta un metodo di callback eseguito su un thread <xref:System.Threading.ThreadPool>.  Il metodo di callback deve presentare una firma che accetti un solo parametro di tipo <xref:System.Object>. In altre parole, sarà necessario passare lo stato tra i delegati di una classe wrapper.  Per ulteriori informazioni, vedere <xref:System.Threading.SendOrPostCallback>.  
  
#### Per implementare il comportamento asincrono interno del componente:  
  
1.  Dichiarare e creare i delegati <xref:System.Threading.SendOrPostCallback> nella classe `PrimeNumberCalculator` .  Creare gli oggetti <xref:System.Threading.SendOrPostCallback> in un metodo di utilità denominato  `InitializeDelegates`.  
  
     Saranno necessari due delegati, ovvero uno per segnalare lo stato di avanzamento al client e uno per informarlo del completamento dell'operazione.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#9](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#9)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#9](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#9)]  
    [!code-csharp[System.ComponentModel.AsyncOperationManager#20](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#20)]
    [!code-vb[System.ComponentModel.AsyncOperationManager#20](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#20)]  
  
2.  Chiamare il metodo `InitializeDelegates` nel costruttore del componente.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#21](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#21)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#21](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#21)]  
  
3.  Dichiarare un delegato nella classe `PrimeNumberCalculator` che gestisce il lavoro effettivo da eseguire in modo asincrono.  Questo delegato esegue il wrapping del metodo di lavoro che esegue il test per verificare se un numero è numero primo.  Il delegato accetta un parametro <xref:System.ComponentModel.AsyncOperation> che verrà utilizzato per tenere traccia del ciclo di vita dell'operazione asincrona.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#22](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#22)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#22](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#22)]  
  
4.  Creare una raccolta per la gestione dei cicli di vita delle operazioni asincrone in sospeso.  Al client è necessario un sistema per tenere traccia delle operazioni nel corso dell'esecuzione e al completamento e tale sistema consiste nella richiesta di passare un token univoco o un ID attività quando il client effettua la chiamata al metodo asincrono.  Il componente `PrimeNumberCalculator` deve tenere traccia di ogni chiamata associando l'ID attività al relativo richiamo.  Se il client passa un ID attività non univoco, il componente `PrimeNumberCalculator` deve generare un'eccezione.  
  
     Il componente `PrimeNumberCalculator` tiene traccia dell'ID attività utilizzando una classe di raccolta speciale denominata <xref:System.Collections.Specialized.HybridDictionary>.  Nella definizione della classe creare un oggetto <xref:System.Collections.Specialized.HybridDictionary> denominato  `userTokenToLifetime`.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#23](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#23)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#23](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#23)]  
  
## Implementazione di eventi pubblici  
 I componenti che implementano il modello asincrono basato su eventi comunicano con i client mediante gli eventi.  Tali eventi vengono richiamati sul thread appropriato con il supporto della classe <xref:System.ComponentModel.AsyncOperation>.  
  
#### Per generare eventi per i client del componente:  
  
1.  Implementare gli eventi pubblici per la generazione di report destinati ai client.  Sono necessari un evento per la generazione di report sullo stato di avanzamento e uno per la generazione di report sul completamento.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#24](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#24)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#24](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#24)]  
  
## Implementazione del metodo di completamento  
 Il delegato di completamento è il metodo richiamato dal comportamento asincrono di threading Free sottostante quando un'operazione asincrona viene terminata per completamento, errore o annullamento.  Questo richiamo si verifica su un thread arbitrario.  
  
 Il metodo in questione rappresenta la posizione in cui l'ID attività del client viene rimosso dalla raccolta interna di token client univoci  e termina il ciclo di vita di una determinata operazione asincrona mediante la chiamata del metodo <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A> sull'oggetto <xref:System.ComponentModel.AsyncOperation> corrispondente.  Questa chiamata genera l'evento di completamento sul thread appropriato per il modello di applicazione.  In seguito alla chiamata del metodo <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A>, questa istanza di <xref:System.ComponentModel.AsyncOperation> non potrà essere più utilizzata. Pertanto, tutti i tentativi successivi di utilizzo genereranno un'eccezione.  
  
 La firma `CompletionMethod` deve contenere qualsiasi stato necessario a descrivere il risultato dell'operazione asincrona.  Il parametro contiene lo stato relativo al numero sottoposto a test nel corso dell'operazione asincrona, la specifica di numero primo, se applicabile, e il valore del primo divisore, se non corrisponde a un numero primo,  nonché lo stato che descrive le eventuali eccezioni generate e l'oggetto <xref:System.ComponentModel.AsyncOperation> corrispondente all'attività in questione.  
  
#### Per completare un'operazione asincrona:  
  
-   Implementare il metodo di completamento  Accetta sei parametri che utilizza per inserire i dati in un oggetto  `CalculatePrimeCompletedEventArgs` restituito al client tramite l'oggetto  `CalculatePrimeCompletedEventHandler` del client.  Tale metodo rimuove l'ID attività del client dalla raccolta interna e termina il ciclo di vita dell'operazione asincrona con una chiamata al metodo <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A>.  L'oggetto <xref:System.ComponentModel.AsyncOperation> esegue il marshalling della chiamata al thread o al contesto appropriato per il modello di applicazione.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#26](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#26)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#26](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#26)]  
  
## Verifica  
 A questo punto, è possibile compilare il componente.  
  
#### Per eseguire il test del componente  
  
-   Compilare il componente.  
  
     Verrà visualizzato un messaggio di avviso del compilatore:  
  
    ```  
    warning CS0169: The private field 'AsynchronousPatternExample.PrimeNumberCalculator.workerDelegate' is never used  
    ```  
  
     Questo messaggio verrà eliminato nella sezione successiva.  
  
## Implementazione dei metodi di lavoro  
 Finora è stato implementato il codice asincrono di supporto del componente `PrimeNumberCalculator`.  A questo punto, è possibile implementare il codice che esegue le operazioni effettive.  Verranno implementati tre metodi: `CalculateWorker`, `BuildPrimeNumberList` e `IsPrime`.  Insieme, i metodi `BuildPrimeNumberList` e `IsPrime` formano un algoritmo, noto come crivello di Eratostene, che determina se un numero è primo mediante la ricerca di tutti i numeri primi fino alla radice quadrata del numero sottoposto a test.  Se non vengono individuati divisori in corrispondenza di tale punto, il numero sottoposto a test è un numero primo.  
  
 Se il componente fosse stato scritto per ottenere i massimi risultati, avrebbe tenuto traccia di tutti i numeri primi rilevati dai vari richiami dei diversi numeri sottoposti a test  Avrebbe inoltre verificato la presenza di divisori triviali come 2, 3 e 5.  Lo scopo di questo esempio è dimostrare come eseguire in modo asincrono operazioni che richiedono molto tempo. Pertanto, questi esempi di ottimizzazione vengono lasciati come esercizio per l'utente.  
  
 Il metodo `CalculateWorker` viene sottoposto a wrapping in un delegato e richiamato in modo asincrono con una chiamata a `BeginInvoke`.  
  
> [!NOTE]
>  La segnalazione dello stato di avanzamento è implementata nel metodo `BuildPrimeNumberList`.  Nei computer veloci gli eventi `ProgressChanged` possono essere generati in rapida successione.  Il thread del client, su cui vengono generati tali eventi, deve essere in grado di gestire la situazione.  Il codice dell'interfaccia utente può venire sovraccaricato dai messaggi e non riuscire a tenere il passo, giungendo a un punto di stallo.  Per un esempio di interfaccia utente in grado di gestire tale situazione, vedere [How to: Implement a Client of the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md).  
  
#### Per eseguire in modo asincrono il calcolo dei numeri primi:  
  
1.  Implementare il metodo di utilità `TaskCanceled`.  Viene così verificato se nella raccolta dei cicli di vita delle attività è presente l'ID attività specificato e, in caso negativo, viene restituito `true`.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#32](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#32)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#32](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#32)]  
  
2.  Implementare il metodo `CalculateWorker`.  Il metodo accetta due parametri, ovvero il numero da sottoporre a test e un oggetto <xref:System.ComponentModel.AsyncOperation>,  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#27](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#27)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#27](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#27)]  
  
3.  Implementare `BuildPrimeNumberList` Il metodo accetta due parametri, ovvero il numero da sottoporre a test e un oggetto <xref:System.ComponentModel.AsyncOperation>,  e utilizza l'oggetto <xref:System.ComponentModel.AsyncOperation> per generare report sullo stato di avanzamento e sui risultati incrementali.  In questo modo è garantito che i gestori eventi del client vengano chiamati sul thread o sul contesto appropriato al modello di applicazione.  Quando `BuildPrimeNumberList` trova un numero primo, lo inserisce come risultato incrementale in un report destinato al gestore eventi del client per l'evento `ProgressChanged`.  È richiesta una classe derivata da <xref:System.ComponentModel.ProgressChangedEventArgs>, denominata `CalculatePrimeProgressChangedEventArgs`, avente una proprietà aggiuntiva `LatestPrimeNumber`.  
  
     Il metodo `BuildPrimeNumberList` inoltre chiama periodicamente il metodo `TaskCanceled` e viene terminato se viene restituito `true`.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#5)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#5)]  
  
4.  Implementare `IsPrime` Tale metodo accetta tre parametri, ovvero un elenco dei numeri primi noti, il numero di cui eseguire il test e un parametro di output per il primo divisore trovato.  Partendo dall'elenco di numeri primi, il metodo determina se il numero sottoposto a test ne fa parte.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#28](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#28)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#28](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#28)]  
  
5.  Derivare `CalculatePrimeProgressChangedEventArgs` da <xref:System.ComponentModel.ProgressChangedEventArgs>.  Questa classe è necessaria per la generazione di report sui risultati incrementali destinati al gestore eventi del client relativo all'evento `ProgressChanged` e presenta una proprietà aggiuntiva denominata `LatestPrimeNumber`.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#29](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#29)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#29](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#29)]  
  
## Verifica  
 A questo punto, è possibile compilare il componente.  
  
#### Per eseguire il test del componente  
  
-   Compilare il componente.  
  
     Gli unici elementi ancora da scrivere sono i metodi di avvio e annullamento delle operazioni asincrone, `CalculatePrimeAsync` e `CancelAsync`.  
  
## Implementazione dei metodi di avvio e annullamento  
 Per avviare il metodo di lavoro sul relativo thread è possibile chiamare `BeginInvoke` sul delegato che lo contiene.  Per gestire il ciclo di vita di una determinata operazione asincrona, è possibile chiamare il metodo <xref:System.ComponentModel.AsyncOperationManager.CreateOperation%2A> sulla classe di supporto <xref:System.ComponentModel.AsyncOperationManager>.  Viene restituito un oggetto <xref:System.ComponentModel.AsyncOperation> che esegue il marshalling delle chiamate sui gestori eventi del client al thread o al contesto appropriato.  
  
 Per annullare una determinata operazione in corso è possibile chiamare <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A> sull'oggetto <xref:System.ComponentModel.AsyncOperation> corrispondente.  In questo modo l'operazione specifica viene terminata e tutte le chiamate successive al relativo oggetto <xref:System.ComponentModel.AsyncOperation> generano un'eccezione.  
  
#### Per implementare la funzionalità di avvio e annullamento:  
  
1.  Implementare il metodo `CalculatePrimeAsync`.  Verificare che il token fornito dal client \(ID attività\) sia univoco rispetto a tutti i token che rappresentano le attività in sospeso.  Se il client passa un token non univoco, `CalculatePrimeAsync` genera un'eccezione.  In caso contrario, il token viene aggiunto alla raccolta di ID attività.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#3)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#3)]  
  
2.  Implementare il metodo `CancelAsync`.  Se nella raccolta dei token è presente il parametro `taskId`, verrà rimosso.  In questo modo viene impedita l'esecuzione delle attività annullate non ancora avviate.  Se l'attività è in esecuzione, il metodo `BuildPrimeNumberList` viene terminato quando rileva che l'ID attività è stato rimosso dalla raccolta dei cicli di vita.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#4)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#4)]  
  
## Verifica  
 A questo punto, è possibile compilare il componente.  
  
#### Per eseguire il test del componente  
  
-   Compilare il componente.  
  
 A questo punto, il componente `PrimeNumberCalculator` è completo e può essere utilizzato.  
  
 Per un client di esempio che utilizzi il componente `PrimeNumberCalculator`, vedere [How to: Implement a Client of the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md).  
  
## Passaggi successivi  
 Per completare l'esempio è possibile scrivere `CalculatePrime`, l'equivalente sincrono del metodo `CalculatePrimeAsync`.  In questo modo il componente `PrimeNumberCalculator` verrà reso completamente conforme al modello asincrono basato su eventi.  
  
 Per migliorare l'esempio è possibile conservare l'elenco di tutti i numeri primi rilevati durante i vari richiami dei diversi numeri sottoposti a test.  Con questo approccio ogni attività potrà usufruire dei vantaggi derivanti dalle attività già eseguite.  Proteggere l'elenco con le aree `lock` in modo da serializzarne l'accesso da parte dei diversi thread.  
  
 Per migliorare ulteriormente l'esempio è possibile eseguire il test di divisori triviali come 2, 3 e 5.  
  
## Vedere anche  
 [Procedura: eseguire un'operazione in background](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)   
 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)   
 [NOT IN BUILD: Multithreading in Visual Basic](http://msdn.microsoft.com/it-it/c731a50c-09c1-4468-9646-54c86b75d269)   
 [How to: Implement a Component That Supports the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)   
 [Multithreaded Programming with the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/multithreaded-programming-with-the-event-based-asynchronous-pattern.md)