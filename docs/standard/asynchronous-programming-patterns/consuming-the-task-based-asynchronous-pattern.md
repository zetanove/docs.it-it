---
title: "Consuming the Task-based Asynchronous Pattern | Microsoft Docs"
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
  - ".NET Framework, and TAP"
  - "asynchronous design patterns, .NET Framework"
  - "TAP, .NET Framework support for"
  - "Task-based Asynchronous Pattern, .NET Framework support for"
  - ".NET Framework, asynchronous design patterns"
ms.assetid: 033cf871-ae24-433d-8939-7a3793e547bf
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Consuming the Task-based Asynchronous Pattern
Quando si utilizza il modello asincrono basato su attività \(TAP\) per lavorare con operazioni asincrone, è possibile utilizzare le callback per ottenere un'attesa non bloccante.  Considerando le attività, questo scopo può essere raggiunto tramite metodi come <xref:System.Threading.Tasks.Task.ContinueWith%2A?displayProperty=fullName>.  Il supporto asincrono basato sul linguaggio nasconde le callback consentendo alle operazioni asincrone di essere in attesa all'interno di un normale flusso di controllo, e il codice generato dal compilatore fornisce lo stesso livello di supporto delle API.  
  
## Sospendere l'esecuzione tramite l'attesa  
 A partire da [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], è possibile utilizzare la parola chiave [await](../Topic/await%20\(C%23%20Reference\).md) in C\# e [Await Operator](../Topic/Await%20Operator%20\(Visual%20Basic\).md) in Visual Basic per attendere in modo asincrono gli oggetti <xref:System.Threading.Tasks.Task> e <xref:System.Threading.Tasks.Task%601>.  Quando si è in attesa di <xref:System.Threading.Tasks.Task>, l'espressione `await` è di tipo `void`.  Quando si è in attesa di <xref:System.Threading.Tasks.Task%601>, l'espressione `await` è di tipo `TResult`.  Un'espressione `await` deve essere presente nel corpo di un metodo asincrono.  Per ulteriori informazioni sul supporto dei linguaggi C\# e Visual Basic in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], vedere le specifiche dei linguaggi C\# e Visual Basic.  
  
 La funzionalità di await installa in modo trasparente una callback sul processo tramite una continuazione.  Questa callback permette la ripresa del metodo asincrono al momento della sospensione.  Quando il metodo asincrono viene ripreso, se l'operazione di attesa si è completata correttamente ed era una <xref:System.Threading.Tasks.Task%601>, viene restituito il corrispondente `TResult`.  Se il <xref:System.Threading.Tasks.Task> o il <xref:System.Threading.Tasks.Task%601> che era in attesa termina con stato <xref:System.Threading.Tasks.TaskStatus>, viene generata un'eccezione <xref:System.OperationCanceledException>.  Se il <xref:System.Threading.Tasks.Task> o il <xref:System.Threading.Tasks.Task%601> che era in attesa termina con stato <xref:System.Threading.Tasks.TaskStatus>, viene generate l'eccezione che ha causato l'errore.  Un `Task` può fallire a causa di più eccezioni, ma solo una di queste eccezioni viene propagata.  Tuttavia, la proprietà <xref:System.Threading.Tasks.Task.Exception%2A?displayProperty=fullName> restituisce un'eccezione <xref:System.AggregateException> che contiene tutti gli errori.  
  
 Se un contesto di sincronizzazione \(oggetto <xref:System.Threading.SynchronizationContext>\) è stato associato al thread che stava eseguendo il metodo asincrono al momento della sospensione \(ad esempio, se la proprietà <xref:System.Threading.SynchronizationContext.Current%2A?displayProperty=fullName> non è `null`\), il metodo asincrono riprende nello stesso contesto di sincronizzazione tramite il metodo <xref:System.Threading.SynchronizationContext.Post%2A> del contesto.  In caso contrario, si basa sull'utilità di pianificazione \(oggetto <xref:System.Threading.Tasks.TaskScheduler>\) corrente al momento della sospensione.  In genere questa è l'utilità di pianificazione predefinita \(<xref:System.Threading.Tasks.TaskScheduler.Default%2A?displayProperty=fullName>\), ed utilizza il pool di thread come destinazione.  Questa utilità di pianificazione determina se l'operazione asincrona in attesa deve riprendere al momento del completamento o se la ripresa deve essere pianificata.  L'utilità di pianificazione predefinita in genere consente alla continuazione di essere eseguita nel thread in cui l'operazione attesa è stata completata.  
  
 Quando un metodo asincrono viene chiamato, esegue in modo sincrono il corpo della funzione fino alla prima espressione di await su un'istanza awaitable che non è ancora terminata, a quel punto la chiamata restituisce il controllo al chiamante.  Se il metodo asincrono non restituisce `void`, viene restituito un oggetto <xref:System.Threading.Tasks.Task%601> o <xref:System.Threading.Tasks.Task> che rappresenta il calcolo corrente.  In un metodo asincrono non void, se viene rilevata un'istruzione return o viene raggiunta la fine del corpo del metodo, il processo termina nello stato finale <xref:System.Threading.Tasks.TaskStatus> .  Se un'eccezione non gestita fa in modo che il controllo lasci il corpo del metodo asincrono, il processo termina nello stato <xref:System.Threading.Tasks.TaskStatus>.  Se tale eccezione è una <xref:System.OperationCanceledException>, l'attività termina invece nello stato <xref:System.Threading.Tasks.TaskStatus>.  In questo modo, il risultato o l'eccezione vengono pubblicati.  
  
 Vi sono diverse varianti importanti di questo comportamento.  Per motivi di prestazioni, se un processo è già stato completato prima che quel processo sia atteso, il controllo non viene ceduto e la funzione prosegue nell'esecuzione.  Inoltre, non è sempre desiderabile tornare al contesto originale e questo comportamento può essere modificato; ciò viene descritto in dettaglio nella sezione successiva.  
  
