---
title: La programmazione asincrona in dettaglio
description: Spiegazione approfondita di come funziona il codice asincrono in .NET
keywords: .NET, .NET Core, .NET standard
author: cartermp
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 1e38f9d9-8f84-46ee-a15f-199aec4f2e34
translationtype: Human Translation
ms.sourcegitcommit: b967d8e55347f44a012e4ad8e916440ae228c8ec
ms.openlocfilehash: 92d94fd7f148bb4c1bbad50212d90d722214085f
ms.lasthandoff: 03/10/2017

---

# <a name="async-in-depth"></a>La programmazione asincrona in dettaglio

La scrittura di codice asincrono associato a I/O e CPU risulta notevolmente semplificata dall'uso del modello asincrono basato su attività di .NET. Il modello viene esposto dai tipi `Task` e `Task<T>` e dalle parole chiave del linguaggio `async` e `await`. In questo articolo viene illustrato come usare il codice asincrono di .NET e vengono specificate informazioni approfondite sul framework asincrono che ne è alla base.

## <a name="task-and-tasklttgt"></a>Task e Task&lt;T&gt;

Le attività sono costrutti usati per implementare il cosiddetto [Modello di concorrenza basato su promise](https://en.wikipedia.org/wiki/Futures_and_promises).  In poche parole offrono la "promessa" che il lavoro verrà completato in un secondo memento, consentendo all'utente di coordinare la promessa con un'API nuova.

*   `Task` rappresenta una singola operazione che non restituisce alcun valore.
*   `Task<T>` rappresenta una singola operazione che restituisce un valore di tipo `T`.

È importante considerare le attività come astrazioni del lavoro che si svolge in modo asincrono e *non* un'astrazione sul threading. Per impostazione predefinita, le attività vengono eseguite sul thread corrente e delegano il lavoro al sistema operativo, in base alle necessità. Facoltativamente, le attività possono essere esplicitamente richieste per l'esecuzione in un thread separato tramite l'API `Task.Run`.

Le attività espongono un protocollo di API per il monitoraggio, attendendo il valore risultante di un'attività cui poi accedono (nel caso di `Task<T>`). L'integrazione del linguaggio, con la parola chiave `await`, offre un'astrazione di livello superiore per l'uso delle attività. 

L'uso di `await` consente all'applicazione o al servizio di eseguire operazioni utili mentre viene eseguita un'attività, cedendo il controllo al chiamante fino al completamento dell'attività. Non è necessario che il codice si basi su callback o eventi perché continui a essere eseguito dopo il completamento dell'attività. Sono il linguaggio e l'integrazione dell'API dell'attività a occuparsi di questo. Se si usa `Task<T>`, al completamento dell'attività la parola chiave `await` "dispiegherà" ulteriormente il valore restituito.  I dettagli di questo processo sono illustrati più sotto.

Per altre informazioni sulle attività e i diversi modi per interagire con esse, vedere l'articolo [Task-based Asynchronous Pattern (TAP)](https://msdn.microsoft.com/library/hh873175.aspx) (Modello asincrono basato su attività).

## <a name="deeper-dive-into-tasks-for-an-io-bound-operation"></a>Approfondimento sulle attività per un'operazione associata ai I/O

La sezione seguente offre una panoramica di ciò che accade con una chiamata I/O asincrona tipica. Iniziamo con alcuni esempi.

Nel primo esempio viene chiamato un metodo asincrono e viene restituita un'attività attiva, ancora da completare.

```csharp
public Task<string> GetHtmlAsync()
{
     // Execution is synchronous here
    var client = new HttpClient();
    
    return client.GetStringAsync("http://www.dotnetfoundation.org");
}
```

Nel secondo esempio viene aggiunto l'uso delle parole chiave `async` e `await` per il funzionamento dell'attività.

```csharp
public async Task<string> GetFirstCharactersCountAsync(string url, int count)
{
    // Execution is synchronous here
    var client = new HttpClient();
    
    // Execution of GetFirstCharactersCountAsync() is yielded to the caller here
    // GetStringAsync returns a Task<string>, which is *awaited*
    var page = await client.GetStringAsync("http://www.dotnetfoundation.org");
    
    // Execution resumes when the client.GetStringAsync task completes,
    // becoming synchronous again.
    
    if (count > page.Length)
    {
        return page;
    }
    else
    {
        return page.Substring(0, count);
    }
}
```

La chiamata a `GetStringAsync()` chiama le librerie .NET di livello inferiore, che possono chiamare altri metodi asincroni, finché non raggiunge le chiamate all'interoperabilità P/Invoke in una libreria di rete nativa. Successivamente, la libreria nativa può eseguire una chiamata in una chiamata API di sistema, come ad esempio `write()` in un socket in Linux. Verrà creato un oggetto attività al limite nativo/gestito, usando possibilmente [TaskCompletionSource](xref:System.Threading.Tasks.TaskCompletionSource%601.SetResult(%600)). L'oggetto attività verrà passato attraverso i livelli, attraverso operazioni o restituzione diretta, e alla fine verrà restituito al chiamante iniziale. 

Nel secondo esempio qui sopra, un oggetto `Task<T>` viene restituito da `GetStringAsync`. L'uso della parola chiave `await` fa sì che il metodo restituisca un oggetto attività nuovo. Il controllo ritorna al chiamante da questa posizione nel metodo `GetFirstCharactersCountAsync`. I metodi e le proprietà dell'oggetto [Task&lt;T&gt;](xref:System.Threading.Tasks.Task%601) consentono ai chiamanti di controllare l'avanzamento dell'attività che verrà completata quando il codice rimanente in GetFirstCharactersCountAsync sarà stato eseguito.

Dopo la chiamata all'API di sistema, la richiesta si trova nello spazio del kernel, in direzione del sottosistema di rete del sistema operativo, ad esempio `/net` in Linux Kernel.  A questo punto il sistema operativo gestisce la richiesta di rete *in modo asincrono*.  I dettagli possono variare a seconda del sistema operativo usato. La chiamata del driver di dispositivo può essere pianificata come un segnale reinviato al runtime oppure può essere eseguita una chiamata del driver di dispositivo e *successivamente* il segnale viene reinviato. Alla fine comunque l'informazione che la richiesta di rete è in corso arriverà al runtime.  A questo punto, il lavoro per il driver di dispositivo sarà pianificato, in corso o già completato (la richiesta è già "in rete"), ma poiché tutto ciò accade in modo asincrono, il driver di dispositivo può gestire immediatamente un'altra operazione.

Ad esempio, in Windows un thread del sistema operativo esegue una chiamata al driver di dispositivo di rete e richiede di eseguire l'operazione di rete tramite un pacchetto di richiesta di interrupt che rappresenta l'operazione.  Il driver di dispositivo riceve il pacchetto, esegue la chiamata alla rete, contrassegna il pacchetto come "in sospeso" e lo restituisce al sistema operativo.  Poiché a questo punto il thread del sistema operativo è a conoscenza del fatto che il pacchetto sia "in sospeso", non ha altro lavoro da eseguire per il processo e lo "restituisce" in modo che possa essere usato per eseguire altre operazioni.

Quando la richiesta viene soddisfatta e i dati vengono restituiti tramite il driver di dispositivo, viene inviata una notifica alla CPU del ricevimento dei nuovi dati tramite un interrupt.  La modalità con cui viene gestito l'interrpt varia a seconda del sistema operativo, ma alla fine i dati vengono passati tramite il sistema operativo finché non raggiungono una chiamata di interoperabilità di sistema. Ad esempio, in Linux un gestore di interrupt pianificherà la metà inferiore dell'IRQ perché passi i dati nel sistema operativo in modo asincrono.  Si noti che *anche* questo avviene in modo asincrono.  Il risultato viene inserito in coda fino a quando il thread disponibile successivo può eseguire il metodo asincrono e "dispiegare" il risultato dell'attività completata.

In tutto questo processo il punto chiave è che **nessun thread è dedicato all'esecuzione dell'attività**.  Sebbene il lavoro venga eseguito in un determinato contesto, ad esempio il sistema operativo deve passare i dati a un driver di dispositivo e rispondere a un interrupt, nessun thread è dedicato all'*attesa* del ritorno dei dati della richiesta.  Ciò consente al sistema di gestire un volume di lavoro maggiore, anziché attendere il completamento delle chiamate I/O.

Tutto ciò può sembrare una mole di lavoro davvero imponente ma, se misurato in termini di tempo, è solo una frazione minima di quanto occorre per il lavoro I/O effettivo. Anche se tutt'altro che precisa, la seguente potrebbe essere la sequenza temporale per tale chiamata:

0-1————————————————————————————————————————————————–2-3

*   Il tempo impiegato dai punti `0` a `1` è tutto quanto accade fino a quando un metodo asincrono cede il controllo al chiamante.
*   Il tempo impiegato dai punti `1` a `2` è il tempo dedicato alle chiamate I/O senza alcun costo della CPU.
*   Infine, il tempo impiegato dai punti `2` a `3` è il passaggio del controllo, e potenzialmente di un valore, nuovamente al metodo asincrono, che a quel punto è ancora in esecuzione.

### <a name="what-does-this-mean-for-a-server-scenario"></a>Che cosa significa questo in uno scenario server?

Questo modello funziona bene con un carico di lavoro di uno scenario di server tipico.  Poiché non vi sono thread dedicati per il blocco delle attività non completate, il pool di thread del server può gestire un numero di richieste Web molto maggiore.

Prendiamo ad esempio due server: uno esegue codice asincrono, l'altro no.  Ai fini di questo esempio, ogni server ha solo 5 thread disponibili per le richieste di servizio.  Si noti che questi numeri sono molto piccoli e servono solo a scopo dimostrativo.

Si supponga che entrambi i server ricevano 6 richieste simultanee. Ogni richiesta esegue un'operazione I/O.  Il server *senza* codice asincrono deve inserire in coda tutte le sei richieste finché uno dei 5 thread non ha completato il lavoro associato a I/O e scritto la risposta. Nel momento in cui entra la ventesima richiesta il server potrebbe iniziare a rallentare, visto che la coda sta iniziando a diventare troppo lunga.

Il server *con* il codice asincrono in esecuzione inserisce in coda tutte le sei richieste ma, dal momento che usa `async` e `await`, tutti i thread vengono liberati all'inizio del lavoro associato a I/O, non al suo completamento.  Quando entra la ventesima richiesta, la coda delle richieste in entrata è molto più piccola, sempre che vi sia una coda in entrata, e il server non risulta rallentato.

Anche se questo è un esempio artificioso, uno scenario reale funzionerebbe in modo molto simile.  Infatti, è assolutamente plausibile che un server sia in grado di gestire un numero molto maggiore di richieste usando `async` e `await` piuttosto che dedicando un thread per ogni richiesta che riceve.

### <a name="what-does-this-mean-for-client-scenario"></a>Che cosa significa questo in uno scenario client?

Il vantaggio principale dato dall'uso di `async` e `await` per un'app client è un aumento della velocità di risposta.  Sebbene sia possibile creare un'app reattiva generando thread manualmente, l'azione di generazione di un thread è un'operazione dispendiosa rispetto al solo suo di `async` e `await`.  Ridurre il più possibile l'impatto sul thread dell'interfaccia utente in materia di I/O è fondamentale, soprattutto per app come un videogame mobile.

E cosa ancora più importante, dal momento che il lavoro associato a I/O virtualmente non passa alcun tempo nella CPU, dedicare un thread della CPU intero all'esecuzione di attività poco utili costituirebbe un uso scarsamente efficiente delle risorse.

Inviare lavoro al thread dell'interfaccia utente, ad esempio l'aggiornamento dell'interfaccia, è anche molto semplice con i metodi `async` e non richiede operazioni aggiuntive, come ad esempio la chiamata a un delegato thread-safe.

## <a name="deeper-dive-into-task-and-taskt-for-a-cpu-bound-operation"></a>Approfondimento delle attività Task e Task<T> per un'operazione associata alla CPU

Il codice `async` associato alla CPU è un po' diverso rispetto al codice `async` associato a I/O.  Dal momento che il lavoro viene eseguito sulla CPU, non c'è modo di evitare di dedicare un thread al calcolo.  L'uso di `async` e `await` offre un metodo chiaro per interagire con un thread in background e mantenere reattivo il chiamante del metodo asincrono.  Si noti che ciò non offre alcuna protezione per i dati condivisi.  Se si usano dati condivisi, sarà necessario applicare una strategia di sincronizzazione appropriata.

Di seguito viene presentata una panoramica della chiamata asincrona associata alla CPU:

```csharp
public async Task<int> CalculateResult(InputData data)
{
    // This queues up the work on the threadpool.
    var expensiveResultTask = Task.Run(() => DoExpensiveCalculation(data));
    
    // Note that at this point, you can do some other work concurrently,
    // as CalculateResult() is still executing!
    
    // Execution of CalculateResult is yielded here!
    var result = await expensiveResultTask;
    
    return result;
}
```

`CalculateResult()` viene eseguito sul thread in cui è stato chiamato.  Quando chiama `Task.Run`, inserisce in coda l'operazione dispendiosa associata alla CPU, `DoExpensiveCalculation()`, nel pool di thread e riceve un handle `Task<int>`.  `DoExpensiveCalculation()` viene infine eseguito contemporaneamente nel thread disponibile successivo, probabilmente su un altro core della CPU.  È possibile eseguire attività simultanee mentre `DoExpensiveCalculation()` è occupato in un altro thread, poiché il thread che ha chiamato `CalculateResult()` è ancora in esecuzione.

Quando viene rilevato `await`, l'esecuzione di `CalculateResult()` viene ceduta al chiamante, consentendo lo svolgimento di altro lavoro con il thread corrente mentre `DoExpensiveCalculation()` sta producendo un risultato.  Al termine dell'operazione, il risultato viene inserito in coda per l'esecuzione sul thread principale.  Alla fine, il thread principale tornerà all'esecuzione di `CalculateResult()` e a quel punto sarà disponibile il risultato di `DoExpensiveCalculation()`.

### <a name="why-does-async-help-here"></a>In che modo il codice asincrono risulta utile in questo scenario?

`async` e `await` sono la procedura consigliata per la gestione di attività associate alla CPU quando è necessaria velocità di risposta. Vi sono diversi modelli per l'uso di codice asincrono con attività associate alla CPU. È importante tenere presente che esiste un costo minimo per l'uso del codice asincrono e che tale uso è sconsigliato per cicli ridotti.  Spetta all'utente determinare come scrivere il codice in base a questa nuova funzionalità.
