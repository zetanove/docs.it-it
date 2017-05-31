---
title: Programmazione asincrona
description: Programmazione asincrona
keywords: .NET, .NET Core
author: cartermp
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: b878c34c-a78f-419e-a594-a2b44fa521a4
ms.translationtype: Human Translation
ms.sourcegitcommit: be7974018ce3195dc7344192d647fe64fb2ebcc4
ms.openlocfilehash: 2983dccc63c38884a24f4183d41b406797d5d10f
ms.contentlocale: it-it
ms.lasthandoff: 05/14/2017

---

# <a name="asynchronous-programming"></a>Programmazione asincrona

Se si hanno esigenze associate a I/O, ad esempio richiesta di dati da una rete o accesso a un database, si può usare la programmazione asincrona.  Si potrebbe anche usare codice associato alla CPU, ad esempio per eseguire un calcolo di spese, che rappresenta uno scenario importante per scrivere codice asincrono.

C# ha un modello di programmazione asincrona a livello di linguaggio che consente di scrivere facilmente codice asincrono senza dover manipolare callback o conformarsi a una libreria che supporti l'asincronia. Questo modalità segue ciò che è noto come [Task-based Asynchronous Pattern (TAP)](https://msdn.microsoft.com/library/hh873175.aspx) (Modello asincrono basato sull'attività).

## <a name="basic-overview-of-the-asynchronous-model"></a>Panoramica di base del modello asincrono

Il nucleo della programmazione asincrona consiste di oggetti `Task` e `Task<T>`, che modellano le operazioni asincrone.  Sono supportati dalle parole chiavi `async` e `await`.  Il modello è piuttosto semplice nella maggior parte dei casi: 

Per il codice associato a I/O, si usa `await` per l'operazione che restituisce un oggetto `Task` o `Task<T>` all'interno di un metodo `async`.

Per il codice associato alla CPU, si usa `await` per l'operazione che viene avviata in un thread in background con il metodo `Task.Run`.

La parola chiave `await` cede il controllo al chiamante del metodo che ha eseguito `await`.  Ciò consente a un'interfaccia utente di essere reattiva e a un sevizio di essere flessibile.

Sono disponibili altri modi per trattare il codice asincrono rispetto a `async` e `await` illustrati nell'articolo su TAP visto precedentemente, per cui questo documento illustrerà da questo momento in poi le attività sui costrutti a livello di linguaggio.

### <a name="io-bound-example-downloading-data-from-a-web-service"></a>Esempio associato a I/O: download di dati da un servizio Web

Potrebbe essere necessario scaricare dati da un servizio Web quando viene premuto un pulsante, ma non si vuole bloccare il thread dell'interfaccia utente. Questo risultato si può ottenere in questo modo:

```csharp
private readonly HttpClient _httpClient = new HttpClient();

downloadButton.Clicked += async (o, e) =>
{
    // This line will yield control to the UI as the request
    // from the web service is happening.
    //
    // The UI thread is now free to perform other work.
    var stringData = await _httpClient.GetStringAsync(URL);
    DoSomethingWithData(stringData);
};
```

E questo è sufficiente. Il codice esprime lo scopo (scaricando alcuni dati in modo asincrono) senza perdere tempo per interagire con gli oggetti Task.

### <a name="cpu-bound-example-performing-a-calculation-for-a-game"></a>Esempio associato alla CPU: esecuzione di un calcolo per un gioco

Si supponga di scrivere un gioco per dispositivi mobili in cui l'uso di un pulsante può causare danni a molti nemici visualizzati sullo schermo.  L'esecuzione del calcolo del danno può essere molto onerosa e in questo modo il thread dell'interfaccia utente dà l'impressione che il gioco si arresti durante l'esecuzione del calcolo.

Il modo migliore per gestire questa situazione è avviare un thread in background che esegua l'operazione tramite `Task.Run`, e usa `await` per il risultato.  Ciò consentirà all'interfaccia utente di essere disponibile durante l'esecuzione dell'attività.

```csharp
private DamageResult CalculateDamageDone()
{
    // Code omitted:
    //
    // Does an expensive calculation and returns
    // the result of that calculation.
}


calculateButton.Clicked += async (o, e) =>
{
    // This line will yield control to the UI CalculateDamageDone()
    // performs its work.  The UI thread is free to perform other work.
    var damageResult = await Task.Run(() => CalculateDamageDone());
    DisplayDamage(damageResult);
};
```