### Configurare la sospensione e la ripresa con Yield e ConfigureAwait  
 Diversi metodi offrono maggiore controllo sull'esecuzione di un metodo asincrono.  Ad esempio, è possibile utilizzare il metodo <xref:System.Threading.Tasks.Task.Yield%2A?displayProperty=fullName> per introdurre un punto yield nel metodo asincrono:  
  
```csharp  
public class Task : …  
{  
    public static YieldAwaitable Yield();  
    …  
}  
  
```  
  
 Questa operazione è equivalente ad eseguire un postback asincrono o a ritornare in modo asincrono al contesto corrente tramite scheduling.  
  
```csharp  
Task.Run(async  delegate  
{  
    for(int i=0; i<1000000; i++)  
    {  
        await Task.Yield(); // fork the continuation into a separate work item  
        ...  
    }  
});  
  
```  
  
 È inoltre possibile utilizzare il metodo <xref:System.Threading.Tasks.Task.ConfigureAwait%2A?displayProperty=fullName> per avere un maggiore controllo sulla sospensione e sul ripristino in un metodo asincrono.  Come accennato in precedenza, per impostazione predefinita il contesto corrente viene acquisito nel momento in cui un metodo asincrono viene sospeso, e tale contesto acquisito viene utilizzato per invocare la continuazione del metodo asincrono al momento della ripresa.  In molti casi, questo è il comportamento desiderato.  In altri casi non è necessario preoccuparsi del contesto di continuazione ed è possibile ottenere migliori prestazioni evitando tali postback al contesto originale.  Per abilitare questa funzionalità, utilizzare il metodo <xref:System.Threading.Tasks.Task.ConfigureAwait%2A?displayProperty=fullName> per notificare l'operazione di await di non acquisire e non riprendere il contesto, ma di continuare l'esecuzione una volta che l'operazione asincrona di cui si era in attesa viene completata:  
  
```csharp  
await someTask.ConfigureAwait(continueOnCapturedContext:false);  
  
```  
  
## Annullare un'operazione asincrona  
 A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], i metodi TAP che supportano l'annullamento forniscono almeno un overload che accetta un token di annullamento \(oggetto <xref:System.Threading.CancellationToken>\).  
  
 Un token di annullamento viene creato tramite un generatore di token di annullamento \(oggetto <xref:System.Threading.CancellationTokenSource>\).  La proprietà <xref:System.Threading.CancellationTokenSource.Token%2A> del generatore restituisce il token di annullamento che verrà segnalato quando verrà chiamato il metodo <xref:System.Threading.CancellationTokenSource.Cancel%2A> del generatore.  Ad esempio, se si desidera scaricare una singola pagina Web e si desidera annullare l'operazione, è necessario creare un oggetto <xref:System.Threading.CancellationTokenSource>, passare il token dell'oggetto al metodo TAP e quindi, quando si è pronti per annullare l'operazione, chiamare il metodo <xref:System.Threading.CancellationTokenSource.Cancel%2A> del generatore:  
  
```csharp  
var cts = new CancellationTokenSource();  
string result = await DownloadStringAsync(url, cts.Token);  
… // at some point later, potentially on another thread  
cts.Cancel();  
  
```  
  
 Per annullare più chiamate asincrone, è possibile passare lo stesso token a tutte le chiamate:  
  
```csharp  
var cts = new CancellationTokenSource();  
    IList<string> results = await Task.WhenAll(from url in urls select DownloadStringAsync(url, cts.Token));  
    // at some point later, potentially on another thread  
    …  
    cts.Cancel();  
  
```  
  
 In alternativa, è possibile passare lo stesso token a un sottoinsieme selettivo di operazioni:  
  
```csharp  
var cts = new CancellationTokenSource();  
    byte [] data = await DownloadDataAsync(url, cts.Token);  
    await SaveToDiskAsync(outputPath, data, CancellationToken.None);  
    … // at some point later, potentially on another thread  
    cts.Cancel();  
  
```  
  
 Le richieste di annullamento possono essere avviate da qualsiasi thread.  
  
 È possibile passare il valore <xref:System.Threading.CancellationToken.None%2A?displayProperty=fullName> a ogni metodo che accetta un token di annullamento per indicare che non verrà mai richiesto l'annullamento.  In questo modo la proprietà <xref:System.Threading.CancellationToken.CanBeCanceled%2A?displayProperty=fullName> restituirà `false` e di conseguenza il metodo chiamato può ottimizzarsi.  A scopo di test, è possibile passare un token di annullamento già annullato di cui si è creata un'istanza utilizzando il costruttore che accetta un valore booleano per indicare se il token verrà avviato in uno stato already\-canceled \(già cancellato\) o not\-cancelable \(non cancellabile\).  
  
 Questo approccio all'annullamento presenta diversi vantaggi:  
  
-   È possibile passare lo stesso token di annullamento a un numero qualsiasi operazioni asincrone e sincrone.  
  
-   La stessa richiesta di annullamento può essere estesa a un numero qualsiasi di listener.  
  
-   Lo sviluppatore dell'API asincrono controlla completamente se l'annullamento può essere richiesto e quando può avere effetto.  
  
-   Il codice che utilizza l'API può determinare in modo selettivo a quali chiamate asincrone verranno propagate le richieste di annullamento.  
  
## Monitoraggio dello stato  
 Alcuni metodi asincroni espongono lo stato di avanzamento tramite un'interfaccia dello stato di avanzamento passata all'interno del metodo asincrono.  Ad esempio, si consideri una funzione che scarica in modo asincrono una stringa di testo e, durante il processo, genera gli aggiornamenti dello stato di avanzamento che include la percentuale di download completata fino a quel momento.  Tale metodo può essere utilizzato in un'applicazione Windows Presentation Foundation \(WPF\) come segue:  
  
```csharp  
private async  void btnDownload_Click(object sender, RoutedEventArgs e)    
{  
    btnDownload.IsEnabled = false;  
    try  
    {  
        txtResult.Text = await DownloadStringAsync(txtUrl.Text,   
            new Progress<int>(p => pbDownloadProgress.Value = p));  
    }  
    finally { btnDownload.IsEnabled = true; }  
}  
  
```  
  
