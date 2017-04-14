---
title: "Lazy Initialization | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "lazy initialization in .NET, introduction"
ms.assetid: 56b4ae5c-4745-44ff-ad78-ffe4fcde6b9b
caps.latest.revision: 22
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# Lazy Initialization
*Inizializzazione differita* di un oggetto significa che la creazione dell'oggetto viene posticipata al primo utilizzo dello stesso. In questo argomento, i termini *inizializzazione differita* e *creazione di istanze differita* sono sinonimi. L'inizializzazione differita viene utilizzata principalmente per migliorare le prestazioni, evitare calcoli inutili e ridurre i requisiti di memoria del programma.  Di seguito sono riportati gli scenari più comuni:  
  
-   Quando si ha un oggetto dispendioso da creare, che il programma potrebbe non utilizzare.  Si supponga ad esempio di avere in memoria un oggetto `Customer` con una proprietà `Orders` contenente una grande matrice di oggetti `Order` che, per essere inizializzato, richiede una connessione di database.  Se l'utente non chiede mai di visualizzare gli ordini o di utilizzare i dati in un calcolo, non vi è alcun motivo di utilizzare la memoria di sistema o i cicli di calcolo per crearlo.  Utilizzando `Lazy<Orders>` per dichiarare l'oggetto `Orders` per l'inizializzazione differita, si può evitare di sprecare risorse di sistema quando l'oggetto non viene utilizzato.  
  
-   Quando si ha un oggetto dispendioso da creare e si desidera posticiparne la creazione fino a che altre operazioni dispendiose non sono state completate.  Si supponga ad esempio che il programma carichi diverse istanze dell'oggetto al suo avvio, ma che solo alcune di esse siano necessarie nell'immediato.  È possibile migliorare le prestazioni di avvio del programma posticipando l'inizializzazione degli oggetti non necessari fino a che gli oggetti necessari non sono stati creati.  
  
 Sebbene sia possibile scrivere codice personalizzato per eseguire l'inizializzazione differita, si consiglia comunque di utilizzare <xref:System.Lazy%601>.  <xref:System.Lazy%601> e i tipi correlati supportano inoltre la thread safety e forniscono criteri di propagazione delle eccezioni coerenti.  
  
 Nella tabella seguente vengono elencati i tipi forniti da .NET Framework versione 4 per abilitare l'inizializzazione differita in diversi scenari.  
  
|Type|Descrizione|  
|----------|-----------------|  
|<xref:System.Lazy%601>|Classe wrapper che fornisce la semantica dell'inizializzazione differita per tutte le librerie di classi o i tipi definiti dall'utente.|  
|<xref:System.Threading.ThreadLocal%601>|Simile a <xref:System.Lazy%601>, eccetto per il fatto che fornisce la semantica dell'inizializzazione differita su base locale dei thread.  Ogni thread può accedere al proprio valore univoco.|  
|<xref:System.Threading.LazyInitializer>|Fornisce metodi `static` \(`Shared` in Visual Basic\) avanzati per l'inizializzazione differita di oggetti senza il sovraccarico di una classe.|  
  