L'operazione è ora completata.  Questo codice esprime con precisione lo scopo dell'evento clic del pulsante, non è necessario gestire manualmente un thread in background e non blocca le funzionalità.

### <a name="what-happens-under-the-covers"></a>Operazioni eseguite in background

Le operazioni asincrone coinvolgono molti elementi.  Se si vuole sapere cosa accade in background con `Task` e `Task<T>`, vedere l'articolo [La programmazione asincrona in dettaglio](../standard/async-in-depth.md) per altre informazioni.

Sul lato degli elementi di C#, il compilatore trasforma il codice in una macchina a stati che tiene traccia di varie operazioni, ad esempio sospendere l'esecuzione quando viene raggiunto `await` e riprendere l'esecuzione quando un'operazione di background è stata completata.

Per gli utenti che amano la teoria, questa è un'implementazione del [Modello futuro di asincronia](https://en.wikipedia.org/wiki/Futures_and_promises).

## <a name="key-pieces-to-understand"></a>Nozioni fondamentali da sapere

*   Il codice asincrono può essere usato per il codice associato a I/O e alla CPU, ma in modo diverso per ogni scenario.
*   Il codice asincrono usa `Task<T>` e `Task`, che sono costrutti usati per modellare le operazioni eseguite in background.
* La parola chiave `async` trasforma un metodo in un metodo asincrono, che consente di usare la parola chiave `await` nel relativo corpo.
*   Quando la parola chiave `await` viene applicata, interrompe il metodo di chiamata e restituisce il controllo al chiamante fino al completamento dell'attività attesa.
*   `await` può essere usato solo all'interno di un metodo asincrono.

## <a name="recognize-cpu-bound-and-io-bound-work"></a>Riconoscere le operazioni associate alla CPU e a I/O

I primi due esempi di questa guida hanno illustrato come usare `async` e `await` per operazioni associate ai I/O e alla CPU.  È molto importante identificare se un processo da eseguire è associato a I/O o alla CPU perché ciò può influire notevolmente sulle prestazioni del codice e potrebbe causare un uso improprio di determinati costrutti.

Rispondere a queste due domande prima di scrivere il codice:

1. Il codice deve "attendere" l'esecuzione di operazioni, ad esempio ricezione di dati da un database?

    Se la risposta è "Sì", l'operazione è **associata a I/O**.

2. Il codice eseguirà un calcolo molto oneroso?

    Se la risposta è "Sì", l'operazione è **associata alla CPU**.
    
Se l'operazione è **associata a I/O**, usare `async` e `await` *senza* `Task.Run`.  *Non si deve* usare la libreria Task Parallel Library.  Il motivo viene illustrato nell'articolo [La programmazione asincrona in dettaglio](../standard/async-in-depth.md).

Se l'operazione è **associata alla CPU** e si è interessati nella velocità di risposta, usare `async` e `await`, ma passare l'operazione a un altro thread *con* `Task.Run`.  Se l'operazione è appropriata per parallelismo e concorrenza, è consigliabile usare anche la libreria Task Parallel Library.

È anche necessario valutare sempre l'esecuzione del codice.  Ad esempio, ci si potrebbe trovare in una situazione in cui l'operazione associata alla CPU non è abbastanza onerosa confrontata al sovraccarico di commutazioni di contesto durante il multithreading.  Ogni scelta presenta un compromesso ed è necessario selezionare il compromesso più adatto alla situazione.

## <a name="more-examples"></a>Altri esempi

Gli esempi seguenti illustrano i diversi modi in cui è possibile scrivere codice asincrono in C#.  Trattano scenari diversi molto comuni.

### <a name="extracting-data-from-a-network"></a>Estrazione di dati da una rete

Questo frammento di codice scarica il contenuto HTML da www.dotnetfoundation.org e conta il numero di volte in cui che la stringa ".NET" è inclusa nel contenuto HTML.  Usa MVC di ASP.NET per definire un metodo del controller Web che esegue questa attività, restituendo il numero.