<a name="combinators"></a>   
## Utilizzare i Combinators incorporati basati su attività.  
 Lo spazio dei nomi di <xref:System.Threading.Tasks> include diversi metodi per la composizione e l'utilizzo delle attività.  
  
### Task.Run  
 La classe <xref:System.Threading.Tasks.Task> include diversi metodi <xref:System.Threading.Tasks.Task.Run%2A> che consentono di ripartire facilmente il lavoro come un <xref:System.Threading.Tasks.Task> o un <xref:System.Threading.Tasks.Task%601> utilizzando il pool di thread, ad esempio:  
  
```csharp  
public async  void button1_Click(object sender, EventArgs e)  
{  
    textBox1.Text = await Task.Run(() =>  
    {  
        // … do compute-bound work here  
        return answer;  
    });  
}  
  
```  
  
 Alcuni di questi metodi <xref:System.Threading.Tasks.Task.Run%2A>, come l'overload <xref:System.Threading.Tasks.Task.Run%28System.Func%7BSystem.Threading.Tasks.Task%7D%29?displayProperty=fullName>, sono la forma abbreviata del metodo <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=fullName>.  Altri overload, come <xref:System.Threading.Tasks.Task.Run%28System.Func%7BSystem.Threading.Tasks.Task%7D%29?displayProperty=fullName>, consentono di utilizzare await all'interno del lavoro ripartito, ad esempio:  
  
```csharp  
public async  void button1_Click(object sender, EventArgs e)  
{  
    pictureBox1.Image = await Task.Run(async() =>  
    {  
        using(Bitmap bmp1 = await DownloadFirstImageAsync())  
        using(Bitmap bmp2 = await DownloadSecondImageAsync())  
        return Mashup(bmp1, bmp2);  
    });  
}  
```  
  
 Questi overload logicamente sono equivalenti a utilizzare il metodo <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=fullName> insieme al metodo di estensione <xref:System.Threading.Tasks.TaskExtensions.Unwrap%2A> nella libreria Task Parallel.  
  
### Task.FromResult  
 Utilizzare il metodo <xref:System.Threading.Tasks.Task.FromResult%2A> negli scenari in cui i dati possono essere già disponibili e devono essere solo restituiti da un metodo che restituisce task del tipo <xref:System.Threading.Tasks.Task%601>:  
  
```csharp  
public Task<int> GetValueAsync(string key)  
{  
    int cachedValue;  
    return TryGetCachedValue(out cachedValue) ?  
        Task.FromResult(cachedValue) :  
        GetValueAsyncInternal();  
}  
  
private async  Task<int> GetValueAsyncInternal(string key)  
{  
    …  
}  
  
```  
  
### Task.WhenAll  
 Utilizzare il metodo <xref:System.Threading.Tasks.Task.WhenAll%2A> per attendere in modo asincrono più operazioni asincrone più rappresentate come attività.  Il metodo dispone di più overload che supportano un set di attività non generiche o un set non uniforme di attività generiche \(ad esempio attendere in modo asincrono più operazioni che restituiscono void, o attendere in modo asincrono più metodi che restituiscono dei valori, dove ogni valore può essere di tipo diverso\) e supportano un set uniforme di attività generiche \(ad esempio attendere in modo asincrono più metodi che restituiscono `TResult`\).  
  
 Si supponga di voler inviare messaggi di posta elettronica a diversi clienti.  È possibile sovrapporre l'invio dei messaggi in modo da non dover attendere che un messaggio termini prima di inviare il seguente.  È inoltre possibile scoprire quando le operazioni di invio sono state completate e se si sono verificati degli errori:  
  
```csharp  
IEnumerable<Task> asyncOps = from addr in addrs select SendMailAsync(addr);  
await Task.WhenAll(asyncOps);  
  
```  
  
 Questo codice non gestisce in modo esplicito le eccezioni che possono verificarsi, ma consente la propagazione delle eccezioni dall' `await` sull'attività risultante da <xref:System.Threading.Tasks.Task.WhenAll%2A>.  Per gestire le eccezioni, utilizzare il codice seguente:  
  
```csharp  
IEnumerable<Task> asyncOps = from addr in addrs select SendMailAsync(addr);  
try  
{  
    await Task.WhenAll(asyncOps);  
}  
catch(Exception exc)  
{  
    ...  
}  
  
```  
  
 In questo caso, se qualsiasi operazione asincrona ha esito negativo, tutte le eccezioni vengono consolidate in un'eccezione <xref:System.AggregateException>, archiviata in <xref:System.Threading.Tasks.Task> che viene restituita dal metodo <xref:System.Threading.Tasks.Task.WhenAll%2A>.  Tuttavia, solo una di tali eccezioni viene propagata dalla parola chiave `await`.  Se si desidera esaminare tutte le eccezioni, è possibile riscrivere il codice precedente come segue:  
  
```csharp  
Task [] asyncOps = (from addr in addrs select SendMailAsync(addr)).ToArray();  
try  
{  
    await Task.WhenAll(asyncOps);  
}  
catch(Exception exc)  
{  
    foreach(Task faulted in asyncOps.Where(t => t.IsFaulted))  
    {  
        … // work with faulted and faulted.Exception  
    }  
}  
  
```  
  
 Si consideri ad esempio di scaricare più file dal web in modo asincrono.  In questo caso tutte le operazioni asincrone hanno tipi di risultato omogenei ed è facile accedere ai risultati:  
  
```csharp  
string [] pages = await Task.WhenAll(  
    from url in urls select DownloadStringAsync(url));  
```  
  
 È possibile utilizzare le stesse tecniche di gestione delle eccezioni che sono state illustrate nel precedente scenario di restituzione di void:  
  
```csharp  
Task [] asyncOps =   
    (from url in urls select DownloadStringAsync(url)).ToArray();  
try  
{  
    string [] pages = await Task.WhenAll(asyncOps);  
    ...  
}  
catch(Exception exc)  
{  
    foreach(Task<string> faulted in asyncOps.Where(t => t.IsFaulted))  
    {  
        … // work with faulted and faulted.Exception  
    }  
}  
  
```  
  