## Inizializzazione differita di base  
 Per definire un tipo inizializzato in modalità differita, ad esempio `MyType`, utilizzare `Lazy<MyType>` \(`Lazy(Of MyType)` in Visual Basic\), come illustrato nell'esempio seguente.  Se nessun delegato viene passato nel costruttore <xref:System.Lazy%601>, il tipo di cui è stato eseguito il wrapping viene creato tramite <xref:System.Activator.CreateInstance%2A?displayProperty=fullName> nel momento in cui si accede per la prima volta alla proprietà di valore.  Se il tipo non dispone di un costruttore predefinito, viene generata un'eccezione in fase di esecuzione.  
  
 Nell'esempio seguente, si supponga che `Orders` sia una classe contenente una matrice di oggetti `Order` recuperati da un database.  Un oggetto `Customer` contiene un'istanza di `Orders`, ma a seconda delle azioni dell'utente, i dati dell'oggetto `Orders` potrebbero non essere necessari.  
  
 [!code-csharp[Lazy#1](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#1)]
 [!code-vb[Lazy#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#1)]  
  
 È inoltre possibile passare un delegato nel costruttore <xref:System.Lazy%601> che richiama un overload del costruttore specifico sul tipo di cui è stato eseguito il wrapping in fase di creazione, quindi eseguire qualunque altro passaggio dell'inizializzazione richiesto, come illustrato nell'esempio seguente.  
  
 [!code-csharp[Lazy#2](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#2)]
 [!code-vb[Lazy#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#2)]  
  
 Una volta creato l'oggetto Lazy, non verrà creata alcuna istanza di `Orders` fino a che l'accesso alla proprietà <xref:System.Lazy%601.Value%2A> della variabile Lazy non sarà stato eseguito per la prima volta.  Al primo accesso, il tipo di cui è stato eseguito il wrapping verrà creato, restituito e archiviato per un accesso futuro.  
  
 [!code-csharp[Lazy#3](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#3)]
 [!code-vb[Lazy#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#3)]  
  
 Un oggetto <xref:System.Lazy%601> restituisce sempre lo stesso oggetto o valore con il quale è stato inizializzato.  Pertanto, la proprietà <xref:System.Lazy%601.Value%2A> è di sola lettura.  Se <xref:System.Lazy%601.Value%2A> archivia un tipo di riferimento, non è possibile assegnargli un nuovo oggetto. Tuttavia, è possibile modificare il valore delle proprietà e dei campi pubblici impostabili. Se <xref:System.Lazy%601.Value%2A> archivia un tipo di valore, non è possibile modificarne il valore.  Ciononostante, è possibile creare una nuova variabile richiamando nuovamente il costruttore di variabili tramite nuovi argomenti.  
  
 [!code-csharp[Lazy#4](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#4)]
 [!code-vb[Lazy#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#4)]  
  
 La nuova istanza differita, al pari di quella precedente, non crea alcuna istanza di `Orders` fino a che non viene eseguito il primo accesso alla proprietà <xref:System.Lazy%601.Value%2A>.  
  
### Inizializzazione thread\-safe  
 Per impostazione predefinita, gli oggetti <xref:System.Lazy%601> sono thread\-safe.  Ciò significa che se il costruttore non specifica il tipo di thread safety, gli oggetti <xref:System.Lazy%601> creati sono thread\-safe.  Negli scenari multithreading, il primo thread che accede alla proprietà <xref:System.Lazy%601.Value%2A> di un oggetto <xref:System.Lazy%601> thread\-safe la inizializza per tutti gli accessi successivi in tutti i thread e tutti i thread condividono gli stessi dati.  Non importa quindi quale thread inizializza l'oggetto, e le race condition sono benigne.  
  
> [!NOTE]
>  È possibile estendere questa coerenza alle condizioni di errore utilizzando la memorizzazione delle eccezioni nella cache.  Per ulteriori informazioni, vedere la sezione successiva, [Eccezioni negli oggetti Lazy](../../../docs/framework/performance/lazy-initialization.md#ExceptionsInLazyObjects).  
  
 Nell'esempio seguente viene illustrato come la stessa istanza di `Lazy<int>` abbia lo stesso valore per tre thread distinti.  
  
 [!code-csharp[Lazy#8](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#8)]
 [!code-vb[Lazy#8](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#8)]  
  
 Se sono necessari dati separati in ogni thread, utilizzare il tipo <xref:System.Threading.ThreadLocal%601>, come descritto più avanti in questo argomento.  
  
 Alcuni costruttori <xref:System.Lazy%601> dispongono di un parametro booleano denominato `isThreadSafe`, utilizzato per specificare se l'accesso alla proprietà <xref:System.Lazy%601.Value%2A> sarà eseguito da più thread.  Se si intende accedere alla proprietà da un unico thread, passare `false` per ottenere un modesto vantaggio in termini di prestazioni.  Se si intende accedere alla proprietà da più thread, passare `true` per indicare all'istanza di <xref:System.Lazy%601> di gestire correttamente le race condition in cui un thread genera un'eccezione in fase di inizializzazione.  
  
 Alcuni costruttori <xref:System.Lazy%601> dispongono di un parametro <xref:System.Threading.LazyThreadSafetyMode> denominato `mode`.  Questi costruttori forniscono una modalità di thread safety aggiuntiva.  Nella tabella seguente viene illustrato come la modalità thread safety di un oggetto <xref:System.Lazy%601> venga influenzata dai parametri del costruttore che specificano tale modalità.  Ciascun costruttore dispone al massimo di uno di questi parametri.  
  
|Thread safety dell'oggetto|Parametro `mode` di `LazyThreadSafetyMode`|Parametro `isThreadSafe` booleano|Nessun parametro di thread safety|  
|--------------------------------|------------------------------------------------|---------------------------------------|---------------------------------------|  
|Completamente thread\-safe; solo un thread alla volta tenta di inizializzare il valore.|<xref:System.Threading.LazyThreadSafetyMode>|`true`|Sì.|  
|Non thread\-safe.|<xref:System.Threading.LazyThreadSafetyMode>|`false`|Non applicabile.|  
|Completamente thread\-safe; i thread concorrono per inizializzare il valore.|<xref:System.Threading.LazyThreadSafetyMode>|Non applicabile.|Non applicabile.|  
  
 Come illustrato nella tabella, la specifica di <xref:System.Threading.LazyThreadSafetyMode?displayProperty=fullName> per il parametro `mode` corrisponde alla specifica di `true` per il parametro `isThreadSafe` e la specifica di <xref:System.Threading.LazyThreadSafetyMode?displayProperty=fullName> corrisponde alla specifica di `false`.  
  
 La specifica di <xref:System.Threading.LazyThreadSafetyMode?displayProperty=fullName> consente a più thread di tentare l'inizializzazione dell'istanza di <xref:System.Lazy%601>.  Solo un thread può raggiungere lo scopo e tutti gli altri ricevono il valore inizializzato da tale thread.  Se viene generata un'eccezione in un thread durante l'inizializzazione, quel thread non riceve il valore impostato dal thread di inizializzazione.  Le eccezioni non vengono memorizzate nella cache, pertanto un tentativo di accesso successivo alla proprietà <xref:System.Lazy%601.Value%2A> può comportare l'esito positivo dell'inizializzazione.  Questo non corrisponde al modo in cui le eccezioni vengono gestite in altre modalità, come descritto nella sezione seguente.  Per ulteriori informazioni, vedere l'enumerazione <xref:System.Threading.LazyThreadSafetyMode>.  
  
<a name="ExceptionsInLazyObjects"></a>   
## Eccezioni negli oggetti Lazy  
 Come detto in precedenza, un oggetto <xref:System.Lazy%601> restituisce sempre lo stesso oggetto o valore con il quale è stato inizializzato, pertanto la proprietà <xref:System.Lazy%601.Value%2A> è di sola lettura.  Se si abilita la memorizzazione delle eccezioni nella cache, questa immutabilità si estende anche al comportamento delle eccezioni.  Se per un oggetto inizializzato in modalità differita è abilitata la memorizzazione delle eccezioni nella cache e l'oggetto genera un'eccezione dal relativo metodo di inizializzazione quando viene eseguito per la prima volta l'accesso alla proprietà <xref:System.Lazy%601.Value%2A>, la stessa eccezione viene generata a ogni tentativo successivo di accedere alla proprietà <xref:System.Lazy%601.Value%2A>.  In altre parole, il costruttore del tipo di cui è stato eseguito il wrapping non viene mai richiamato, neppure negli scenari multithreading.  L'oggetto <xref:System.Lazy%601> non può pertanto generare un'eccezione per un accesso e restituire un valore per un accesso successivo.  
  
 La memorizzazione delle eccezioni nella cache è abilitata quando si utilizza un costruttore <xref:System.Lazy%601?displayProperty=fullName> che accetta un metodo di inizializzazione \(parametro `valueFactory`\). È ad esempio abilitata quando si utilizza il costruttore `Lazy(T)(Func(T))`.  Se il costruttore accetta inoltre un valore <xref:System.Threading.LazyThreadSafetyMode> \(parametro `mode`\), specificare <xref:System.Threading.LazyThreadSafetyMode?displayProperty=fullName> o <xref:System.Threading.LazyThreadSafetyMode?displayProperty=fullName>.  Specificando un metodo di inizializzazione, viene abilitata la memorizzazione delle eccezioni nella cache per queste due modalità.  Il metodo di inizializzazione può essere molto semplice.  Può ad esempio chiamare il costruttore predefinito per `T`: `new Lazy<Contents>(() => new Contents(), mode)` in C\# o `New Lazy(Of Contents)(Function() New Contents())` in Visual Basic.  Se si utilizza un costruttore <xref:System.Lazy%601?displayProperty=fullName> che non specifica un metodo di inizializzazione, le eccezioni generate dal costruttore predefinito per `T` non vengono memorizzate nella cache.  Per ulteriori informazioni, vedere l'enumerazione <xref:System.Threading.LazyThreadSafetyMode>.  
  
> [!NOTE]
>  Se si crea un oggetto <xref:System.Lazy%601> con il parametro del costruttore `isThreadSafe` impostato su `false` o il parametro del costruttore `mode` impostato su <xref:System.Threading.LazyThreadSafetyMode?displayProperty=fullName>, è necessario accedere all'oggetto <xref:System.Lazy%601> da un singolo thread o fornire la sincronizzazione.  Questa procedura si applica a tutti gli aspetti dell'oggetto, inclusa la memorizzazione delle eccezioni nella cache.  
  
 Come indicato nella sezione precedente, gli oggetti <xref:System.Lazy%601> creati specificando <xref:System.Threading.LazyThreadSafetyMode?displayProperty=fullName> gestiscono le eccezioni in modo diverso.  Con <xref:System.Threading.LazyThreadSafetyMode>, più thread possono competere per inizializzare l'istanza di <xref:System.Lazy%601>.  In questo caso, le eccezioni non vengono memorizzate nella cache e i tentativi di accesso successivo alla proprietà <xref:System.Lazy%601.Value%2A> possono continuare finché l'inizializzazione non ha esito positivo.  
  
 Nella tabella seguente vengono riepilogati i modi in cui i costruttori <xref:System.Lazy%601> controllano la memorizzazione delle eccezioni nella cache.  
  
|Costruttore|Modalità di thread safety|Utilizza il metodo di inizializzazione|Le eccezioni vengono memorizzate nella cache|  
|-----------------|-------------------------------|--------------------------------------------|--------------------------------------------------|  
|Lazy\(T\)\(\)|\(<xref:> System.Threading.LazyThreadSafetyMode.ExecutionAndPublication?qualifyHint=False&autoUpgrade=True\)|No|No|  
|Lazy\(T\)\(Func\(T\)\)|\(<xref:> System.Threading.LazyThreadSafetyMode.ExecutionAndPublication?qualifyHint=False&autoUpgrade=True\)|Yes|Yes|  
|Lazy\(T\)\(Boolean\)|`True` \(<xref:> System.Threading.LazyThreadSafetyMode.ExecutionAndPublication?qualifyHint=False&autoUpgrade=True\) o `false` \(<xref:> System.Threading.LazyThreadSafetyMode.None?qualifyHint=False&autoUpgrade=True\)|No|No|  
|Lazy\(T\)\(Func\(T\), Boolean\)|`True` \(<xref:> System.Threading.LazyThreadSafetyMode.ExecutionAndPublication?qualifyHint=False&autoUpgrade=True\) o `false` \(<xref:> System.Threading.LazyThreadSafetyMode.None?qualifyHint=False&autoUpgrade=True\)|Yes|Yes|  
|Lazy\(T\)\(LazyThreadSafetyMode\)|Specificata dall'utente|No|No|  
|Lazy\(T\)\(Func\(T\), LazyThreadSafetyMode\)|Specificata dall'utente|Yes|No se l'utente specifica <xref:> System.Threading.LazyThreadSafetyMode.PublicationOnly?qualifyHint=False&autoUpgrade=True; in caso contrario, sì.|  
  
## Implementazione di una proprietà inizializzata in modalità differita  
 Per implementare una proprietà pubblica tramite inizializzazione differita, definire il campo sottostante della proprietà come <xref:System.Lazy%601> e restituire la proprietà <xref:System.Lazy%601.Value%2A> dalla funzione di accesso `get` della proprietà.  
  
 [!code-csharp[Lazy#5](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#5)]
 [!code-vb[Lazy#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#5)]  
  
 La proprietà <xref:System.Lazy%601.Value%2A> è di sola lettura; di conseguenza, la proprietà che la espone non possiede alcuna funzione di accesso `set`.  Se è necessaria una proprietà di lettura\/scrittura supportata da un oggetto <xref:System.Lazy%601>, la funzione di accesso `set` deve creare un nuovo oggetto <xref:System.Lazy%601> e assegnarlo all'archivio di backup.  La funzione di accesso `set` deve creare un'espressione lambda che restituisce il nuovo valore della proprietà passato alla funzione di accesso `set` e passare tale espressione al costruttore per il nuovo oggetto <xref:System.Lazy%601>.  Il successivo accesso alla proprietà <xref:System.Lazy%601.Value%2A> causerà l'inizializzazione del nuovo oggetto <xref:System.Lazy%601> e la relativa proprietà <xref:System.Lazy%601.Value%2A> restituirà il nuovo valore assegnato alla proprietà.  Lo scopo di questa soluzione complessa è mantenere le protezioni di multithreading predefinite in <xref:System.Lazy%601>.  In caso contrario, le funzioni di accesso della proprietà dovrebbero memorizzare nella cache il primo valore restituito dalla proprietà <xref:System.Lazy%601.Value%2A> e modificare solo il valore memorizzato nella cache e sarebbe inoltre necessario scrivere codice thread\-safe personalizzato.  Date le inizializzazioni aggiuntive richieste da una proprietà di lettura\/scrittura supportata da un oggetto <xref:System.Lazy%601>, le prestazioni potrebbero non essere accettabili.  Inoltre, a seconda dello scenario specifico, potrebbe essere necessario un coordinamento aggiuntivo per evitare race condition tra proprietà SET e GET.  
  
## Inizializzazione differita locale dei thread  
 In alcuni scenari multithreading, potrebbe essere necessario dare a ogni thread i propri dati privati.  Tali dati sono definiti *dati locali dei thread*.  In .NET Framework versione 3.5 e precedenti, è possibile applicare l'attributo `ThreadStatic` a una variabile statica per renderla locale a livello di thread.  Tuttavia, l'utilizzo dell'attributo `ThreadStatic` può causare errori non immediatamente evidenti.  Ad esempio, anche le istruzioni di inizializzazione di base causeranno l'inizializzazione della variabile solo nel primo thread che vi accede, come illustrato nell'esempio seguente.  
  
 [!code-csharp[Lazy#6](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#6)]
 [!code-vb[Lazy#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#6)]  
  
 In tutti gli altri thread, la variabile verrà inizializzata tramite il valore predefinito \(zero\).  In alternativa, in .NET Framework versione 4, è possibile utilizzare il tipo <xref:System.Threading.ThreadLocal%601?displayProperty=fullName> per creare una variabile locale dei thread basata su istanze che venga inizializzata in tutti i thread dal delegato <xref:System.Action%601> specificato.  Nell'esempio seguente, tutti i thread che accedono a `counter` vedranno il valore iniziale 1.  
  
 [!code-csharp[Lazy#7](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#7)]
 [!code-vb[Lazy#7](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#7)]  
  
 <xref:System.Threading.ThreadLocal%601> esegue il wrapping del proprio oggetto in modo molto simile a <xref:System.Lazy%601>, con queste differenze sostanziali:  
  
-   Ogni thread inizializza la variabile locale dei thread tramite i propri dati privati, che non sono accessibili dagli altri thread.  
  
-   La proprietà <xref:System.Threading.ThreadLocal%601.Value%2A?displayProperty=fullName> è di lettura\/scrittura e può essere modificata un numero illimitato di volte.  Ciò può influire sulla propagazione delle eccezioni; ad esempio, l'operazione `get` può generare un'eccezione mentre l'operazione successiva può correttamente inizializzare il valore.  
  
-   Se non viene fornito alcun delegato di inizializzazione, <xref:System.Threading.ThreadLocal%601> inizializzerà il tipo di cui è stato eseguito il wrapping tramite il valore predefinito del tipo.  A questo proposito, <xref:System.Threading.ThreadLocal%601> è coerente con l'attributo <xref:System.ThreadStaticAttribute>.  
  
 Nell'esempio seguente viene illustrato come ogni thread che accede all'istanza di `ThreadLocal<int>` ottenga la propria copia univoca dei dati.  
  
 [!code-csharp[Lazy#9](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#9)]
 [!code-vb[Lazy#9](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#9)]  
  
## Variabili locali dei thread in Parallel.For e ForEach  
 Quando si utilizza il metodo <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> o <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> per scorrere le origini dati in parallelo, è possibile utilizzare gli overload che dispongono di supporto incorporato per i dati locali dei thread.  In questi metodi, la località dei thread si ottiene utilizzando delegati locali per creare, accedere e pulire i dati.  Per ulteriori informazioni, vedere [How to: Write a Parallel.For Loop with Thread\-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-for-loop-with-thread-local-variables.md) e [How to: Write a Parallel.ForEach Loop with Thread\-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-foreach-loop-with-thread-local-variables.md).  
  
## Utilizzo dell'inizializzazione differita per scenari con sovraccarico ridotto  
 Negli scenari in cui è necessario inizializzare in modalità differita un gran numero di oggetti, si può stabilire che l'esecuzione del wrapping di ogni oggetto in <xref:System.Lazy%601> richieda troppa memoria o troppe risorse di elaborazione.  Oppure, è possibile che siano previsti requisiti severi circa l'esposizione dell'inizializzazione differita.  In tali casi, è possibile utilizzare i metodi `static` \(`Shared` in Visual Basic\) della classe <xref:System.Threading.LazyInitializer?displayProperty=fullName> per inizializzare in modalità differita ogni oggetto senza eseguirne il wrapping in un'istanza di <xref:System.Lazy%601>.  
  
 Nell'esempio seguente, si supponga che, anziché eseguire il wrapping di un intero oggetto `Orders` in un unico oggetto <xref:System.Lazy%601>, si abbiano singoli oggetti `Order` inizializzati in modalità differita solo se necessari.  
  
 [!code-csharp[Lazy#10](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#10)]
 [!code-vb[Lazy#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#10)]  
  
 In questo esempio, la procedura di inizializzazione viene richiamata su ogni iterazione del ciclo.  Negli scenari multithreading, il primo thread a richiamare la procedura di inizializzazione è quello il cui valore viene visto da tutti i thread.  Anche gli altri thread richiamano la procedura di inizializzazione, ma i loro risultati non vengono utilizzati.  Se questo tipo di race condition potenziale non è accettabile, utilizzare l'overload di <xref:System.Threading.LazyInitializer.EnsureInitialized%2A?displayProperty=fullName> che accetta un argomento booleano e un oggetto di sincronizzazione.  
  
## Vedere anche  
 [Managed Threading Basics](../../../docs/standard/threading/managed-threading-basics.md)   
 [Threads and Threading](../../../docs/standard/threading/threads-and-threading.md)   
 [Task Parallel Library \(TPL\)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)   
 [How to: Perform Lazy Initialization of Objects](../../../docs/framework/performance/how-to-perform-lazy-initialization-of-objects.md)