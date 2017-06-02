---
title: "Modello di progettazione observer | Microsoft Docs"
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
  - "IObservable(Of T) (interfaccia) [F#]"
  - "IObservable<T> (interfaccia)"
  - "IObservable(Of T) (interfaccia)"
  - "IObservable<T> (interfaccia)"
  - "observer (modello di progettazione) [.NET Framework]"
ms.assetid: 3680171f-f522-453c-aa4a-54f755a78f88
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Modello di progettazione observer
Lo schema progettuale osservatore consente a un sottoscrittore di effettuare la registrazione con e ricevere notifiche da un provider.  È appropriato per qualsiasi scenario che richieda la notifica basata su push.  Lo schema definisce un *provider*, anche noto come *oggetto* o *osservabile* e zero, uno o più *osservatori*.  Gli osservatori effettuano la registrazione con il provider e ogni volta che si verifica una condizione, un evento o un cambiamento di stato predefinito, il provider invia automaticamente una notifica a tutti gli osservatori chiamando uno dei relativi metodi.  In questa chiamata al metodo, il provider può anche fornire informazioni sullo stato corrente degli osservatori.  In .NET Framework, lo schema progettuale osservatore viene applicato implementando le interfacce generiche <xref:System.IObservable%601?displayProperty=fullName> e <xref:System.IObserver%601?displayProperty=fullName>.  Il parametro di tipo generico rappresenta il tipo che fornisce le informazioni di notifica.  
  
## Applicazione dello schema  
 Lo schema progettuale osservatore è appropriato per le notifiche distribuite basate su push, poiché supporta una netta separazione tra due diversi componenti o livelli dell'applicazione, ad esempio un livello di origine dati \(logica di business\) e un livello di interfaccia utente \(visualizzazione\).  Lo schema può essere implementato ogni volta che un provider usa callback per fornire ai client informazioni aggiornate.  
  
 Per implementare lo schema è necessario fornire gli elementi seguenti:  
  
-   Un provider o oggetto, che corrisponde all'oggetto che invia le notifiche agli osservatori.  Un provider è una classe o una struttura che implementa l'interfaccia <xref:System.IObservable%601>.  Il provider deve implementare un singolo metodo, <xref:System.IObservable%601.Subscribe%2A?displayProperty=fullName>, che viene chiamato dagli osservatori che desiderano ricevere notifiche dal provider.  
  
-   Un osservatore, che è un oggetto che riceve le notifiche da un provider.  Un osservatore è una classe o una struttura che implementa l'interfaccia <xref:System.IObserver%601>.  L'osservatore deve implementare tre metodi, che vengono tutti chiamati dal provider:  
  
    -   <xref:System.IObserver%601.OnNext%2A?displayProperty=fullName>, che fornisce all'osservatore informazioni nuove o correnti.  
  
    -   <xref:System.IObserver%601.OnError%2A?displayProperty=fullName>, che informa l'osservatore che si è verificato un errore.  
  
    -   <xref:System.IObserver%601.OnCompleted%2A?displayProperty=fullName>, che indica che il provider ha completato l'invio di notifiche.  
  
-   Un meccanismo che consenta al provider di tenere traccia degli osservatori.  In genere, il provider usa un oggetto contenitore, ad esempio un oggetto <xref:System.Collections.Generic.List%601?displayProperty=fullName>, per contenere i riferimenti alle implementazioni di <xref:System.IObserver%601> che hanno sottoscritto le notifiche.  Usando un contenitore di archiviazione a questo scopo, si consente al provider di gestire da zero a un numero illimitato di osservatori.  L'ordine in cui gli osservatori ricevono le notifiche non è definito. Il provider può usare qualsiasi metodo per determinare l'ordine.  
  
-   Un'implementazione di <xref:System.IDisposable> che consenta al provider di rimuovere gli osservatori quando la notifica è completa.  Gli osservatori ricevono un riferimento all'implementazione di <xref:System.IDisposable> dal metodo <xref:System.IObservable%601.Subscribe%2A>, pertanto possono anche chiamare il metodo <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> per annullare la sottoscrizione prima che il provider abbia completato l'invio di notifiche.  
  
