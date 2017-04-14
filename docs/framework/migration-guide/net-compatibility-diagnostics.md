---
title: "Diagnostica compatibilit&#224; .NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5e481270-b62a-4cb4-8dda-5b4c5b59d61d
caps.latest.revision: 7
author: "twsouthwick"
ms.author: "tasou"
manager: "wpickett"
caps.handback.revision: 7
---
# Diagnostica compatibilit&#224; .NET
La diagnostica compatibilità .NET sono basati su Roslyn che consentono di identificare problemi di compatibilità tra versioni di .NET Framework. Questo elenco contiene tutti gli analizzatori disponibili, anche se solo un subset verrà applicata a ogni operazione di migrazione specifico. Gli analizzatori determinerà quali problemi sono applicabili per la migrazione pianificata ed esporrà solo quelle. Per problemi di dividono versioni interessate, vedere: [compatibilità delle applicazioni](../../../docs/framework/migration-guide/application-compatibility.md).  
  
 Ogni problema include le seguenti informazioni:  
  
-   La descrizione di cosa è cambiato da una versione precedente.  
  
-   Il suggerimento è una descrizione di come la modifica interessa i clienti e se le soluzioni sono disponibili per mantenere la compatibilità tra versioni.  
  
-   È una valutazione dell'importanza di modifica. Problema di compatibilità dell'applicazione sono suddivisi come segue:  
  
    |||  
    |-|-|  
    |Principale|Una modifica significativa che influisce su un numero elevato di App o che richiede variazioni sostanziali del codice.|  
    |Secondario|Una modifica che influisce su un numero ridotto di App o che richiede variazioni marginali del codice.|  
    |Caso limite|Una modifica che influisce sulle App in scenari molto specifici e non comuni.|  
    |Trasparente|Una modifica e senza effetti evidenti sullo sviluppatore o sull'utente dell'applicazione.|  
  
-   Versione indica quando la modifica viene innanzitutto visualizzato in framework. Alcune delle modifiche vengono annullate e che viene indicato anche.  
  
-   Il tipo di modifica:  
  
    |||  
    |-|-|  
    |Ridestinazione:|La modifica interessa le app che vengono ricompilate per una nuova versione di .NET Framework.|  
    |Runtime|La modifica viene applicata un'app esistente che utilizza una versione precedente di .NET Framework ma viene eseguita in una versione successiva.|  
  
-   Le API interessate, se presente.  
  
-   Gli ID di diagnostica disponibili  
  
<a name="diagnostic1"></a>   
## <a name="1-soapformatter-cannot-deserialize-hashtable-and-similar-ordered-collection-objects"></a>1: SoapFormatter Impossibile deserializzare la tabella hash e simili ordinati oggetti della raccolta  
  