### Task.WhenAny  
 È possibile utilizzare il metodo <xref:System.Threading.Tasks.Task.WhenAny%2A> per attendere in modo asincrono più operazioni asincrone rappresentate come attività da completare.  Questo metodo ha quattro casi di utilizzo principali:  
  
-   Ridondanza: Esegue ripetutamente un'operazione e seleziona quella che termina prima \(ad esempio contatta più servizi web di quotazioni di borsa che genereranno un solo risultato e seleziona quello che completa più velocemente\).  
  
-   Interfoliazione: Avvia più operazioni e attende il completamento di tutte, ma le elabora non appena terminano.  
  
-   Limitazione: Fornisce operazioni aggiuntive per iniziare mentre gli altri terminano.  Questa è un'estensione dello scenario di interfoliazione.  
  
-   Abbandono iniziale: Ad esempio, un'operazione rappresentata dall'attività T1 può essere raggruppata in un'attività <xref:System.Threading.Tasks.Task.WhenAny%2A> con un'altra attività T2 ed è possibile attendere l'attività <xref:System.Threading.Tasks.Task.WhenAny%2A>.  L'attività T2 potrebbe rappresentare un timeout, un annullamento, o un altro segnale che fa sì che l'attività <xref:System.Threading.Tasks.Task.WhenAny%2A> termini prima che termini T1.  
  
#### Ridondanza  
 Si consideri il caso in cui si desidera decidere se comprare delle azioni o meno.  Esistono numerosi servizi web attendibili che consigliano su azioni, ma dipendentemente dal traffico giornaliero, ogni servizio può risultare lento in determinati momenti.  È possibile utilizzare il metodo <xref:System.Threading.Tasks.Task.WhenAny%2A> per ricevere una notifica quando una qualsiasi operazione termina:  
  
```csharp  
var recommendations = new List<Task<bool>>()   
{   
    GetBuyRecommendation1Async(symbol),   
    GetBuyRecommendation2Async(symbol),  
    GetBuyRecommendation3Async(symbol)  
};  
Task<bool> recommendation = await Task.WhenAny(recommendations);  
if (await recommendation) BuyStock(symbol);  
  
```  
  
 A differenza di <xref:System.Threading.Tasks.Task.WhenAll%2A>, che restituisce i risultati senza wrapping di tutte le attività che sono stati completate correttamente, <xref:System.Threading.Tasks.Task.WhenAny%2A> restituisce l'attività completata.  Se un'attività ha esito negativo, è importante sottolineare che ha avuto esito negativo e se l'attività ha esito positivo, è importante sapere a quale attività è associato il valore restituito.  Pertanto, è necessario accedere al risultato dell'attività restituita, o attenderlo ulteriormente, come mostra l'esempio riportato di seguito.  
  
 Come con <xref:System.Threading.Tasks.Task.WhenAll%2A>, è necessario essere in grado di adattare le eccezioni.  Poiché l'attività terminata viene restituita, è possibile attendere l'attività restituita per propagare gli errori ed eseguire `try/catch` in modo appropriato, ad esempio:  
  
```csharp  
Task<bool> [] recommendations = …;  
while(recommendations.Count > 0)  
{   
    Task<bool> recommendation = await Task.WhenAny(recommendations);      
    try  
    {  
        if (await recommendation) BuyStock(symbol);  
        break;  
    }  
    catch(WebException exc)  
    {  
        recommendations.Remove(recommendation);  
    }  
}  
  
```  
  
 Inoltre, anche se il primo processo viene completato correttamente, le attività successive possono dare esito negativo.  In questa fase sono disponibili diverse opzioni per la gestione delle eccezioni: è possibile attendere finché tutte le attività avviate non sono terminate, nel qual caso è possibile utilizzare il metodo <xref:System.Threading.Tasks.Task.WhenAll%2A>, oppure è possibile decidere che tutte le eccezioni sono importanti e devono essere registrate.  Per fare ciò, è possibile utilizzare le continuazioni per ricevere una notifica quando le attività terminano in modo asincrono:  
  
```csharp  
foreach(Task recommendation in recommendations)  
{  
    var ignored = recommendation.ContinueWith(  
        t => { if (t.IsFaulted) Log(t.Exception); });  
}  
  
```  
  
 oppure:  
  
```csharp  
foreach(Task recommendation in recommendations)  
{  
    var ignored = recommendation.ContinueWith(  
        t => Log(t.Exception), TaskContinuationOptions.OnlyOnFaulted);  
}  
  
```  
  
 o anche:  
  
```  
private static async  void LogCompletionIfFailed(IEnumerable<Task> tasks)  
{  
    foreach(var task in tasks)  
    {  
        try { await task; }  
        catch(Exception exc) { Log(exc); }  
    }  
}  
…  
LogCompletionIfFailed(recommendations);  
  
```  
  
 Infine, è possibile annullare tutte le operazioni rimanenti:  
  
```csharp  
var cts = new CancellationTokenSource();  
var recommendations = new List<Task<bool>>()   
{   
    GetBuyRecommendation1Async(symbol, cts.Token),   
    GetBuyRecommendation2Async(symbol, cts.Token),  
    GetBuyRecommendation3Async(symbol, cts.Token)  
};  
  
Task<bool> recommendation = await Task.WhenAny(recommendations);  
cts.Cancel();  
if (await recommendation) BuyStock(symbol);  
  
```  
  
#### Interfogliatura  
 Si consideri il caso in cui si scarichino delle immagini dal web e ogni immagine venga elaborata, ad esempio aggiungendo l'immagine a un controllo dell'interfaccia utente.  È necessario eseguire l'elaborazione sequenzialmente sul thread UI, ma si desidera scaricare quante più immagini possibili contemporaneamente.  Inoltre, non si desidera aspettare che le immagini siano tutte scaricate prima di aggiungerle alla UI, ma si desidera aggiungerle man mano che vengono scaricate:  
  