> [!NOTE]
> Se si prevede di eseguire l'analisi HTML effettiva, non è consigliabile usare espressioni regolari.  Usare invece una libreria di analisi, se questo è l'obiettivo del codice di produzione.

```csharp
private readonly HttpClient _httpClient = new HttpClient();

[HttpGet]
[Route("DotNetCount")]
public async Task<int> GetDotNetCountAsync()
{
    // Suspends GetDotNetCountAsync() to allow the caller (the web server)
    // to accept another request, rather than blocking on this one.
    var html = await _httpClient.DownloadStringAsync("http://dotnetfoundation.org");

    return Regex.Matches(html, ".NET").Count;
}
```

Di seguito viene illustrato lo stesso scenario scritto per un'app di Windows universale, che esegue la stessa attività quando viene premuto un pulsante:

```csharp
private readonly HttpClient _httpClient = new HttpClient();

private async void SeeTheDotNets_Click(object sender, RoutedEventArgs e)
{
    // Capture the task handle here so we can await the background task later.
    var getDotNetFoundationHtmlTask = _httpClient.GetStringAsync("http://www.dotnetfoundation.org");

    // Any other work on the UI thread can be done here, such as enabling a Progress Bar.
    // This is important to do here, before the "await" call, so that the user
    // sees the progress bar before execution of this method is yielded.
    NetworkProgressBar.IsEnabled = true;
    NetworkProgressBar.Visibility = Visibility.Visible;

    // The await operator suspends SeeTheDotNets_Click, returning control to its caller.
    // This is what allows the app to be responsive and not hang on the UI thread.
    var html = await getDotNetFoundationHtmlTask;
    int count = Regex.Matches(html, ".NET").Count;

    DotNetCountLabel.Text = $"Number of .NETs on dotnetfoundation.org: {count}";

    NetworkProgressBar.IsEnabled = false;
    NetworkProgressBar.Visbility = Visibility.Collapsed;
}
```

### <a name="waiting-for-multiple-tasks-to-complete"></a>Attesa per il completamento di più attività

Ci si potrebbe trovare in una situazione in cui è necessario recuperare più elementi di dati allo stesso tempo.  L'API `Task` include due metodi, `Task.WhenAll` e `Task.WhenAny` che consentono di scrivere codice asincrono che esegue un'attesa senza blocchi su più processi in background.

Questo esempio illustra come è possibile acquisire dati `User` per un set di `userId`.

```csharp

public async Task<User> GetUser(int userId)
{
    // Code omitted:
    //
    // Given a user Id {userId}, retrieves a User object corresponding
    // to the entry in the database with {userId} as its Id.
}

public static Task<IEnumerable<User>> GetUsers(IEnumerable<int> userIds)
{
    var getUserTasks = new List<Task<User>>();
    
    foreach (int userId in userIds)
    {
        getUserTasks.Add(GetUser(id));
    }
    
    return await Task.WhenAll(getUserTasks);
}
```

Questo è un altro modo per scrivere il codice in maniera più concisa tramite LINQ:

```csharp

public async Task<User> GetUser(int userId)
{
    // Code omitted:
    //
    // Given a user Id {userId}, retrieves a User object corresponding
    // to the entry in the database with {userId} as its Id.
}

public static async Task<User[]> GetUsers(IEnumerable<int> userIds)
{
    var getUserTasks = userIds.Select(id => GetUser(id));
    return await Task.WhenAll(getUserTasks);
}
```
Sebbene produca una quantità minore di codice, è necessario prestare molta attenzione quando si combina LINQ con codice asincrono.  Poiché LINQ usa un'esecuzione posticipata (lazy), le chiamate asincrone non verranno eseguite immediatamente come avviene in un ciclo `foreach()` a meno che non si forzi la sequenza generata per l'iterazione con una chiamata a `.ToList()` o `.ToArray()`.

## <a name="important-info-and-advice"></a>Consigli e informazioni importanti

Sebbene la programmazione asincrona è relativamente semplice, ci sono alcuni dettagli da tenere presente per evitare comportamenti non previsti.

*  `async`I metodi  **devono avere una parola chiave**  `await`  **nel corpo, altrimenti non verranno eseguiti.**

