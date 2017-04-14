---
title: "Custom Partitioners for PLINQ and TPL | Microsoft Docs"
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
  - "tasks, partitioners"
ms.assetid: 96153688-9a01-47c4-8430-909cee9a2887
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Custom Partitioners for PLINQ and TPL
Uno dei passaggi basilari per la parallelizzazione di un'operazione su un'origine dati consiste nel *suddividere* l'origine in più sezioni, cui è possibile accedere contemporaneamente da più thread.  PLINQ e TPL \(Task Parallel Library\) forniscono partitioner predefiniti che funzionano in maniera trasparente quando si scrive una query parallela o un ciclo <xref:System.Threading.Tasks.Parallel.ForEach%2A>.  Per gli scenari più avanzati, è possibile collegare il proprio partitioner.  
  
## Tipi di partizionamento  
 Esistono molti modi per suddividere in partizioni un'origine dati.  Quelli più efficaci prevedono la cooperazione di più thread nell'elaborazione della sequenza di origine originale senza separazione fisica dell'origine in più sottosequenze.  Per le matrici e le altre origini indicizzate, quali raccolte <xref:System.Collections.IList> in cui la lunghezza è nota in anticipo, il tipo più semplice di partizionamento è il *partizionamento per intervalli*.  Ogni thread riceve indici iniziali e finali univoci, in modo che possa elaborare l'intervallo dell'origine senza sovrascrivere un altro thread o essere sovrascritto.  L'unico sovraccarico coinvolto nel partizionamento per intervalli è il lavoro iniziale di creazione degli intervalli. Non è richiesta alcuna sincronizzazione aggiuntiva successiva.  Questo tipo di partizionamento può pertanto garantire buone prestazioni, a condizione che il carico di lavoro sia suddiviso in modo uniforme.  Uno svantaggio del partizionamento per intervalli è che un thread che completa il proprio lavoro prima degli altri non può contribuire al completamento del lavoro degli altri thread.  
  
 Per gli elenchi collegati o altre raccolte la cui lunghezza non è nota, è possibile utilizzare il *partizionamento a blocchi*.  Nel partizionamento a blocchi ogni thread o attività in una query o un ciclo parallelo utilizza un determinato numero di elementi di origine in un unico blocco, li elabora, quindi torna a recuperare altri elementi.  Il partitioner si assicura che tutti gli elementi vengano distribuiti e che non ci siano duplicati.  Un blocco può avere qualsiasi dimensione.  Il partitioner illustrato in [How to: Implement Dynamic Partitions](../../../docs/standard/parallel-programming/how-to-implement-dynamic-partitions.md), ad esempio, determina la creazione di blocchi che contengono un solo elemento.  Fintantoché i blocchi non sono troppo grandi, in questo tipo di partizionamento è implicita la funzionalità di bilanciamento del carico, in quanto l'assegnazione di elementi ai thread non è predeterminata.  Il partitioner deve tuttavia affrontare il sovraccarico della sincronizzazione ogni volta che il thread ottiene un altro blocco da elaborare.  La quantità di lavoro richiesta per la sincronizzazione in questi casi è inversamente proporzionale alla dimensione dei blocchi.  
  
 In generale, il partizionamento per intervalli è più veloce solo quando il tempo di esecuzione del delegato è da ridotto a moderato, nell'origine è presente un numero elevato di elementi e il lavoro totale di ogni partizione è pressoché equivalente.  Il partizionamento a blocchi è pertanto generalmente più veloce nella maggior parte dei casi.  Nelle origini con un numero ridotto di elementi o con tempi di esecuzione più lunghi per il delegato, le prestazioni del partizionamento a blocchi e quelle del partizionamento per intervalli sono quasi equivalenti.  
  
 I partitioner TPL supportano inoltre un numero dinamico di partizioni.  Ciò significa che possono creare partizioni in qualsiasi momento, ad esempio, quando il ciclo <xref:System.Threading.Tasks.Parallel.ForEach%2A> genera una nuova attività.  Questa funzionalità consente il ridimensionamento del partitioner insieme al ciclo stesso.  Anche nei partitioner dinamici è implicita la funzionalità del bilanciamento del carico.  Quando si crea un partitioner personalizzato, è necessario che l'utilizzo del partizionamento dinamico sia supportato in un ciclo <xref:System.Threading.Tasks.Parallel.ForEach%2A>.  
  