```csharp  
List<Task<Bitmap>> imageTasks =   
    (from imageUrl in urls select GetBitmapAsync(imageUrl)).ToList();  
while(imageTasks.Count > 0)  
{  
    try  
    {  
        Task<Bitmap> imageTask = await Task.WhenAny(imageTasks);  
        imageTasks.Remove(imageTask);  
  
        Bitmap image = await imageTask;  
        panel.AddImage(image);  
    }  
    catch{}  
}  
  
```  
  
 È inoltre possibile applicare l'interfoliazione a uno scenario che include un'elaborazione complessa a livello di calcolo sul <xref:System.Threading.ThreadPool> delle immagini scaricate; ad esempio:  
  
```csharp  
List<Task<Bitmap>> imageTasks =   
    (from imageUrl in urls select GetBitmapAsync(imageUrl)  
         .ContinueWith(t => ConvertImage(t.Result)).ToList();  
while(imageTasks.Count > 0)  
{  
    try  
    {  
        Task<Bitmap> imageTask = await Task.WhenAny(imageTasks);  
        imageTasks.Remove(imageTask);  
  
        Bitmap image = await imageTask;  
        panel.AddImage(image);  
    }  
    catch{}  
}  
  
```  
  
#### Limitazione  
 Si consideri l'esempio dell'interfoliazione, con la differenza che l'utente sta scaricando un numero così elevato di immagini che i download devono essere limitati; ad esempio, si desidera che solo uno specifico numero di download sia realizzato contemporaneamente.  A tale scopo, è possibile avviare un sottoinsieme di operazioni asincrone.  Mentre le operazioni terminano, è possibile avviare operazioni aggiuntive che prendano il loro posto:  
  
```csharp  
const int CONCURRENCY_LEVEL = 15;  
Uri [] urls = …;  
int nextIndex = 0;  
var imageTasks = new List<Task<Bitmap>>();  
while(nextIndex < CONCURRENCY_LEVEL && nextIndex < urls.Length)  
{  
    imageTasks.Add(GetBitmapAsync(urls[nextIndex]));  
    nextIndex++;  
}  
  
while(imageTasks.Count > 0)  
{  
    try  
    {  
        Task<Bitmap> imageTask = await Task.WhenAny(imageTasks);  
        imageTasks.Remove(imageTask);  
  
        Bitmap image = await imageTask;  
        panel.AddImage(image);  
    }  
    catch(Exception exc) { Log(exc); }  
  
    if (nextIndex < urls.Length)  
    {  
        imageTasks.Add(GetBitmapAsync(urls[nextIndex]));  
        nextIndex++;  
    }  
}  
  
```  
  
#### Interruzione prematura  
 Si consideri di essere in attesa in modo asincrono che un'operazione termini e contemporaneamente di rispondere alla richiesta di interruzione da parte di un utente \(ad esempio, l'utente ha fatto clic su un pulsante di annullamento\).  Nel seguente codice viene illustrato questo scenario:  
  
```csharp  
private CancellationTokenSource m_cts;   
  
public void btnCancel_Click(object sender, EventArgs e)  
{  
    if (m_cts != null) m_cts.Cancel();  
}  
  
public async  void btnRun_Click(object sender, EventArgs e)  
{  
    m_cts = new CancellationTokenSource();  
    btnRun.Enabled = false;  
    try  
    {  
        Task<Bitmap> imageDownload = GetBitmapAsync(txtUrl.Text);   
        await UntilCompletionOrCancellation(imageDownload, m_cts.Token);  
        if (imageDownload.IsCompleted)  
        {  
            Bitmap image = await imageDownload;  
            panel.AddImage(image);  
        }  
        else imageDownload.ContinueWith(t => Log(t));  
    }  
    finally { btnRun.Enabled = true; }  
}  
  
private static async  Task UntilCompletionOrCancellation(  
    Task asyncOp, CancellationToken ct)  
{  
    var tcs = new TaskCompletionSource<bool>();  
    using(ct.Register(() => tcs.TrySetResult(true)))  
        await Task.WhenAny(asyncOp, tcs.Task);  
    return asyncOp;  
}  
  
```  
  
 Questa implementazione riabilita l'interfaccia utente non appena si decide di annullare l'operazione, ma non annulla le operazioni asincrone sottostanti.  Un'alternativa consiste nell'annullare le operazioni in sospeso quando si decide di interrompere, ma di non ristabilire l'interfaccia utente finché le operazioni non siano terminate, probabilmente perché a causa della richiesta dell'interruzione, sono terminate prima:  
  
```csharp  
private CancellationTokenSource m_cts;  
  
public async  void btnRun_Click(object sender, EventArgs e)  
{  
    m_cts = new CancellationTokenSource();  
  
    btnRun.Enabled = false;  
    try  
    {  
        Task<Bitmap> imageDownload = GetBitmapAsync(txtUrl.Text, m_cts.Token);   
        await UntilCompletionOrCancellation(imageDownload, m_cts.Token);  
        Bitmap image = await imageDownload;  
        panel.AddImage(image);  
    }  
    catch(OperationCanceledException) {}  
    finally { btnRun.Enabled = true; }  
}  
  
```  
  
 Un altro esempio di interruzione prematura richiede l'uso del metodo <xref:System.Threading.Tasks.Task.WhenAny%2A> insieme al metodo <xref:System.Threading.Tasks.Task.Delay%2A>, come descritto nella sezione successiva.  
  