|||  
|-|-|  
|Dettagli|SoapFormatter non garantisce che gli oggetti serializzati in un unico .NET Framework versione verrà deserializzare correttamente in una versione diversa. In particolare, alcune raccolte ordinati (ad esempio, Hashtable) aggiunti membri tra 4.0 e 4.5 in modo che non possono deserializzare gli oggetti di questi tipi con .NET 4.0 se fossero serialzied con .NET 4.5. Si noti che, se i dati serializzati viene serializzati e deserializzati con la stessa versione di .NET Framework, non verrà generato alcun problema.|  
|Suggerimento|Serializzazione SoapFormatter deve essere sostituita con la serializzazione BinaryFormatter o NetDataContractSerialization adattabile alle modifiche di .NET Framework.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter.Deserialize%28System.IO.Stream%29?displayProperty=fullName><br /><br /> <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter.Deserialize%28System.IO.Stream%2CSystem.Runtime.Remoting.Messaging.HeaderHandler%29?displayProperty=fullName><br /><br /> <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter.Serialize%28System.IO.Stream%2CSystem.Object%29?displayProperty=fullName><br /><br /> [SoapFormatter.Serialize (intestazione di flusso, oggetto,\<xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter.Serialize%28System.IO.Stream%2CSystem.Object%2CSystem.Runtime.Remoting.Messaging.Header%5B%5D%29?displayProperty=fullName>|  
|Analizzatori|CD0001B<br /><br /> CD0001A|  
  
<a name="diagnostic3"></a>   
## <a name="3-wpf-datatemplate-elements-are-now-visible-to-uia"></a>3: elementi DataTemplate WPF sono ora visibili di automazione  
  
|||  
|-|-|  
|Dettagli|In precedenza, gli elementi DataTemplate erano invisibili per automazione interfaccia utente. A partire da 4.5, automazione interfaccia utente rileva questi elementi. Questo è utile in molti casi, ma è possibile interrompere i test che dipendono da strutture ad albero di automazione che non contengono elementi DataTemplate.|  
|Suggerimento|Test dell'interfaccia utente Auomation per questa applicazione potrebbe essere necessario aggiornato per l'account per l'albero di automazione ora inclusi elementi DataTemplate invisibili in precedenza. Ad esempio, i test che prevede che alcuni elementi che possono essere uno accanto a altro ora debba aspettarsi che gli elementi precedentemente invisibili UIA tra. O test che si basano su alcuni conteggi o gli indici per gli elementi di automazione può essere necessario aggiornato con nuovi valori.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.DataTemplate.%23ctor?displayProperty=fullName><br /><br /> <xref:System.Windows.DataTemplate.%23ctor%28System.Object%29?displayProperty=fullName>|  
|Analizzatori|CD0003|  
  
<a name="diagnostic4"></a>   
## <a name="4-wpf-textbox-selected-text-appears-a-different-color-when-the-text-box-is-inactive"></a>4: testo di TextBox WPF selezionato viene visualizzato un colore diverso quando la casella di testo è inattiva  
  
|||  
|-|-|  
|Dettagli|In .NET 4.5, quando un controllo casella di testo WPF è inattivo (non necessariamente lo stato attivo), il testo selezionato all'interno della casella verrà visualizzato un colore diverso rispetto a quando il controllo è attivo.|  
|Suggerimento|Comportamento precedente (.NET 4.0) può essere ripristinato impostando il [FrameworkCompatibilityPreferences.AreInactiveSelectionHighlightBrushKeysSupported](https://msdn.microsoft.com/en-us/library/system.windows.frameworkcompatibilitypreferences.areinactiveselectionhighlightbrushkeyssupported\(v=vs.110\).aspx) la proprietà su false.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Controls.TextBox?displayProperty=fullName>|  
|Analizzatori|CD0004|  
  
<a name="diagnostic5"></a>   
## <a name="5-listtforeach-can-throw-exception-when-modifying-list-item"></a>5: List<>\>. ForEach può generare eccezioni quando si modifica l'elemento elenco  
  
|||  
|-|-|  
|Dettagli|A partire da .NET 4.5, un `List<T>.ForEach` enumeratore genererà un'eccezione InvalidOperationException se un elemento nella raccolta chiamante viene modificato. In precedenza, questo non genererebbe un'eccezione ma potrebbe provocare situazioni di race condition.|  
|Suggerimento|Idealmente, codice deve essere corretto per non modificare gli elenchi durante l'enumerazione dei relativi elementi perché non è un'operazione sicura. Per ripristinare il comportamento precedente, tuttavia, un'app potrebbero avere come destinazione .NET 4.0.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Collections.Generic.List%601.ForEach%28System.Action%7B%600%7D%29?displayProperty=fullName>|  
|Analizzatori|CD0005|  
  
<a name="diagnostic6"></a>   
## <a name="6-systemuri-parsing-adheres-to-rfc-3987"></a>6: l'analisi di System. URI conforme alla specifica RFC 3987  
  
|||  
|-|-|  
|Dettagli|L'analisi dell'URI è stato modificato in diversi modi in .NET 4.5. Si noti tuttavia che queste modifiche influiscono solo sul codice destinato a .NET 4.5. Se un binario è destinato a .NET 4.0, si assisterà il comportamento precedente. Modifiche per l'analisi dell'URI in .NET 4.5 includono:<br /><br /> Analisi di URI eseguirà la normalizzazione e caratteri di controllo in base alle regole IRI più recenti nella specifica RFC 3987<br /><br /> Formato di normalizzazione Unicode C verrà eseguita solo sulla parte host dell'URI<br /><br /> Mailto non valido: URI ora genererà un'eccezione<br /><br /> Ora vengono mantenuti i punti finali alla fine di un segmento di percorso<br /><br /> `file://`URI senza caratteri di escape il `?` carattere<br /><br /> Caratteri di controllo Unicode `U+0080` tramite `U+009F` non sono supportati<br /><br /> Virgola `,` o `%2c` non sono automaticamente senza caratteri escape|  
|Suggerimento|Se la semantica di analisi di .NET 4.0 URI precedente (spesso non), possono essere utilizzati con come destinazione .NET 4.0. Questo può essere eseguito utilizzando un TargetFrameworkAttribute nell'assembly o tramite il sistema di progetto di Visual Studio dell'interfaccia utente nella pagina 'proprietà del progetto'.|  
|Ambito|Principale|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Uri.%23ctor%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Uri.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Uri.%23ctor%28System.String%2CSystem.UriKind%29?displayProperty=fullName><br /><br /> <xref:System.Uri.%23ctor%28System.Uri%2CSystem.String%29?displayProperty=fullName><br /><br /> <xref:System.Uri.TryCreate%28System.String%2CSystem.UriKind%2CSystem.Uri%40%29?displayProperty=fullName><br /><br /> <xref:System.Uri.TryCreate%28System.Uri%2CSystem.String%2CSystem.Uri%40%29?displayProperty=fullName><br /><br /> <xref:System.Uri.TryCreate%28System.Uri%2CSystem.Uri%2CSystem.Uri%40%29?displayProperty=fullName>|  
|Analizzatori|CD0006D<br /><br /> CD0006C<br /><br /> CD0006F<br /><br /> CD0006E<br /><br /> CD0006A<br /><br /> CD0006G<br /><br /> CD0006B|  
  
<a name="diagnostic10"></a>   
## <a name="10-systemuri-escaping-now-supports-rfc-3986-httptoolsietforghtmlrfc3986"></a>10: l'escape dell'URI ora supporta RFC 3986 (http://tools.ietf.org/html/rfc3986)  
  
|||  
|-|-|  
|Dettagli|L'escape dell'URI è stata modificata in .NET 4.5 per supportare [RFC 3986](http://tools.ietf.org/html/rfc3986). Modifiche specifiche includono:<br /><br /> Tramite il metodo `EscapeDataString` viene effettuato l'escape dei caratteri riservati basati su RFC 3986.<br /><br /> Tramite il metodo `EscapeUriString` non viene effettuato l'escape dei caratteri riservati.<br /><br /> `UnescapeDataString` non genera un'eccezione se rileva una sequenza di escape non valida.<br /><br /> I caratteri di escape non riservati non sono sottoposti a escape.|  
|Suggerimento|Aggiornare le applicazioni non fare affidamento sulla UnescapeDataString per generare nel caso di una sequenza di escape non valido. Tali sequenze devono essere rilevate direttamente a questo punto.<br /><br /> Allo stesso modo, ci si aspetta che le stringhe Escaped e l'URI senza caratteri escape e dati possono variare rispetto a .NET 4.0 e 4.5 di .NET e non devono essere confrontate direttamente tra le versioni di .NET. Ma deve essere analizzati e normalizzati in una sola versione di .NET prima di apportare eventuali confronti.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Uri.EscapeDataString%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Uri.EscapeUriString%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Uri.UnescapeDataString%28System.String%29?displayProperty=fullName>|  
|Analizzatori|CD0010A<br /><br /> CD0010B<br /><br /> CD0010C|  
  
<a name="diagnostic11"></a>   
## <a name="11-systemnetpeertopeercollaboration-unavailable-on-windows-8"></a>11: PeerToPeer disponibile in Windows 8  
  
|||  
|-|-|  
|Dettagli|Lo spazio dei nomi PeerToPeer non è disponibile in Windows 8 o versioni successive.|  
|Suggerimento|Applicazioni che supportano Windows 8 o versioni successive devono essere aggiornate per non dipendono da questo spazio dei nomi o i relativi membri.|  
|Ambito|Principale|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Net.PeerToPeer.Collaboration?displayProperty=fullName>|  
|Analizzatori|CD0011|  
  
<a name="diagnostic12"></a>   
## <a name="12-mef-catalogs-implement-ienumerable-and-therefore-can-no-longer-be-used-to-create-a-serializer"></a>12: i cataloghi MEF implementano IEnumerable e pertanto non può essere utilizzati per creare un serializzatore  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.5, i cataloghi MEF implementano IEnumerable e pertanto non possono essere utilizzati per creare un serializzatore (oggetto XmlSerializer). Il tentativo di serializzare un catalogo MEF genera un'eccezione.|  
|Suggerimento|Non è più possibile usare MEF per creare un serializzatore|  
|Ambito|Principale|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0012|  
  
<a name="diagnostic13"></a>   
## <a name="13-missing-target-framework-moniker-results-in-40-behavior"></a>13: moniker del Framework di destinazione mancante produce un comportamento 4.0  
  
|||  
|-|-|  
|Dettagli|Applicazioni senza un [TargetFrameworkAttribute](https://msdn.microsoft.com/en-us/library/system.runtime.versioning.targetframeworkattribute\(v=vs.110\).aspx) applicato all'assembly livello eseguiranno l'esecuzione automatica utilizzando la semantica (quirks) di .NET Framework 4.0. Per garantire la qualità elevata, è consigliabile che tutti i file binari in modo esplicito essere attribuito un TargetFrameworkAttribute che indica la versione di .NET Framework sono state compilate con. Si noti che l'utilizzo di moniker del framework di destinazione in un file di progetto verranno caues MSBuild per applicare automaticamente un TargetFrameworkAttribute.|  
|Suggerimento|Oggetto [attributo target framework](https://msdn.microsoft.com/en-us/library/system.runtime.versioning.targetframeworkattribute\(v=vs.110\).aspx) deve essere specificato tramite l'aggiunta dell'attributo direttamente all'assembly oppure specificando un framework di destinazione nel [file di progetto o interfaccia utente grafica di proprietà del progetto tramite Visual Studio](http://blogs.msdn.com/b/visualstudio/archive/2010/05/19/visual-studio-managed-multi-targeting-part-1-concepts-target-framework-moniker-target-framework.aspx).|  
|Ambito|Principale|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0013|  
  
<a name="diagnostic14"></a>   
## <a name="14-no-longer-able-to-set-enableviewstatemac-to-false"></a>14: non è più in grado di impostare EnableViewStateMac su false  
  
|||  
|-|-|  
|Dettagli|ASP.NET non consente più agli sviluppatori di specificare `<pages enableViewStateMac="false"/>` o `<@Page EnableViewStateMac="false" %>`. L'algoritmo Message Authentication Code (MAC) dello stato di visualizzazione viene ora applicato per tutte le richieste con stato di visualizzazione incorporato. Sono interessate solo le applicazioni impostata in modo esplicito la proprietà EnableViewStateMac su false.|  
|Suggerimento|EnableViewStateMac devono essere considerati su true e gli eventuali errori risultanti MAC devono essere risolti (come spiegato in [questo](https://support.microsoft.com/en-us/kb/2915218) indicazioni, che contiene più risoluzioni in base alle specifiche di cosa sta provocando errori MAC).|  
|Ambito|Principale|  
|Versione|4.5.2|  
|Tipo|Runtime|  
|Analizzatori|CD0014|  
  
<a name="diagnostic18"></a>   
## <a name="18-blockingcollectionttrytakefromany-does-not-throw-anymore"></a>18: BlockingCollection<>\>. Non genera più TryTakeFromAny venga  
  
|||  
|-|-|  
|Dettagli|Se una delle raccolte di input viene contrassegnata come completata, `BlockingCollection<T>.TryTakeFromAny(BlockingCollection<T>[], T)` non restituisce -1 e `BlockingCollection<T>.TakeFromAny` non genera un'eccezione. Tale modifica consente di usare le raccolte quando una di esse è vuota o completata, ma l'altra contiene ancora elementi che possono essere recuperati.|  
|Suggerimento|Se TryTakeFromAny venga restituire -1 o TakeFromAny venga generazione sono stato utilizzato per scopi di flusso di controllo in caso di una raccolta di blocco vengono completate, tale codice deve essere impostato per utilizzare `.Any(b => b.IsCompleted)` per rilevare tale condizione.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|[BlockingCollection<>\>. TakeFromAny venga (BlockingCollection<>\>\<xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny%28System.Collections.Concurrent.BlockingCollection%7B%600%7D%5B%5D%2C%600%40%29?displayProperty=fullName><br /><br /> [BlockingCollection<>\>. TakeFromAny venga (BlockingCollection<>\>\<xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny%28System.Collections.Concurrent.BlockingCollection%7B%600%7D%5B%5D%2C%600%40%2CSystem.Threading.CancellationToken%29?displayProperty=fullName><br /><br /> [BlockingCollection<>\>. TryTakeFromAny venga (BlockingCollection<>\>\<xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny%28System.Collections.Concurrent.BlockingCollection%7B%600%7D%5B%5D%2C%600%40%29?displayProperty=fullName><br /><br /> [BlockingCollection<>\>. TryTakeFromAny venga (BlockingCollection<>\>\<xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny%28System.Collections.Concurrent.BlockingCollection%7B%600%7D%5B%5D%2C%600%40%2CSystem.Int32%29?displayProperty=fullName><br /><br /> [BlockingCollection<>\>. TryTakeFromAny venga (BlockingCollection<>\>\<xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny%28System.Collections.Concurrent.BlockingCollection%7B%600%7D%5B%5D%2C%600%40%2CSystem.TimeSpan%29?displayProperty=fullName>|  
|Analizzatori|CD0018A<br /><br /> CD0018B|  
  
<a name="diagnostic19"></a>   
## <a name="19-xmlschemaexception-now-sets-line-positions-properly"></a>19: XmlSchemaException ora set posizioni corretto allineamento  
  
|||  
|-|-|  
|Dettagli|Se il valore LoadOptions.SetLineInfo viene passato al metodo Load e si verifica un errore di convalida, le proprietà XmlSchemaException.LineNumber e XmlSchemaException.LinePosition contengono ora informazioni sulla riga.|  
|Suggerimento|Codice di gestione delle eccezioni che si presuppone che XmlSchemaException.LineNumber e XmlSchemaException.LinePosition non sarà set deve essere aggiornato poiché queste proprietà verranno ora impostate correttamente quando SetLineInfo viene utilizzato durante il caricamento di XML.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Xml.Linq.LoadOptions?displayProperty=fullName>|  
|Analizzatori|CD0019|  
  
<a name="diagnostic20"></a>   
## <a name="20-systemactivities-is-now-aptca"></a>20: System. Activities è ora APTCA  
  
|||  
|-|-|  
|Dettagli|L'assembly viene contrassegnato con l'attributo AllowPartiallyTrustedCallersAttribute.|  
|Suggerimento|Le classi derivate non possono essere contrassegnate con SecurityCriticalAttribute. In precedenza, i tipi derivati dovevano essere contrassegnato con SecurityCriticalAttribute. Tuttavia, questa modifica non dovrebbe avere un impatto reale.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0020|  
  
<a name="diagnostic21"></a>   
## <a name="21-workflow-30-types-are-obsolete"></a>21: tipi di flusso di lavoro 3.0 sono obsoleti  
  
|||  
|-|-|  
|Dettagli|API di Windows Workflow Foundation (WWF) 3.0 (quelli dello spazio dei nomi System. workflow) sono ora obsolete.|  
|Suggerimento|Nuove API 4.0 WWF (in System. Activities) da utilizzare in sostituzione. Un esempio di utilizzo le nuove API sono reperibili [qui](https://msdn.microsoft.com/en-us/library/jj205427.aspx) e sono disponibili ulteriori indicazioni [qui](http://blogs.msdn.com/b/workflowteam/archive/2012/02/08/deprecatingwf3.aspx). In alternativa, poiché le API 3.0 WWF sono ancora supportate, essi possono essere utilizzati e l'avviso in fase di compilazione evitato eliminandolo o usando un compilatore precedente.|  
|Ambito|Principale|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0021|  
  
<a name="diagnostic22"></a>   
## <a name="22-some-workflow-drag-and-drop-apis-are-obsolete"></a>22: un flusso di lavoro trascinamento della selezione API sono obsoleti  
  
|||  
|-|-|  
|Dettagli|Questa API di trascinamento del flusso di lavoro è obsoleta e genererà avvisi del compilatore se l'applicazione viene rigenerato con 4.5.|  
|Suggerimento|Nuova [DragDropHelper](https://msdn.microsoft.com/en-us/library/system.activities.presentation.dragdrophelper\(v=vs.110\).aspx) è necessario utilizzare le API che supportano le operazioni con più oggetti. In alternativa, è possibile eliminare gli avvisi di compilazione o può essere evitate utilizzando un compilatore precedente. Le API sono ancora supportate.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Activities.Presentation.DragDropHelper.DoDragMove%28System.Activities.Presentation.WorkflowViewElement%2CSystem.Windows.Point%29?displayProperty=fullName><br /><br /> <xref:System.Activities.Presentation.DragDropHelper.GetCompositeView%28System.Windows.DragEventArgs%29?displayProperty=fullName><br /><br /> <xref:System.Activities.Presentation.DragDropHelper.GetDraggedModelItem%28System.Windows.DragEventArgs%29?displayProperty=fullName><br /><br /> <xref:System.Activities.Presentation.DragDropHelper.GetDroppedObject%28System.Windows.DependencyObject%2CSystem.Windows.DragEventArgs%2CSystem.Activities.Presentation.EditingContext%29?displayProperty=fullName>|  
|Analizzatori|CD0022|  
  
<a name="diagnostic23"></a>   
## <a name="23-new-ambiguous-dispatcherinvoke-overloads-could-result-in-different-behavior"></a>23: nuovi overload Dispatcher.Invoke (ambiguo) potrebbe causare un comportamento differente  
  
|||  
|-|-|  
|Dettagli|.NET Framework 4.5 aggiunti nuovi overload per Dispatcher.Invoke che includono un parametro di tipo System. Action. Se il codice esistente viene ricompilato, i compilatori possono risolvere le chiamate ai metodi Dispatcher.Invoke con un parametro del delegato come chiamate ai metodi Dispatcher.Invoke con un parametro System. Action. Se una chiamata a un overload Dispatcher.Invoke con un parametro del delegato viene risolta come una chiamata a un overload Dispatcher.Invoke con un parametro System. Action, potrebbero verificarsi le seguenti differenze nel comportamento:<br /><br /> Se si verifica un'eccezione, non vengono generati gli eventi Dispatcher.UnhandledExceptionFilter e Dispatcher.UnhandledException. Al contrario, le eccezioni vengono gestite dall'evento UnobservedTaskException.<br /><br /> Le chiamate ad alcuni membri, ad esempio DispatcherOperation.Result, bloccate fino al completamento dell'operazione.|  
|Suggerimento|Per evitare ambiguità (e potenziali differenze nella gestione o comportamenti di blocco di eccezioni), codice Dispatcher.Invoke chiamante può passare un vuoto object [] come secondo parametro della chiamata Invoke per essere certi di risoluzione dell'overload del metodo .NET 4.0.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|API interessate|[Dispatcher.Invoke (delegato, l'oggetto\<xref:System.Windows.Threading.Dispatcher.Invoke%28System.Delegate%2CSystem.Object%5B%5D%29?displayProperty=fullName><br /><br /> [Dispatcher.Invoke (oggetto delegato, intervallo di tempo,\<xref:System.Windows.Threading.Dispatcher.Invoke%28System.Delegate%2CSystem.TimeSpan%2CSystem.Object%5B%5D%29?displayProperty=fullName><br /><br /> [Dispatcher.Invoke (delegato, l'intervallo di tempo, DispatcherPriority, l'oggetto\<xref:System.Windows.Threading.Dispatcher.Invoke%28System.Delegate%2CSystem.TimeSpan%2CSystem.Windows.Threading.DispatcherPriority%2CSystem.Object%5B%5D%29?displayProperty=fullName><br /><br /> [Dispatcher.Invoke (oggetto delegato, DispatcherPriority,\<xref:System.Windows.Threading.Dispatcher.Invoke%28System.Delegate%2CSystem.Windows.Threading.DispatcherPriority%2CSystem.Object%5B%5D%29?displayProperty=fullName>|  
|Analizzatori|CD0023|  
  
<a name="diagnostic24"></a>   
## <a name="24-encoderparameter-ctor-is-obsolete"></a>24: ctor EncoderParameter è obsoleto  
  
|||  
|-|-|  
|Dettagli|Il `EncoderParameter.EncoderParameter(Encoder, Int32, Int32, Int32)` costruttore è obsoleto e introdurrà avvisi di compilazione se utilizzato.|  
|Suggerimento|Sebbene il `EncoderParameter.EncoderParameter(Encoder, Int32, Int32, Int32)` costruttore continueranno a funzionare, è necessario usare invece il costruttore seguente per evitare l'avviso di compilazione obsoleto quando nuovamente la compilazione di codice con gli strumenti di .NET 4.5: [EncoderParameter.EncoderParameter (codificatore, Int32, EncoderParameterValueType, IntPtr)](https://msdn.microsoft.com/en-us/library/hh875096\(v=vs.110\).aspx).|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Drawing.Imaging.EncoderParameter.%23ctor%28System.Drawing.Imaging.Encoder%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%29?displayProperty=fullName>|  
|Analizzatori|CD0024|  
  
<a name="diagnostic26"></a>   
## <a name="26-change-in-behavior-for-taskwaitall-methods-with-time-out-arguments"></a>26: modifica del comportamento per i metodi Task.WaitAll con argomenti di timeout  
  
|||  
|-|-|  
|Dettagli|Task.WaitAll comportamento è stato reso più coerenza in .NET 4.5.<br /><br /> In .NET Framework 4, questi metodi di comportamento è incoerente. Alla scadenza del timeout, se una o più attività sono state completate o annullate prima della chiamata di metodo, il metodo genera un'eccezione AggregateException. Alla scadenza del timeout, se nessuna attività sono stata completata o annullata prima della chiamata di metodo, ma uno o più attività sono entrate in questi stati dopo la chiamata al metodo, il metodo ha restituito false.<br />In .NET Framework 4.5, questi overload del metodo ora restituiscono false se tutte le attività ancora in esecuzione quando l'intervallo di timeout scaduto e generano un'eccezione AggregateException solo se è stata annullata un'attività di input (indipendentemente dal fatto che fosse prima o dopo la chiamata al metodo) e altre attività non sono ancora in esecuzione.|  
|Suggerimento|Se è stato rilevato un'AggregateException come mezzo per rilevare un'attività che è stata annullata prima della chiamata al metodo WaitAll richiamata che codice deve invece di eseguire il rilevamento stesso tramite la proprietà IsCanceled (ad esempio:. Qualsiasi (t => t.IsCanceled)) in quanto .NET 4.6 solo genererà in questo caso se vengono completate tutte le attività di attesa prima del timeout.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|[Task.WaitAll (attività\<xref:System.Threading.Tasks.Task.WaitAll%28System.Threading.Tasks.Task%5B%5D%2CSystem.Int32%29?displayProperty=fullName><br /><br /> [Task.WaitAll (attività\<xref:System.Threading.Tasks.Task.WaitAll%28System.Threading.Tasks.Task%5B%5D%2CSystem.Int32%2CSystem.Threading.CancellationToken%29?displayProperty=fullName><br /><br /> [Task.WaitAll (attività\<xref:System.Threading.Tasks.Task.WaitAll%28System.Threading.Tasks.Task%5B%5D%2CSystem.TimeSpan%29?displayProperty=fullName>|  
|Analizzatori|CD0026|  
  
<a name="diagnostic27"></a>   
## <a name="27-change-in-behavior-in-data-definition-language-ddl-apis"></a>27: modifica del comportamento nella definizione del linguaggio DDL (Data) API  
  
|||  
|-|-|  
|Dettagli|Il comportamento delle API DDL quando viene specificato AttachDBFilename è cambiato come segue:<br /><br /> Le stringhe di connessione non devono specificare un valore di catalogo iniziale. In precedenza, era necessario AttatchDBFilename sia catalogo iniziale.<br /><br /> Se vengono specificati sia AttatchDBFilename catalogo iniziale e il file MDF indicato è presente, il metodo ObjectContext.DatabaseExists restituisce true. In precedenza, ha restituito false.<br /><br /> Se vengono specificati sia AttatchDBFilename catalogo iniziale e il file MDF indicato è presente, la chiamata al metodo ObjectContext.DeleteDatabase Elimina i file.<br /><br /> Se ObjectContext.DeleteDatabase viene chiamato quando la stringa di connessione specifica un valore di AttachDBFilename con un file MDF non esiste e un catalogo iniziale che non esiste, il metodo genera un'eccezione InvalidOperationException. In precedenza, generava un'eccezione SqlException.|  
|Suggerimento|Queste modifiche semplificano la creazione di strumenti e applicazioni che usano le API DDL. Tali modifiche possono influire sulla compatibilità delle applicazioni negli scenari seguenti:<br /><br /> L'utente scrive codice che esegue un comando DROP DATABASE direttamente anziché chiamando ObjectContext.DeleteDatabase se ObjectContext.DatabaseExists restituisce true. Questa operazione interrompe il codice esistente se il database non è collegato ma il file MDF esiste.<br /><br /> L'utente scrive codice che prevede che il metodo ObjectContext.DeleteDatabase per generare un'eccezione SqlException anziché un'eccezione InvalidOperationException quando il file di catalogo iniziale e MDF non esiste.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0027|  
  
<a name="diagnostic28"></a>   
## <a name="28-machinekeyencode-and-machinekeydecode-methods-are-now-obsolete"></a>28: metodi machineKey e MachineKey.Decode sono ora obsoleti  
  
|||  
|-|-|  
|Dettagli|Questi metodi sono ora obsoleti. La compilazione del codice che chiama tali metodi genera un avviso del compilatore.|  
|Suggerimento|Le alternative consigliate sono [MachineKey.Protect](https://msdn.microsoft.com/en-us/library/system.web.security.machinekey.protect\(v=vs.110\).aspx) e [MachineKey.Unprotect](https://msdn.microsoft.com/en-us/library/system.web.security.machinekey.unprotect\(v=vs.110\).aspx). In alternativa, è possibile eliminare gli avvisi di compilazione o può essere evitate utilizzando un compilatore precedente. Le API sono ancora supportate.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Web.Security.MachineKey.Decode%28System.String%2CSystem.Web.Security.MachineKeyProtection%29?displayProperty=fullName><br /><br /> [MachineKey (Byte\<xref:System.Web.Security.MachineKey.Encode%28System.Byte%5B%5D%2CSystem.Web.Security.MachineKeyProtection%29?displayProperty=fullName>|  
|Analizzatori|CD0028|  
  
<a name="diagnostic29"></a>   
## <a name="29-the-replace-method-in-odata-urls-is-disabled-by-default"></a>29: il metodo Replace negli URL OData è disabilitato per impostazione predefinita  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.5, il metodo Replace negli URL OData è disabilitato per impostazione predefinita. Quando sostituire OData è disabilitato (ora per impostazione predefinita), tutte le richieste utente incluse le funzioni di sostituzione (che sono frequenti) avrà esito negativo.|  
|Suggerimento|Se è necessario il metodo replace (che è non comune), possono essere riabilitato tramite un [le impostazioni di configurazione](https://msdn.microsoft.com/en-us/library/system.data.services.configuration.dataservicesfeaturessection.replacefunction.aspx). Tuttavia, un metodo replace abilitato possibile aprire le vulnerabilità di sicurezza e deve essere utilizzato solo dopo un attento esame.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Data.Services.DataService%601?displayProperty=fullName>|  
|Analizzatori|CD0029|  
  
<a name="diagnostic30"></a>   
## <a name="30-systemservicemodelwebwebservicehost-object-no-longer-adds-a-default-endpoint"></a>30: oggetto WebServiceHost non aggiunge non è più un endpoint predefinito  
  
|||  
|-|-|  
|Dettagli|L'oggetto WebServiceHost aggiunge non è più un endpoint predefinito se è stato aggiunto un endpoint esplicito dal codice dell'applicazione.|  
|Suggerimento|Se gli utenti verranno si aspettano di essere in grado di connettersi a un endpoint predefinito e altri endpoint espliciti sono state aggiunte le WebServiceHost, deve inoltre possibile aggiungere endpoint predefiniti in modo esplicito (mediante AddDefaultEndpoints).|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%28System.Type%2CSystem.ServiceModel.Channels.Binding%2CSystem.String%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%28System.Type%2CSystem.ServiceModel.Channels.Binding%2CSystem.String%2CSystem.Uri%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%28System.Type%2CSystem.ServiceModel.Channels.Binding%2CSystem.Uri%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%28System.Type%2CSystem.ServiceModel.Channels.Binding%2CSystem.Uri%2CSystem.Uri%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHostBase.AddServiceEndpoint%28System.ServiceModel.Description.ServiceEndpoint%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHostBase.AddServiceEndpoint%28System.String%2CSystem.ServiceModel.Channels.Binding%2CSystem.String%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHostBase.AddServiceEndpoint%28System.String%2CSystem.ServiceModel.Channels.Binding%2CSystem.String%2CSystem.Uri%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHostBase.AddServiceEndpoint%28System.String%2CSystem.ServiceModel.Channels.Binding%2CSystem.Uri%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHostBase.AddServiceEndpoint%28System.String%2CSystem.ServiceModel.Channels.Binding%2CSystem.Uri%2CSystem.Uri%29?displayProperty=fullName>|  
|Analizzatori|CD0030A<br /><br /> CD0030B|  
  
<a name="diagnostic31"></a>   
## <a name="31-eventsourcewriteevent-impls-must-pass-writeevent-the-same-parameters-that-it-received-plus-id"></a>31: implementazioni WriteEvent devono passare WriteEvent gli stessi parametri ricevuti (più ID)  
  
|||  
|-|-|  
|Dettagli|Il runtime applica ora il contratto che specifica le operazioni seguenti: una classe derivata da EventSource che definisce un metodo di eventi ETW deve chiamare il metodo WriteEvent della classe base con l'ID evento seguito dagli stessi argomenti passati al metodo eventi ETW.|  
|Suggerimento|Se un listener di eventi legge i dati di EventSource in-process per un'origine evento che viola questo contratto, viene generata un'eccezione IndexOutOfRangeException.|  
|Ambito|Secondario|  
|Versione|4.5.1|  
|Tipo|Runtime|  
|Analizzatori|CD0031|  
  
<a name="diagnostic32"></a>   
## <a name="32-minfreememorypercentagetoactiveservice-is-now-respected"></a>32: MinFreeMemoryPercentageToActiveService ora viene rispettato  
  
|||  
|-|-|  
|Dettagli|Questa impostazione stabilisce la memoria minima che deve essere disponibile nel server prima di poter attivare un servizio WCF. È progettato per evitare eccezioni OutOfMemoryException. In .NET Framework 4.5, questa impostazione non aveva alcun effetto. In .NET Framework 4.5.1, l'impostazione viene applicata.|  
|Suggerimento|Viene generata un'eccezione se la quantità di memoria libera disponibile sul server Web è inferiore alla percentuale definita dall'impostazione di configurazione. Alcuni servizi WCF correttamente avviati ed eseguiti in un ambiente di memoria limitato potrebbero avere esito negativo.|  
|Ambito|Secondario|  
|Versione|4.5.1|  
|Tipo|Runtime|  
|Analizzatori|CD0032|  
  
<a name="diagnostic33"></a>   
## <a name="33-xmltextreader-dtd-entity-expansion-is-limited-to-10000000-characters"></a>33: espansione di entità XmlTextReader DTD è limitata a 10.000.000 di caratteri  
  
|||  
|-|-|  
|Dettagli|Espansione delle entità DTD è limitata a 10.000.000 di caratteri. Il caricamento di file XML senza espansione o con espansione limitata dell'entità DTD non è interessato dall'operazione. I file con entità DTD che si espandono oltre 10.000.000 di caratteri non vengono caricati e generano un'eccezione.|  
|Suggerimento|Se il limite di espansione dell'entità DTD è 10.000.000 troppo basso, il valore può essere sostituito con il [XmlReaderSettings.MaxCharactersFromEntities](https://msdn.microsoft.com/en-us/library/system.xml.xmlreadersettings.maxcharactersfromentities%28v=vs.110%29.aspx) proprietà. Un XmlReaderSettings con il valore corretto MaxCharactersFromEntity può essere passato a [XmlReader. create](https://msdn.microsoft.com/en-us/library/System.Xml.XmlReader.Create\(v=vs.110\).aspx)|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Xml.XmlTextReader.%23ctor?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.IO.Stream%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.IO.Stream%2CSystem.Xml.XmlNameTable%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.IO.Stream%2CSystem.Xml.XmlNodeType%2CSystem.Xml.XmlParserContext%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.IO.TextReader%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.IO.TextReader%2CSystem.Xml.XmlNameTable%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.String%2CSystem.IO.Stream%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.String%2CSystem.IO.Stream%2CSystem.Xml.XmlNameTable%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.String%2CSystem.IO.TextReader%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.String%2CSystem.IO.TextReader%2CSystem.Xml.XmlNameTable%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.String%2CSystem.Xml.XmlNameTable%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.String%2CSystem.Xml.XmlNodeType%2CSystem.Xml.XmlParserContext%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.Xml.XmlNameTable%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader?displayProperty=fullName>|  
|Analizzatori|CD0033|  
  
<a name="diagnostic35"></a>   
## <a name="35-xslt-style-sheet-exception-message-changed"></a>35: messaggio di eccezione foglio di stile XSLT modificato  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4.5, il testo del messaggio di errore quando un file XSLT è troppo complesso è "foglio di stile è troppo complesso". Nelle versioni precedenti il messaggio di errore era "Errore di compilazione XSLT". Il codice di applicazione che dipende dal testo del messaggio di errore non funzionerà più. Tuttavia, i tipi di eccezione rimangono gli stessi, pertanto questa modifica dovrebbe avere un impatto reale.|  
|Suggerimento|Aggiornare il codice dell'applicazione a seconda del messaggio excepton da questa condizione di errore aspettarsi che il nuovo messaggio, o (più) aggiornare il codice per dipendere solo il tipo di eccezione ([XsltException](https://msdn.microsoft.com/en-us/library/system.xml.xsl.xsltexception\(v=vs.110\).aspx)), che non è stato modificato.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|[XslCompiledTransform.Load (MethodInfo, Byte\[\], tipo\<xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Reflection.MethodInfo%2CSystem.Byte%5B%5D%2CSystem.Type%5B%5D%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.String%2CSystem.Xml.Xsl.XsltSettings%2CSystem.Xml.XmlResolver%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Type%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Xml.XPath.IXPathNavigable%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Xml.XPath.IXPathNavigable%2CSystem.Xml.Xsl.XsltSettings%2CSystem.Xml.XmlResolver%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Xml.XmlReader%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Xml.XmlReader%2CSystem.Xml.Xsl.XsltSettings%2CSystem.Xml.XmlResolver%29?displayProperty=fullName>|  
|Analizzatori|CD0035|  
  
<a name="diagnostic36"></a>   
## <a name="36-wf-serializes-expressionsliteralt-datetimes-differently-now-breaks-custom-xaml-parsers"></a>36: WF serializza Expressions.Literal<> \</> \> date e ore in modo diverso dopo (interrompe i parser XAML personalizzati)  
  
|||  
|-|-|  
|Dettagli|L'oggetto associato [ValueSerializer](https://msdn.microsoft.com/en-us/library/system.windows.markup.valueserializer\(v=vs.110\).aspx) oggetto convertirà un valore DateTime o DateTimeOffset oggetto i cui componenti secondo e millisecondo sono diversi da zero e (per un valore DateTime di valore) la cui proprietà DateTime. Kind non è specificato per la sintassi degli elementi di proprietà anziché una stringa. Questa modifica consente i valori DateTime e DateTimeOffset sia attivato round. I parser XAML personalizzati che presuppongono che il codice XAML di input si trovi nella sintassi degli attributi non funzioneranno correttamente.|  
|Suggerimento|Questa modifica consente i valori DateTime e DateTimeOffset sia attivato round. I parser XAML personalizzati che presuppongono che il codice XAML di input si trovi nella sintassi degli attributi non funzioneranno correttamente.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0036|  
  
<a name="diagnostic37"></a>   
## <a name="37-new-enum-values-in-wpfs-pagerangeselection"></a>37: nuovi valori di enumerazione PageRangeSelection di WPF  
  
|||  
|-|-|  
|Dettagli|Sono stati aggiunti due nuovi membri (CurrentPage e SelectedPage) il [PageRangeSelection](https://msdn.microsoft.com/en-us/library/system.windows.controls.pagerangeselection\(v=vs.110\).aspx) enum.|  
|Suggerimento|Nella maggior parte dei casi, queste modifiche non influiscono su codice utente. Codice che dipende da un determinato numero di elementi esistenti in Enum.GetNames o enum. GetValues chiama il PageRangeSelection tipo deve essere modificato, tuttavia.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Controls.PageRangeSelection?displayProperty=fullName>|  
|Analizzatori|CD0037|  
  
<a name="diagnostic38"></a>   
## <a name="38-wpf-dispatchersynchronizationcontextcreatecopy-now-returns-a-new-copy-instead-of-the-current-instance"></a>38: WPF DispatcherSynchronizationContext.CreateCopy restituisce ora una nuova copia anziché l'istanza corrente  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4, DispatcherSynchronizationContext.CreateCopy() ha restituito un riferimento all'istanza corrente, principalmente come ottimizzazione delle prestazioni. In .NET Framework 4.5, restituisce una nuova istanza che rende possibile per la prima volta a concludere che riferimenti uguali indichino che è il thread in esecuzione nel contesto di sincronizzazione corretto.  È improbabile che il codice che verifica l'identità di questi riferimenti sarà interessato, ma a causa della modifica, è opportuno sottoporre il codice che chiama DispatcherSynchronizationContext.CreateCopy come parte della migrazione a .NET Framework 4.5 o versione successiva.|  
|Suggerimento|Tenere presente che DispatcherSynchronizationContext.CreateCopy() restituirà ora un nuovo oggetto SynchronizationContext.  Codice utilizzato equivalenza dei riferimenti generati in questo modo non è stato in precedenza, effettivamente verifica se nel contesto corretto, ma non quando compilato con .NET 4.5 o versione successiva.  Anche se improbabile provocare problemi di esercitare i percorsi di codice interessata dovrebbe essere sufficiente per determinare se ciò costituisce un problema.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Threading.DispatcherSynchronizationContext.CreateCopy?displayProperty=fullName>|  
|Analizzatori|CD0038|  
  
<a name="diagnostic39"></a>   
## <a name="39-systemthreadingtaskstask-no-longer-throw-objectdisposedexception-after-object-is-disposed"></a>39: System.Threading.Tasks.Task non generano più ObjectDisposedException dopo l'oggetto è stato eliminato  
  
|||  
|-|-|  
|Dettagli|Ad eccezione di Task.IAsyncResult.AsyncWaitHandle, System.Threading.Tasks.Task metodi non è più un'eccezione ObjectDisposedException dopo che l'oggetto viene eliminato.<br />Questa modifica supporta l'uso di attività memorizzate nella cache. Ad esempio, un metodo può restituire un'attività memorizzata nella cache per rappresentare un'operazione già completata anziché allocare una nuova attività. Ciò non è possibile nelle versioni precedenti di .NET Framework, perché qualsiasi utente dell'attività può rimuoverla e renderla così inutilizzabile.|  
|Suggerimento|Tenere presente che i metodi di attività potrebbero non generano più ObjectDisposedExceptions in casi quando viene eliminato l'oggetto. Se un'applicazione è stato a seconda di sapere che è stata eliminata in un'attività di questa eccezione, deve essere aggiornato per verificare in modo esplicito lo stato dell'attività utilizzando [Task.Status](https://msdn.microsoft.com/en-us/library/system.threading.tasks.task.status\(v=vs.110\).aspx).|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0039|  
  
<a name="diagnostic40"></a>   
## <a name="40-different-exception-handling-for-objectcontextcreatedatabase-and-dbproviderservicescreatedatabase-methods"></a>40: diverse eccezioni per i metodi ObjectContext.CreateDatabase e DbProviderServices.CreateDatabase  
  
|||  
|-|-|  
|Dettagli|A partire da .NET 4.5, se la creazione del database non riesce, `CreateDatabase` metodi tenterà di eliminare il database vuoto. Se tale operazione ha esito positivo, originale `SQLException` verranno propagate (anziché la `InvalidOperationException` sempre generata in .NET 4.0)|  
|Suggerimento|Quando intercettare un'eccezione InvalidOperationException durante l'esecuzione ObjectContext.CreateDatabase o DbProviderServices.CreateDatabase, SQLExceptions ora devono inoltre essere rilevate.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Data.Common.DbProviderServices.CreateDatabase%28System.Data.Common.DbConnection%2CSystem.Nullable%7BSystem.Int32%7D%2CSystem.Data.Metadata.Edm.StoreItemCollection%29?displayProperty=fullName><br /><br /> <xref:System.Data.Objects.ObjectContext.CreateDatabase?displayProperty=fullName>|  
|Analizzatori|CD0040|  
  
<a name="diagnostic41"></a>   
## <a name="41-objectcontexttranslate-and-objectcontextexecutestorequery-now-support-enum-type"></a>41: ObjectContext.Translate e ObjectContext.ExecuteStoreQuery ora supporta tipo enum  
  
|||  
|-|-|  
|Dettagli|In .NET 4.0, il parametro generico `T` di `ObjectContext.Translate` e `ObjectContext.ExecuteStoreQuery` metodi potrebbero non essere un tipo enum. Tale scenario è ora supportato.|  
|Suggerimento|Se Traduci o ExecuteStoreQuery è stato chiamato su un tipo enum in .NET 4.0, '0' è stato restituito. Se tale comportamento era opportuno, le chiamate devono essere sostituite con una costante 0 (o l'equivalente di enumerazione di esso).|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|[ObjectContext.ExecuteStoreQuery<>\>(stringa, oggetto\<xref:System.Data.Objects.ObjectContext.ExecuteStoreQuery%60%601%28System.String%2CSystem.Object%5B%5D%29?displayProperty=fullName><br /><br /> [ObjectContext.ExecuteStoreQuery<>\>(String, String, MergeOption, oggetto\<xref:System.Data.Objects.ObjectContext.ExecuteStoreQuery%60%601%28System.String%2CSystem.String%2CSystem.Data.Objects.MergeOption%2CSystem.Object%5B%5D%29?displayProperty=fullName><br /><br /> <xref:System.Data.Objects.ObjectContext.Translate%60%601%28System.Data.Common.DbDataReader%29?displayProperty=fullName><br /><br /> <xref:System.Data.Objects.ObjectContext.Translate%60%601%28System.Data.Common.DbDataReader%2CSystem.String%2CSystem.Data.Objects.MergeOption%29?displayProperty=fullName>|  
|Analizzatori|CD0041|  
  
<a name="diagnostic42"></a>   
## <a name="42-enumerableemptytresult-always-returns-cached-instance"></a>42: Enumerable<> \</> \> sempre istanza memorizzata nella cache restituisce  
  
|||  
|-|-|  
|Dettagli|A partire da .NET 4.5, `Enumerable.Empty` restituisce sempre un'istanza interna memorizzata nella cache `IEnumerable<T>`.<br /><br /> In precedenza, `Enumerable.Empty` necessario memorizzare nella cache un oggetto vuoto `IEnumerable<T>` al momento della chiamata API, vale a dire che in alcune condizioni in cui `Enumerable.Empty` è stato chiamato in modo rapido e, contemporaneamente diversi per diverse chiamate all'API è stato possibile restituire istanze del tipo.|  
|Suggerimento|Poiché il comportamento precedente è non deterministico, è improbabile che dipendono da tale codice. Tuttavia, nel caso improbabile che enumerabili vuoti vengono confrontati e prevede talvolta essere uguali, devono essere create esplicite matrici vuote (`new T[0]`) anziché `Enumerable.Empty`.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Linq.Enumerable.Empty%60%601?displayProperty=fullName>|  
|Analizzatori|CD0042|  
  
<a name="diagnostic43"></a>   
## <a name="43-httprequestcontentencoding-property-prohibits-utf7"></a>43: proprietà ContentEncoding impedisce UTF7  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.5, la codifica UTF-7 non è consentita in corpi di HttpRequests. In alcuni casi i dati per le applicazioni che dipendono dai dati UTF-7 in ingresso non verranno decodificati correttamente.|  
|Suggerimento|In teoria, le applicazioni devono essere aggiornate per non utilizzare la codifica UTF-7 in HttpRequests. In alternativa, è possibile ripristinare il comportamento legacy tramite il `aspnet:AllowUtf7RequestContentEncoding` dell'attributo di [appSettings](https://msdn.microsoft.com/en-us/library/hh975440\(v=vs.110\).aspx) elemento.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Web.HttpRequest.ContentEncoding?displayProperty=fullName>|  
|Analizzatori|CD0043|  
  
<a name="diagnostic44"></a>   
## <a name="44-httputilityjavascriptstringencode-escapes-ampersand"></a>44: HttpUtility.JavaScriptStringEncode escape e commerciale  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.5, JavaScriptStringEncode ignora il carattere e commerciale (&).|  
|Suggerimento|Se l'applicazione dipende dal comportamento precedente di questo metodo, è possibile aggiungere un'impostazione aspnet:JavaScriptDoNotEncodeAmpersand per il [elemento appSettings di ASP.NET](https://msdn.microsoft.com/en-us/library/hh975440\(v=vs.110\).aspx) nel file di configurazione.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Web.HttpUtility.JavaScriptStringEncode%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Web.HttpUtility.JavaScriptStringEncode%28System.String%2CSystem.Boolean%29?displayProperty=fullName>|  
|Analizzatori|CD0044A<br /><br /> CD0044B|  
  
<a name="diagnostic46"></a>   
## <a name="46-eventlistener-truncates-strings-with-embedded-nulls"></a>46: EventListener tronca le stringhe con caratteri null incorporati  
  
|||  
|-|-|  
|Dettagli|EventListener tronca le stringhe con caratteri null incorporati. Caratteri null non sono supportati dalla classe EventSource. La modifica interessa solo le applicazioni che utilizzano EventListener per leggere i dati di EventSource nel processo e che utilizzano caratteri null come delimitatori.|  
|Suggerimento|EventSource dati devono essere aggiornati, se possibile, per non utilizzare caratteri null incorporati.|  
|Ambito|Microsoft Edge|  
|Versione|4.5.1|  
|Tipo|Runtime|  
|API interessate|<xref:System.Diagnostics.Tracing.EventListener.%23ctor?displayProperty=fullName><br /><br /> <xref:System.Diagnostics.Tracing.EventListener.EnableEvents%28System.Diagnostics.Tracing.EventSource%2CSystem.Diagnostics.Tracing.EventLevel%29?displayProperty=fullName><br /><br /> <xref:System.Diagnostics.Tracing.EventListener.EnableEvents%28System.Diagnostics.Tracing.EventSource%2CSystem.Diagnostics.Tracing.EventLevel%2CSystem.Diagnostics.Tracing.EventKeywords%29?displayProperty=fullName><br /><br /> <xref:System.Diagnostics.Tracing.EventListener.EnableEvents%28System.Diagnostics.Tracing.EventSource%2CSystem.Diagnostics.Tracing.EventLevel%2CSystem.Diagnostics.Tracing.EventKeywords%2CSystem.Collections.Generic.IDictionary%7BSystem.String%2CSystem.String%7D%29?displayProperty=fullName> \</String, String>|  
|Analizzatori|CD0046|  
  
<a name="diagnostic48"></a>   
## <a name="48-obsoleteattribute-exports-as-both-obsoleteattribute-and-deprecatedattribute-in-winmd-scenarios"></a>48: ObsoleteAttribute Esporta come ObsoleteAttribute sia DeprecatedAttribute negli scenari di WinMD  
  
|||  
|-|-|  
|Dettagli|Quando si crea una raccolta di metadati Windows (file con estensione winmd), l'attributo ObsoleteAttribute viene esportato come una proprietà ObsoleteAttribute sia Windows.Foundation.DeprecatedAttribute.|  
|Suggerimento|La ricompilazione del codice sorgente esistente che utilizza l'attributo ObsoleteAttribute può generare avvisi quando utilizza quel codice da C + + CX o JavaScript.<br /><br /> Si consiglia di non applicare ObsoleteAttribute sia Windows.Foundation.DeprecatedAttribute al codice in assembly gestiti, può verificarsi avvisi di compilazione.|  
|Ambito|Microsoft Edge|  
|Versione|4.5.1|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0048A<br /><br /> CD0048B|  
  
<a name="diagnostic49"></a>   
## <a name="49-resolveassemblyreference-task-now-warns-on-dependencies-with-the-wrong-architecture"></a>49: ResolveAssemblyReference (attività) a questo punto, viene visualizzato un avviso sulle dipendenze con l'architettura errata  
  
|||  
|-|-|  
|Dettagli|L'attività genera un avviso, MSB3270, che indica la mancata corrispondenza di un riferimento o di una delle sue dipendenze all'architettura dell'app. Ad esempio, ciò si verifica se un'applicazione che è stata compilata con l'opzione anycpu include un x86 riferimento. Uno scenario di questo tipo potrebbe provocare un errore dell'app in fase di esecuzione (nel caso descritto, se l'app viene distribuita come processo x64).|  
|Suggerimento|Le possibili conseguenze riguardano le aree seguenti:<br /><br /> La ricompilazione genera avvisi che non venivano visualizzati quando l'app veniva compilata con una versione precedente di MSBuild. Tuttavia, dal momento che l'avviso identifica una possibile fonte di errore di runtime, deve essere analizzato e affrontato.<br /><br /> Se gli avvisi vengono considerati errori, la compilazione dell'app non verrà completata.|  
|Ambito|Secondario|  
|Versione|4.5.1|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0049|  
  
<a name="diagnostic51"></a>   
## <a name="51-wpf-textbox-defaults-to-undo-limit-of-100"></a>51: casella di testo WPF predefiniti per annullare limite di 100  
  
|||  
|-|-|  
|Dettagli|In .NET 4.5, il limite di annullamento predefinito per una casella di testo WPF è 100 (anziché essere illimitato in .NET 4.0)|  
|Suggerimento|Se un limite di annullamento di 100 è troppo basso, il limite può essere impostato in modo esplicito con proprietà UndoLimit della casella di testo|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Controls.TextBox?displayProperty=fullName>|  
|Analizzatori|CD0051|  
  
<a name="diagnostic55"></a>   
## <a name="55-exceptions-during-unobserved-processing-in-systemthreadingtaskstask-no-longer-propagate-on-finalizer-thread"></a>55: eccezioni durante l'elaborazione non osservata in System.Threading.Tasks.Task non è più propagata nel thread del finalizzatore  
  
|||  
|-|-|  
|Dettagli|Poiché la classe System.Threading.Tasks.Task rappresenta un'operazione asincrona, intercetta tutte le eccezioni non gravi che si verificano durante l'elaborazione asincrona. In .NET Framework 4.5, se un'eccezione non viene osservata e il codice è mai in attesa dell'attività, l'eccezione non verrà più propagata nel thread finalizzatore e il processo di arresto anomalo durante l'operazione di garbage collection. Questa modifica migliora l'affidabilità delle applicazioni che utilizzano la classe dell'attività per eseguire l'elaborazione asincrona non osservata.|  
|Suggerimento|Se un'applicazione dipende da eccezioni non osservate asincrone propagazione al thread del finalizzatore, il comportamento precedente può essere ripristinato fornendo un gestore appropriato per il [TaskScheduler.UnobservedTaskException](https://msdn.microsoft.com/en-us/library/system.threading.tasks.taskscheduler.unobservedtaskexception\(v=vs.110\).aspx) evento, oppure impostando un [elemento di configurazione di runtime](https://msdn.microsoft.com/en-us/library/jj160346%28v=vs.110%29.aspx).|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Threading.Tasks.Task.Run%28System.Action%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Run%28System.Action%2CSystem.Threading.CancellationToken%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Run%28System.Func%7BSystem.Threading.Tasks.Task%7D%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Run%28System.Func%7BSystem.Threading.Tasks.Task%7D%2CSystem.Threading.CancellationToken%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Run%60%601%28System.Func%7BSystem.Threading.Tasks.Task%7B%60%600%7D%7D%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Run%60%601%28System.Func%7BSystem.Threading.Tasks.Task%7B%60%600%7D%7D%2CSystem.Threading.CancellationToken%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Run%60%601%28System.Func%7B%60%600%7D%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Run%60%601%28System.Func%7B%60%600%7D%2CSystem.Threading.CancellationToken%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Start?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Start%28System.Threading.Tasks.TaskScheduler%29?displayProperty=fullName>|  
|Analizzatori|CD0055|  
  
<a name="diagnostic58"></a>   
## <a name="58-iasyncresultcompletedsynchronously-property-must-be-correct-for-the-resulting-task-to-complete"></a>58: proprietà CompletedSynchronously deve essere corretta per il completamento dell'attività risultante  
  
|||  
|-|-|  
|Dettagli|Quando si chiama TaskFactory.FromAsync, l'implementazione della proprietà CompletedSynchronously deve essere corretta per il completamento dell'attività risultante. Ovvero, la proprietà deve restituire true se e solo se l'implementazione è stata completata in modo sincrono. Precedentemente, la proprietà non veniva verificata.|  
|Suggerimento|Se le implementazioni di IAsyncResult correttamente restituire true per la proprietà CompletedSynchronusly solo quando un'attività è stata completata in modo sincrono, non verrà osservata alcuna interruzione. Gli utenti devono esaminare le implementazioni di IAsyncResult per garantire che valutano in modo corretto se un'attività è stata completata in modo sincrono o non sono proprietari (se presente).|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Threading.Tasks.TaskFactory.FromAsync%28System.Func%7BSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2CSystem.Object%29?displayProperty=fullName> \</AsyncCallback, Object, IAsyncResult><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%28System.Func%7BSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName> \</AsyncCallback, Object, IAsyncResult><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%28System.IAsyncResult%2CSystem.Action%7BSystem.IAsyncResult%7D%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%28System.IAsyncResult%2CSystem.Action%7BSystem.IAsyncResult%7D%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%28System.IAsyncResult%2CSystem.Action%7BSystem.IAsyncResult%7D%2CSystem.Threading.Tasks.TaskCreationOptions%2CSystem.Threading.Tasks.TaskScheduler%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%601%28System.Func%7BSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%600%7D%2CSystem.Object%29?displayProperty=fullName> \</IAsyncResult, TResult> \</AsyncCallback, Object, IAsyncResult><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%601%28System.Func%7BSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%600%7D%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName> \</IAsyncResult, TResult> \</AsyncCallback, Object, IAsyncResult><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%601%28System.Func%7B%60%600%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2C%60%600%2CSystem.Object%29?displayProperty=fullName> </TArg1, AsyncCallback, Object, IAsyncResult><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%601%28System.Func%7B%60%600%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2C%60%600%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName> \</TArg1, AsyncCallback, Object, IAsyncResult><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%601%28System.IAsyncResult%2CSystem.Func%7BSystem.IAsyncResult%2C%60%600%7D%29?displayProperty=fullName> \</IAsyncResult, TResult><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%601%28System.IAsyncResult%2CSystem.Func%7BSystem.IAsyncResult%2C%60%600%7D%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName> \</IAsyncResult, TResult><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%601%28System.IAsyncResult%2CSystem.Func%7BSystem.IAsyncResult%2C%60%600%7D%2CSystem.Threading.Tasks.TaskCreationOptions%2CSystem.Threading.Tasks.TaskScheduler%29?displayProperty=fullName> \</IAsyncResult, TResult><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%602%28System.Func%7B%60%600%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%601%7D%2C%60%600%2CSystem.Object%29?displayProperty=fullName> \</IAsyncResult, TResult> \</TArg1, AsyncCallback, Object, IAsyncResult> \</TArg1, TResult><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%602%28System.Func%7B%60%600%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%601%7D%2C%60%600%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName> \</IAsyncResult, TResult> \</TArg1, AsyncCallback, Object, IAsyncResult> \</TArg1, TResult><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%602%28System.Func%7B%60%600%2C%60%601%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2C%60%600%2C%60%601%2CSystem.Object%29?displayProperty=fullName> </TArg1, TArg2, AsyncCallback, Object, IAsyncResult> </TArg1, TArg2><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%602%28System.Func%7B%60%600%2C%60%601%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2C%60%600%2C%60%601%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName> \</TArg1, TArg2, AsyncCallback, Object, IAsyncResult> \</TArg1, TArg2><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%603%28System.Func%7B%60%600%2C%60%601%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%602%7D%2C%60%600%2C%60%601%2CSystem.Object%29?displayProperty=fullName> \</IAsyncResult, TResult> \</TArg1, TArg2, AsyncCallback, Object, IAsyncResult> \</TArg1, TArg2, TResult><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%603%28System.Func%7B%60%600%2C%60%601%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%602%7D%2C%60%600%2C%60%601%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName> \</IAsyncResult, TResult> \</TArg1, TArg2, AsyncCallback, Object, IAsyncResult> \</TArg1, TArg2, TResult><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%603%28System.Func%7B%60%600%2C%60%601%2C%60%602%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2C%60%600%2C%60%601%2C%60%602%2CSystem.Object%29?displayProperty=fullName> </TArg1, TArg2, TArg3, AsyncCallback, Object, IAsyncResult> </TArg1, TArg2, TArg3><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%603%28System.Func%7B%60%600%2C%60%601%2C%60%602%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2C%60%600%2C%60%601%2C%60%602%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName> \</TArg1, TArg2, TArg3, AsyncCallback, Object, IAsyncResult> \</TArg1, TArg2, TArg3><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%604%28System.Func%7B%60%600%2C%60%601%2C%60%602%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%603%7D%2C%60%600%2C%60%601%2C%60%602%2CSystem.Object%29?displayProperty=fullName> \</IAsyncResult, TResult> \</TArg1, TArg2, TArg3, AsyncCallback, Object, IAsyncResult> \</TArg1, TArg2, TArg3, TResult><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%604%28System.Func%7B%60%600%2C%60%601%2C%60%602%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%603%7D%2C%60%600%2C%60%601%2C%60%602%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName> \</IAsyncResult, TResult> \</TArg1, TArg2, TArg3, AsyncCallback, Object, IAsyncResult> \</TArg1, TArg2, TArg3, TResult>|  
|Analizzatori|CD0058|  
  
<a name="diagnostic59"></a>   
## <a name="59-log-file-name-created-by-the-objectcontextcreatedatabase-method-has-changed-to-match-sql-server-specifications"></a>59: nome di file di log creati dal metodo ObjectContext.CreateDatabase è stato modificato in modo che corrisponda alle specifiche di SQL Server  
  
|||  
|-|-|  
|Dettagli|Quando il metodo CreateDatabase viene richiamato direttamente o tramite Code First con il provider SqlClient e un valore di AttachDBFilename nella stringa di connessione, viene creato un file di registro denominato filename_log.ldf anziché filename.ldf (in cui filename è il nome del file specificato dal valore di AttachDBFilename). Questa modifica migliora il debug fornendo un file di log il cui nome si basa sulle specifiche di SQL Server.|  
|Suggerimento|Se il nome di file di log è importante per un'applicazione, l'applicazione deve essere aggiornato in modo da prevedere il formato del nome file ldf standard.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Data.Objects.ObjectContext.CreateDatabase?displayProperty=fullName>|  
|Analizzatori|CD0059|  
  
<a name="diagnostic60"></a>   
## <a name="60-pageloadcomplete-event-no-longer-causes-systemwebuiwebcontrolsentitydatasource-control-to-invoke-data-binding"></a>60: evento Page.LoadComplete non, non è più controllo System.Web.UI.WebControls.EntityDataSource richiamare l'associazione dati  
  
|||  
|-|-|  
|Dettagli|Il `Page.LoadComplete` eventi non, non è più il controllo System.Web.UI.WebControls.EntityDataSource richiamare l'associazione dati per le modifiche ai parametri di creazione/aggiornamento/eliminazione. Questa modifica elimina un accesso estraneo al database, impedisce che i valori dei controlli reimpostazione e genera un comportamento è coerenza con altri controlli di dati, come SqlDataSource e ObjectDataSource. Questa modifica determina un comportamento diverso nel caso improbabile in cui le applicazioni si affidino al richiamo dell'associazione dati nell'evento `Page.LoadComplete`.|  
|Suggerimento|Se è necessario per l'associazione dati, richiamare manualmente databind in un evento di postback riportato in precedenza.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0060|  
  
<a name="diagnostic61"></a>   
## <a name="61-webutilityhtmldecode-no-longer-decodes-invalid-input-sequences"></a>61: WebUtility.HtmlDecode non decodifica non è più sequenze di input non valide  
  
|||  
|-|-|  
|Dettagli|Per impostazione predefinita, i metodi di decodifica non decodificano più una sequenza di input non valido in una stringa UTF-16 non valida. Al contrario, viene restituito l'input originale.|  
|Suggerimento|La modifica dell'output del decodificatore è importante solo se si archiviano dati binari anziché dati UTF-16 nelle stringhe. Per controllare in modo esplicito questo comportamento, impostare il `aspnet:AllowRelaxedUnicodeDecoding` dell'attributo di [appSettings](https://msdn.microsoft.com/en-us/library/ms228154\(v=vs.110\).aspx) elemento su true per abilitare il comportamento legacy o su false per abilitare il comportamento corrente.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Net.WebUtility.HtmlDecode%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Net.WebUtility.HtmlDecode%28System.String%2CSystem.IO.TextWriter%29?displayProperty=fullName><br /><br /> <xref:System.Net.WebUtility.UrlDecode%28System.String%29?displayProperty=fullName>|  
|Analizzatori|CD0061|  
  
<a name="diagnostic63"></a>   
## <a name="63-apps-published-with-clickonce-that-use-a-sha-256-code-signing-certificate-may-fail-on-windows-2003"></a>63: le applicazioni pubblicate con ClickOnce che usano un certificato di firma del codice SHA-256 potrebbero avere esito negativo in Windows 2003  
  
|||  
|-|-|  
|Dettagli|Il file eseguibile è firmato con SHA256. In precedenza, veniva firmato con SHA1 indipendentemente dal fatto che il certificato di firma del codice fosse SHA-1 o SHA-256. Si applica a:<br /><br /> Tutte le applicazioni compilate con Visual Studio 2012 o versioni successive.<br /><br /> Applicazioni compilate con Visual Studio 2010 o versioni precedenti su sistemi in cui è presente .NET Framework 4.5.<br /><br /> Se inoltre è presente .NET Framework 4.5 o versione successiva, il manifesto ClickOnce viene firmato anche con SHA-256 per i certificati SHA-256 indipendentemente dalla versione di .NET Framework per cui è stato compilato.|  
|Suggerimento|La modifica firma il file eseguibile di ClickOnce interessa solo i sistemi Windows Server 2003; essi richiedono l'installazione di 938397 KB.<br /><br /> La modifica relativa alla firma del manifesto con SHA-256 anche quando un'app è destinata a .NET Framework 4.0 o a versioni precedenti introduce una dipendenza del runtime da .NET Framework 4.5 o da una versione successiva.|  
|Ambito|Microsoft Edge|  
|Versione|4.5-4.6|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0063|  
  
<a name="diagnostic68"></a>   
## <a name="68-dbparameterprecision-and-dbparameterscale-are-now-public-virtual-members"></a>68: DbParameter.Precision e DbParameter.Scale sono ora membri virtuali pubblici  
  
|||  
|-|-|  
|Dettagli|DbParameter.Precision e DbParameter.Scale vengono implementate come proprietà virtuali pubbliche. Sostituiscono le corrispondenti implementazioni esplicite dell'interfaccia, DbParameter.IDbDataParameter.Precision e DbParameter.IDbDataParameter.Scale.|  
|Suggerimento|Quando si compila nuovamente un provider di database ADO.NET, queste differenze richiederà la parola chiave 'override' da applicare alle proprietà di precisione e scala. Questo è necessario solo quando si compila nuovamente i componenti. i file binari esistenti continueranno a funzionare.|  
|Ambito|Secondario|  
|Versione|4.5.1|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Data.Common.DbParameter.Precision?displayProperty=fullName><br /><br /> <xref:System.Data.Common.DbParameter.Scale?displayProperty=fullName>|  
|Analizzatori|CD0068|  
  
<a name="diagnostic73"></a>   
## <a name="73-dataobjectgetdata-now-retrieves-data-as-utf-8"></a>73: DataObject.GetData ora recupera i dati come UTF-8  
  
|||  
|-|-|  
|Dettagli|Per le applicazioni destinate a .NET Framework 4 o in esecuzione su .NET Framework 4.5.1 o versioni precedenti, DataObject.GetData recupera dati in formato HTML come una stringa ASCII. Di conseguenza, i caratteri non ASCII, ovvero quelli i cui codici ASCII sono maggiori di 0x7F, vengono rappresentati da due caratteri casuali.<br /><br /> Per le applicazioni destinate a .NET Framework 4.5 o versione successivo ed eseguite in .NET Framework 4.5.2, `DataObject.GetData` recupera dati in formato HTML come UTF-8, che rappresenta correttamente i caratteri maggiori di 0x7F.|  
|Suggerimento|Se è implementata una soluzione alternativa per il problema di codifica con le stringhe in formato HTML (ad esempio codificando in modo esplicito la stringa HTML recuperata dagli Appunti passandola al metodo UTF8Encoding.GetString) e si intende adattare l'app dalla versione 4 di 4.5, è necessario rimuovere questa soluzione alternativa.<br /><br /> Se per qualche motivo, è necessario il comportamento precedente, l'applicazione può destinate a .NET Framework 4.0 per ottenere tale comportamento.|  
|Ambito|Microsoft Edge|  
|Versione|4.5.2|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Windows.DataObject.GetData%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Windows.DataObject.GetData%28System.String%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Windows.DataObject.GetData%28System.Type%29?displayProperty=fullName>|  
|Analizzatori|CD0073|  
  
<a name="diagnostic75"></a>   
## <a name="75-targetframeworkname-for-default-app-domain-no-longer-defaults-to-null-if-not-set"></a>75: TargetFrameworkName per dominio applicazione predefinito non è più predefinita è null se non impostato  
  
|||  
|-|-|  
|Dettagli|Il TargetFrameworkName è stata precedentemente null nel dominio applicazione predefinito, a meno che non è stata impostata in modo esplicito. A partire da 4.6, la proprietà TargetFrameworkName per il dominio applicazione predefinito avrà un valore predefinito derivato da TargetFrameworkAttribute (se presente). Domini applicazione non predefinito continuerà a ereditano le TargetFrameworkName dal dominio applicazione predefinito (che non predefinito su null in 4.6), a meno che non sia sottoposto a override in modo esplicito.|  
|Suggerimento|Codice deve essere aggiornato in modo non dipendono `AppDomainSetup.TargetFrameworkName` l'impostazione su null. Se è necessario che questa proprietà continua a restituire null, è possibile configurare esplicitamente a tale valore.|  
|Ambito|Microsoft Edge|  
|Versione|4.6|  
|Tipo|Runtime|  
|API interessate|<xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=fullName>|  
|Analizzatori|CD0075B<br /><br /> CD0075A|  
  
<a name="diagnostic76"></a>   
## <a name="76-x509certificate2tostringbool-does-not-throw-now-when-net-cannot-handle-the-certificate"></a>76: X509Certificate2.ToString(bool) non genera ora quando .NET non può gestire il certificato  
  
|||  
|-|-|  
|Dettagli|In precedenza, questo metodo genera se 'true' è stato passato per il parametro verbose e sono stati installati certificati che non sono supportate da .net Framework. A questo punto, il metodo abbia esito positivo e restituire una stringa valida che omette le parti inaccessibile di certifiate.|  
|Suggerimento|Qualsiasi codice in base X509Certificate2.ToString(bool) deve essere aggiornato in modo da prevedere che la stringa restituita può escludere alcuni dati del certificato (ad esempio la chiave pubblica, la chiave privata ed estensioni) in alcuni casi in cui l'API avrebbe precedentemente generato.|  
|Ambito|Microsoft Edge|  
|Versione|4.6|  
|Tipo|Runtime|  
|API interessate|<xref:System.Security.Cryptography.X509Certificates.X509Certificate2.ToString%28System.Boolean%29?displayProperty=fullName>|  
|Analizzatori|CD0076|  
  
<a name="diagnostic77"></a>   
## <a name="77-reflection-objects-can-no-longer-be-passed-from-managed-code-to-out-of-process-dcom-clients"></a>77: gli oggetti di reflection non possono essere passati dal codice gestito ai client DCOM out-of-process  
  
|||  
|-|-|  
|Dettagli|Gli oggetti di reflection non possono essere più passati dal codice gestito ai client DCOM out-of-process. Sono interessati i tipi seguenti:<br /><br /> Assembly<br /><br /> MemberInfo (e i tipi derivati, tra cui FieldInfo MethodInfo, tipo e TypeInfo)<br /><br /> MethodBody<br /><br /> Modulo<br /><br /> ParameterInfo.<br /><br /> Le chiamate a `IMarshal` per l'oggetto restituito `E_NOINTERFACE`.|  
|Suggerimento|Aggiornare il codice di marshalling per lavorare con gli oggetti di reflection non|  
|Ambito|Secondario|  
|Versione|4.6|  
|Tipo|Runtime|  
|Analizzatori|CD0077|  
  
<a name="diagnostic78"></a>   
## <a name="78-contentdisposition-datetimes-returns-slightly-different-string"></a>78: ContentDisposition DateTimes restituisce stringhe leggermente diversi  
  
|||  
|-|-|  
|Dettagli|Rappresentazioni di stringa di ContentDispositions sono state aggiornate, a partire da 4.6, per rappresentare sempre il componente ore della data e ora con due cifre. Si tratta di rispettare [RFC822](http://www.ietf.org/rfc/rfc0822.txt) e [RFC2822](http://www.ietf.org/rfc/rfc2822.txt). In questo modo `ContentDisposition.ToString` per restituire una stringa leggermente diversa in 4.6 negli scenari in cui uno degli elementi di tempo della disposizione precedeva 10:00 AM. Si noti che ContentDispositions talvolta vengono serializzati tramite convertendoli in stringhe, pertanto è necessario esaminare eventuali operazioni ContentDisposition ToString, serializzazione o chiamate GetHashCode.|  
|Suggerimento|Non si prevede che le rappresentazioni di stringa di ContentDispositions da diverse versioni di .NET Framework confronterà correttamente tra loro. Convertire le stringhe al ContentDispositions, se possibile, prima di eseguire un confronto.|  
|Ambito|Secondario|  
|Versione|4.6|  
|Tipo|Runtime|  
|API interessate|<xref:System.Net.Mime.ContentDisposition.GetHashCode?displayProperty=fullName><br /><br /> <xref:System.Net.Mime.ContentDisposition.ToString?displayProperty=fullName>|  
|Analizzatori|CD0078|  
  
<a name="diagnostic82"></a>   
## <a name="82-workflowdesignerload-doesnt-remove-symbol-property"></a>82: WorkflowDesigner.Load non rimuovere proprietà simbolo  
  
|||  
|-|-|  
|Dettagli|Se la destinazione di .NET Framework 4.5 in Progettazione flussi di lavoro e il caricamento di un flusso di lavoro 3.5 rieseguito nell'host con il metodo WorkflowDesigner.Load(), viene generata una XamlDuplicateMemberException durante il salvataggio del flusso di lavoro.|  
|Suggerimento|Questo bug si manifesta solo quando la destinazione di .NET Framework 4.5 nella finestra di progettazione del flusso di lavoro, pertanto è possibile evitarlo impostando il `WorkflowDesigner.Context.Services.GetService<DesignerConfigurationService>().TargetFrameworkName` a .NET Framework 4.0.<br /><br /> In alternativa, il problema potrebbe essere evitato utilizzando il [WorkflowContext.Load(string)](https://msdn.microsoft.com/en-us/library/ee425926\(v=vs.110\).aspx) per caricare il flusso di lavoro, anziché [WorkflowDesigner.Load()](https://msdn.microsoft.com/en-us/library/ee403482\(v=vs.110\).aspx).|  
|Ambito|Principale|  
|Versione|4.5-4.5.2|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Activities.Presentation.WorkflowDesigner.Load?displayProperty=fullName>|  
|Analizzatori|CD0082|  
  
<a name="diagnostic83"></a>   
## <a name="83-sqlconnectionopen-fails-on-windows-7-with-non-ifs-winsock-bsp-or-lsp-present"></a>83: SqlConnection.Open ha esito negativo in Windows 7 con LSP presente o non IFS Winsock BSP  
  
|||  
|-|-|  
|Dettagli|SqlConneciton.Open e OpenAsync non riuscire in .NET Framework 4.5 se in esecuzione in un computer Windows 7 con un LSP non IFS Winsock BSP sono presenti nel computer.<br /><br /> Per determinare se è installato un non - IFS BSP o LSP, utilizzare il `netsh WinSock Show Catalog` comando ed esaminare ogni `Winsock Catalog Provider Entry` elemento restituito. Se il valore dei flag del servizio è il `0x20000` bit impostato, il provider utilizza gli handle IFS e funzionerà correttamente. Se il `0x20000` bit è chiaro (non impostato), è un non - IFS BSP o LSP.|  
|Suggerimento|Questo bug è stato risolto in .NET Framework 4.5.2, pertanto può essere evitata eseguendo l'aggiornamento di .NET Framework. In alternativa, è possibile evitare rimuovendo qualsiasi installato LSP Winsock di non - IFS.|  
|Ambito|Secondario|  
|Versione|4.5-4.5.2|  
|Tipo|Runtime|  
|API interessate|<xref:System.Data.SqlClient.SqlConnection.Open?displayProperty=fullName><br /><br /> <xref:System.Data.SqlClient.SqlConnection.OpenAsync%28System.Threading.CancellationToken%29?displayProperty=fullName>|  
|Analizzatori|CD0083|  
  
<a name="diagnostic84"></a>   
## <a name="84-icommandcanexecutechanged-event-behaviour-changed-in-net-45"></a>84: comportamento evento ICommand.CanExecuteChanged modificato in .NET 4.5  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4.5, un CanExecuteChangedEvent è stata ignorata a meno che il mittente dell'evento sia lo stesso oggetto dell'oggetto che ha generato l'evento. Questo bug è stato risolto in .NET Framework 4.5 servcing aggiornamenti.|  
|Suggerimento|Questo bug è stato risolto in .NET Framework 4.5 Service Release, pertanto può essere evitato assicurandosi che .NET Framework è aggiornato o eseguendo l'aggiornamento a .NET Framework 4.5.1. In alternativa, è possibile modificare il codice dell'applicazione utilizzando ICommand per assicurarsi che il mittente quando viene generato un comando di CanExecuteChanged è lo stesso oggetto che genera l'evento.|  
|Ambito|Secondario|  
|Versione|4.5-4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Input.ICommand.CanExecuteChanged?displayProperty=fullName>|  
|Analizzatori|CD0084|  
  
<a name="diagnostic85"></a>   
## <a name="85-some-net-apis-cause-first-chance-handled-entrypointnotfoundexceptions"></a>85: alcune API di .NET che per primi (gestito) EntryPointNotFoundExceptions  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4.5, un numero ridotto di metodi .NET ha iniziato a generare EntryPointNotFoundExceptions per primi. Queste eccezioni sono state gestite all'interno di .net Framework, ma potrebbe interrompere l'automazione di test che non si aspettava di eccezioni first-chance. Queste stesse API interrompono alcuni scenari di ApiVerifier HighVersionLie è abilitata.|  
|Suggerimento|È possibile evitare questo problema eseguendo l'aggiornamento a .NET Framework 4.5.1. In alternativa, automazione di test può essere aggiornata per non interrompere l'esecuzione EntryPointNotFoundExceptions first-chance.|  
|Ambito|Microsoft Edge|  
|Versione|4.5-4.5.1|  
|Tipo|Runtime|  
|API interessate|<xref:System.Diagnostics.Debug.Assert%28System.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Diagnostics.Debug.Assert%28System.Boolean%2CSystem.String%29?displayProperty=fullName><br /><br /> <xref:System.Diagnostics.Debug.Assert%28System.Boolean%2CSystem.String%2CSystem.String%29?displayProperty=fullName><br /><br /> [Debug. Assert (Boolean, String, String, oggetto\<xref:System.Diagnostics.Debug.Assert%28System.Boolean%2CSystem.String%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%29?displayProperty=fullName>|  
|Analizzatori|CD0085|  
  
<a name="diagnostic86"></a>   
## <a name="86-scrolling-a-wpf-treeview-or-grouped-listbox-in-a-virtualizingstackpanel-can-cause-a-hang"></a>86: lo scorrimento di un controllo TreeView di WPF o ListBox raggruppati in un VirtualizingStackPanel può causare un blocco  
  
|||  
|-|-|  
|Dettagli|In v&4;.5 di .NET Framework, lo scorrimento di un controllo TreeView di WPF in un pannello stack virtualizzato può causare blocchi se sono presenti i margini nel riquadro di visualizzazione (tra gli elementi nella visualizzazione albero, ad esempio, o su un elemento ItemsPresenter). Inoltre, in alcuni casi, elementi di dimensioni diversi nella vista possono causare l'instabilità anche se sono non presenti margini.|  
|Suggerimento|È possibile evitare questo problema eseguendo l'aggiornamento a .NET Framework 4.5.1. In alternativa, i margini possono essere rimossa dalle raccolte di visualizzazione (ad esempio controlli TreeView) all'interno di pannelli stack virtualizzati se tutti gli elementi contenuti sono della stessa dimensione.|  
|Ambito|Principale|  
|Versione|4.5-4.5.1|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Controls.VirtualizingStackPanel.SetIsVirtualizing%28System.Windows.DependencyObject%2CSystem.Boolean%29?displayProperty=fullName>|  
|Analizzatori|CD0086<br /><br /> CD0086|  
  
<a name="diagnostic89"></a>   
## <a name="89-typeisassignablefrom-returns-wrong-result-for-generic-variables-with-constraints"></a>89: Type.IsAssignableFrom restituisce il risultato non corretto per le variabili generiche con vincoli  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4.5, in modo errato restituisce Type.IsAssignableFrom `false` in tutti i casi per alcuni tipi generici con vincoli.|  
|Suggerimento|Questo problema è stato risolto in un aggiornamento per la manutenzione. Aggiornare .NET Framework 4.5, o eseguire l'aggiornamento a .NET Framework 4.5.1 o versioni successive, per risolvere questo problema. In alternativa, evitare di utilizzare IsAssignableFrom con tipi generici che dispongono di vincoli sui parametri generici. API Reflection possono essere utilizzate come una soluzione alternativa.|  
|Ambito|Secondario|  
|Versione|4.5-4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Type.IsAssignableFrom%28System.Type%29?displayProperty=fullName>|  
|Analizzatori|CD0089<br /><br /> CD0089|  
  
<a name="diagnostic91"></a>   
## <a name="91-entityframework-60-loads-very-slowly-in-apps-launched-from-visual-studio"></a>91: EntityFramework 6.0 carica molto lentamente in App avviata da Visual Studio  
  
|||  
|-|-|  
|Dettagli|Avvia un'applicazione da Visual Studio 2013 che utilizza EntityFramework 6.0 può essere molto lenta.|  
|Suggerimento|Questo problema viene risolto in EntityFramework 6.0.2. Aggiornare EntityFramework per evitare il problema di prestazioni.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0091|  
  
<a name="diagnostic92"></a>   
## <a name="92-multi-line-aspnet-textbox-spacing-changed-when-using-antixssencoder"></a>92: spaziatura di ASP.Net multilinea modificato quando si utilizza AntiXSSEncoder  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4.0, altre righe inserite tra righe di una casella di testo su più righe durante il postback, se si utilizza il `AntiXSSEncoder`. In .NET Framework 4.5, tali le interruzioni di riga non sono inclusi, ma solo se l'applicazione web è destinato a .NET 4.5|  
|Suggerimento|Tenere presente che 4.0 App web a .NET 4.5 possono disporre le caselle di testo su più righe migliorate per non inserire le interruzioni di riga. Se non è auspicabile, l'applicazione può avere il comportamento precedente durante l'esecuzione in .NET Framework 4.5 destinate a .NET Framework 4.0.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0092|  
  
<a name="diagnostic95"></a>   
## <a name="95-concurrentqueuettrypeek-can-return-an-erroneous-null-via-its-out-parameter"></a>95: ConcurrentQueue<>\>. TryPeek può restituire un valore errato null tramite il parametro out  
  
|||  
|-|-|  
|Dettagli|In alcuni scenari a thread multipli, `ConcurentQueue<T>.TryPeek` può restituire true, ma popolare il parametro out con un valore null (anziché il valore corretto, visualizzato).|  
|Suggerimento|Questo problema viene risolto in .NET Framework 4.5.1. Per risolvere il problema, l'aggiornamento a tale Framework.|  
|Ambito|Principale|  
|Versione|4.5-4.5.1|  
|Tipo|Runtime|  
|API interessate|<xref:System.Collections.Concurrent.ConcurrentQueue%601.TryPeek%28%600%40%29?displayProperty=fullName>|  
|Analizzatori|CD0095|  
  
<a name="diagnostic98"></a>   
## <a name="98-multiple-items-in-a-single-tablelayoutpanel-cell-may-be-rearranged"></a>98: possono essere modificati più elementi in una singola cella di TableLayoutPanel  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4.5, se più elementi vengono inseriti nella stessa cella di TableLayoutPanel, potrebbe visualizzati in un ordine diverso rispetto alle .NET Framework 4.0.|  
|Suggerimento|Questo comportamento è stato ripristinato in un aggiornamento di manutenzione per .NET Framework 4.5. Aggiornare .NET Framework 4.5, o eseguire l'aggiornamento a .NET Framework 4.5.1 o versioni successive, per risolvere questo problema. In alternativa, evitare il caso di più elementi nella stessa cella TableLayourPanel ambiguo.|  
|Ambito|Secondario|  
|Versione|4.5-4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Forms.TableLayoutControlCollection.Add%28System.Windows.Forms.Control%2CSystem.Int32%2CSystem.Int32%29?displayProperty=fullName>|  
|Analizzatori|CD0098|  
  
<a name="diagnostic100"></a>   
## <a name="100-foreach-iterator-variable-is-now-scoped-within-the-iteration-so-closure-capturing-semantics-are-different-in-c5"></a>100: variabile di iteratore Foreach ambita all'interno dell'iterazione, pertanto la semantica di acquisizione di chiusura è diversa (in C#&5;)  
  
|||  
|-|-|  
|Dettagli|A partire da c# 5 (Visual Studio 2012), le variabili iteratore foreach sono limitate all'interno dell'iterazione. Ciò può provocare interruzioni se codice è stato in precedenza in base alle variabili non da includere nella chiusura del foreach. Il sintomo di questa modifica è che una variabile di iteratore passata a un delagate verrà considerata il valore al momento che il delegato è stato creato, anziché il valore al momento che è stato richiamato il delegato.|  
|Suggerimento|Idealmente, codice deve essere aggiornato in modo da prevedere il nuovo comportamento del compilatore. Se è richiesta la semantica precedente, la variabile di iteratore può essere sostituita con una variabile separata che viene inserita in modo esplicito all'ambito del ciclo esterno.|  
|Ambito|Principale|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0100|  
  
<a name="diagnostic101"></a>   
## <a name="101-htmltextwriter-does-not-render-br-element-correctly"></a>101: HtmlTextWriter non esegue il rendering\`<br>\>' elemento correttamente  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.6, chiamata `HtmlTextWriter.RenderBeginTag()` e `HtmlTextWriter.RenderEndTag()` con un `<BR />` elemento correttamente inserirà un solo `<BR />` (anziché due)|  
|Suggerimento|Se un'applicazione dipende da aggiuntivo `<BR />` tag, `HtmlTextWriter.RenderBeginTag()` deve essere chiamato una seconda volta. Si noti che modificare questo comportamento influisce solo sulle App destinate a .NET Framework 4.6, pertanto, un'altra opzione è una versione precedente di .NET Framework di destinazione per ottenere il comportamento precedente.|  
|Ambito|Microsoft Edge|  
|Versione|4.6|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Web.UI.HtmlTextWriter.RenderBeginTag%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Web.UI.HtmlTextWriter.RenderBeginTag%28System.Web.UI.HtmlTextWriterTag%29?displayProperty=fullName>|  
|Analizzatori|CD0101|  
  
<a name="diagnostic104"></a>   
## <a name="104-calling-itemsrefresh-on-a-wpf-listbox-listview-or-datagrid-with-items-selected-can-cause-duplicate-items-to-appear-in-the-element"></a>104: chiamata Items.Refresh su WPF ListBox, ListView o DataGrid con gli elementi selezionati possono causare voci duplicate nell'elemento  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4.5, chiamata ListBox.Items.Refresh dal codice, mentre gli elementi sono selezionati in un controllo ListBox può causare gli elementi selezionati essere duplicati nell'elenco. Si verifica un problema simile con ListView e DataGrid. Questo problema viene risolto in .NET Framework 4.6.|  
|Suggerimento|Questo problema potrebbe essere evitarlo a livello di codice se si deseleziona elementi prima che venga chiamato aggiornamento e quindi nuovamente selezionandole dopo il completamento della chiamata. In alternativa, questo problema è stato risolto in .NET Framework 4.6 e può essere indirizzato eseguendo l'aggiornamento a tale versione di .NET Framework.|  
|Ambito|Secondario|  
|Versione|4.5-4.6|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Data.CollectionView.Refresh?displayProperty=fullName>|  
|Analizzatori|CD0104|  
  
<a name="diagnostic105"></a>   
## <a name="105-etw-eventlisteners-do-not-capture-events-from-providers-with-explicit-keywords-like-the-tpl-provider"></a>105: EventListeners ETW non acquisire gli eventi dai provider con parole chiave esplicite (ad esempio, il provider TPL)  
  
|||  
|-|-|  
|Dettagli|ETW EventListeners con maschera di parola chiave vuota non acquisire correttamente gli eventi dai provider con parole chiave esplicite. In .NET Framework 4.5, il provider TPL iniziato fornendo le parole chiave esplicite e ha attivato questo problema. In .NET Framework 4.6 EventListeners sono stati aggiornati per non presentano il problema.|  
|Suggerimento|Per risolvere questo problema, sostituire le chiamate ai EnableEvents (eventSource, livello) con le chiamate all'overload che specifica in modo esplicito la maschera "le parole chiave" utilizzare EnableEvents: `EnableEvents(eventSource, level, unchecked((EventKeywords)0xFFFFffffFFFFffff))`.<br /><br /> In alternativa, questo problema è stato risolto in .NET Framework 4.6 e può essere indirizzato eseguendo l'aggiornamento a tale versione di .NET Framework.|  
|Ambito|Microsoft Edge|  
|Versione|4.5-4.6|  
|Tipo|Runtime|  
|API interessate|<xref:System.Diagnostics.Tracing.EventListener.EnableEvents%28System.Diagnostics.Tracing.EventSource%2CSystem.Diagnostics.Tracing.EventLevel%29?displayProperty=fullName>|  
|Analizzatori|CD0105|  
  
<a name="diagnostic109"></a>   
## <a name="109-building-an-entity-framework-edmx-with-visual-studio-2013-can-fail-with-error-msb4062-if-using-the-entitydeploysplit-or-entityclean-tasks"></a>109: creazione di un edmx di Entity Framework con Visual Studio 2013 può avere esito negativo con errore MSB4062 se utilizza le attività EntityDeploySplit o EntityClean  
  
|||  
|-|-|  
|Dettagli|Strumenti di MSBuild 12.0 (inclusi in Visual Studio 2013) modificare percorsi dei file msbuild, causando vecchi file di destinazioni di Entity Framework non è valido. Il risultato è che `EntityDeploySplit` e `EntityClean` attività esito negativo perché non sono in grado di trovare `Microsoft.Data.Entity.Build.Tasks.dll`. Si noti che questo tipo di interruzione a causa di una modifica del set di strumenti (msbuild/VS), non a causa di una modifica di .NET Framework. Si verificherà solo quando si aggiornano gli strumenti di sviluppo, non quando semplicemente l'aggiornamento di .NET Framework.|  
|Suggerimento|File di destinazioni di Entity Framework sono fisse per lavorare con il nuovo msbuild layout a partire da .NET Framework 4.6. Per correggere il problema, eseguire l'aggiornamento a tale versione di Framework. In alternativa, [questo](http://stackoverflow.com/a/24249247/131944) soluzione alternativa può essere utilizzato per applicare patch direttamente i file di destinazioni.|  
|Ambito|Principale|  
|Versione|4.5.1-4.6|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0109|  
  
<a name="diagnostic111"></a>   
## <a name="111-xsd-schema-validation-now-correctly-detects-violations-of-unique-constraints-if-compound-keys-are-used-and-one-key-is-empty"></a>111: la convalida dello Schema XSD viene ora rileva le violazioni di vincoli unique correttamente se vengono utilizzate le chiavi composte e una chiave è vuota  
  
|||  
|-|-|  
|Dettagli|Versioni di .NET Framework precedenti a 4.6 era presente un bug che causa la convalida XSD non rilevare vincoli univoci per le chiavi composte se una delle chiavi è vuota. In .NET Framework 4.6, questo problema viene risolto. Ciò comporterà la convalida più corretta, ma può anche comportare alcune XML non convalida che in precedenza sarebbe necessario.|  
|Suggerimento|Se più ampio, è necessario .NET Framework 4.0 convalida, l'applicazione convalida può utilizzare versione 4.5 (o versioni precedenti) di .NET Framework. Quando il passaggio a .NET 4.6, tuttavia, revisione del codice deve essere effettuata per assicurarsi che le chiavi composte duplicate, come descritto nella descrizione del problema, non possono convalidare.|  
|Ambito|Microsoft Edge|  
|Versione|4.6|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0111|  
  
<a name="diagnostic112"></a>   
## <a name="112-calling-attributegetcustomattributes-on-an-indexer-property-no-longer-throws-ambiguousmatchexception-if-the-ambiguity-can-be-resolved-by-indexs-type"></a>112: GetCustomAttributes chiamata su una proprietà dell'indicizzatore non genera più AmbiguousMatchException se è possibile risolvere l'ambiguità dal tipo di indice  
  
|||  
|-|-|  
|Dettagli|Prima di .NET Framework 4.6, chiamata `GetCustomAttribute(s)` in un indicizzatore proprietà che è diverso da un'altra proprietà solo per il tipo di indice comporta un `AmbiguousMatchException`. A partire da .NET Framework 4.6, gli attributi della proprietà verranno correttamente restituiti.|  
|Suggerimento|Tenere presente che GetCustomAttribute(s) il codice funzionerà più frequentemente. Se un'applicazione in precedenza si basava sul `AmbiguousMatchException`, reflection dovrebbe ora essere usata per cercare in modo esplicito più indicizzatori, al contrario.|  
|Ambito|Microsoft Edge|  
|Versione|4.6|  
|Tipo|Runtime|  
|API interessate|<xref:System.Attribute.GetCustomAttribute%28System.Reflection.MemberInfo%2CSystem.Type%29?displayProperty=fullName><br /><br /> <xref:System.Attribute.GetCustomAttribute%28System.Reflection.MemberInfo%2CSystem.Type%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Attribute.GetCustomAttributes%28System.Reflection.MemberInfo%29?displayProperty=fullName><br /><br /> <xref:System.Attribute.GetCustomAttributes%28System.Reflection.MemberInfo%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Attribute.GetCustomAttributes%28System.Reflection.MemberInfo%2CSystem.Type%29?displayProperty=fullName><br /><br /> <xref:System.Attribute.GetCustomAttributes%28System.Reflection.MemberInfo%2CSystem.Type%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttribute%28System.Reflection.MemberInfo%2CSystem.Type%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttribute%28System.Reflection.MemberInfo%2CSystem.Type%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttribute%60%601%28System.Reflection.MemberInfo%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttribute%60%601%28System.Reflection.MemberInfo%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttributes%28System.Reflection.MemberInfo%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttributes%28System.Reflection.MemberInfo%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttributes%28System.Reflection.MemberInfo%2CSystem.Type%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttributes%28System.Reflection.MemberInfo%2CSystem.Type%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttributes%60%601%28System.Reflection.MemberInfo%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttributes%60%601%28System.Reflection.MemberInfo%2CSystem.Boolean%29?displayProperty=fullName>|  
|Analizzatori|CD0112|  
  
<a name="diagnostic113"></a>   
## <a name="113-intermittently-unable-to-scroll-to-bottom-item-in-itemscontrols-like-listbox-and-datagrid-when-using-custom-datatemplates"></a>113: talvolta non è possibile scorrere fino all'elemento inferiore ItemsControls (come ListBox e DataGrid) quando si utilizza un DataTemplate personalizzato  
  
|||  
|-|-|  
|Dettagli|In alcuni casi, un bug in .NET Framework 4.5 provoca l'ItemsControls (come ListBox, ComboBox, DataGrid e così via) non scorrere fino al relativo elemento inferiore quando si utilizza un DataTemplate personalizzato. Se le barre di scorrimento viene tentata una seconda volta (dopo lo scorrimento di backup), funzionerà quindi.|  
|Suggerimento|Questo problema è stato risolto in .NET Framework 4.5.2 e può essere indirizzato eseguendo l'aggiornamento a tale versione (o versione successiva) di .NET Framework. In alternativa, gli utenti possono trascinare le barre di scorrimento per gli elementi finali di queste raccolte, ma potrebbero essere necessario provare due volte eseguire questa operazione correttamente.|  
|Ambito|Secondario|  
|Versione|4.5-4.5.2|  
|Tipo|Runtime|  
|Analizzatori|CD0113|  
  
<a name="diagnostic114"></a>   
## <a name="114-glyphruncomputeinkboundingbox-and-formattedtextextent-return-different-values-beginning-in-net-45"></a>114: GlyphRun.ComputeInkBoundingBox() e FormattedText.Extent restituiscono valori diversi a partire da .NET 4.5  
  
|||  
|-|-|  
|Dettagli|Sono stati apportati miglioramenti GlyphRun.ComputeInkBoundingBox() e FormattedText.Extent in .NET Framework 4.5 per risolvere i problemi in cui le finestre sono troppo piccole per i glifi contenuti in alcuni casi in .NET Framework 4.0. Di conseguenza, alcune finestre di delimitazione sarà maggiore a partire da .NET Framework 4.5, risultante in alcune differenze nel layout dell'interfaccia utente.|  
|Suggerimento|Tenere presente che alcune dimensioni di delimitazione glifo sono aumentati. Questi cambiamenti miglioreranno in genere presentazione e casella hit testing, ma se si desidera il precedente comportamento (pre-.NET 4.5), è scelto di aggiungendo la seguente voce al file app. config:<br /><br /> `<appsettings> <add key="IncludeAllInkInBoundingBox" value="false"> </appsettings>`|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Media.GlyphRun.ComputeInkBoundingBox?displayProperty=fullName><br /><br /> <xref:System.Windows.Media.FormattedText.Extent?displayProperty=fullName>|  
|Analizzatori|CD0114|  
  
<a name="diagnostic124"></a>   
## <a name="124-calling-datagridcommitedit-from-a-celleditending-handler-drops-focus"></a>124: DataGrid.CommitEdit chiamata da un gestore CellEditEnding Elimina lo stato attivo  
  
|||  
|-|-|  
|Dettagli|Chiamando DataGrid.CommitEdit da uno dei gestori di eventi CellEditEnding di DataGrid, al controllo DataGrid di perde lo stato attivo.|  
|Suggerimento|Questo bug è stato risolto in .NET Framework 4.5.2, pertanto può essere evitata eseguendo l'aggiornamento di .NET Framework. In alternativa, è possibile evitare selezionando in modo esplicito nuovamente DataGrid dopo la chiamata a CommitEdit.|  
|Ambito|Microsoft Edge|  
|Versione|4.5-4.5.2|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Controls.DataGrid.CommitEdit?displayProperty=fullName><br /><br /> <xref:System.Windows.Controls.DataGrid.CommitEdit%28System.Windows.Controls.DataGridEditingUnit%2CSystem.Boolean%29?displayProperty=fullName>|  
|Analizzatori|CD0124|  
  
<a name="diagnostic125"></a>   
## <a name="125-aspnet-mvc-now-escapes-spaces-in-strings-passed-in-via-route-parameters"></a>125: ASP.NET MVC, ora Ignora spazi nelle stringhe passate tramite i parametri di route  
  
|||  
|-|-|  
|Dettagli|Per la conformità allo standard RFC 2396, gli spazi nei percorsi di route ora escape durante il popolamento di parametri dell'azione da una route. Pertanto, mentre `/controller/action/some data` in precedenza sarebbe corrispondono alla route `/controller/action/{data}` e fornire `some data` come parametro di dati, viene ora fornita `some%20data` invece.|  
|Suggerimento|Codice deve essere aggiornato per unescape parametri della stringa da una route. Se è necessaria l'URI originale, è possibile accedervi con l'API Request.RequestUri.OriginalString.|  
|Ambito|Secondario|  
|Versione|4.5.2|  
|Tipo|Runtime|  
|API interessate|<xref:System.Web.Http.RouteAttribute.%23ctor%28System.String%29?displayProperty=fullName>|  
|Analizzatori|CD0125|  
  
<a name="diagnostic127"></a>   
## <a name="127-vbnet-no-longer-supports-partial-namespace-qualification-for-systemwindows-apis"></a>127: Visual Basic.NET non supporta più parziale dello spazio dei nomi qualifica a APIs System.Windows  
  
|||  
|-|-|  
|Dettagli|A partire da .NET 4.5.2, progetti di Visual Basic.NET non possono specificare System.Windows APIs con spazi dei nomi parzialmente qualificati. Ad esempio, che fa riferimento a `Windows.Forms.DialogResult` avrà esito negativo. Al contrario, codice deve fare riferimento al nome completo (`System.Windows.Forms.DialogResult`) o importare lo spazio dei nomi specifico e fare riferimento solo a `DialogResult`.|  
|Suggerimento|Codice deve essere aggiornato per fare riferimento a `System.Windows` API con semplici nomi (e importare lo spazio dei nomi rilevante) o con nomi completi.|  
|Ambito|Secondario|  
|Versione|4.5.2|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0127|  
  
<a name="diagnostic129"></a>   
## <a name="129-two-way-data-binding-to-a-property-with-a-non-public-setter-is-not-supported"></a>129: associazione dati bidirezionale a una proprietà con setter non pubblico non è supportato  
  
|||  
|-|-|  
|Dettagli|Il tentativo di associare i dati a una proprietà senza un setter pubblico non è mai stata uno scenario supportato. A partire da .NET Framework 4.5.1, questo scenario verrà generata un'eccezione InvalidOperationException. Si noti che la nuova eccezione verrà generata soltanto per le app destinate specificamente a .NET Framework 4.5.1. Se un'applicazione destinata a .NET Framework 4.5, la chiamata verrà consentita. Se l'app destinate a una particolare versione di .NET Framework, l'associazione verrà considerato come unidirezionale.|  
|Suggerimento|L'applicazione deve essere aggiornato per utilizzare l'associazione unidirezionale o espone pubblicamente il setter della proprietà. In alternativa, la destinazione di .NET Framework 4.5 comporterà l'applicazione può presentare il comportamento precedente.|  
|Ambito|Secondario|  
|Versione|4.5.1|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Windows.Data.BindingMode?displayProperty=fullName>|  
|Analizzatori|CD0129|  
  
<a name="diagnostic130"></a>   
## <a name="130-marshalsizeof-and-marshalptrtostructure-overloads-break-dynamic-code"></a>130: Marshal. sizeof e Marshal. PtrToStructure overload interruzione dinamica del codice  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.5.1, associazione dinamica per i metodi `Marshal.SizeOf` o `Marshal.PtrToStructure` , tramite Windows PowerShell, IronPython o la dinamica parola chiave c#, ad esempio, può comportare `MethodInvocationExceptions` perché sono stati aggiunti nuovi overload dei metodi seguenti che potrebbero risultare ambigui per i motori di script.|  
|Suggerimento|Aggiornare gli script per indicare chiaramente quali deve essere overload utilizzato. Questo può in genere eseguito in modo esplicito il cast di parametri di tipo i metodi come `System.Type`. Vedere [questo collegamento](https://support.microsoft.com/en-us/kb/2909958/) per ulteriori dettagli ed esempi per risolvere il problema.|  
|Ambito|Secondario|  
|Versione|4.5.1|  
|Tipo|Runtime|  
|Analizzatori|CD0130|  
  
<a name="diagnostic131"></a>   
## <a name="131-previewlostkeyboardfocus-is-called-repeatedly-if-its-handler-shows-a-windows-forms-message-box"></a>131: PreviewLostKeyboardFocus viene chiamato più volte se il gestore viene visualizzata una finestra di messaggio Windows Form  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.5, la chiamata a `System.Windows.Forms.MessageBox.Show` da un `UIElement.PreviewLostKeyboardFocus` gestore causerà il gestore venga nuovamente generato quando viene chiusa la finestra di messaggio, il risultato di un ciclo infinito di finestre di messaggio.|  
|Suggerimento|Sono disponibili due opzioni per risolvere questo problema:<br /><br /> Può essere evitato chiamando `System.Windows.MessageBox.Show` anziché `System.Windows.Forms.MessageBox.Show`.<br /><br /> Può essere evitato visualizzando la finestra di messaggio da un `LostKeyboardFocus` gestore dell'evento (in contrapposizione a un `PreviewLostKeyboardFocus` gestore eventi).|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.ContentElement.PreviewLostKeyboardFocus?displayProperty=fullName><br /><br /> <xref:System.Windows.IInputElement.PreviewLostKeyboardFocus?displayProperty=fullName><br /><br /> <xref:System.Windows.UIElement.PreviewLostKeyboardFocus?displayProperty=fullName><br /><br /> <xref:System.Windows.UIElement3D.PreviewLostKeyboardFocus?displayProperty=fullName>|  
|Analizzatori|CD0131|  
  
<a name="diagnostic133"></a>   
## <a name="133-a-concurrentdictionary-serialized-in-net-45-with-netdatacontractserializer-cannot-be-deserialized-by-net-451-or-452"></a>133: Impossibile deserializzare un oggetto ConcurrentDictionary serializzato in .NET 4.5 con NetDataContractSerializer da .NET 4.5.1 o 4.5.2  
  
|||  
|-|-|  
|Dettagli|A causa di modifiche interne al tipo di `System.Collections.Concurrent.ConcurrentDictionary` oggetti serializzati con .NET Framework 4.5 utilizzando il `NetDataContractSerializer` non può essere deserializzato in .NET Framework 4.5.1 o in .NET Framework 4.5.2.<br /><br /> Si noti che lo spostamento nella direzione opposta (serializzazione con .NET Framework 4.5.x e la deserializzazione con .NET Framework 4.5) funziona. Analogamente, tutta la serializzazione tra versioni 4. x funziona con .NET Framework 4.6.<br /><br /> La serializzazione e deserializzazione con una sola versione di .NET Framework non sono interessati.|  
|Suggerimento|Se è necessario serializzare e deserializzare un oggetto ConcurrentDictionary tra .NET Framework 4.5 e .NET Framework 4.5.1/4.5.2, utilizzare un serializzatore alternativo come il serializzatore DataContractSerializer o BinaryFormatter anziché di NetDataContractSerializer.<br /><br /> In alternativa, perché questo problema viene risolto in .NET Framework 4.6, potrebbero essere risolti eseguendo l'aggiornamento a tale versione di .NET Framework.|  
|Ambito|Secondario|  
|Versione|4.5.1-4.6|  
|Tipo|Runtime|  
|Analizzatori|CD0133|  
  
<a name="diagnostic134"></a>   
## <a name="134-persian-calendar-now-uses-the-hijri-solar-algorithm"></a>134: calendario persiano ora utilizza l'algoritmo solare Hijri  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.6, la classe PersianCalendar utilizza l'algoritmo solare Hijri. Convertire le date comprese tra il PersianCalendar e altri calendari può produrre un inizio risultati leggermente diverso con .NET Framework 4.6 per le date precedenti a 1800 o successive a quella 2023 (gregoriano).<br /><br /> Inoltre, `PersianCalendar.MinSupportedDateTime` è ora `March 22, 0622 instead of March 21, 0622`.|  
|Suggerimento|Tenere presente che alcune date anticipata o in ritardo potrebbero essere leggermente diverse quando si utilizza il PersianCalendar in .NET 4.6. Inoltre, quando si serializza le date comprese tra i processi che possono essere eseguite nelle diverse versioni di .NET Framework, non archiviarle come le stringhe di data PersianCalendar (poiché tali valori potrebbero essere diversi).|  
|Ambito|Secondario|  
|Versione|4.6|  
|Tipo|Runtime|  
|API interessate|<xref:System.Globalization.PersianCalendar?displayProperty=fullName>|  
|Analizzatori|CD0134|  
  
<a name="diagnostic138"></a>   
## <a name="138-calling-createdefaultauthorizationcontext-with-a-null-argument-has-changed"></a>138: CreateDefaultAuthorizationContext chiamata con un argomento null è stato modificato  
  
|||  
|-|-|  
|Dettagli|L'implementazione di AuthorizationContext restituito da una chiamata per il `CreateDefaultAuthorizationContext(IList<IAuthorizationPolicy>)` con un authorizationPolicies null argomento ha modificato la relativa implementazione in .NET Framework 4.6.|  
|Suggerimento|In rari casi, le app WCF che usano l'autenticazione personalizzata possono riscontrare differenze di comportamento. In questi casi, il comportamento precedente può essere ripristinato in uno dei due modi:<br /><br /> Ricompilare l'app per destinarla a una versione precedente rispetto a .NET Framework 4.6. Per i servizi ospitati in IIS, utilizzare il <httpRuntime targetframework="x.x"></httpRuntime> \> elemento da una versione precedente di .NET Framework di destinazione.<br /><br /> Aggiungere la riga seguente per il `<appSettings>` sezione del file app. config:`<add key="appContext.SetSwitch:Switch.System.IdentityModel.EnableCachedEmptyDefaultAuthorizationContext" value="true" />`|  
|Ambito|Secondario|  
|Versione|4.6|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.IdentityModel.Policy.AuthorizationContext.CreateDefaultAuthorizationContext%28System.Collections.Generic.IList%7BSystem.IdentityModel.Policy.IAuthorizationPolicy%7D%29?displayProperty=fullName>|  
|Analizzatori|CD0138|  
  
<a name="diagnostic141"></a>   
## <a name="141-wpf-treeviewitem-must-be-used-within-a-treeview"></a>141: TreeViewItem WPF devono essere utilizzati all'interno di un controllo TreeView  
  
|||  
|-|-|  
|Dettagli|È stata introdotta una modifica in 4.5 che limita l'utilizzo di elementi del controllo TreeViewItem all'esterno di un controllo TreeView. Questa situazione si manifesta nelle condizioni seguenti:<br /><br /> Elemento padre visivo dell'oggetto TreeViewItem non è un pannello. (Un oggetto TreeViewItem generato per un controllo TreeView disporrà di un pannello come elemento padre)<br /><br /> L'oggetto TreeViewItem è un discendente di un VirtualizingStackPanel che agisce come "host di elementi" per un controllo elenco (ListBox, DataGrid, ListView e così via). La virtualizzazione non desidera essere abilitati.<br /><br /> Il VirtualizingStackPanel è lo scorrimento elemento (`ScrollUnit="Item"`).<br /><br /> Qualcuno chiama `VirtualizingStackPanel.MakeVisible(v)` per scorrere un elemento `v` nella visualizzazione. Questa operazione può essere eseguita in modo esplicito o implicito in diversi modi. probabilmente la più comune modalità è semplicemente facendo clic su `v` assegnargli lo stato attivo.<br /><br /> La catena visual padre da `v` alle passate tramite l'oggetto TreeViewItem VirtualizingStackPanel.<br /><br /> In altre parole, questo si verifica quando un oggetto TreeViewItem viene utilizzato all'esterno di un controllo TreeView e l'utente fa clic su un discendente di TreeViewItem per visualizzarlo. Se l'oggetto TreeViewItem non ha attivabili discendenti, non verrà mai visualizzata questo problema. Un esempio di una situazione in cui questo viene raggiunto è quando un oggetto TreeViewItem è la radice di una classe DataTemplate.  Quando viene raggiunto questo problema, si verifica un'eccezione InvalidCastException che si verifica all'interno del framework WPF.|  
|Suggerimento|Un hotfix verrà resa disponibile per questo oggetto.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0141|  
  
<a name="diagnostic143"></a>   
## <a name="143-x509certificateclaimsetfindclaims-considers-all-claimtypes"></a>143: X509CertificateClaimSet.FindClaims considera ClaimType tutti  
  
|||  
|-|-|  
|Dettagli|Nelle applicazioni destinate a .NET Framework 4.6.1, se un X509 set di attestazioni viene inizializzato da un certificato con più voci DNS nel relativo campo SAN, il metodo FindClaims tenta di corrispondenza dell'argomento claimType con tutte le voci DNS.<br /><br /> Per le applicazioni destinate a versioni precedenti di .NET Framework, il metodo FindClaims tenta di corrispondenza dell'argomento claimType solo con l'ultima voce DNS.|  
|Suggerimento|Questa modifica influisce solo sulle applicazioni destinate a .NET Framework 4.6.1. Questa modifica potrebbe essere disabilitata (o abilitata se destinata pre-4.6.1) con il [DisableMultipleDNSEntries](https://msdn.microsoft.com/en-us/library/mt620030%28v=vs.110%29.aspx) opzione di compatibilità.|  
|Ambito|Secondario|  
|Versione|4.6.1|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%28System.String%2CSystem.String%29?displayProperty=fullName>|  
|Analizzatori|CD0143|  
  
<a name="diagnostic144"></a>   
## <a name="144-applicationfiltermessage-no-longer-throws-for-re-entrant-implementations-of-imessagefilterprefiltermessage"></a>144: Application.FilterMessage non genera più per le implementazioni rientrante IMessageFilter.PreFilterMessage  
  
|||  
|-|-|  
|Dettagli|.NET Framework precedenti alla 4.6.1, chiamata Application.FilterMessage con un IMessageFilter.PreFilterMessage quale denominato AddMessageFilter o RemoveMessageFilter (durante la chiamata anche DoEvents) provocherebbe una IndexOutOfRangeException.<br /><br /> A partire da applicazioni destinate a .NET Framework 4.6.1, questa eccezione non viene più generata e rientranti filtri come descritto in precedenza possono essere utilizzati.|  
|Suggerimento|Tenere presente che Application.FilterMessage non verrà generata per il comportamento IMessageFilter.PreFilterMessage rientrante descritto sopra. Questo influisce solo sulle applicazioni destinate a .NET Framework 4.6.1.<br /><br /> App destinate a .NET Framework 4.6.1 può rifiutare esplicitamente questa modifica (o le applicazioni possono partecipare destinazione Framework precedenti) utilizzando il [DontSupportReentrantFilterMessage](https://msdn.microsoft.com/en-us/library/mt620032%28v=vs.110%29.aspx) opzione di compatibilità.|  
|Ambito|Microsoft Edge|  
|Versione|4.6.1|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Windows.Forms.Application.FilterMessage%28System.Windows.Forms.Message%40%29?displayProperty=fullName>|  
|Analizzatori|CD0144|  
  
<a name="diagnostic145"></a>   
## <a name="145-currentculture-is-not-preserved-across-wpf-dispatcher-operations"></a>145: CurrentCulture non viene mantenuto tra le operazioni del Dispatcher di WPF  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.6, CurrentCulture e CurrentUICulture modifiche all'interno di un [Dispatcher](https://msdn.microsoft.com/en-us/library/system.windows.threading.dispatcher%28v=vs.110%29.aspx) andranno persi al termine dell'operazione del dispatcher. Analogamente, CurrentCulture e CurrentUICulture effettuate all'esterno di un'operazione di Dispatcher potrebbe non essere riflesse quando viene eseguita l'operazione.<br /><br /> Parlando in pratica, ciò significa che le modifiche di CurrentCulture e CurrentUICulture potrebbero non transitare tra callback UI WPF e altro codice in un'applicazione WPF.<br /><br /> Ciò è dovuto a una modifica in [ExecutionContext](https://msdn.microsoft.com/en-us/library/system.threading.executioncontext%28v=vs.110%29.aspx) che causa CurrentCulture e CurrentUICulture deve essere archiviata all'inizio di contesto di esecuzione con le applicazioni destinate a .NET Framework 4.6. Le operazioni del dispatcher WPF archiviano il contesto di esecuzione utilizzato per avviare l'operazione e ripristinare il contesto precedente al completamento dell'operazione. Poiché CurrentCulture e CurrentUICulture fanno ora parte di tale contesto, le modifiche all'interno di un'operazione di dispatcher non vengono mantenute all'esterno dell'operazione.|  
|Suggerimento|Le applicazioni interessate da questa modifica potrebbero aggirare il problema archiviazione CurrentCulture desiderato o CurrentUICulture in un campo e il controllo in tutte le operazioni di Dispatcher organi (inclusi i gestori di callback di evento dell'interfaccia utente) sono impostati i valori corretti CurrentCulture e CurrentUICulture. In alternativa, in quanto l'ExecutionContext modificare sottostante questa modifica WPF influisce solo sulle App destinate a .NET Framework 4.6 o versione successiva, questa interruzione può essere evitato mediante destinati a .NET Framework 4.5.2.|  
|Ambito|Secondario|  
|Versione|4.6|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0145|