### Configurazione di partitioner con bilanciamento del carico per PLINQ  
 Alcuni overload del metodo <xref:System.Collections.Concurrent.Partitioner.Create%2A?displayProperty=fullName> consentono di creare un partitioner per una matrice o un'origine <xref:System.Collections.IList>, nonché di specificare se deve essere effettuato il tentativo di bilanciare il carico di lavoro tra i thread.  Quando il partitioner viene configurato per il bilanciamento del carico, viene utilizzato il partizionamento a blocchi e gli elementi vengono passati a ogni partizione in piccoli blocchi man mano che vengono richiesti.  Questo approccio consente di assicurarsi che in tutte le partizioni siano presenti elementi da elaborare fino a che non è stato completato l'intero ciclo o l'intera query.  È possibile utilizzare un overload aggiuntivo per rendere possibile il partizionamento del bilanciamento del carico di qualsiasi origine <xref:System.Collections.IEnumerable>.  
  
 In generale, per la corretta esecuzione del bilanciamento del carico è necessario che le partizioni richiedano elementi al partitioner con una certa frequenza.  Al contrario, un partitioner che esegue il partizionamento statico può assegnare contemporaneamente gli elementi a ogni partitioner mediante il partizionamento per intervalli o a blocchi.  Ciò comporta un sovraccarico minore rispetto al bilanciamento del carico, ma potrebbe richiedere più tempo per l'esecuzione se un thread viene completato con un volume di lavoro significativamente superiore rispetto agli altri.  Per impostazione predefinita, quando viene passato un IList o una matrice, PLINQ utilizza sempre il partizionamento per intervalli senza bilanciamento del carico.  Per abilitare il bilanciamento del carico per PLINQ, utilizzare il metodo `Partitioner.Create`, come mostrato nell'esempio seguente.  
  
 [!code-csharp[TPL_Partitioners#02](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioners.cs#02)]
 [!code-vb[TPL_Partitioners#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_partitioners/vb/partitionsnippets_vb.vb#02)]  
  
 Il modo migliore per stabilire se è opportuno utilizzare il bilanciamento del carico in qualsiasi scenario specificato consiste nello sperimentare e misurare il tempo necessario per il completamento delle operazioni con carichi e configurazioni di computer rappresentativi.  Il partizionamento statico potrebbe ad esempio garantire un aumento di velocità significativo in un computer con processore multi\-core che presenta un numero limitato di core, ma potrebbe comportare rallentamenti in computer che presentano un numero di core relativamente elevato.  
  
 Nella tabella riportata di seguito sono elencati i sovraccarichi disponibili del metodo <xref:System.Collections.Concurrent.Partitioner.Create%2A>.  L'utilizzo di tali partitioner non è limitato a PLINQ o <xref:System.Threading.Tasks.Task>.  Possono infatti essere utilizzati anche con qualsiasi costrutto parallelo personalizzato.  
  
|Overload|Utilizza il bilanciamento del carico|  
|--------------|------------------------------------------|  
|<xref:System.Collections.Concurrent.Partitioner.Create%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29>|Sempre|  
|[Create\<TSource\>\(TSource\<xref:System.Collections.Concurrent.Partitioner.Create%60%601%28%60%600%5B%5D%2CSystem.Boolean%29>|Quando l'argomento booleano viene specificato come true|  
|<xref:System.Collections.Concurrent.Partitioner.Create%60%601%28System.Collections.Generic.IList%7B%60%600%7D%2CSystem.Boolean%29>|Quando l'argomento booleano viene specificato come true|  
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int32%2CSystem.Int32%29>|Mai|  
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int32%2CSystem.Int32%2CSystem.Int32%29>|Mai|  
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int64%2CSystem.Int64%29>|Mai|  
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int64%2CSystem.Int64%2CSystem.Int64%29>|Mai|  
  
### Configurazione di partitioner a intervalli statici per Parallel.ForEach  
 In un ciclo <xref:System.Threading.Tasks.Parallel.For%2A> il corpo del ciclo viene fornito al metodo come delegato.  Il costo della chiamata al delegato è quasi equivalente a quello di una chiamata al metodo virtuale.  In alcuni scenari il corpo di un ciclo parallelo può arrivare a essere sufficientemente ridotto da rendere significativo quello della chiamata al delegato su ogni iterazione del ciclo.  In situazioni di questo tipo è possibile utilizzare uno degli overload <xref:System.Collections.Concurrent.Partitioner.Create%2A> per creare un <xref:System.Collections.Generic.IEnumerable%601> di partizioni a intervalli sugli elementi di origine.  È quindi possibile passare questa raccolta di intervalli a un metodo <xref:System.Threading.Tasks.Parallel.ForEach%2A> il cui corpo è costituito da un ciclo `for` normale.  Il vantaggio di questo approccio è che il costo della chiamata al delegato viene sostenuto una sola volta per intervallo anziché una volta per elemento.  Nell'esempio seguente viene illustrato il modello di base.  
  
 [!code-csharp[TPL_Partitioners#01](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioner01.cs#01)]
 [!code-vb[TPL_Partitioners#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_partitioners/vb/partitionercreate01.vb#01)]  
  
 Ogni thread del ciclo riceve il proprio <xref:System.Tuple%602>, che contiene i valori di indice iniziale e finale nel sottointervallo specificato.  Il ciclo `for` interno utilizza i valori `fromInclusive` e `toExclusive` per eseguire il ciclo sulla matrice o direttamente su <xref:System.Collections.IList>.  
  
 Uno degli overload di <xref:System.Collections.Concurrent.Partitioner.Create%2A> consente di specificare la dimensione e il numero delle partizioni.  Tale overload può essere utilizzato negli scenari in cui il volume di lavoro per elemento è così ridotto che anche una sola chiamata del metodo virtuale per elemento ha un impatto notevole sulle prestazioni.  
  
## Partitioner personalizzati  
 In alcuni scenari potrebbe valere la pena o potrebbe addirittura essere necessario implementare un partitioner personalizzato.  È ad esempio possibile suddividere una classe di raccolte personalizzata in modo più efficace di come sarebbe possibile utilizzando i partitioner predefiniti basandosi sulla conoscenza della struttura interna della classe.  In alternativa, è possibile creare partizioni a intervalli di varie dimensioni basandosi sulla conoscenza del tempo necessario per l'elaborazione degli elementi in posizioni diverse nella raccolta di origine.  
  
 Per creare un partitioner personalizzato di base, derivare una classe da <xref:System.Collections.Concurrent.Partitioner%601?displayProperty=fullName> ed eseguire l'override dei metodi virtuali, come descritto nella tabella seguente.  
  
|||  
|-|-|  
|<xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>|Questo metodo viene chiamato una volta dal thread principale e restituisce un IList\(IEnumerator\(TSource\)\).  Ogni thread di lavoro del ciclo o della query può chiamare `GetEnumerator` nell'elenco per recuperare un <xref:System.Collections.Generic.IEnumerator%601> su una partizione distinta.|  
|<xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A>|Restituisce `true` se si implementa <xref:System.Collections.Concurrent.Partitioner%601.GetDynamicPartitions%2A>. In caso contrario, restituisce `false`.|  
|<xref:System.Collections.Concurrent.Partitioner%601.GetDynamicPartitions%2A>|Se <xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A> è `true`, è possibile scegliere di chiamare questo metodo anziché <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>.|  
  
 Se i risultati devono essere ordinabili o si richiede l'accesso indicizzato agli elementi, derivare da <xref:System.Collections.Concurrent.OrderablePartitioner%601?displayProperty=fullName> ed eseguire l'override dei metodi virtuali, come descritto nella tabella seguente.  
  
|||  
|-|-|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetPartitions%2A>|Questo metodo viene chiamato una volta dal thread principale e restituisce un `IList(IEnumerator(TSource))`.  Ogni thread di lavoro del ciclo o della query può chiamare `GetEnumerator` nell'elenco per recuperare un <xref:System.Collections.Generic.IEnumerator%601> su una partizione distinta.|  
|<xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A>|Restituisce `true` se si implementa <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetDynamicPartitions%2A>. In caso contrario, restituisce false.|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetDynamicPartitions%2A>|Generalmente si limita a chiamare <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A>.|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A>|Se <xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A> è `true`, è possibile scegliere di chiamare questo metodo anziché <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>.|  
  
 Nella tabella seguente vengono forniti dettagli aggiuntivi sulle modalità con cui i tre tipi di partitioner con bilanciamento del carico implementano la classe <xref:System.Collections.Concurrent.OrderablePartitioner%601>.  
  
|Metodo\/Proprietà|IList \/ Matrice senza bilanciamento del carico|IList \/ Matrice con bilanciamento del carico|IEnumerable|  
|-----------------------|-----------------------------------------------------|---------------------------------------------------|-----------------|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderablePartitions%2A>|Utilizza il partizionamento per intervalli|Utilizza il partizionamento a blocchi ottimizzato per gli elenchi per l'elemento partitionCount specificato|Utilizza il partizionamento a blocchi creando un numero statico di partizioni.|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A?displayProperty=fullName>|Genera un'eccezione non supportata|Utilizza il partizionamento a blocchi ottimizzato per gli elenchi e le partizioni dinamiche|Utilizza il partizionamento a blocchi creando un numero dinamico di partizioni.|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.KeysOrderedInEachPartition%2A>|Restituisce `true`|Restituisce `true`|Restituisce `true`|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.KeysOrderedAcrossPartitions%2A>|Restituisce `true`|Restituisce `false`|Restituisce `false`|  
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.KeysNormalized%2A>|Restituisce `true`|Restituisce `true`|Restituisce `true`|  
|<xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A>|Restituisce `false`|Restituisce `true`|Restituisce `true`|  
  
### Partizioni dinamiche  
 Se si prevede che il partitioner verrà utilizzato in un metodo <xref:System.Threading.Tasks.Parallel.ForEach%2A>, è necessario riuscire a restituire un numero dinamico di partizioni.  Ciò significa che il partitioner può fornire su richiesta in qualsiasi momento un enumeratore per una nuova partizione durante l'esecuzione del ciclo.  Fondamentalmente ogni volta che il ciclo aggiunge una nuova attività parallela, richiede una nuova partizione per l'attività.  Se si ha necessità che i dati siano ordinabili, derivare da <xref:System.Collections.Concurrent.OrderablePartitioner%601?displayProperty=fullName> in modo che a ogni elemento di ogni partizione venga assegnato un indice univoco.  
  
 Per ulteriori informazioni e un esempio, vedere [How to: Implement Dynamic Partitions](../../../docs/standard/parallel-programming/how-to-implement-dynamic-partitions.md).  
  
### Contratto per i partitioner  
 Quando si implementa un partitioner personalizzato, seguire le linee guida indicate di seguito per consentire la corretta interazione con PLINQ e <xref:System.Threading.Tasks.Parallel.ForEach%2A> in TPL:  
  
-   Se <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A> viene chiamato con un argomento con valore zero o un valore inferiore per `partitionsCount`, viene generata l'eccezione <xref:System.ArgumentOutOfRangeException>.  Anche se PLINQ e TPL non passeranno mai in un `partitionCount` uguale a 0, si consiglia comunque di evitare che ciò accada.  
  
-   <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A> e <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderablePartitions%2A> devono restituire sempre un numero di partizioni pari a `partitionsCount`.  Se il partitioner perde dati e non può creare il numero di partizioni richiesto, il metodo deve restituire un enumeratore vuoto per ognuna delle partizioni rimanenti.  In caso contrario, sia PLINQ sia TPL genereranno un'eccezione <xref:System.InvalidOperationException>.  
  
-   <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>, <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderablePartitions%2A>, <xref:System.Collections.Concurrent.Partitioner%601.GetDynamicPartitions%2A> e <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A> non devono mai restituire `null` \(`Nothing` in Visual Basic\).  In caso contrario, PLINQ \/ TPL genererà un'eccezione <xref:System.InvalidOperationException>.  
  
-   I metodi che restituiscono partizioni devono sempre restituire partizioni che possono enumerare in modo completo e univoco l'origine dati.  Nell'origine dati non devono essere presenti duplicati né elementi ignorati, a meno che non sia richiesto in maniera specifica dalla progettazione del partitioner.  Se questa regola non viene rispettata, è possibile che l'ordine di output venga alterato.  
  
-   Le funzioni Get booleane indicate di seguito devono sempre restituire esattamente i valori seguenti in modo che l'ordine di output non venga alterato:  
  
    -   `KeysOrderedInEachPartition`: ogni partizione restituisce elementi con indici di chiave incrementali.  
  
    -   `KeysOrderedAcrossPartitions`: Per tutte le partizioni restituite, gli indici di chiave della partizione *i* hanno un valore superiore degli indici di chiave della partizione *i*\-1.  
  
    -   `KeysNormalized`: tutti gli indici di chiave subiscono incrementi progressivi costanti senza interruzioni, a partire da zero.  
  
-   Tutti gli indici devono essere univoci.  Non possono esistere indici duplicati.  Se questa regola non viene rispettata, è possibile che l'ordine di output venga alterato.  
  
-   Tutti gli indici devono essere non negativi.  Se questa regola non viene rispettata, è possibile che PLINQ\/TPL generi eccezioni.  
  
## Vedere anche  
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)   
 [How to: Implement Dynamic Partitions](../../../docs/standard/parallel-programming/how-to-implement-dynamic-partitions.md)   
 [How to: Implement a Partitioner for Static Partitioning](../../../docs/standard/parallel-programming/how-to-implement-a-partitioner-for-static-partitioning.md)