### Task.Delay  
 È possibile utilizzare il metodo <xref:System.Threading.Tasks.Task.Delay%2A> per introdurre delle pause nell'esecuzione asincrona di un metodo.  Ciò è utile per molti tipi di funzionalità, incluse la compilazione dei i cicli di polling e il posticipo della gestione di input utente per un periodo di tempo predeterminato.  Il metodo <xref:System.Threading.Tasks.Task.Delay%2A> può essere utile anche in combinazione con <xref:System.Threading.Tasks.Task.WhenAny%2A> per implementare dei timeout di attesa.  
  
 Se un'attività che fa parte di una più grande operazione asincrona, ad esempio un servizio web ASP.NET impiega troppo tempo per terminare, potrebbe soffrirne l'operazione globale, specialmente se non termina mai.  Per questo motivo, è importante potersi interrompere quando si è in attesa in un'operazione asincrona.  I metodi sincroni <xref:System.Threading.Tasks.Task.Wait%2A>, <xref:System.Threading.Tasks.Task.%2A> WaitAll?qualifyHint=False&autoUpgrade=True e <xref:System.Threading.Tasks.Task.%2A> WaitAny?qualifyHint=False&autoUpgrade=True accettano valori di timeout, ma i corrispondenti metodi <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A>\/<xref:System.Threading.Tasks.Task.WhenAny%2A> e il precedentemente menzionato <xref:System.Threading.Tasks.Task.WhenAll%2A>\/<xref:System.Threading.Tasks.Task.WhenAny%2A> no.  In alternativa, è possibile combinare <xref:System.Threading.Tasks.Task.Delay%2A> e <xref:System.Threading.Tasks.Task.WhenAny%2A> per implementare un timeout.  
  
 Ad esempio, in un'applicazione con interfaccia utente si desidera scaricare un'immagine e disabilitare l'interfaccia utente mentre si sta scaricando l'immagine.  Tuttavia, se il download è troppo lungo, si desidera abilitare nuovamente l'interfaccia utente e rimuovere il download:  
  
```csharp  
public async  void btnDownload_Click(object sender, EventArgs e)  
{  
    btnDownload.Enabled = false;  
    try  
    {  
        Task<Bitmap> download = GetBitmapAsync(url);  
        if (download == await Task.WhenAny(download, Task.Delay(3000)))  
        {  
            Bitmap bmp = await download;  
            pictureBox.Image = bmp;  
            status.Text = “Downloaded”;  
        }  
        else  
        {  
            pictureBox.Image = null;  
            status.Text = “Timed out”;  
            var ignored = download.ContinueWith(  
                t => Trace(“Task finally completed”));  
        }  
    }  
    finally { btnDownload.Enabled = true; }  
}  
  
```  
  
 Lo stesso vale per più download, poiché <xref:System.Threading.Tasks.Task.WhenAll%2A> restituisce un'attività:  
  
```csharp  
public async  void btnDownload_Click(object sender, RoutedEventArgs e)  
{  
    btnDownload.Enabled = false;  
    try  
    {  
        Task<Bitmap[]> downloads =   
            Task.WhenAll(from url in urls select GetBitmapAsync(url));  
        if (downloads == await Task.WhenAny(downloads, Task.Delay(3000)))  
        {  
            foreach(var bmp in downloads) panel.AddImage(bmp);  
            status.Text = “Downloaded”;  
        }  
        else  
        {  
            status.Text = “Timed out”;  
            downloads.ContinueWith(t => Log(t));  
        }  
    }  
    finally { btnDownload.Enabled = true; }  
}  
  
```  
  
## Compilazione di Combinator basati su attività  
 Poiché un'attività può rappresentare completamente un'operazione asincrona e fornire funzionalità sincrone e asincrone per effettuare join con l'operazione, recuperare i risultati e così via, è possibile compilare utili librerie dei combinator che costituiscono le attività per costruire modelli più grandi.  Come illustrato nella sezione precedente, .NET Framework include diversi combinator incorporati, ma è possibile costruirne di personalizzati.  Nelle sezioni seguenti vengono forniti alcuni esempi di potenziali metodi e tipi di combinator.  
  
### RetryOnFault  
 In molte situazioni, è possibile ritentare un'operazione se un tentativo precedente ha dato esito negativo.  Per il codice sincrono, è possibile sviluppare un metodo di supporto, come mostrato nell'esempio seguente con `RetryOnFault`, per eseguire questa operazione:  
  
```csharp  
public static T RetryOnFault<T>(  
    Func<T> function, int maxTries)  
{  
    for(int i=0; i<maxTries; i++)  
    {  
        try { return function(); }  
        catch { if (i == maxTries-1) throw; }  
    }  
    return default(T);  
}  
  
```  
  
 È possibile compilare un metodo di supporto quasi identico per le operazioni asincrone implementate con TAP e restituire in questo modo delle attività:  
  
```csharp  
public static async  Task<T> RetryOnFault<T>(  
    Func<Task<T>> function, int maxTries)  
{  
    for(int i=0; i<maxTries; i++)  
    {  
        try { return await function().ConfigureAwait(false); }  
        catch { if (i == maxTries-1) throw; }  
    }  
    return default(T);  
}  
```  
  
 È quindi possibile utilizzare questo combinator per codificare nuovi tentativi nella logica dell'applicazione; ad esempio:  
  
```csharp  
// Download the URL, trying up to three times in case of failure  
string pageContents = await RetryOnFault(  
    () => DownloadStringAsync(url), 3);  
  
```  
  
 È possibile estendere ulteriormente la funzione `RetryOnFault`.  Ad esempio, la funzione potrebbe accettare un altro `Func<Task>` che verrà richiamato tra i nuovi tentativi per determinare quando eseguire nuovamente l'operazione; ad esempio:  
  
```csharp  
public static async  Task<T> RetryOnFault<T>(  
    Func<Task<T>> function, int maxTries, Func<Task> retryWhen)  
{  
    for(int i=0; i<maxTries; i++)  
    {  
        try { return await function().ConfigureAwait(false); }  
        catch { if (i == maxTries-1) throw; }  
        await retryWhen().ConfigureAwait(false);  
    }  
    return default(T);  
}  
```  
  
 È quindi possibile utilizzare la funzione come descritto di seguito per attendere un secondo prima di ritentare l'operazione:  
  
```csharp  
// Download the URL, trying up to three times in case of failure,  
// and delaying for a second between retries  
string pageContents = await RetryOnFault(  
    () => DownloadStringAsync(url), 3, () => Task.Delay(1000));  
  
```  
  