-   Un oggetto contenente i dati che il provider invia agli osservatori.  Il tipo di questo oggetto corrisponde al parametro di tipo generico delle interfacce <xref:System.IObservable%601> e <xref:System.IObserver%601>.  Sebbene questo oggetto possa essere lo stesso dell'implementazione di <xref:System.IObservable%601>, in genere è un tipo distinto.  
  
> [!NOTE]
>  Oltre all'implementazione dello schema progettuale osservatore, potrebbe risultare interessante l'esplorazione delle librerie compilate usando le interfacce <xref:System.IObservable%601> e <xref:System.IObserver%601>.  Le [estensioni Rx \(Reactive Extensions\) per .NET](http://go.microsoft.com/fwlink/?LinkId=186345) rappresentano ad esempio un set di metodi di estensione e operatori di sequenza standard LINQ che supportano la programmazione asincrona.  
  
## Implementazione dello schema  
 Nell'esempio seguente, lo schema progettuale osservatore viene usato per implementare un sistema di informazioni per il ritiro dei bagagli in aeroporto.  Una classe `BaggageInfo` fornisce informazioni sui voli in arrivo e sui nastri in cui possono essere ritirati i bagagli per ogni volo,  come illustrato nell'esempio seguente.  
  
 [!code-csharp[Conceptual.ObserverDesignPattern#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesignpattern/cs/provider.cs#1)]
 [!code-vb[Conceptual.ObserverDesignPattern#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesignpattern/vb/provider.vb#1)]  
  
 Una classe `BaggageHandler` è responsabile della ricezione di informazioni sui voli in arrivo e sui nastri per il ritiro dei bagagli.  Internamente, gestisce due raccolte:  
  
-   `observers`: una raccolta di client che riceveranno informazioni aggiornate.  
  
-   `flights`: una raccolta di voli e dei nastri ad essi assegnati.  
  
 Entrambe le raccolte sono rappresentate da oggetti <xref:System.Collections.Generic.List%601> generici di cui viene creata un'istanza nel costruttore della classe `BaggageHandler`.  Il codice sorgente per la classe `BaggageHandler` è illustrato nell'esempio seguente.  
  
 [!code-csharp[Conceptual.ObserverDesignPattern#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesignpattern/cs/provider.cs#2)]
 [!code-vb[Conceptual.ObserverDesignPattern#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesignpattern/vb/provider.vb#2)]  
  
 I client che desiderano ricevere informazioni aggiornate chiamano il metodo `BaggageHandler.Subscribe`.  Se il client in precedenza non ha sottoscritto le notifiche, un riferimento all'implementazione di <xref:System.IObserver%601> del client viene aggiunto alla raccolta `observers`.  
  
 Il metodo di overload `BaggageHandler.BaggageStatus` può essere chiamato per indicare che i bagagli di un volo stanno per essere scaricati o che lo scaricamento è terminato.  Nel primo caso, al metodo vengono passati un numero di volo, l'aeroporto di provenienza e il nastro in cui vengono scaricati i bagagli.  Nel secondo caso, al metodo viene passato solo un numero di volo.  Per i bagagli scaricati, il metodo verifica se le informazioni di `BaggageInfo` passate al metodo sono presenti nella raccolta `flights`.  Se non lo sono, il metodo aggiunge le informazioni e chiama il metodo `OnNext` di ogni osservatore.  Per i voli per cui è terminato lo scaricamento dei bagagli, il metodo controlla se le informazioni su tale volo sono archiviate nella raccolta `flights`.  In caso affermativo, il metodo chiama il metodo `OnNext` di ogni osservatore e rimuove l'oggetto `BaggageInfo` dalla raccolta `flights`.  
  
 Quando l'ultimo volo del giorno è atterrato e i relativi bagagli sono stati gestiti, viene chiamato il metodo `BaggageHandler.LastBaggageClaimed`.  Questo metodo chiama il metodo `OnCompleted` di ogni osservatore per indicare che tutte le notifiche sono state completate, quindi cancella la raccolta `observers`.  
  
 Il metodo <xref:System.IObservable%601.Subscribe%2A> del provider restituisce un'implementazione di <xref:System.IDisposable> che consente agli osservatori di interrompere la ricezione delle notifiche prima che venga chiamato il metodo <xref:System.IObserver%601.OnCompleted%2A>.  Il codice sorgente per la classe `Unsubscriber(Of BaggageInfo)` è illustrato nell'esempio seguente.  Quando viene creata un'istanza della classe nel metodo `BaggageHandler.Subscribe`, vengono passati un riferimento alla raccolta `observers` e un riferimento all'osservatore che viene aggiunto alla raccolta.  Questi riferimenti sono assegnati a variabili locali.  Quando il metodo `Dispose` dell'oggetto viene chiamato, controlla se l'osservatore è ancora presente nella raccolta `observers` e, in caso affermativo, lo rimuove.  
  
 [!code-csharp[Conceptual.ObserverDesignPattern#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesignpattern/cs/provider.cs#3)]
 [!code-vb[Conceptual.ObserverDesignPattern#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesignpattern/vb/provider.vb#3)]  
  
 Nell'esempio seguente viene fornita un'implementazione di <xref:System.IObserver%601> denominata `ArrivalsMonitor`, una classe base che fornisce informazioni relative al ritiro dei bagagli.  Le informazioni vengono visualizzate in ordine alfabetico, in base al nome della città di provenienza.  I metodi `ArrivalsMonitor` sono contrassegnati come `overridable` \(in Visual Basic\) o `virtual` \(in C\#\), in modo che possano essere sottoposti a override da una classe derivata.  
  
 [!code-csharp[Conceptual.ObserverDesignPattern#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesignpattern/cs/observer.cs#4)]
 [!code-vb[Conceptual.ObserverDesignPattern#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesignpattern/vb/observer.vb#4)]  
  
 La classe `ArrivalsMonitor` include i metodi `Subscribe` e `Unsubscribe`.  Il metodo `Subscribe` consente alla classe di salvare l'implementazione di <xref:System.IDisposable> restituita dalla chiamata a <xref:System.IObservable%601.Subscribe%2A> in una variabile privata.  Il metodo `Unsubscribe` consente alla classe di annullare la sottoscrizione delle notifiche chiamando l'implementazione di <xref:System.IDisposable.Dispose%2A> del provider.  `ArrivalsMonitor` fornisce anche le implementazioni dei metodi <xref:System.IObserver%601.OnNext%2A>, <xref:System.IObserver%601.OnError%2A> e <xref:System.IObserver%601.OnCompleted%2A>.  Solo l'implementazione di <xref:System.IObserver%601.OnNext%2A> contiene una quantità significativa di codice.  Il metodo opera con un oggetto <xref:System.Collections.Generic.List%601> privato, ordinato e generico che gestisce le informazioni sugli aeroporti di origine per i voli in arrivo e sui nastri su cui sono disponibili i bagagli.  Se la classe `BaggageHandler` segnala un nuovo volo in arrivo, l'implementazione del metodo <xref:System.IObserver%601.OnNext%2A> aggiunge le informazioni relative al volo all'elenco.  Se la classe `BaggageHandler` segnala che i bagagli del volo sono stati scaricati, il metodo <xref:System.IObserver%601.OnNext%2A> rimuove il volo dall'elenco.  Ogni volta che viene apportata una modifica, l'elenco viene ordinato e visualizzato nella console.  
  
 L'esempio seguente contiene il punto di ingresso dell'applicazione che crea un'istanza della classe `BaggageHandler`, nonché due istanze della classe `ArrivalsMonitor` e usa il metodo `BaggageHandler.BaggageStatus` per aggiungere e rimuovere informazioni sui voli in arrivo.  In ognuno dei casi, gli osservatori ricevono gli aggiornamenti e visualizzano correttamente le informazioni relative al ritiro dei bagagli.  
  
 [!code-csharp[Conceptual.ObserverDesignPattern#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesignpattern/cs/program.cs#5)]
 [!code-vb[Conceptual.ObserverDesignPattern#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesignpattern/vb/module1.vb#5)]  
  
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Procedure consigliate per un modello di progettazione observer](../../../docs/standard/events/observer-design-pattern-best-practices.md)|Descrive le procedure consigliate per lo sviluppo di applicazioni che implementano lo schema progettuale observer.|  
|[Procedura: Implementare un provider](../../../docs/standard/events/how-to-implement-a-provider.md)|Fornisce un'implementazione dettagliata di un provider per un'applicazione di monitoraggio della temperatura.|  
|[Procedura: Implementare un elemento Observer](../../../docs/standard/events/how-to-implement-an-observer.md)|Fornisce un'implementazione dettagliata di un osservatore per un'applicazione di monitoraggio della temperatura.|