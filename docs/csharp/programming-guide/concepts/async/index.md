---
title: Programmazione asincrona con Async e Await (C#) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 9bcf896a-5826-4189-8c1a-3e35fa08243a
caps.latest.revision: 5
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 931f984b2267d0782cdbad22cb00f7a698de357e
ms.lasthandoff: 03/13/2017

---
# <a name="asynchronous-programming-with-async-and-await-c"></a>Programmazione asincrona con Async e Await
È possibile evitare colli di bottiglia nelle prestazioni e migliorare la risposta generale dell'applicazione utilizzando la programmazione asincrona. Le tecniche tradizionali per la scrittura di applicazioni asincrone, tuttavia, possono essere complesse, rendendone difficile la scrittura, il debug e la gestione.  
  
 Visual Studio 2012 introduce un approccio semplificato, la programmazione asincrona, che sfrutta il supporto asincrono in .NET Framework 4.5 e versioni successive oltre che in Windows Runtime. Il compilatore esegue il lavoro difficile che prima veniva svolto dallo sviluppatore e l'applicazione mantiene una struttura logica simile al codice sincrono. Di conseguenza, si ottengono tutti i vantaggi della programmazione asincrona con meno lavoro richiesto.  
  
 In questo argomento viene fornita una panoramica di come e quando utilizzare la programmazione asincrona e vengono forniti collegamenti per supportare gli argomenti contenenti informazioni dettagliate ed esempi.  
  
##  <a name="BKMK_WhentoUseAsynchrony"></a> Async migliora la velocità di risposta  
 La modalità asincrona è essenziale per le attività che potenzialmente bloccano l'esecuzione, ad esempio quando l'applicazione accede al Web. L'accesso a una risorsa Web può essere talvolta lento o ritardato. Se tale attività viene bloccata in un processo sincrono, l'intera applicazione deve attendere. In un processo asincrono l'applicazione può invece continuare con un altro lavoro che non dipende dalla risorsa Web finché l'attività di blocco non termina.  
  
 Nella tabella seguente sono mostrate le aree tipiche in cui la programmazione asincrona migliora la risposta. Le API elencate da .NET Framework 4.5 e Windows Runtime contengono metodi che supportano la programmazione asincrona.  
  
|Area dell'applicazione|API di supporto che contengono metodi asincroni|  
|----------------------|------------------------------------------------|  
|Accesso Web|<xref:System.Net.Http.HttpClient>, [SyndicationClient](http://go.microsoft.com/fwlink/p/?LinkId=259441)|  
|Utilizzo dei file|[StorageFile](http://go.microsoft.com/fwlink/p/?LinkId=248220), <xref:System.IO.StreamWriter>, <xref:System.IO.StreamReader>, <xref:System.Xml.XmlReader>|  
|Utilizzo delle immagini|[MediaCapture](http://go.microsoft.com/fwlink/p/?LinkId=261839), [BitmapEncoder](http://go.microsoft.com/fwlink/p/?LinkId=261840), [BitmapDecoder](http://go.microsoft.com/fwlink/p/?LinkId=261841)|  
|Programmazione WCF|[Operazioni sincrone e asincrone](http://go.microsoft.com/fwlink/p/?LinkID=192382)|   
  
La modalità asincrona è particolarmente importante per le applicazioni che accedono al thread dell'interfaccia utente poiché tutte le attività correlate all'interfaccia utente in genere condividono un thread. Se un processo è bloccato in un'applicazione sincrona, tutte le attività saranno bloccate. L'applicazione non risponde e si potrebbe pensare che si sia verificato un errore mentre si tratta solo di un'applicazione attesa.  
  
 Quando si utilizzano i metodi asincroni, l'applicazione continua a rispondere all'interfaccia utente. È possibile ad esempio ridimensionare o ridurre a icona una finestra oppure è possibile chiudere l'applicazione se non si desidera attendere il completamento.  
  
 L'approccio basato su modalità asincrona aggiunge l'equivalente di una trasmissione automatica all'elenco di opzioni da cui è possibile scegliere quando si progettano operazioni asincrone. In questo modo si ottengono tutti i vantaggi della programmazione asincrona tradizionale con meno lavoro richiesto allo sviluppatore.  
  
##  <a name="BKMK_HowtoWriteanAsyncMethod"></a> I metodi asincroni sono più semplici da scrivere  
 Le parole chiave [async](../../../../csharp/language-reference/keywords/async.md) e [await](../../../../csharp/language-reference/keywords/await.md) in C# sono il punto centrale della programmazione asincrona. Tramite queste due parole chiave, è possibile usare le risorse di .NET Framework o di Windows Runtime per creare un metodo asincrono con la stessa facilità con cui è possibile creare un metodo sincrono. I metodi asincroni definiti mediante `async` e `await` sono denominati metodi asincroni.  
  
 Nell'esempio seguente viene illustrato un metodo asincrono. Quasi tutti gli elementi del codice dovrebbe essere completamente noti all'utente. I commenti richiamano le funzionalità che si aggiungono per creare la modalità asincrona.  
  
 È possibile trovare il file di esempio completo Windows Presentation Foundation (WPF) alla fine di questo argomento e scaricare l'esempio dalla pagina [Async Sample: Example from "Asynchronous Programming with Async and Await"](http://go.microsoft.com/fwlink/?LinkID=261549) (Esempio di attività asincrona: Programmazione asincrona con async e await).  
  
```csharp  
// Three things to note in the signature:  
//  - The method has an async modifier.   
//  - The return type is Task or Task<T>. (See "Return Types" section.)  
//    Here, it is Task<int> because the return statement returns an integer.  
//  - The method name ends in "Async."  
async Task<int> AccessTheWebAsync()  
{   
    // You need to add a reference to System.Net.Http to declare client.  
    HttpClient client = new HttpClient();  
  
    // GetStringAsync returns a Task<string>. That means that when you await the  
    // task you'll get a string (urlContents).  
    Task<string> getStringTask = client.GetStringAsync("http://msdn.microsoft.com");  
  
    // You can do work here that doesn't rely on the string from GetStringAsync.  
    DoIndependentWork();  
  
    // The await operator suspends AccessTheWebAsync.  
    //  - AccessTheWebAsync can't continue until getStringTask is complete.  
    //  - Meanwhile, control returns to the caller of AccessTheWebAsync.  
    //  - Control resumes here when getStringTask is complete.   
    //  - The await operator then retrieves the string result from getStringTask.  
    string urlContents = await getStringTask;  
  
    // The return statement specifies an integer result.  
    // Any methods that are awaiting AccessTheWebAsync retrieve the length value.  
    return urlContents.Length;  
}  
```  
  
 Se `AccessTheWebAsync` non ha alcuna operazione da eseguire tra la chiamata di `GetStringAsync` e il relativo completamento, è possibile semplificare il codice chiamando l'istruzione singola seguente e rimanendo in attesa.  
  
```csharp  
string urlContents = await client.GetStringAsync();  
```  
  
 Le seguenti caratteristiche riepilogano gli aspetti che rendono l'esempio precedente un metodo asincrono.  
  
-   La firma del metodo include un modificatore `async`.  
  
-   Il nome di un metodo asincrono termina per convenzione con un suffisso "Async".  
  
-   Il tipo restituito è uno dei seguenti:  
  
    -   <xref:System.Threading.Tasks.Task%601> se nel metodo è presente un'istruzione return in cui l'operando è di tipo TResult.  
  
    -   <xref:System.Threading.Tasks.Task> se nel metodo non è presente un'istruzione return oppure è presente un'istruzione return senza l'operando.  
  
    -   `Void` se si sta scrivendo un gestore eventi asincrono.  
  
     Per ulteriori informazioni, vedere la sezione "Tipi restituiti e parametri" più avanti in questo argomento.  
  
-   Il metodo include in genere almeno un'espressione await, che contrassegna un punto in cui il metodo non può continuare fino a quando l'operazione asincrona attesa non sia completata. Nel frattempo, il metodo viene sospeso e il controllo ritorna al chiamante del metodo. Nella sezione successiva di questo argomento viene illustrato quello che accade in corrispondenza del punto di sospensione.  
  
 Nei metodi asincroni utilizzare le parole chiave e i tipi forniti per indicare l'operazione da eseguire e il compilatore esegue il resto dell'operazione, inclusa la traccia di cosa deve verificarsi quando il controllo viene restituito a un punto di attesa in un metodo sospeso. Alcuni processi di routine, come cicli e gestione delle eccezioni, possono essere difficili da gestire nel codice asincrono tradizionale. In un metodo asincrono scrivere questi elementi come in una soluzione sincrona e il problema viene risolto.  
  
 Per altre informazioni sulla modalità asincrona in versioni precedenti di .NET Framework, vedere [TPL and Traditional .NET Framework Asynchronous Programming](http://msdn.microsoft.com/library/e7b31170-a156-433f-9f26-b1fc7cd1776f) (TPL e programmazione asincrona .NET Framework tradizionale).  
  
##  <a name="BKMK_WhatHappensUnderstandinganAsyncMethod"></a> Operazioni eseguite in un metodo asincrono  
 La cosa più importante da capire nella programmazione asincrona è il modo in cui il flusso del controllo si sposta da un metodo all'altro. Nel diagramma seguente viene descritto il processo.  
  
 ![Tracciare un programma asincrono](../../../../csharp/programming-guide/concepts/async/media/navigationtrace.png "NavigationTrace")  
  
 I numeri nel diagramma corrispondono ai passaggi seguenti.  
  
1.  Un gestore eventi chiama e attende il metodo asincrono `AccessTheWebAsync`.  
  
2.  `AccessTheWebAsync` crea un'istanza di <xref:System.Net.Http.HttpClient> e chiama il metodo asincrono <xref:System.Net.Http.HttpClient.GetStringAsync%2A> per scaricare il contenuto di un sito Web come stringa.  
  
3.  Si verifica un evento in `GetStringAsync` che ne sospende lo stato di avanzamento forse perché deve attendere il termine dello scaricamento di un sito Web o un'altra attività di blocco. Per evitare di bloccare le risorse, `GetStringAsync` restituisce il controllo al chiamante `AccessTheWebAsync`.  
  
     `GetStringAsync` restituisce <xref:System.Threading.Tasks.Task%601> dove `TResult` è una stringa e `AccessTheWebAsync` assegna le attività alla variabile `getStringTask`. L'attività rappresenta il processo in corso per la chiamata a `GetStringAsync`, con l'impegno di produrre un valore stringa effettivo a completamento del lavoro.  
  
4.  Poiché `getStringTask` non è stata ancora attesa, `AccessTheWebAsync` può continuare con altro lavoro che non dipende dal risultato finale ottenuto da `GetStringAsync`. Tale lavoro è rappresentato da una chiamata al metodo sincrono `DoIndependentWork`.  
  
5.  `DoIndependentWork` è un metodo sincrono che esegue il proprio lavoro e lo restituisce al chiamante.  
  
6.  `AccessTheWebAsync` ha esaurito il lavoro che può eseguire senza un risultato da `getStringTask`. `AccessTheWebAsync` deve quindi calcolare e restituire la lunghezza della stringa scaricata, ma il metodo non può calcolare il valore finché quest'ultimo non contiene la stringa.  
  
     Di conseguenza, `AccessTheWebAsync` utilizza un operatore await per sospendere lo stato di avanzamento e restituire il controllo al metodo che ha chiamato `AccessTheWebAsync`. `AccessTheWebAsync` restituisce `Task<int>` al chiamante. L'attività rappresenta l'intenzione di produrre un risultato di tipo Integer che è la lunghezza della stringa scaricata.  
  
    > [!NOTE]
    >  Se l'operazione `GetStringAsync` (e quindi `getStringTask`) viene completata prima che `AccessTheWebAsync` ne attenda il risultato, il controllo resta a `AccessTheWebAsync`. I costi per sospendere e tornare a `AccessTheWebAsync` sarebbero sprecati se il processo asincrono chiamato (`getStringTask`) fosse già completato e AccessTheWebSync non dovesse attendere il risultato finale.  
  
     Nel chiamante (in questo esempio il gestore eventi), il modello di elaborazione continua. Il chiamante può eseguire altre attività che non dipendono dal risultato di `AccessTheWebAsync` prima di attendere tale risultato oppure può mettersi immediatamente in attesa.   Il gestore eventi è in attesa di `AccessTheWebAsync` e `AccessTheWebAsync` è in attesa di `GetStringAsync`.  
  
7.  `GetStringAsync` termina e produce un risultato di stringa. Il risultato di stringa non viene restituito dalla chiamata a `GetStringAsync` nel modo previsto. Tenere presente che il metodo non ha restituito un'attività al passaggio 3. Il risultato della stringa viene invece memorizzato nell'attività che rappresenta il completamento del metodo, ovvero `getStringTask`. L'operatore await recupera il risultato da `getStringTask`. L'istruzione di assegnazione assegna il risultato recuperato a `urlContents`.  
  
8.  Quando `AccessTheWebAsync` ha il risultato di stringa, il metodo può calcolare la lunghezza della stringa. Il lavoro di `AccessTheWebAsync` è quindi completo e il gestore eventi in attesa può riprendere l'attività. Nell'esempio completo alla fine dell'argomento è possibile confermare che il gestore eventi recupera e stampa il valore del risultato di lunghezza.  
  
 Se non si ha familiarità con la programmazione asincrona, valutare la differenza tra il comportamento sincrono e asincrono. Viene restituito un metodo sincrono quando il lavoro è completato (passaggio 5), ma un metodo asincrono restituisce un valore di attività quando il relativo lavoro viene sospeso (passaggi 3 e 6). Una volta che il metodo asincrono completa l'operazione, l'attività viene contrassegnata come completata e il risultato, se disponibile, viene archiviato nell'attività.  
  
 Per altre informazioni sul flusso di controllo, vedere [Flusso di controllo in programmi asincroni (C#)](../../../../csharp/programming-guide/concepts/async/control-flow-in-async-programs.md).  
  
##  <a name="BKMK_APIAsyncMethods"></a> Metodi asincroni per API  
 Metodi come `GetStringAsync` che supportano la programmazione asincrona In .NET Framework 4.5 o versioni successive sono presenti diversi membri che utilizzano `async` e `await`. È possibile riconoscere questi membri dal suffisso "Async" associato al nome del membro e dal tipo restituito di <xref:System.Threading.Tasks.Task> o <xref:System.Threading.Tasks.Task%601>. Ad esempio, la classe `System.IO.Stream` contiene metodi quali <xref:System.IO.Stream.CopyToAsync%2A>, <xref:System.IO.Stream.ReadAsync%2A> e <xref:System.IO.Stream.WriteAsync%2A>, oltre ai metodi sincroni <xref:System.IO.Stream.CopyTo%2A>, <xref:System.IO.Stream.Read%2A> e <xref:System.IO.Stream.Write%2A>.  
  
 Windows Runtime contiene inoltre molti metodi che è possibile usare con `async` e `await` in app Windows. Per altre informazioni e metodi di esempio, vedere [Guida introduttiva: Chiamata di API asincrone in C# o Visual Basic](http://go.microsoft.com/fwlink/?LinkId=248545), [Programmazione asincrona (app di Windows Runtime)](http://go.microsoft.com/fwlink/?LinkId=259592) e [WhenAny: bridging tra .NET Framework e Windows Runtime](https://msdn.microsoft.com/library/jj635140(v=vs.120).aspx).  
  
##  <a name="BKMK_Threads"></a> Thread  
 I metodi asincroni vengono considerati operazioni non bloccanti. Un'espressione `await` in un metodo asincrono non blocca il thread corrente quando l'attività attesa è in esecuzione. Al contrario, l'espressione registra il resto del metodo come continuazione e restituisce il controllo al chiamante del metodo asincrono.  
  
 Le parole chiave `async` e `await` non determinano la creazione di thread aggiuntivi. I metodi asincroni non richiedono multithreading perché un metodo asincrono non viene eseguito nel proprio thread. Il metodo viene eseguito nel contesto di sincronizzazione corrente e utilizza il tempo sul thread solo se il metodo è attivo. È possibile usare <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=fullName> per spostare un processo associato alla CPU in un thread in background. Quest'ultimo, tuttavia, non è di alcun ausilio in un processo che attende solo che i risultati diventino disponibili.  
  
 L'approccio alla programmazione asincrona basato su async è quasi sempre preferibile agli approcci esistenti. In particolare, questo approccio è preferibile a <xref:System.ComponentModel.BackgroundWorker> per le operazioni di I/O poiché il codice è più semplice e non è necessario proteggersi da situazioni di race condition. In combinazione con <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=fullName>, la programmazione asincrona è migliore di <xref:System.ComponentModel.BackgroundWorker> per le operazioni associate alla CPU perché separa i dettagli di coordinamento per l'esecuzione del codice dal processo che `Task.Run` trasferisce al pool di thread.  
  
##  <a name="BKMK_AsyncandAwait"></a> Async e Await  
 Se si specifica che un metodo è asincrono usando un modificatore [async](../../../../csharp/language-reference/keywords/async.md), vengono attivate le due funzionalità seguenti.  
  
-   Il metodo asincrono contrassegnato può usare [await](../../../../csharp/language-reference/keywords/await.md) per definire i punti di sospensione. L'operatore await indica al compilatore che il metodo asincrono non può continuare oltre un dato punto prima del completamento del processo asincrono in attesa. Nel frattempo il controllo viene restituito al chiamante del metodo asincrono.  
  
     La sospensione di un metodo asincrono in corrispondenza di un'espressione `await` non costituisce l'uscita dal metodo e i blocchi `finally` non vengono eseguiti.  
  
-   Il metodo asincrono contrassegnato può essere atteso da metodi che lo chiamano.  
  
 Un metodo asincrono contiene in genere una o più occorrenze di un operatore `await`, mentre l'assenza di espressioni `await` non provoca un errore del compilatore. Se un metodo asincrono non usa un operatore `await` per contrassegnare un punto di sospensione, si comporterà come un metodo sincrono nonostante la presenza del modificatore `async`. Il compilatore genera un avviso per tali metodi.  
  
 `async` e `await` sono parole chiave contestuali. Per ulteriori informazioni ed esempi, vedere gli argomenti seguenti:  
  
-   [async](../../../../csharp/language-reference/keywords/async.md)  
  
-   [await](../../../../csharp/language-reference/keywords/await.md)  
  
##  <a name="BKMK_ReturnTypesandParameters"></a> Tipi restituiti e parametri  
 Nella programmazione .NET Framework un metodo asincrono restituisce in genere <xref:System.Threading.Tasks.Task> o <xref:System.Threading.Tasks.Task%601>. In un metodo asincrono un operatore `await` viene applicato a un'attività restituita da una chiamata a un altro metodo asincrono.  
  
 Specificare <xref:System.Threading.Tasks.Task%601> come tipo restituito se il metodo contiene un'istruzione [return](../../../../csharp/language-reference/keywords/return.md) che specifica un operando di tipo `TResult`.  
  
 Utilizzare `Task` come tipo restituito se il metodo non include un'istruzione return o contiene un'istruzione return che non restituisce un operando.  
  
 Nell'esempio seguente viene illustrato come dichiarare e chiamare un metodo che restituisce <xref:System.Threading.Tasks.Task%601> o <xref:System.Threading.Tasks.Task>.  
  
```csharp  
// Signature specifies Task<TResult>  
async Task<int> TaskOfTResult_MethodAsync()  
{  
    int hours;  
    // . . .  
    // Return statement specifies an integer result.  
    return hours;  
}  
  
// Calls to TaskOfTResult_MethodAsync  
Task<int> returnedTaskTResult = TaskOfTResult_MethodAsync();  
int intResult = await returnedTaskTResult;  
// or, in a single statement  
int intResult = await TaskOfTResult_MethodAsync();  
  
// Signature specifies Task  
async Task Task_MethodAsync()  
{  
    // . . .  
    // The method has no return statement.    
}  
  
// Calls to Task_MethodAsync  
Task returnedTask = Task_MethodAsync();  
await returnedTask;  
// or, in a single statement  
await Task_MethodAsync();  
  
```  
  
 Ogni attività restituita rappresenta il lavoro attualmente in fase di esecuzione. Un'attività include le informazioni sullo stato del processo asincrono e, infine, il risultato finale del processo o l'eccezione che il processo genera se non viene completato.  
  
 Un metodo asincrono può avere un tipo restituito `void`. Il tipo restituito viene utilizzato principalmente per definire i gestori eventi, dove un tipo restituito `void` è necessario. I gestori eventi asincroni fungono spesso da punto di partenza per i programmi asincroni.  
  
 Un metodo asincrono con un tipo restituito `void` non può essere atteso e il chiamante di un metodo che restituisce void non può rilevare eventuali eccezioni generate dal metodo.  
  
 Un metodo asincrono non può dichiarare parametri [ref](../../../../csharp/language-reference/keywords/ref.md) o [out](../../../../csharp/language-reference/keywords/out.md), ma può chiamare metodi che hanno tali parametri.  
  
 Per altre informazioni ed esempi, vedere [Tipi restituiti asincroni (C#)](../../../../csharp/programming-guide/concepts/async/async-return-types.md). Per altre informazioni su come intercettare eccezioni nei metodi asincroni, vedere [try-catch](../../../../csharp/language-reference/keywords/try-catch.md).  
  
 Nella programmazione Windows Runtime, alle API asincrone è associato uno dei tipi restituiti seguenti, che sono simili alle attività:  
  
-   [IAsyncOperation](http://go.microsoft.com/fwlink/p/?LinkId=261896), corrispondente a <xref:System.Threading.Tasks.Task%601>  
  
-   [IAsyncAction](http://go.microsoft.com/fwlink/p/?LinkId=261897), corrispondente a <xref:System.Threading.Tasks.Task>  
  
-   [IAsyncActionWithProgress](http://go.microsoft.com/fwlink/p/?LinkId=261898)  
  
-   [IAsyncOperationWithProgress](http://go.microsoft.com/fwlink/p/?LinkID=259454)  
  
 Per altre informazioni e un esempio, vedere [Guida introduttiva: Uso dell'operatore await per la programmazione asincrona](http://go.microsoft.com/fwlink/p/?LinkId=248545).  
  
##  <a name="BKMK_NamingConvention"></a> Convenzione di denominazione  
 Per convenzione, il suffisso "Async" viene aggiunto ai nomi dei metodi che presentano un modificatore `async`.  
  
 È possibile ignorare la convenzione se un evento, una classe base o un contratto di interfaccia suggerisce un nome diverso. Ad esempio, non è necessario rinominare i gestori eventi comuni, come `Button1_Click`.  
  
##  <a name="BKMK_RelatedTopics"></a> Argomenti correlati ed esempi (Visual Studio)  
  
|Titolo|Descrizione|Esempio|  
|-----------|-----------------|------------|  
|[Procedura dettagliata: Accesso al Web con Async e Await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)|Mostra come convertire una soluzione WPF sincrona in una soluzione WPF asincrona. L'applicazione scarica una serie di siti Web.|[Async Sample: Accessing the Web Walkthrough](http://go.microsoft.com/fwlink/p/?LinkID=255191&clcid=0x409) (Esempio di attività asincrona: Accesso alla procedura dettagliata Web)|  
|[Procedura: Estendere la procedura dettagliata asincrona tramite Task.WhenAll (C#)](../../../../csharp/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md)|Aggiunge <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> alla procedura dettagliata precedente. L'utilizzo di `WhenAll` consente di avviare tutti i download contemporaneamente.||  
|[Procedura: Eseguire più richieste Web in parallelo tramite async e await (C#)](../../../../csharp/programming-guide/concepts/async/how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await.md)|Viene illustrato come avviare contemporaneamente diverse attività.|[Async Sample: Make Multiple Web Requests in Parallel](http://go.microsoft.com/fwlink/p/?LinkID=254906&clcid=0x409) (Esempio di attività asincrona: Esecuzione di più richieste Web in parallelo)|  
|[Tipi restituiti asincroni (C#)](../../../../csharp/programming-guide/concepts/async/async-return-types.md)|Vengono illustrati i tipi che i metodi asincroni possono restituire e viene spiegato quando ogni tipo è appropriato.||  
|[Flusso di controllo in programmi asincroni (C#)](../../../../csharp/programming-guide/concepts/async/control-flow-in-async-programs.md)|Traccia in dettaglio il flusso di controllo con una successione di espressioni await in un programma asincrono.|[Async Sample: Control Flow in Async Programs](http://go.microsoft.com/fwlink/p/?LinkID=255285&clcid=0x409) (Esempio di attività asincrona: Flusso di controllo in programmi asincroni)|  
|[Ottimizzazione dell'applicazione Async (C#)](../../../../csharp/programming-guide/concepts/async/fine-tuning-your-async-application.md)|Mostra come aggiungere la seguente funzionalità alla soluzione asincrono:<br /><br /> -   [Annullare un'attività asincrona o un elenco di attività (C#)](../../../../csharp/programming-guide/concepts/async/cancel-an-async-task-or-a-list-of-tasks.md)<br />-   [Annullare attività asincrone dopo un periodo di tempo (C#)](../../../../csharp/programming-guide/concepts/async/cancel-async-tasks-after-a-period-of-time.md)<br />-   [Annullare le attività asincrone rimanenti dopo che ne è stata completata una (C#)](../../../../csharp/programming-guide/concepts/async/cancel-remaining-async-tasks-after-one-is-complete.md)<br />-   [Avviare più attività asincrone ed elaborarle quando vengono completate (C#)](../../../../csharp/programming-guide/concepts/async/start-multiple-async-tasks-and-process-them-as-they-complete.md)|[Async Sample: Fine Tuning Your Application](http://go.microsoft.com/fwlink/p/?LinkID=255046&clcid=0x409) (Esempio di attività asincrona: Ottimizzazione dell'applicazione)|  
|[Gestione della reentrancy nelle app asincrone (C#)](../../../../csharp/programming-guide/concepts/async/handling-reentrancy-in-async-apps.md)|Viene illustrato come gestire i casi in cui un'operazione asincrona attiva viene riavviata mentre è in esecuzione.||  
|[WhenAny: bridging tra .NET Framework e Windows Runtime](https://msdn.microsoft.com/library/jj635140(v=vs.120).aspx)|Viene illustrato come eseguire il bridging tra tipi di attività in .NET Framework e IAsyncOperations in [!INCLUDE[wrt](../../../../csharp/includes/wrt_md.md)] per usare <xref:System.Threading.Tasks.Task.WhenAny%2A> con un metodo [!INCLUDE[wrt](../../../../csharp/includes/wrt_md.md)].|[Async Sample: Bridging between .NET and Windows Runtime (AsTask and WhenAny)](http://go.microsoft.com/fwlink/p/?LinkID=260638) (Esempio di attività asincrona: Bridging tra .NET e Windows Runtime (AsTask e WhenAny))|  
|Annullamento asincrono: bridging tra .NET Framework e Windows Runtime|Viene illustrato come eseguire il bridging tra tipi di attività in .NET Framework e IAsyncOperations in [!INCLUDE[wrt](../../../../csharp/includes/wrt_md.md)] per usare <xref:System.Threading.CancellationTokenSource> con un metodo [!INCLUDE[wrt](../../../../csharp/includes/wrt_md.md)].|[Async Sample: Bridging between .NET and Windows Runtime (AsTask & Cancellation)](http://go.microsoft.com/fwlink/p/?LinkId=263004) (Esempio di attività asincrona: Bridging tra .NET e Windows Runtime (AsTask e Cancellation))|  
|[Uso della funzionalità Async per l'accesso ai file (C#)](../../../../csharp/programming-guide/concepts/async/using-async-for-file-access.md)|Vengono elencati e illustrati i vantaggi dell'utilizzo di async e await per accedere ai file.||  
|[Modello asincrono basato su attività (TAP)](http://msdn.microsoft.com/library/8cef1fcf-6f9f-417c-b21f-3fd8bac75007)|Descrive un nuovo modello per la modalità asincrona in .NET Framework. Il modello è basato sui tipi <xref:System.Threading.Tasks.Task> e <xref:System.Threading.Tasks.Task%601>.||  
|[Video sulla modalità asincrona su Channel 9](http://go.microsoft.com/fwlink/p/?LinkID=267466)|Vengono forniti collegamenti a una serie di video sulla programmazione asincrona.||  
  
##  <a name="BKMK_CompleteExample"></a> Esempio completo  
 Il codice seguente rappresenta il file MainWindow.xaml.cs dell'applicazione Windows Presentation Foundation (WPF) discussa in questo argomento. È possibile scaricare l'esempio dalla pagina [Async Sample: Example from "Asynchronous Programming with Async and Await"](http://go.microsoft.com/fwlink/p/?LinkID=261549) (Esempio di attività asincrona: Programmazione asincrona con async e await).  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Threading.Tasks;  
using System.Windows;  
using System.Windows.Controls;  
using System.Windows.Data;  
using System.Windows.Documents;  
using System.Windows.Input;  
using System.Windows.Media;  
using System.Windows.Media.Imaging;  
using System.Windows.Navigation;  
using System.Windows.Shapes;  
  
// Add a using directive and a reference for System.Net.Http;  
using System.Net.Http;  
  
namespace AsyncFirstExample  
{  
    public partial class MainWindow : Window  
    {  
        // Mark the event handler with async so you can use await in it.  
        private async void StartButton_Click(object sender, RoutedEventArgs e)  
        {  
            // Call and await separately.  
            //Task<int> getLengthTask = AccessTheWebAsync();  
            //// You can do independent work here.  
            //int contentLength = await getLengthTask;  
  
            int contentLength = await AccessTheWebAsync();  
  
            resultsTextBox.Text +=  
                String.Format("\r\nLength of the downloaded string: {0}.\r\n", contentLength);  
        }  
  
        // Three things to note in the signature:  
        //  - The method has an async modifier.   
        //  - The return type is Task or Task<T>. (See "Return Types" section.)  
        //    Here, it is Task<int> because the return statement returns an integer.  
        //  - The method name ends in "Async."  
        async Task<int> AccessTheWebAsync()  
        {   
            // You need to add a reference to System.Net.Http to declare client.  
            HttpClient client = new HttpClient();  
  
            // GetStringAsync returns a Task<string>. That means that when you await the  
            // task you'll get a string (urlContents).  
            Task<string> getStringTask = client.GetStringAsync("http://msdn.microsoft.com");  
  
            // You can do work here that doesn't rely on the string from GetStringAsync.  
            DoIndependentWork();  
  
            // The await operator suspends AccessTheWebAsync.  
            //  - AccessTheWebAsync can't continue until getStringTask is complete.  
            //  - Meanwhile, control returns to the caller of AccessTheWebAsync.  
            //  - Control resumes here when getStringTask is complete.   
            //  - The await operator then retrieves the string result from getStringTask.  
            string urlContents = await getStringTask;  
  
            // The return statement specifies an integer result.  
            // Any methods that are awaiting AccessTheWebAsync retrieve the length value.  
            return urlContents.Length;  
        }  
  
        void DoIndependentWork()  
        {  
            resultsTextBox.Text += "Working . . . . . . .\r\n";  
        }  
    }  
}  
  
// Sample Output:  
  
// Working . . . . . . .  
  
// Length of the downloaded string: 41564.  
```  
  
## <a name="see-also"></a>Vedere anche  
 [async](../../../../csharp/language-reference/keywords/async.md)   
 [await](../../../../csharp/language-reference/keywords/await.md)