### NeedOnlyOne  
 Talvolta, è possibile utilizzare la ridondanza per migliorare la latenza e le probabilità di successo di un'operazione.  Si considerino diversi servizi web che forniscono quotazioni azionarie, ma in diversi momenti del giorno, ogni servizio può fornire diversi livelli di qualità e tempi di risposta.  Per la gestione di tali fluttuazioni, è possibile inviare richieste a tutti i servizi web e non appena si riceve una risposta da una, annullare le richieste rimanenti.  È possibile implementare una funzione di supporto per rendere di più facile applicazione questo modello comune che consiste nell'avviare più operazioni, attenderne una qualsiasi e quindi annullare le altre.  La funzione `NeedOnlyOne` dell'esempio seguente illustra questo scenario:  
  
```csharp  
public static async  Task<T> NeedOnlyOne(  
    params Func<CancellationToken,Task<T>> [] functions)  
{  
    var cts = new CancellationTokenSource();  
    var tasks = (from function in functions  
                 select function(cts.Token)).ToArray();  
    var completed = await Task.WhenAny(tasks).ConfigureAwait(false);  
    cts.Cancel();  
    foreach(var task in tasks)   
    {  
        var ignored = task.ContinueWith(  
            t => Log(t), TaskContinuationOptions.OnlyOnFaulted);  
    }  
    return completed;  
}  
```  
  
 È quindi possibile utilizzare la funzione come segue:  
  
```csharp  
double currentPrice = await NeedOnlyOne(  
    ct => GetCurrentPriceFromServer1Async(“msft”, ct),  
    ct => GetCurrentPriceFromServer2Async(“msft”, ct),  
    ct => GetCurrentPriceFromServer3Async(“msft”, ct));  
```  
  
### Operazioni interfogliate  
 Esiste un potenziale problema di prestazioni quando si utilizza il metodo <xref:System.Threading.Tasks.Task.WhenAny%2A> per supportare uno scenario di interfoliazione nel caso in cui si utilizzino set di attività molto grandi.  Ogni chiamata a <xref:System.Threading.Tasks.Task.WhenAny%2A> comporta che una continuazione venga registrata con ogni attività.  Per N numero di attività, questo comporta O\(N2\) continuazioni create durante l'operazione di interfoliazione.  Se si utilizza un ampio set di attività, è possibile utilizzare un combinator \(`Interleaved` nell'esempio\) per risolvere il problema di prestazioni:  
  
```csharp  
static IEnumerable<Task<T>> Interleaved<T>(IEnumerable<Task<T>> tasks)  
{  
    var inputTasks = tasks.ToList();  
    var sources = (from _ in Enumerable.Range(0, inputTasks.Count)   
                   select new TaskCompletionSource<T>()).ToList();  
    int nextTaskIndex = -1;  
    foreach (var inputTask in inputTasks)  
    {  
        inputTask.ContinueWith(completed =>  
        {  
            var source = sources[Interlocked.Increment(ref nextTaskIndex)];  
            if (completed.IsFaulted)   
                source.TrySetException(completed.Exception.InnerExceptions);  
            else if (completed.IsCanceled)   
                source.TrySetCanceled();  
            else   
                source.TrySetResult(completed.Result);  
        }, CancellationToken.None,   
           TaskContinuationOptions.ExecuteSynchronously,   
           TaskScheduler.Default);  
    }  
    return from source in sources   
           select source.Task;  
}  
  
```  
  
 È quindi possibile utilizzare il combinator per elaborare i risultati delle attività man mano che terminano, ad esempio:  
  
```csharp  
IEnumerable<Task<int>> tasks = ...;  
foreach(var task in Interleaved(tasks))  
{  
    int result = await task;  
    …  
}  
```  
  
### WhenAllOrFirstException  
 In alcuni scenari di dispersione\/raccolta di dati, potrebbe essere necessario attendere il completamento di tutti i processi di un set a meno che uno di questi non fallisca, nel qual caso si desidera arrestare l'attesa non appena si verifica l'eccezione.  È possibile eseguire questa operazione con un metodo combinator come `WhenAllOrFirstException` nell'esempio seguente:  
  
```csharp  
public static Task<T[]> WhenAllOrFirstException<T>(IEnumerable<Task<T>> tasks)  
{  
    var inputs = tasks.ToList();  
    var ce = new CountdownEvent(inputs.Count);  
    var tcs = new TaskCompletionSource<T[]>();  
  
    Action<Task> onCompleted = (Task completed) =>  
    {  
        if (completed.IsFaulted)   
            tcs.TrySetException(completed.Exception.InnerExceptions);  
        if (ce.Signal() && !tcs.Task.IsCompleted)  
            tcs.TrySetResult(inputs.Select(t => t.Result).ToArray());  
    };  
  
    foreach (var t in inputs) t.ContinueWith(onCompleted);  
    return tcs.Task;  
}  
  
```  
  
## Costruire strutture dati basate su eventi  
 Oltre alla possibilità di costruire combinator personalizzati basati su attività, avere una struttura di dati in <xref:System.Threading.Tasks.Task> e in <xref:System.Threading.Tasks.Task%601> che rappresenta sia i risultati di un'operazione asincrona che la sincronizzazione necessaria con cui effettuare il join lo rende un tipo molto potente su cui basarsi per costruire strutture dati personalizzate da utilizzare in scenari asincroni.  
  
### AsyncCache  
 Un aspetto importante di un'attività è che può essere distribuita a diversi clienti, tutti la possono attendere, registrarvi continuazioni, ottenerne il risultato o delle eccezioni \(nel caso di <xref:System.Threading.Tasks.Task%601>\), e così via.  Ciò rende <xref:System.Threading.Tasks.Task> e <xref:System.Threading.Tasks.Task%601> perfettamente appropriati per essere utilizzati in un'infrastruttura asincrona di memorizzazione nella cache.  Di seguito è riportato un esempio di una piccola ma potente cache asincrona costruita basandosi su <xref:System.Threading.Tasks.Task%601>:  
  