Questo è importante da tenere presente.  Se `await` non viene usato nel corpo di un metodo `async`, il compilatore C# genererà un avviso, ma il codice verrà compilato ed eseguito come se fosse un metodo normale.  Si noti che anche questo sarebbe estremamente inefficiente, perché la macchina a stati generata dal compilatore C# per il metodo asincrono non produrrebbe niente.

*   **È consigliabile aggiungere "async" come suffisso di ogni nome di metodo scritto.**

Questa è la convenzione usata in .NET per differenziare più facilmente i metodi sincroni dai metodi asincroni. Si noti che alcuni metodi non chiamati in modo esplicito dal codice, ad esempio un gestore di eventi o un metodo di controller del Web, non vengono necessariamente applicati. Poiché questi metodi non vengono chiamati in modo esplicito dal codice, non è importante denominarli in modo esplicito.

*   `async void`  **deve essere usato solo per i gestori eventi.**

`async void` è l'unico modo per consentire ai gestori eventi asincroni di funzionare correttamente, poiché gli eventi non hanno tipi restituiti (quindi non possono usare `Task` e `Task<T>`). Qualsiasi altro uso di `async void` non segue il modello TAP e può essere difficile da usare, ad esempio:

  *   Le eccezioni generate in un metodo `async void` non possono essere rilevate al di fuori di tale metodo.
  *   I metodi `async void` sono molto difficili da testare.
  *   I metodi `async void` possono causare effetti collaterali seri se il chiamante non li prevede asincroni.

*   **Prestare attenzione quando si usano le espressioni lambda asincrone in espressioni LINQ**

Le espressioni lambda in LINQ usano esecuzioni posticipate, ovvero il codice potrebbe essere eseguito in qualsiasi momento quando meno previsto. L'introduzione delle attività di blocco in questa operazione produce facilmente un deadlock se il codice non è scritto in maniera corretta. L'annidamento di codice asincrono come questo può anche rendere più difficile la valutazione dell'esecuzione del codice. Async e LINQ sono molto efficaci, ma devono essere usati insieme con precauzione e in modo chiaro.

*   **Scrivere codice che attende attività in modo non bloccante**

Il blocco del thread corrente come mezzo per attendere il completamento di un'attività può risultare in deadlock e in thread di contesto bloccati e può richiedere una gestione degli errori più complessa. La tabella seguente offre indicazioni su come gestire l'attesa di attività in un modo non bloccante:

| Usare questo | Invece di questo | Quando si vuole eseguire questa operazione |
| --- | --- | --- |
| `await` | `Task.Wait` o `Task.Result` | Recuperare il risultato di un'attività in background |
| `await Task.WhenAny` | `Task.WaitAny` | Attendere che un'attività sia completa |
| `await Task.WhenAll` | `Task.WaitAll` | Attendere che tutte le attività siano complete |
| `await Task.Delay` | `Thread.Sleep` | Attendere un periodo di tempo |

*   **Scrivere codice con meno dettagli sullo stato**

È consigliabile non dipendere dallo stato di oggetti globali o dall'esecuzione di alcuni metodi. È preferibile dipendere dai valori restituiti dei metodi. Perché?

  *   Sarà più facile valutare il codice.
  *   Sarà più facile testare il codice.
  *   La combinazione di codice sincrono e asincrono è molto più semplice.
  *   È possibile evitare completamente le race condition.
  *   La dipendenza dai valori restituiti semplifica il coordinamento di codice asincrono.
  *   (Extra) funziona particolarmente bene con l'inserimento di dipendenze.

È consigliabile raggiungere una completa o quasi completa [trasparenza referenziale](https://en.wikipedia.org/wiki/Referential_transparency_%28computer_science%29) nel codice. Ciò risulterà in una base di codice completamente prevedibile, testabile e gestibile.

## <a name="other-resources"></a>Altre risorse

* L'articolo [La programmazione asincrona in dettaglio](../standard/async-in-depth.md) offre altre informazioni sul funzionamento di Task.
* L'articolo [Six Essential Tips for Async](https://channel9.msdn.com/Series/Three-Essential-Tips-for-Async) (Sei suggerimenti essenziali per la modalità asincrona) di Lucian Wischik è una risorsa eccellente per la programmazione asincrona.