```csharp  
public class AsyncCache<TKey, TValue>  
{  
    private readonly Func<TKey, Task<TValue>> _valueFactory;  
    private readonly ConcurrentDictionary<TKey, Lazy<Task<TValue>>> _map;  
  
    public AsyncCache(Func<TKey, Task<TValue>> valueFactory)  
    {  
        if (valueFactory == null) throw new ArgumentNullException("loader");  
        _valueFactory = valueFactory;  
        _map = new ConcurrentDictionary<TKey, Lazy<Task<TValue>>>();  
    }  
  
    public Task<TValue> this[TKey key]  
    {  
        get  
        {  
            if (key == null) throw new ArgumentNullException("key");  
            return _map.GetOrAdd(key, toAdd =>   
                new Lazy<Task<TValue>>(() => _valueFactory(toAdd))).Value;  
        }  
    }  
}  
  
```  
  
 La classe [AsyncCache\<TKey, TValue\>](http://go.microsoft.com/fwlink/p/?LinkId=251941) accetta come delegato al costruttore una funzione che accetta `TKey` e restituisce <xref:System.Threading.Tasks.Task%601>.  Tutti i valori della cache a cui si è acceduto precedentemente vengono archiviati nel dizionario interno e l' `AsyncCache` fa in modo che venga generata solo un'attività per chiave, anche si accede alla cache contemporaneamente.  
  
 Ad esempio, è possibile costruire una cache per le pagine web scaricate:  
  
```csharp  
private AsyncCache<string,string> m_webPages =   
    new AsyncCache<string,string>(DownloadStringAsync);  
  
```  
  
 È possibile utilizzare tale cache nei metodi asincroni ogni volta che è necessario accedere al contenuto di una pagina web.  La classe `AsyncCache` assicura che si scarichino il minor numero di pagine possibile e memorizza nella cache i risultati.  
  
```csharp  
private async  void btnDownload_Click(object sender, RoutedEventArgs e)   
{  
    btnDownload.IsEnabled = false;  
    try  
    {  
        txtContents.Text = await m_webPages["http://www.microsoft.com"];  
    }  
    finally { btnDownload.IsEnabled = true; }  
}  
  
```  
  
### AsyncProducerConsumerCollection  
 È inoltre possibile utilizzare le attività per costruire strutture dati per coordinare le attività asincrone.  Si consideri uno dei classici modelli di progettazione paralleli: produttore\/consumatore.  In questo modello, i produttori generano dati che sono consumati dai consumatori e i produttori e i consumatori possono operare in parallelo.  Ad esempio, il consumatore elabora l'elemento 1, che è stato precedentemente generato da un produttore che sta scrivendo l'elemento 2. Per il modello produttore\/consumatore, si necessita invariabilmente di una struttura dati in cui memorizzare il lavoro creato dai produttori in modo che i consumatori possano essere informati di nuovi dati e possano gestirli una volta disponibili.  
  
 Questa è una semplice struttura dati costruita basandosi sulle attività che consente ai metodi asincroni di essere utilizzati come produttori e consumatori:  
  
```csharp  
public class AsyncProducerConsumerCollection<T>  
{  
    private readonly Queue<T> m_collection = new Queue<T>();  
    private readonly Queue<TaskCompletionSource<T>> m_waiting =   
        new Queue<TaskCompletionSource<T>>();  
  
    public void Add(T item)  
    {  
        TaskCompletionSource<T> tcs = null;  
        lock (m_collection)  
        {  
            if (m_waiting.Count > 0) tcs = m_waiting.Dequeue();  
            else m_collection.Enqueue(item);  
        }  
        if (tcs != null) tcs.TrySetResult(item);  
    }  
  
    public Task<T> Take()  
    {  
        lock (m_collection)  
        {  
            if (m_collection.Count > 0)   
            {  
                return Task.FromResult(m_collection.Dequeue());   
            }  
            else   
            {  
                var tcs = new TaskCompletionSource<T>();  
                m_waiting.Enqueue(tcs);  
                return tcs.Task;  
            }  
        }  
    }  
}  
  
```  
  
 Con tale struttura dei dati, è possibile scrivere del codice come il seguente:  
  
```csharp  
private static AsyncProducerConsumerCollection<int> m_data = …;  
…  
private static async  Task ConsumerAsync()  
{  
    while(true)  
    {  
        int nextItem = await m_data.Take();  
        ProcessNextItem(nextItem);  
    }  
}  
…  
private static void Produce(int data)  
{  
    m_data.Add(data);  
}  
```  
  
 Lo spazio dei nomi <xref:System.Threading.Tasks.Dataflow> include il tipo <xref:System.Threading.Tasks.Dataflow.BufferBlock%601>, utilizzabile in modo simile, ma senza dover costruire un tipo di raccolta personalizzato:  
  
```csharp  
private static BufferBlock<int> m_data = …;  
…  
private static async  Task ConsumerAsync()  
{  
    while(true)  
    {  
        int nextItem = await m_data.ReceiveAsync();  
        ProcessNextItem(nextItem);  
    }  
}  
…  
private static void Produce(int data)  
{  
    m_data.Post(data);  
}  
  
```  
  
> [!NOTE]
>  Lo spazio dei nomi <xref:System.Threading.Tasks.Dataflow> è disponibile in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] tramite **NuGet**.  Per installare l'assembly che contiene lo spazio dei nomi <xref:System.Threading.Tasks.Dataflow>, aprire il progetto in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)], scegliere **Gestire i pacchetti NuGet** dal menu Progetto e cercare online il pacchetto Microsoft.Tpl.Dataflow.  
  
## Vedere anche  
 [Task\-based Asynchronous Pattern \(TAP\)](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)   
 [Implementing the Task\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/implementing-the-task-based-asynchronous-pattern.md)   
 [Interop with Other Asynchronous Patterns and Types](../../../docs/standard/asynchronous-programming-patterns/interop-with-other-asynchronous-patterns-and-types.md)