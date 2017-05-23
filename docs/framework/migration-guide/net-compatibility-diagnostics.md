---
title: .NET Compatibility Diagnostics | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5e481270-b62a-4cb4-8dda-5b4c5b59d61d
caps.latest.revision: 7
author: twsouthwick
ms.author: tasou
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 19006cc5f24ffc66b92e53e8174c6bd33c249679
ms.openlocfilehash: 06ebf87e02c8fd745d9c2f3a55eca329323a7d91
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="net-compatibility-diagnostics"></a>.NET Compatibility Diagnostics
.NET Compatibility Diagnostics include analizzatori basati su Roslyn che consentono di identificare problemi di compatibilità delle applicazioni tra versioni diverse di .NET Framework. Questo elenco contiene tutti gli analizzatori disponibili, anche se solo un subset sarà applicabile a ogni specifica migrazione. Saranno gli analizzatori a determinare i problemi applicabili alla migrazione pianificata e a segnalare solo quelli. Per un elenco dei problemi suddivisi in base alle versioni interessate, vedere [Compatibilità delle applicazioni](../../../docs/framework/migration-guide/application-compatibility.md).  
  
 Per ogni problema sono incluse le informazioni seguenti:  
  
-   Descrizione delle modifiche rispetto a una versione precedente.  
  
-   Il suggerimento è una descrizione degli effetti della modifica sui clienti e indica se sono disponibili eventuali soluzioni per mantenere la compatibilità tra versioni diverse.  
  
-   Valutazione dell'importanza della modifica. I problemi di compatibilità delle applicazioni sono classificati come segue:  
  
    |||  
    |-|-|  
    |Principale|Una modifica significativa che influisce su un numero elevato di app o che richiede variazioni sostanziali del codice.|  
    |Secondario|Una modifica che influisce su un numero ridotto di app o che richiede variazioni marginali del codice.|  
    |Caso limite|Una modifica che influisce sulle app in scenari molto specifici e non comuni.|  
    |Trasparente|Una modifica senza effetti evidenti sullo sviluppatore o sull'utente dell'applicazione.|  
  
-   La versione indica quando la modifica è comparsa per la prima volta nel framework. Alcune delle modifiche vengono annullate e anche questa situazione è indicata.  
  
-   Tipo di modifica:  
  
    |||  
    |-|-|  
    |Ridestinazione|La modifica influisce sulle app ricompilate per una nuova versione di .NET Framework.|  
    |Runtime|La modifica influisce su un'app esistente destinata a una versione precedente di .NET Framework, ma che viene eseguita su una versione successiva.|  
  
-   Le eventuali API interessate.  
  
-   ID delle diagnostiche disponibili  
  
<a name="diagnostic1"></a>   
## <a name="1-soapformatter-cannot-deserialize-hashtable-and-similar-ordered-collection-objects"></a>1: SoapFormatter cannot deserialize Hashtable and similar ordered collection objects  
  
|||  
|-|-|  
|Dettagli|SoapFormatter non garantisce che gli oggetti serializzati nell'ambito di una versione di .NET Framework possano essere deserializzati correttamente in una versione diversa. In particolare, in alcune raccolte ordinate, come Hashtable, sono stati aggiunti membri tra le versioni 4.0 e 4.5 e ne consegue che questi oggetti non possono essere deserializzati con .NET 4.0 se vengono serializzati con .NET 4.5. Si noti che, se i dati serializzati vengono sia serializzati che deserializzati con la stessa versione di .NET Framework, non si verificherà alcun problema.|  
|Suggerimento|La serializzazione SoapFormatter deve essere sostituita con la serializzazione BinaryFormatter o con NetDataContractSerialization per evitare effetti in caso di modifiche di .NET Framework.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter.Deserialize%28System.IO.Stream%29?displayProperty=fullName><br /><br /> <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter.Deserialize%28System.IO.Stream%2CSystem.Runtime.Remoting.Messaging.HeaderHandler%29?displayProperty=fullName><br /><br /> <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter.Serialize%28System.IO.Stream%2CSystem.Object%29?displayProperty=fullName><br /><br /> <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter.Serialize%28System.IO.Stream%2CSystem.Object%2CSystem.Runtime.Remoting.Messaging.Header%5B%5D%29?displayProperty=fullName>|  
|Analizzatori|CD0001B<br /><br /> CD0001A|  
  
<a name="diagnostic3"></a>   
## <a name="3-wpf-datatemplate-elements-are-now-visible-to-uia"></a>3: WPF DataTemplate elements are now visible to UIA  
  
|||  
|-|-|  
|Dettagli|Gli elementi DataTemplate erano in precedenza invisibili per Automazione interfaccia utente. A partire dalla versione 4.5, Automazione interfaccia utente rileva questi elementi. Questo è utile in molti casi, ma potrebbe causare problemi per i test che dipendono da alberi di automazione interfaccia utente che non contengono elementi DataTemplate.|  
|Suggerimento|Potrebbe essere necessario aggiornare i test di Automazione interfaccia utente per questa app per tenere conto dell'albero di automazione interfaccia utente che ora include elementi DataTemplate precedentemente invisibili. Ad esempio, nei test che prevedono che alcuni elementi siano adiacenti può essere ora necessario prevedere che possono infrapporsi elementi di Automazione interfaccia utente precedentemente invisibili. Oppure, potrebbe essere necessario aggiornare con nuovi valori i test che si basano su conteggi o indici specifici per gli elementi di Automazione interfaccia utente.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.DataTemplate.%23ctor?displayProperty=fullName><br /><br /> <xref:System.Windows.DataTemplate.%23ctor%28System.Object%29?displayProperty=fullName>|  
|Analizzatori|CD0003|  
  
<a name="diagnostic4"></a>   
## <a name="4-wpf-textbox-selected-text-appears-a-different-color-when-the-text-box-is-inactive"></a>4: WPF TextBox selected text appears a different color when the text box is inactive  
  
|||  
|-|-|  
|Dettagli|In .NET 4.5, se un controllo casella di testo WPF è inattivo (non ha lo stato attivo), il testo selezionato nella casella verrà visualizzato con un colore diverso rispetto a quando il controllo è attivo.|  
|Suggerimento|È possibile ripristinare il comportamento precedente (.NET 4.0) impostando la proprietà [FrameworkCompatibilityPreferences.AreInactiveSelectionHighlightBrushKeysSupported](https://msdn.microsoft.com/library/system.windows.frameworkcompatibilitypreferences.areinactiveselectionhighlightbrushkeyssupported\(v=vs.110\).aspx) su false.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Controls.TextBox?displayProperty=fullName>|  
|Analizzatori|CD0004|  
  
<a name="diagnostic5"></a>   
## <a name="5-listtforeach-can-throw-exception-when-modifying-list-item"></a>5: List\<T>.ForEach can throw exception when modifying list item  
  
|||  
|-|-|  
|Dettagli|A partire da .NET 4.5, un enumeratore `List<T>.ForEach` genererà un'eccezione InvalidOperationException in caso di modifica di un elemento nella raccolta chiamante. Nelle versioni precedenti questa condizione non genera un'eccezione ma può causare situazioni di race condition.|  
|Suggerimento|Idealmente, il codice dovrebbe essere corretto per evitare la modifica degli elenchi durante l'enumerazione dei relativi elementi, perché questa non è mai un'operazione sicura. Per ripristinare il comportamento precedente, tuttavia, un'app può essere destinata a .NET 4.0.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Collections.Generic.List%601.ForEach%28System.Action%7B%600%7D%29?displayProperty=fullName>|  
|Analizzatori|CD0005|  
  
<a name="diagnostic6"></a>   
## <a name="6-systemuri-parsing-adheres-to-rfc-3987"></a>6: System.Uri parsing adheres to RFC 3987  
  
|||  
|-|-|  
|Dettagli|L'analisi URI ha subito vari cambiamenti in .NET 4.5. Si noti, tuttavia, che queste modifiche influiscono solo sul codice destinato a .NET 4.5. Se un file binario è destinato a .NET 4.0, verrà rispettato il comportamento precedente. Le modifiche introdotte per l'analisi URI in .NET 4.5 includono:<br /><br /> L'analisi URI eseguirà la normalizzazione e il controllo dei caratteri in base alle regole IRI più recenti nella specifica RFC 3987<br /><br /> Il formato di normalizzazione Unicode C verrà applicato solo alla parte host dell'URI<br /><br /> Gli URI mailto: non validi causeranno ora un'eccezione<br /><br /> I punti finali alla fine di un segmento di percorso vengono ora mantenuti<br /><br /> Negli URI `file://` non viene usato un codice di escape per il carattere `?`<br /><br /> I caratteri di controllo Unicode da `U+0080` a `U+009F` non sono supportati<br /><br /> Per i caratteri virgola `,` o `%2c` non viene rimosso automaticamente il codice di escape|  
|Suggerimento|Se la semantica di analisi URI di .NET 4.0 precedente è ancora necessaria, anche se spesso non lo è, è possibile usarla scegliendo .NET 4.0 come destinazione. A tale scopo è possibile usare un TargetFrameworkAttribute nell'assembly o l'interfaccia utente del sistema di progetti di Visual Studio nella pagina delle proprietà del progetto.|  
|Ambito|Principale|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Uri.%23ctor%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Uri.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Uri.%23ctor%28System.String%2CSystem.UriKind%29?displayProperty=fullName><br /><br /> <xref:System.Uri.%23ctor%28System.Uri%2CSystem.String%29?displayProperty=fullName><br /><br /> <xref:System.Uri.TryCreate%28System.String%2CSystem.UriKind%2CSystem.Uri%40%29?displayProperty=fullName><br /><br /> <xref:System.Uri.TryCreate%28System.Uri%2CSystem.String%2CSystem.Uri%40%29?displayProperty=fullName><br /><br /> <xref:System.Uri.TryCreate%28System.Uri%2CSystem.Uri%2CSystem.Uri%40%29?displayProperty=fullName>|  
|Analizzatori|CD0006D<br /><br /> CD0006C<br /><br /> CD0006F<br /><br /> CD0006E<br /><br /> CD0006A<br /><br /> CD0006G<br /><br /> CD0006B|  
  
<a name="diagnostic10"></a>   
## <a name="10-systemuri-escaping-now-supports-rfc-3986-httptoolsietforghtmlrfc3986"></a>10: System.Uri escaping now supports RFC 3986 (http://tools.ietf.org/html/rfc3986)  
  
|||  
|-|-|  
|Dettagli|La funzionalità di escape URI è stata modificata in .NET 4.5 per supportare la specifica [RFC 3986](http://tools.ietf.org/html/rfc3986). Le modifiche specifiche includono:<br /><br /> Tramite il metodo `EscapeDataString` viene effettuato l'escape dei caratteri riservati basati su RFC 3986.<br /><br /> Tramite il metodo `EscapeUriString` non viene effettuato l'escape dei caratteri riservati.<br /><br /> `UnescapeDataString` non genera un'eccezione se rileva una sequenza di escape non valida.<br /><br /> I caratteri di escape non riservati non sono sottoposti a escape.|  
|Suggerimento|Aggiornare le applicazioni in modo che non si basino sul fatto che UnescapeDataString generi un'eccezione in presenza di una sequenza di escape non valida. Queste sequenze devono ora essere rilevate direttamente.<br /><br /> Allo stesso modo, prevedere che gli URI e le stringhe di dati con e senza codice di escape possano variare da .NET 4.0 a .NET 4.5 ed evitare confronti diretti tra versioni diverse di .NET. Questi elementi devono essere invece analizzati e normalizzati in una singola versione di .NET prima di eseguire eventuali confronti.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Uri.EscapeDataString%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Uri.EscapeUriString%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Uri.UnescapeDataString%28System.String%29?displayProperty=fullName>|  
|Analizzatori|CD0010A<br /><br /> CD0010B<br /><br /> CD0010C|  
  
<a name="diagnostic11"></a>   
## <a name="11-systemnetpeertopeercollaboration-unavailable-on-windows-8"></a>11: System.Net.PeerToPeer.Collaboration unavailable on Windows 8  
  
|||  
|-|-|  
|Dettagli|Lo spazio dei nomi System.Net.PeerToPeer.Collaboration non è disponibile in Windows 8 o versioni successive.|  
|Suggerimento|Le app che supportano Windows 8 o versioni successive devono essere aggiornate in modo da non dipendere da questo spazio dei nomi o i relativi membri.|  
|Ambito|Principale|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Net.PeerToPeer.Collaboration?displayProperty=fullName>|  
|Analizzatori|CD0011|  
  
<a name="diagnostic12"></a>   
## <a name="12-mef-catalogs-implement-ienumerable-and-therefore-can-no-longer-be-used-to-create-a-serializer"></a>12: MEF catalogs implement IEnumerable and therefore can no longer be used to create a serializer  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.5 i cataloghi MEF implementano IEnumerable e quindi non possono più essere usati per creare un serializzatore (oggetto XmlSerializer). Il tentativo di serializzare un catalogo MEF genera un'eccezione.|  
|Suggerimento|Non è più possibile usare MEF per creare un serializzatore|  
|Ambito|Principale|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0012|  
  
<a name="diagnostic13"></a>   
## <a name="13-missing-target-framework-moniker-results-in-40-behavior"></a>13: Missing Target Framework Moniker results in 4.0 behavior  
  
|||  
|-|-|  
|Dettagli|Le applicazioni senza un [TargetFrameworkAttribute](https://msdn.microsoft.com/library/system.runtime.versioning.targetframeworkattribute\(v=vs.110\).aspx) applicato a livello di assembly verranno eseguite automaticamente con la semantica (non standard) di .NET Framework 4.0. Per garantire un livello di qualità elevato, è consigliabile applicare a tutti i file binari in modo esplicito un TargetFrameworkAttribute che indica la versione di .NET Framework con cui sono stati compilati. Si noti che l'uso di un moniker del framework di destinazione in un file di progetto causerà l'applicazione automatica di un TargetFrameworkAttribute da MSBuild.|  
|Suggerimento|È consigliabile specificare un [attributo del framework di destinazione](https://msdn.microsoft.com/library/system.runtime.versioning.targetframeworkattribute\(v=vs.110\).aspx) aggiungendo direttamente l'attributo all'assembly oppure specificando un framework di destinazione nel [file di progetto o tramite l'interfaccia utente grafica delle proprietà del progetto di Visual Studio](http://blogs.msdn.com/b/visualstudio/archive/2010/05/19/visual-studio-managed-multi-targeting-part-1-concepts-target-framework-moniker-target-framework.aspx).|  
|Ambito|Principale|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0013|  
  
<a name="diagnostic14"></a>   
## <a name="14-no-longer-able-to-set-enableviewstatemac-to-false"></a>14: No longer able to set EnableViewStateMac to false  
  
|||  
|-|-|  
|Dettagli|ASP.NET non consente più agli sviluppatori di specificare `<pages enableViewStateMac="false"/>` o `<@Page EnableViewStateMac="false" %>`. L'algoritmo Message Authentication Code (MAC) dello stato di visualizzazione viene ora applicato per tutte le richieste con stato di visualizzazione incorporato. Riguarda solo le app che impostano in modo esplicito la proprietà EnableViewStateMac su false.|  
|Suggerimento|Partire dal presupposto che la proprietà EnableViewStateMac sia true e risolvere eventuali errori MAC risultanti, come spiegato in [queste](https://support.microsoft.com/kb/2915218) istruzioni che contengono più soluzioni in base alle cause specifiche degli errori MAC.|  
|Ambito|Principale|  
|Versione|4.5.2|  
|Tipo|Runtime|  
|Analizzatori|CD0014|  
  
<a name="diagnostic18"></a>   
## <a name="18-blockingcollectionttrytakefromany-does-not-throw-anymore"></a>18: BlockingCollection\<T>.TryTakeFromAny does not throw anymore  
  
|||  
|-|-|  
|Dettagli|Se una delle raccolte di input viene contrassegnata come completata, `BlockingCollection<T>.TryTakeFromAny(BlockingCollection<T>[], T)` non restituisce più -1 e `BlockingCollection<T>.TakeFromAny` non genera più un'eccezione. Tale modifica consente di usare le raccolte quando una di esse è vuota o completata, ma l'altra contiene ancora elementi che possono essere recuperati.|  
|Suggerimento|Se il metodo TryTakeFromAny con restituzione di -1 o con generazione di un'eccezione è stato usato per scopi di controllo di flusso in caso di completamento di una raccolta di blocco, tale codice deve ora essere modificato per usare `.Any(b => b.IsCompleted)` per rilevare tale condizione.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny%28System.Collections.Concurrent.BlockingCollection%7B%600%7D%5B%5D%2C%600%40%29?displayProperty=fullName><br /><br /> <xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny%28System.Collections.Concurrent.BlockingCollection%7B%600%7D%5B%5D%2C%600%40%2CSystem.Threading.CancellationToken%29?displayProperty=fullName><br /><br /> <xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny%28System.Collections.Concurrent.BlockingCollection%7B%600%7D%5B%5D%2C%600%40%29?displayProperty=fullName><br /><br /> <xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny%28System.Collections.Concurrent.BlockingCollection%7B%600%7D%5B%5D%2C%600%40%2CSystem.Int32%29?displayProperty=fullName><br /><br /> <xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny%28System.Collections.Concurrent.BlockingCollection%7B%600%7D%5B%5D%2C%600%40%2CSystem.TimeSpan%29?displayProperty=fullName>|  
|Analizzatori|CD0018A<br /><br /> CD0018B|  
  
<a name="diagnostic19"></a>   
## <a name="19-xmlschemaexception-now-sets-line-positions-properly"></a>19: XmlSchemaException now sets line positions properly  
  
|||  
|-|-|  
|Dettagli|Se il valore LoadOptions.SetLineInfo viene passato al metodo Load e si verifica un errore di convalida, le proprietà XmlSchemaException.LineNumber e XmlSchemaException.LinePosition contengono ora informazioni sulla riga.|  
|Suggerimento|È necessario aggiornare il codice di gestione delle eccezioni che presuppone che le proprietà XmlSchemaException.LineNumber e XmlSchemaException.LinePosition non vengano impostate, perché queste proprietà vengono ora impostate correttamente quando il metodo SetLineInfo viene usato durante il caricamento di XML.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Xml.Linq.LoadOptions?displayProperty=fullName>|  
|Analizzatori|CD0019|  
  
<a name="diagnostic20"></a>   
## <a name="20-systemactivities-is-now-aptca"></a>20: System.Activities is now APTCA  
  
|||  
|-|-|  
|Dettagli|L'assembly è contrassegnato con l'attributo AllowPartiallyTrustedCallersAttribute.|  
|Suggerimento|Non è possibile contrassegnare le classi derivate con SecurityCriticalAttribute. In precedenza, i tipi derivati dovevano essere contrassegnati con SecurityCriticalAttribute. Tuttavia, questa modifica non dovrebbe avere un impatto reale.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0020|  
  
<a name="diagnostic21"></a>   
## <a name="21-workflow-30-types-are-obsolete"></a>21: WorkFlow 3.0 types are obsolete  
  
|||  
|-|-|  
|Dettagli|Le API Windows Workflow Foundation (WWF) 3.0 (dallo spazio dei nomi System.Workflow) sono obsolete.|  
|Suggerimento|È ora necessario usare le nuove API WWF 4.0 (in System. Activities). Un esempio di uso delle nuove API è disponibile [qui](https://msdn.microsoft.com/library/jj205427.aspx) e altre indicazioni sono disponibili [qui](http://blogs.msdn.com/b/workflowteam/archive/2012/02/08/deprecatingwf3.aspx). In alternativa, dato che le API WWF 3.0 sono ancora supportate, è possibile usarle ed evitare l'avviso in fase di compilazione, eliminandolo o usando un compilatore precedente.|  
|Ambito|Principale|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0021|  
  
<a name="diagnostic22"></a>   
## <a name="22-some-workflow-drag-and-drop-apis-are-obsolete"></a>22: Some WorkFlow drag and drop APIs are obsolete  
  
|||  
|-|-|  
|Dettagli|L'API WorkFlow Drag/Drop è obsoleta e causerà avvisi del compilatore se l'app viene ricompilata per la versione 4.5.|  
|Suggerimento|In sostituzione, è necessario usare le nuove API [DragDropHelper](https://msdn.microsoft.com/library/system.activities.presentation.dragdrophelper\(v=vs.110\).aspx) che supportano operazioni con più oggetti. In alternativa, è possibile eliminare gli avvisi di compilazione o evitarli usando un compilatore precedente. Le API sono ancora supportate.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Activities.Presentation.DragDropHelper.DoDragMove%28System.Activities.Presentation.WorkflowViewElement%2CSystem.Windows.Point%29?displayProperty=fullName><br /><br /> <xref:System.Activities.Presentation.DragDropHelper.GetCompositeView%28System.Windows.DragEventArgs%29?displayProperty=fullName><br /><br /> <xref:System.Activities.Presentation.DragDropHelper.GetDraggedModelItem%28System.Windows.DragEventArgs%29?displayProperty=fullName><br /><br /> <xref:System.Activities.Presentation.DragDropHelper.GetDroppedObject%28System.Windows.DependencyObject%2CSystem.Windows.DragEventArgs%2CSystem.Activities.Presentation.EditingContext%29?displayProperty=fullName>|  
|Analizzatori|CD0022|  
  
<a name="diagnostic23"></a>   
## <a name="23-new-ambiguous-dispatcherinvoke-overloads-could-result-in-different-behavior"></a>23: New (ambiguous) Dispatcher.Invoke overloads could result in different behavior  
  
|||  
|-|-|  
|Dettagli|.NET Framework 4.5 aggiunge nuovi overload a Dispatcher.Invoke che includono un parametro di tipo System.Action. Se il codice esistente viene ricompilato, i compilatori possono risolvere le chiamate ai metodi Dispatcher.Invoke che dispongono di un parametro Delegate come chiamate ai metodi Dispatcher.Invoke con un parametro System.Action. Se una chiamata a un overload di Dispatcher.Invoke con un parametro Delegate viene risolta come una chiamata a un overload di Dispatcher.Invoke con un parametro System.Action, è possibile che si verifichino le seguenti differenze nel comportamento:<br /><br /> Se si verifica un'eccezione, gli eventi Dispatcher.UnhandledExceptionFilter e Dispatcher.UnhandledException non vengono generati. Le eccezioni vengono invece gestite dall'evento UnobservedTaskException.<br /><br /> Le chiamate ad alcuni membri, come DispatcherOperation.Result, si bloccano fino al completamento dell'operazione.|  
|Suggerimento|Per evitare ambiguità (e potenziali differenze nella gestione delle eccezioni o per i comportamenti di blocco), il codice che chiama Dispatcher.Invoke può passare un oggetto vuoto [] come secondo parametro della chiamata Invoke per essere certi di usare l'overload del metodo .NET 4.0.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Windows.Threading.Dispatcher.Invoke%28System.Delegate%2CSystem.Object%5B%5D%29?displayProperty=fullName><br /><br /> <xref:System.Windows.Threading.Dispatcher.Invoke%28System.Delegate%2CSystem.TimeSpan%2CSystem.Object%5B%5D%29?displayProperty=fullName><br /><br /> <xref:System.Windows.Threading.Dispatcher.Invoke%28System.Delegate%2CSystem.TimeSpan%2CSystem.Windows.Threading.DispatcherPriority%2CSystem.Object%5B%5D%29?displayProperty=fullName><br /><br /> <xref:System.Windows.Threading.Dispatcher.Invoke%28System.Delegate%2CSystem.Windows.Threading.DispatcherPriority%2CSystem.Object%5B%5D%29?displayProperty=fullName>|  
|Analizzatori|CD0023|  
  
<a name="diagnostic24"></a>   
## <a name="24-encoderparameter-ctor-is-obsolete"></a>24: EncoderParameter constructor is obsolete  
  
|||  
|-|-|  
|Dettagli|Il costruttore `EncoderParameter.EncoderParameter(Encoder, Int32, Int32, Int32)` è ora obsoleto e l'eventuale uso causerà avvisi di compilazione.|  
|Suggerimento|Anche se il costruttore `EncoderParameter.EncoderParameter(Encoder, Int32, Int32, Int32)` continuerà a funzionare, è necessario usare il costruttore seguente per evitare l'avviso di compilazione obsoleto durante la ricompilazione del codice con gli strumenti di .NET 4.5: [EncoderParameter.EncoderParameter(Encoder, Int32, EncoderParameterValueType, IntPtr)](https://msdn.microsoft.com/library/hh875096\(v=vs.110\).aspx).|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Drawing.Imaging.EncoderParameter.%23ctor%28System.Drawing.Imaging.Encoder%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%29?displayProperty=fullName>|  
|Analizzatori|CD0024|  
  
<a name="diagnostic26"></a>   
## <a name="26-change-in-behavior-for-taskwaitall-methods-with-time-out-arguments"></a>26: Change in behavior for Task.WaitAll methods with time-out arguments  
  
|||  
|-|-|  
|Dettagli|Il comportamento dei metodi Task.WaitAll è diventato più coerente in .NET 4.5.<br /><br /> In .NET Framework 4 il comportamento di questi metodi è incoerente. Alla scadenza del timeout, se una o più attività sono state completate o annullate prima della chiamata al metodo, il metodo genera un'eccezione AggregateException. Alla scadenza del timeout, se nessuna attività è stata completata o annullata prima della chiamata al metodo, ma una o più attività sono entrate in questi stati dopo la chiamata al metodo, il metodo restituisce false.<br />In.NET Framework 4.5 questi overload del metodo restituiscono ora false se una o più attività sono ancora in esecuzione allo scadere dell'intervallo di timeout e generano un'eccezione AggregateException solo se è stata annullata un'attività di input (indipendentemente dal fatto che sia stata annullata prima o dopo la chiamata del metodo) e non sono in esecuzione altre attività.|  
|Suggerimento|Se è prevista l'intercettazione di AggregateException come mezzo per rilevare un'attività che viene annullata prima della chiamata del metodo WaitAll, tale codice deve invece eseguire lo stesso rilevamento tramite la proprietà IsCanceled (ad esempio: .Any(t => t.IsCanceled)) in quanto .NET 4.6 genererà un'eccezione in questo caso solo se vengono completate tutte le attività in attesa prima del timeout.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Threading.Tasks.Task.WaitAll%28System.Threading.Tasks.Task%5B%5D%2CSystem.Int32%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.WaitAll%28System.Threading.Tasks.Task%5B%5D%2CSystem.Int32%2CSystem.Threading.CancellationToken%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.WaitAll%28System.Threading.Tasks.Task%5B%5D%2CSystem.TimeSpan%29?displayProperty=fullName>|  
|Analizzatori|CD0026|  
  
<a name="diagnostic27"></a>   
## <a name="27-change-in-behavior-in-data-definition-language-ddl-apis"></a>27: Change in behavior in Data Definition Language (DDL) APIs  
  
|||  
|-|-|  
|Dettagli|Il comportamento delle API DDL quando si specifica AttachDBFilename è cambiato come segue:<br /><br /> Le stringhe di connessione non devono specificare un valore Initial Catalog. In precedenza, erano necessari sia AttatchDBFilename che Initial Catalog.<br /><br /> Se vengono specificati sia AttatchDBFilename che Initial Catalog e il file MDF indicato esiste, il metodo ObjectContext.DatabaseExists restituisce true. In precedenza, restituiva false.<br /><br /> Se vengono specificati sia AttatchDBFilename che Initial Catalog e il file MDF indicato esiste, la chiamata del metodo ObjectContext.DeleteDatabase elimina il file.<br /><br /> Se ObjectContext.DeleteDatabase viene chiamato quando la stringa di connessione specifica un valore AttachDBFilename con un file MDF e un valore Initial Catalog inesistenti, il metodo genera un'eccezione InvalidOperationException. In precedenza, generava un'eccezione SqlException.|  
|Suggerimento|Queste modifiche semplificano la creazione di strumenti e applicazioni che usano le API DDL. Tali modifiche possono influire sulla compatibilità delle applicazioni negli scenari seguenti:<br /><br /> L'utente scrive codice che esegue un comando DROP DATABASE direttamente anziché chiamando ObjectContext.DeleteDatabase se ObjectContext.DatabaseExists restituisce true. Questa operazione interrompe il codice esistente se il database non è collegato ma il file MDF esiste.<br /><br /> L'utente scrive codice che prevede che il metodo ObjectContext.DeleteDatabase generi un'eccezione SqlException invece di un'eccezione InvalidOperationException se il valore Initial Catalog e il file MDF non esistono.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0027|  
  
<a name="diagnostic28"></a>   
## <a name="28-machinekeyencode-and-machinekeydecode-methods-are-now-obsolete"></a>28: MachineKey.Encode and MachineKey.Decode methods are now obsolete  
  
|||  
|-|-|  
|Dettagli|Questi metodi sono ora obsoleti. La compilazione del codice che chiama tali metodi genera un avviso del compilatore.|  
|Suggerimento|Le alternative consigliate sono [MachineKey.Protect](https://msdn.microsoft.com/library/system.web.security.machinekey.protect\(v=vs.110\).aspx) e [MachineKey.Unprotect](https://msdn.microsoft.com/library/system.web.security.machinekey.unprotect\(v=vs.110\).aspx). In alternativa, è possibile eliminare gli avvisi di compilazione o evitarli usando un compilatore precedente. Le API sono ancora supportate.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Web.Security.MachineKey.Decode%28System.String%2CSystem.Web.Security.MachineKeyProtection%29?displayProperty=fullName><br /><br /> <xref:System.Web.Security.MachineKey.Encode%28System.Byte%5B%5D%2CSystem.Web.Security.MachineKeyProtection%29?displayProperty=fullName>|  
|Analizzatori|CD0028|  
  
<a name="diagnostic29"></a>   
## <a name="29-the-replace-method-in-odata-urls-is-disabled-by-default"></a>29: The Replace method in OData URLs is disabled by default  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.5, il metodo Replace negli URL OData è disabilitato per impostazione predefinita. Quando il metodo Replace è disabilitato per OData, ora per impostazione predefinita, le eventuali richieste utente che includono funzioni di sostituzione (non comuni) avranno esito negativo.|  
|Suggerimento|Se il metodo Replace è necessario (situazione non comune) è possibile riabilitarlo tramite le [impostazioni di configurazione](https://msdn.microsoft.com/library/system.data.services.configuration.dataservicesfeaturessection.replacefunction.aspx). L'abilitazione di un metodo Replace, tuttavia, può introdurre vulnerabilità per la sicurezza ed è consigliabile usarlo solo dopo attente valutazioni.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Data.Services.DataService%601?displayProperty=fullName>|  
|Analizzatori|CD0029|  
  
<a name="diagnostic30"></a>   
## <a name="30-systemservicemodelwebwebservicehost-object-no-longer-adds-a-default-endpoint"></a>30: System.ServiceModel.Web.WebServiceHost object no longer adds a default endpoint  
  
|||  
|-|-|  
|Dettagli|L'oggetto System.ServiceModel.Web.WebServiceHost non aggiunge più un endpoint predefinito se è stato aggiunto un endpoint esplicito tramite il codice dell'applicazione.|  
|Suggerimento|Se gli utenti si aspettano di essere in grado di connettersi a un endpoint predefinito e altri endpoint espliciti sono state aggiunti a WebServiceHost, deve essere possibile anche aggiungere endpoint predefiniti in modo esplicito mediante AddDefaultEndpoints.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%28System.Type%2CSystem.ServiceModel.Channels.Binding%2CSystem.String%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%28System.Type%2CSystem.ServiceModel.Channels.Binding%2CSystem.String%2CSystem.Uri%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%28System.Type%2CSystem.ServiceModel.Channels.Binding%2CSystem.Uri%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%28System.Type%2CSystem.ServiceModel.Channels.Binding%2CSystem.Uri%2CSystem.Uri%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHostBase.AddServiceEndpoint%28System.ServiceModel.Description.ServiceEndpoint%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHostBase.AddServiceEndpoint%28System.String%2CSystem.ServiceModel.Channels.Binding%2CSystem.String%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHostBase.AddServiceEndpoint%28System.String%2CSystem.ServiceModel.Channels.Binding%2CSystem.String%2CSystem.Uri%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHostBase.AddServiceEndpoint%28System.String%2CSystem.ServiceModel.Channels.Binding%2CSystem.Uri%29?displayProperty=fullName><br /><br /> <xref:System.ServiceModel.ServiceHostBase.AddServiceEndpoint%28System.String%2CSystem.ServiceModel.Channels.Binding%2CSystem.Uri%2CSystem.Uri%29?displayProperty=fullName>|  
|Analizzatori|CD0030A<br /><br /> CD0030B|  
  
<a name="diagnostic31"></a>   
## <a name="31-eventsourcewriteevent-impls-must-pass-writeevent-the-same-parameters-that-it-received-plus-id"></a>31: EventSource.WriteEvent impls must pass WriteEvent the same parameters that it received (plus ID)  
  
|||  
|-|-|  
|Dettagli|Il runtime applica ora il contratto che specifica quanto segue: una classe derivata da EventSource che definisce un metodo di eventi ETW deve chiamare il metodo EventSource.WriteEvent della classe di base con l'ID evento seguito dagli stessi argomenti passati al metodo di eventi ETW.|  
|Suggerimento|Viene generata un'eccezione IndexOutOfRangeException se un EventListener legge i dati EventSource in-process per un'origine evento che viola questo contratto.|  
|Ambito|Secondario|  
|Versione|4.5.1|  
|Tipo|Runtime|  
|Analizzatori|CD0031|  
  
<a name="diagnostic32"></a>   
## <a name="32-minfreememorypercentagetoactiveservice-is-now-respected"></a>32: MinFreeMemoryPercentageToActiveService is now respected  
  
|||  
|-|-|  
|Dettagli|Questa impostazione consente di stabilire la quantità minima di memoria che deve essere disponibile nel server per poter attivare un servizio WCF. È progettata in modo da prevenire le eccezioni OutOfMemoryException. In .NET Framework 4.5 questa impostazione non ha alcun effetto. In .NET Framework 4.5.1 questa impostazione viene applicata.|  
|Suggerimento|Viene generata un'eccezione se la quantità di memoria libera disponibile sul server Web è inferiore alla percentuale definita dall'impostazione di configurazione. Alcuni servizi WCF correttamente avviati ed eseguiti in un ambiente di memoria limitato potrebbero avere esito negativo.|  
|Ambito|Secondario|  
|Versione|4.5.1|  
|Tipo|Runtime|  
|Analizzatori|CD0032|  
  
<a name="diagnostic33"></a>   
## <a name="33-xmltextreader-dtd-entity-expansion-is-limited-to-10000000-characters"></a>33: XmlTextReader DTD entity expansion is limited to 10,000,000 characters  
  
|||  
|-|-|  
|Dettagli|L'espansione dell'entità DTD è ora limitata a 10.000.000 di caratteri. Il caricamento di file XML senza espansione o con espansione limitata dell'entità DTD non è interessato dall'operazione. I file con entità DTD che si espandono oltre 10.000.000 di caratteri non vengono caricati e generano un'eccezione.|  
|Suggerimento|Se il limite di espansione dell'entità DTD di 10.000.000 è troppo basso, il valore può essere sostituito con la proprietà [XmlReaderSettings.MaxCharactersFromEntities](https://msdn.microsoft.com/library/system.xml.xmlreadersettings.maxcharactersfromentities%28v=vs.110%29.aspx). Un XmlReaderSettings con il valore corretto MaxCharactersFromEntity può essere passato a [XmlReader.Create](https://msdn.microsoft.com/library/System.Xml.XmlReader.Create\(v=vs.110\).aspx).|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Xml.XmlTextReader.%23ctor?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.IO.Stream%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.IO.Stream%2CSystem.Xml.XmlNameTable%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.IO.Stream%2CSystem.Xml.XmlNodeType%2CSystem.Xml.XmlParserContext%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.IO.TextReader%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.IO.TextReader%2CSystem.Xml.XmlNameTable%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.String%2CSystem.IO.Stream%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.String%2CSystem.IO.Stream%2CSystem.Xml.XmlNameTable%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.String%2CSystem.IO.TextReader%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.String%2CSystem.IO.TextReader%2CSystem.Xml.XmlNameTable%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.String%2CSystem.Xml.XmlNameTable%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.String%2CSystem.Xml.XmlNodeType%2CSystem.Xml.XmlParserContext%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader.%23ctor%28System.Xml.XmlNameTable%29?displayProperty=fullName><br /><br /> <xref:System.Xml.XmlTextReader?displayProperty=fullName>|  
|Analizzatori|CD0033|  
  
<a name="diagnostic35"></a>   
## <a name="35-xslt-style-sheet-exception-message-changed"></a>35: XSLT style sheet exception message changed  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4.5 il testo del messaggio di errore quando un file XSLT è troppo complesso è "Foglio di stile troppo complesso". Nelle versioni precedenti il messaggio di errore era "Errore di compilazione XSLT". Il codice di applicazione che dipende dal testo del messaggio di errore non funzionerà più. Tuttavia, i tipi di eccezione rimangono gli stessi e pertanto questa modifica non dovrebbe avere un impatto reale.|  
|Suggerimento|Aggiornare il codice dell'app che dipende dal messaggio di eccezione da questa condizione di errore in modo che preveda il nuovo messaggio oppure, ancora meglio, aggiornare il codice in modo che dipenda solo dal tipo di eccezione ([XsltException](https://msdn.microsoft.com/library/system.xml.xsl.xsltexception\(v=vs.110\).aspx)), che non è stato modificato.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Reflection.MethodInfo%2CSystem.Byte%5B%5D%2CSystem.Type%5B%5D%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.String%2CSystem.Xml.Xsl.XsltSettings%2CSystem.Xml.XmlResolver%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Type%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Xml.XPath.IXPathNavigable%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Xml.XPath.IXPathNavigable%2CSystem.Xml.Xsl.XsltSettings%2CSystem.Xml.XmlResolver%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Xml.XmlReader%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Xml.XmlReader%2CSystem.Xml.Xsl.XsltSettings%2CSystem.Xml.XmlResolver%29?displayProperty=fullName>|  
|Analizzatori|CD0035|  
  
<a name="diagnostic36"></a>   
## <a name="36-wf-serializes-expressionsliteralt-datetimes-differently-now-breaks-custom-xaml-parsers"></a>36: WF serializes Expressions.Literal\<T> DateTimes differently now (breaks custom XAML parsers)  
  
|||  
|-|-|  
|Dettagli|L'oggetto [ValueSerializer](https://msdn.microsoft.com/library/system.windows.markup.valueserializer\(v=vs.110\).aspx) associato convertirà un oggetto DateTime o DateTimeOffset i cui componenti Second e Millisecond sono diversi da zero e (per un valore DateTime) la cui proprietà DateTime.Kind non è Unspecified nella sintassi degli elementi di proprietà invece di una stringa. Tale modifica consente di eseguire il round trip dei valori di DateTime e DateTimeOffset. I parser XAML personalizzati che presuppongono che il codice XAML di input si trovi nella sintassi degli attributi non funzioneranno correttamente.|  
|Suggerimento|Tale modifica consente di eseguire il round trip dei valori di DateTime e DateTimeOffset. I parser XAML personalizzati che presuppongono che il codice XAML di input si trovi nella sintassi degli attributi non funzioneranno correttamente.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0036|  
  
<a name="diagnostic37"></a>   
## <a name="37-new-enum-values-in-wpfs-pagerangeselection"></a>37: New enum values in WPF's PageRangeSelection  
  
|||  
|-|-|  
|Dettagli|Sono stati aggiunti due nuovi membri (CurrentPage e SelectedPage) all'enumerazione [PageRangeSelection](https://msdn.microsoft.com/library/system.windows.controls.pagerangeselection\(v=vs.110\).aspx).|  
|Suggerimento|Nella maggior parte dei casi queste modifiche non influiscono sul codice utente. È tuttavia consigliabile modificare il codice che dipende da un determinato numero di elementi esistenti nelle chiamate Enum.GetNames o Enum.GetValues per il tipo PageRangeSelection.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Controls.PageRangeSelection?displayProperty=fullName>|  
|Analizzatori|CD0037|  
  
<a name="diagnostic38"></a>   
## <a name="38-wpf-dispatchersynchronizationcontextcreatecopy-now-returns-a-new-copy-instead-of-the-current-instance"></a>38: WPF DispatcherSynchronizationContext.CreateCopy now returns a new copy instead of the current instance  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4 DispatcherSynchronizationContext.CreateCopy() restituisce un riferimento all'istanza corrente, principalmente come ottimizzazione delle prestazioni. In .NET Framework 4.5 restituisce una nuova istanza che rende possibile per la prima volta concludere che riferimenti uguali indicano che il thread in esecuzione è nel contesto di sincronizzazione corretto.  È improbabile che ciò influisca sul codice che verifica l'identità di questi riferimenti, ma a causa della modifica, è opportuno testare il codice che chiama DispatcherSynchronizationContext.CreateCopy nell'ambito della migrazione a .NET Framework 4.5 o versione successiva.|  
|Suggerimento|Tenere presente che DispatcherSynchronizationContext.CreateCopy() restituirà ora un nuovo oggetto SynchronizationContext.  Nelle versioni precedenti, il codice che usa l'equivalenza dei riferimenti generati in questo modo non controlla in effetti se il contesto attivo è corretto, ma questa verifica viene eseguita se il codice viene compilato per .NET 4.5 o versione successiva.  Anche se è improbabile che si verifichino problemi, il test dei percorsi del codice interessati dovrebbe essere sufficiente per determinare se ciò costituisce un problema.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Threading.DispatcherSynchronizationContext.CreateCopy?displayProperty=fullName>|  
|Analizzatori|CD0038|  
  
<a name="diagnostic39"></a>   
## <a name="39-systemthreadingtaskstask-no-longer-throw-objectdisposedexception-after-object-is-disposed"></a>39: System.Threading.Tasks.Task no longer throw ObjectDisposedException after object is disposed  
  
|||  
|-|-|  
|Dettagli|Ad eccezione di Task.IAsyncResult.AsyncWaitHandle, i metodi System.Threading.Tasks.Task non generano più un'eccezione ObjectDisposedException dopo l'eliminazione dell'oggetto.<br />Questa modifica supporta l'uso di attività memorizzate nella cache. Ad esempio, un metodo può restituire un'attività memorizzata nella cache per rappresentare un'operazione già completata anziché allocare una nuova attività. Ciò non è possibile nelle versioni precedenti di .NET Framework, perché qualsiasi utente dell'attività può rimuoverla e renderla così inutilizzabile.|  
|Suggerimento|Tenere presente che i metodi Task potrebbero non generare più eccezioni ObjectDisposedException nei casi in cui viene eliminato l'oggetto. Se un'app dipende da questa eccezione per venire a conoscenza dell'eliminazione di un'attività, è necessario aggiornarla in modo che controlli in modo esplicito lo stato dell'attività tramite [Task.Status](https://msdn.microsoft.com/library/system.threading.tasks.task.status\(v=vs.110\).aspx).|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0039|  
  
<a name="diagnostic40"></a>   
## <a name="40-different-exception-handling-for-objectcontextcreatedatabase-and-dbproviderservicescreatedatabase-methods"></a>40: Different exception handling for ObjectContext.CreateDatabase and DbProviderServices.CreateDatabase methods  
  
|||  
|-|-|  
|Dettagli|A partire da .NET 4.5, se la creazione del database non riesce, i metodi `CreateDatabase` tenteranno di eliminare il database vuoto. Se tale operazione ha esito positivo, verrà propagata l'eccezione `SQLException` originale, al posto dell'eccezione `InvalidOperationException` che viene sempre generata in .NET 4.0.|  
|Suggerimento|Quando si intercetta un'eccezione InvalidOperationException durante l'esecuzione di ObjectContext.CreateDatabase o DbProviderServices.CreateDatabase, devono essere ora intercettate anche le eccezioni SQLException.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Data.Common.DbProviderServices.CreateDatabase%28System.Data.Common.DbConnection%2CSystem.Nullable%7BSystem.Int32%7D%2CSystem.Data.Metadata.Edm.StoreItemCollection%29?displayProperty=fullName><br /><br /> <xref:System.Data.Objects.ObjectContext.CreateDatabase?displayProperty=fullName>|  
|Analizzatori|CD0040|  
  
<a name="diagnostic41"></a>   
## <a name="41-objectcontexttranslate-and-objectcontextexecutestorequery-now-support-enum-type"></a>41: ObjectContext.Translate e ObjectContext.ExecuteStoreQuery ora supporta tipo enum  
  
|||  
|-|-|  
|Dettagli|In .NET 4.0 il parametro generico `T` dei metodi `ObjectContext.Translate` e `ObjectContext.ExecuteStoreQuery` non può essere un tipo enum. Questo scenario è ora supportato.|  
|Suggerimento|Se si chiama Translate o ExecuteStoreQuery su un tipo enum in .NET 4.0, viene restituito '0'. Se tale comportamento è quello desiderabile, le chiamate devono essere sostituite con una costante 0 (o l'enum equivalente).|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Data.Objects.ObjectContext.ExecuteStoreQuery%60%601%28System.String%2CSystem.Object%5B%5D%29?displayProperty=fullName><br /><br /> <xref:System.Data.Objects.ObjectContext.ExecuteStoreQuery%60%601%28System.String%2CSystem.String%2CSystem.Data.Objects.MergeOption%2CSystem.Object%5B%5D%29?displayProperty=fullName><br /><br /> <xref:System.Data.Objects.ObjectContext.Translate%60%601%28System.Data.Common.DbDataReader%29?displayProperty=fullName><br /><br /> <xref:System.Data.Objects.ObjectContext.Translate%60%601%28System.Data.Common.DbDataReader%2CSystem.String%2CSystem.Data.Objects.MergeOption%29?displayProperty=fullName>|  
|Analizzatori|CD0041|  
  
<a name="diagnostic42"></a>   
## <a name="42-enumerableemptytresult-always-returns-cached-instance"></a>42: Enumerable.Empty\<TResult> always returns cached instance  
  
|||  
|-|-|  
|Dettagli|A partire da .NET 4.5, `Enumerable.Empty` restituisce sempre un'istanza di `IEnumerable<T>` interna memorizzata nella cache.<br /><br /> In precedenza, `Enumerable.Empty` memorizza nella cache un `IEnumerable<T>` al momento della chiamata dell'API e questo significa che in alcune condizioni in cui `Enumerable.Empty` viene chiamato velocemente e in simultanea, possono essere restituite istanze diverse del tipo per chiamate diverse all'API.|  
|Suggerimento|Dato che il comportamento precedente è non deterministico, è improbabile che esista codice dipendente. Tuttavia, nel caso improbabile che i tipi enumerabili vuoti vengano usati per confronti prevedendo che talvolta possano essere diversi, è consigliabile creare matrici vuote esplicite (`new T[0]`) invece di usare `Enumerable.Empty`.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Linq.Enumerable.Empty%60%601?displayProperty=fullName>|  
|Analizzatori|CD0042|  
  
<a name="diagnostic43"></a>   
## <a name="43-httprequestcontentencoding-property-prohibits-utf7"></a>43: HttpRequest.ContentEncoding property prohibits UTF7  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.5, la codifica UTF-7 non è consentita nel corpo di richieste HttpRequest. In alcuni casi i dati per le applicazioni che dipendono dai dati UTF-7 in ingresso non verranno decodificati correttamente.|  
|Suggerimento|È consigliabile idealmente aggiornare le applicazioni in modo da non usare la codifica UTF-7 in HttpRequest. In alternativa, è possibile ripristinare il comportamento legacy usando l'attributo `aspnet:AllowUtf7RequestContentEncoding` dell'elemento [appSettings](https://msdn.microsoft.com/library/hh975440\(v=vs.110\).aspx).|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Web.HttpRequest.ContentEncoding%2A?displayProperty=fullName>|  
|Analizzatori|CD0043|  
  
<a name="diagnostic44"></a>   
## <a name="44-httputilityjavascriptstringencode-escapes-ampersand"></a>44: HttpUtility.JavaScriptStringEncode escapes ampersand  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.5, JavaScriptStringEncode esegue l'escape del carattere e commerciale (&).|  
|Suggerimento|Se l'app dipende dal comportamento precedente di questo metodo, è possibile aggiungere un'impostazione aspnet:JavaScriptDoNotEncodeAmpersand all'[elemento appSettings di ASP.NET](https://msdn.microsoft.com/library/hh975440\(v=vs.110\).aspx) nel file di configurazione.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Web.HttpUtility.JavaScriptStringEncode%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Web.HttpUtility.JavaScriptStringEncode%28System.String%2CSystem.Boolean%29?displayProperty=fullName>|  
|Analizzatori|CD0044A<br /><br /> CD0044B|  
  
<a name="diagnostic46"></a>   
## <a name="46-eventlistener-truncates-strings-with-embedded-nulls"></a>46: EventListener truncates strings with embedded nulls  
  
|||  
|-|-|  
|Dettagli|EventListener tronca le stringhe con valori null incorporati. I caratteri null non sono supportati dalla classe EventSource. La modifica influisce solo sulle app che usano EventListener per leggere i dati EventSource in-process e che usano i caratteri null come delimitatori.|  
|Suggerimento|I dati EventSource devono essere aggiornati, se possibile, in modo da non usare caratteri null incorporati.|  
|Ambito|Microsoft Edge|  
|Versione|4.5.1|  
|Tipo|Runtime|  
|API interessate|<xref:System.Diagnostics.Tracing.EventListener.%23ctor?displayProperty=fullName><br /><br /> <xref:System.Diagnostics.Tracing.EventListener.EnableEvents%28System.Diagnostics.Tracing.EventSource%2CSystem.Diagnostics.Tracing.EventLevel%29?displayProperty=fullName><br /><br /> <xref:System.Diagnostics.Tracing.EventListener.EnableEvents%28System.Diagnostics.Tracing.EventSource%2CSystem.Diagnostics.Tracing.EventLevel%2CSystem.Diagnostics.Tracing.EventKeywords%29?displayProperty=fullName><br /><br /> <xref:System.Diagnostics.Tracing.EventListener.EnableEvents%28System.Diagnostics.Tracing.EventSource%2CSystem.Diagnostics.Tracing.EventLevel%2CSystem.Diagnostics.Tracing.EventKeywords%2CSystem.Collections.Generic.IDictionary%7BSystem.String%2CSystem.String%7D%29?displayProperty=fullName>|  
|Analizzatori|CD0046|  
  
<a name="diagnostic48"></a>   
## <a name="48-obsoleteattribute-exports-as-both-obsoleteattribute-and-deprecatedattribute-in-winmd-scenarios"></a>48: ObsoleteAttribute exports as both ObsoleteAttribute and DeprecatedAttribute in WinMD scenarios  
  
|||  
|-|-|  
|Dettagli|Quando si crea una raccolta di metadati Windows (file con estensione winmd), l'attributo ObsoleteAttribute viene esportato sia come ObsoleteAttribute che come Windows.Foundation.DeprecatedAttribute.|  
|Suggerimento|La ricompilazione del codice sorgente esistente che usa l'attributo ObsoleteAttribute può generare avvisi quando tale codice viene usato da C++/CX o JavaScript.<br /><br /> Non è consigliabile applicare sia ObsoleteAttribute che Windows.Foundation.DeprecatedAttribute al codice negli assembly gestiti, perché potrebbero essere restituiti avvisi di compilazione.|  
|Ambito|Microsoft Edge|  
|Versione|4.5.1|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0048A<br /><br /> CD0048B|  
  
<a name="diagnostic49"></a>   
## <a name="49-resolveassemblyreference-task-now-warns-on-dependencies-with-the-wrong-architecture"></a>49: ResolveAssemblyReference task now warns on dependencies with the wrong architecture  
  
|||  
|-|-|  
|Dettagli|L'attività genera un avviso, MSB3270, che indica la mancata corrispondenza di un riferimento o di una delle sue dipendenze all'architettura dell'app. Questa situazione si verifica ad esempio se un'app compilata con l'opzione anycpu include un riferimento x86. Uno scenario di questo tipo potrebbe provocare un errore dell'app in fase di esecuzione (nel caso descritto, se l'app viene distribuita come processo x64).|  
|Suggerimento|Le possibili conseguenze riguardano le aree seguenti:<br /><br /> La ricompilazione genera avvisi che non venivano visualizzati quando l'app veniva compilata con una versione precedente di MSBuild. Tuttavia, dal momento che l'avviso identifica una possibile fonte di errore di runtime, deve essere analizzato e affrontato.<br /><br /> Se gli avvisi vengono considerati errori, la compilazione dell'app non verrà completata.|  
|Ambito|Secondario|  
|Versione|4.5.1|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0049|  
  
<a name="diagnostic51"></a>   
## <a name="51-wpf-textbox-defaults-to-undo-limit-of-100"></a>51: WPF TextBox defaults to undo limit of 100  
  
|||  
|-|-|  
|Dettagli|In .NET 4.5, il limite di annullamento predefinito per una casella di testo WPF è 100, anziché essere illimitato come in .NET 4.0|  
|Suggerimento|Se un limite di annullamento di 100 è troppo basso, il limite può essere impostato in modo esplicito con la proprietà UndoLimit del controllo TextBox|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Controls.TextBox?displayProperty=fullName>|  
|Analizzatori|CD0051|  
  
<a name="diagnostic55"></a>   
## <a name="55-exceptions-during-unobserved-processing-in-systemthreadingtaskstask-no-longer-propagate-on-finalizer-thread"></a>55: Exceptions during unobserved processing in System.Threading.Tasks.Task no longer propagate on finalizer thread  
  
|||  
|-|-|  
|Dettagli|Dato che la classe System.Threading.Tasks.Task rappresenta un'operazione asincrona, intercetta tutte le eccezioni non gravi che si verificano durante l'elaborazione asincrona. In .NET Framework 4.5, se un'eccezione non viene osservata e il codice non è mai in attesa nell'attività, tale eccezione non verrà più propagata nel thread finalizzatore e il processo verrà arrestato in modo anomalo durante un'operazione di Garbage Collection. Questa modifica migliora l'affidabilità delle applicazioni che usano la classe Task per eseguire l'elaborazione asincrona non osservata.|  
|Suggerimento|Se un'applicazione dipende dalla propagazione delle eccezioni asincrone non osservate al thread del finalizzatore, il comportamento precedente può essere ripristinato fornendo un gestore appropriato per l'evento [TaskScheduler.UnobservedTaskException](https://msdn.microsoft.com/library/system.threading.tasks.taskscheduler.unobservedtaskexception\(v=vs.110\).aspx) oppure impostando un [elemento di configurazione di runtime](https://msdn.microsoft.com/library/jj160346%28v=vs.110%29.aspx).|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Threading.Tasks.Task.Run%28System.Action%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Run%28System.Action%2CSystem.Threading.CancellationToken%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Run%28System.Func%7BSystem.Threading.Tasks.Task%7D%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Run%28System.Func%7BSystem.Threading.Tasks.Task%7D%2CSystem.Threading.CancellationToken%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Run%60%601%28System.Func%7BSystem.Threading.Tasks.Task%7B%60%600%7D%7D%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Run%60%601%28System.Func%7BSystem.Threading.Tasks.Task%7B%60%600%7D%7D%2CSystem.Threading.CancellationToken%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Run%60%601%28System.Func%7B%60%600%7D%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Run%60%601%28System.Func%7B%60%600%7D%2CSystem.Threading.CancellationToken%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Start?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.Task.Start%28System.Threading.Tasks.TaskScheduler%29?displayProperty=fullName>|  
|Analizzatori|CD0055|  
  
<a name="diagnostic58"></a>   
## <a name="58-iasyncresultcompletedsynchronously-property-must-be-correct-for-the-resulting-task-to-complete"></a>58: IAsyncResult.CompletedSynchronously property must be correct for the resulting task to complete  
  
|||  
|-|-|  
|Dettagli|Quando si chiama TaskFactory.FromAsync, l'implementazione della proprietà IAsyncResult.CompletedSynchronously deve essere corretta per consentire il completamento dell'attività risultante. Ovvero la proprietà deve restituire true unicamente se l'implementazione è stata completata in modo sincrono. Precedentemente, la proprietà non veniva verificata.|  
|Suggerimento|Se le implementazioni di IAsyncResult restituiscono correttamente true per la proprietà CompletedSynchronusly solo quando un'attività viene completata in modo sincrono, non verrà applicata alcuna interruzione. È consigliabile che gli utenti verifichino le eventuali implementazioni di IAsyncResult di loro proprietà, per assicurarsi che valutino in modo corretto se un'attività viene completata o meno in modo sincrono.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Threading.Tasks.TaskFactory.FromAsync%28System.Func%7BSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2CSystem.Object%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%28System.Func%7BSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%28System.IAsyncResult%2CSystem.Action%7BSystem.IAsyncResult%7D%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%28System.IAsyncResult%2CSystem.Action%7BSystem.IAsyncResult%7D%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%28System.IAsyncResult%2CSystem.Action%7BSystem.IAsyncResult%7D%2CSystem.Threading.Tasks.TaskCreationOptions%2CSystem.Threading.Tasks.TaskScheduler%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%601%28System.Func%7BSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%600%7D%2CSystem.Object%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%601%28System.Func%7BSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%600%7D%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%601%28System.Func%7B%60%600%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2C%60%600%2CSystem.Object%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%601%28System.Func%7B%60%600%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2C%60%600%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%601%28System.IAsyncResult%2CSystem.Func%7BSystem.IAsyncResult%2C%60%600%7D%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%601%28System.IAsyncResult%2CSystem.Func%7BSystem.IAsyncResult%2C%60%600%7D%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%601%28System.IAsyncResult%2CSystem.Func%7BSystem.IAsyncResult%2C%60%600%7D%2CSystem.Threading.Tasks.TaskCreationOptions%2CSystem.Threading.Tasks.TaskScheduler%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%602%28System.Func%7B%60%600%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%601%7D%2C%60%600%2CSystem.Object%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%602%28System.Func%7B%60%600%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%601%7D%2C%60%600%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%602%28System.Func%7B%60%600%2C%60%601%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2C%60%600%2C%60%601%2CSystem.Object%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%602%28System.Func%7B%60%600%2C%60%601%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2C%60%600%2C%60%601%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%603%28System.Func%7B%60%600%2C%60%601%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%602%7D%2C%60%600%2C%60%601%2CSystem.Object%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%603%28System.Func%7B%60%600%2C%60%601%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%602%7D%2C%60%600%2C%60%601%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%603%28System.Func%7B%60%600%2C%60%601%2C%60%602%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2C%60%600%2C%60%601%2C%60%602%2CSystem.Object%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%603%28System.Func%7B%60%600%2C%60%601%2C%60%602%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Action%7BSystem.IAsyncResult%7D%2C%60%600%2C%60%601%2C%60%602%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%604%28System.Func%7B%60%600%2C%60%601%2C%60%602%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%603%7D%2C%60%600%2C%60%601%2C%60%602%2CSystem.Object%29?displayProperty=fullName><br /><br /> <xref:System.Threading.Tasks.TaskFactory.FromAsync%60%604%28System.Func%7B%60%600%2C%60%601%2C%60%602%2CSystem.AsyncCallback%2CSystem.Object%2CSystem.IAsyncResult%7D%2CSystem.Func%7BSystem.IAsyncResult%2C%60%603%7D%2C%60%600%2C%60%601%2C%60%602%2CSystem.Object%2CSystem.Threading.Tasks.TaskCreationOptions%29?displayProperty=fullName>|  
|Analizzatori|CD0058|  
  
<a name="diagnostic59"></a>   
## <a name="59-log-file-name-created-by-the-objectcontextcreatedatabase-method-has-changed-to-match-sql-server-specifications"></a>59: Log file name created by the ObjectContext.CreateDatabase method has changed to match SQL Server specifications  
  
|||  
|-|-|  
|Dettagli|Quando il metodo CreateDatabase viene chiamato direttamente oppure tramite Code First con il provider SqlClient e un valore AttachDBFilename nella stringa di connessione, viene creato un file di log denominato nomefile_log.ldf invece di nomefile.ldf (dove nomefile rappresenta il nome del file specificato dal valore AttachDBFilename). Questa modifica migliora il debug fornendo un file di log il cui nome si basa sulle specifiche di SQL Server.|  
|Suggerimento|Se il nome del file di log è importante per un'app, l'app deve essere aggiornata in modo da prevedere il formato nomefile_log.ldf standard.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Data.Objects.ObjectContext.CreateDatabase?displayProperty=fullName>|  
|Analizzatori|CD0059|  
  
<a name="diagnostic60"></a>   
## <a name="60-pageloadcomplete-event-no-longer-causes-systemwebuiwebcontrolsentitydatasource-control-to-invoke-data-binding"></a>60: Page.LoadComplete event no longer causes System.Web.UI.WebControls.EntityDataSource control to invoke data binding  
  
|||  
|-|-|  
|Dettagli|L'evento `Page.LoadComplete` non determina più la chiamata di data binding da parte del controllo System.Web.UI.WebControls.EntityDataSource per modifiche ai parametri di creazione/aggiornamento/eliminazione. Questa modifica determina l'eliminazione di un accesso estraneo al database, impedisce la reimpostazione dei valori dei controlli e genera un comportamento coerente con altri controlli di dati, quali SqlDataSource e ObjectDataSource. Questa modifica determina un comportamento diverso nel caso improbabile in cui le applicazioni si affidino al richiamo dell'associazione dati nell'evento `Page.LoadComplete`.|  
|Suggerimento|Se il data binding è necessario, richiamare manualmente databind in un evento in una posizione precedente nel postback.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0060|  
  
<a name="diagnostic61"></a>   
## <a name="61-webutilityhtmldecode-no-longer-decodes-invalid-input-sequences"></a>61: WebUtility.HtmlDecode no longer decodes invalid input sequences  
  
|||  
|-|-|  
|Dettagli|Per impostazione predefinita, i metodi di decodifica non decodificano più una sequenza di input non valido in una stringa UTF-16 non valida. Al contrario, viene restituito l'input originale.|  
|Suggerimento|La modifica dell'output del decodificatore è importante solo se si archiviano dati binari anziché dati UTF-16 nelle stringhe. Per controllare questo comportamento in modo esplicito, impostare l'attributo `aspnet:AllowRelaxedUnicodeDecoding` dell'elemento [appSettings](https://msdn.microsoft.com/library/ms228154\(v=vs.110\).aspx) su true per abilitare il comportamento legacy o su false per consentire il comportamento corrente.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Net.WebUtility.HtmlDecode%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Net.WebUtility.HtmlDecode%28System.String%2CSystem.IO.TextWriter%29?displayProperty=fullName><br /><br /> <xref:System.Net.WebUtility.UrlDecode%28System.String%29?displayProperty=fullName>|  
|Analizzatori|CD0061|  
  
<a name="diagnostic63"></a>   
## <a name="63-apps-published-with-clickonce-that-use-a-sha-256-code-signing-certificate-may-fail-on-windows-2003"></a>63: Apps published with ClickOnce that use a SHA-256 code-signing certificate may fail on Windows 2003  
  
|||  
|-|-|  
|Dettagli|Il file eseguibile è firmato con SHA256. In precedenza, veniva firmato con SHA1 indipendentemente dal fatto che il certificato di firma del codice fosse SHA-1 o SHA-256. Si applica a:<br /><br /> Tutte le applicazioni compilate con Visual Studio 2012 o versioni successive.<br /><br /> Applicazioni compilate con Visual Studio 2010 o versioni precedenti su sistemi in cui è presente .NET Framework 4.5.<br /><br /> Se inoltre è presente .NET Framework 4.5 o versione successiva, il manifesto ClickOnce viene firmato anche con SHA-256 per i certificati SHA-256 indipendentemente dalla versione di .NET Framework per cui è stato compilato.|  
|Suggerimento|La modifica della firma del file eseguibile di ClickOnce interessa solo i sistemi Windows Server 2003 in cui è richiesta l'installazione di quanto indicato nell'articolo 938397 della Knowledge Base.<br /><br /> La modifica relativa alla firma del manifesto con SHA-256 anche quando un'app è destinata a .NET Framework 4.0 o a versioni precedenti introduce una dipendenza del runtime da .NET Framework 4.5 o da una versione successiva.|  
|Ambito|Microsoft Edge|  
|Versione|4.5-4.6|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0063|  
  
<a name="diagnostic68"></a>   
## <a name="68-dbparameterprecision-and-dbparameterscale-are-now-public-virtual-members"></a>68: DbParameter.Precision and DbParameter.Scale are now public virtual members  
  
|||  
|-|-|  
|Dettagli|DbParameter.Precision e DbParameter.Scale sono implementati come proprietà virtuali pubbliche. Sostituiscono le corrispondenti implementazioni esplicite dell'interfaccia DbParameter.IDbDataParameter.Precision e DbParameter.IDbDataParameter.Scale.|  
|Suggerimento|Quando si ricompila un provider di database ADO.NET, queste differenze richiederanno l'applicazione della parola chiave 'override' alle proprietà Precision e Scale. Questo è necessario solo quando si ricompilano i componenti. I file binari esistenti continueranno a funzionare.|  
|Ambito|Secondario|  
|Versione|4.5.1|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Data.Common.DbParameter.Precision?displayProperty=fullName><br /><br /> <xref:System.Data.Common.DbParameter.Scale?displayProperty=fullName>|  
|Analizzatori|CD0068|  
  
<a name="diagnostic73"></a>   
## <a name="73-dataobjectgetdata-now-retrieves-data-as-utf-8"></a>73: DataObject.GetData now retrieves data as UTF-8  
  
|||  
|-|-|  
|Dettagli|Per le app destinate a .NET Framework 4 o che vengono eseguite in .NET Framework 4.5.1 o versioni precedenti, DataObject.GetData recupera dati in formato HTML sotto forma di stringa ASCII. Di conseguenza, i caratteri non ASCII, ovvero quelli i cui codici ASCII sono maggiori di 0x7F, vengono rappresentati da due caratteri casuali.<br /><br /> Per le app destinate a .NET Framework 4.5 o versione successiva ed eseguite in .NET Framework 4.5.2, `DataObject.GetData` recupera i dati in formato HTML come UTF-8, che rappresenta correttamente i caratteri con codici maggiori di 0x7F.|  
|Suggerimento|Se è stata implementata una soluzione alternativa per il problema di codifica con le stringhe in formato HTML, ad esempio codificando in modo esplicito la stringa HTML recuperata dagli Appunti passandola al metodo UTF8Encoding.GetString, e si intende ridestinare l'app dalla versione 4 alla versione 4.5, è necessario rimuovere questa soluzione alternativa.<br /><br /> Se per qualche motivo è necessario il comportamento precedente, l'app può essere destinata a .NET Framework 4.0 per ottenere tale comportamento.|  
|Ambito|Microsoft Edge|  
|Versione|4.5.2|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Windows.DataObject.GetData%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Windows.DataObject.GetData%28System.String%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Windows.DataObject.GetData%28System.Type%29?displayProperty=fullName>|  
|Analizzatori|CD0073|  
  
<a name="diagnostic75"></a>   
## <a name="75-targetframeworkname-for-default-app-domain-no-longer-defaults-to-null-if-not-set"></a>75: TargetFrameworkName for default app domain no longer defaults to null if not set  
  
|||  
|-|-|  
|Dettagli|La proprietà TargetFrameworkName era precedentemente null nel dominio dell'app predefinito, se non impostata in modo esplicito. A partire dalla versione 4.6, la proprietà TargetFrameworkName per il dominio dell'app predefinito avrà un valore predefinito derivato da TargetFrameworkAttribute, se presente. I domini dell'app non predefiniti continueranno a ereditare la proprietà TargetFrameworkName dal dominio dell'app predefinito, che non sarà impostata su null per impostazione predefinita nella versione 4.6, a meno che non sia sottoposta a override in modo esplicito.|  
|Suggerimento|Il codice deve essere aggiornato in modo che non dipenda dal fatto che l'impostazione predefinita di `AppDomainSetup.TargetFrameworkName` sia null. Se è necessario che questa proprietà continui a restituire null, è possibile impostarla in modo esplicito su tale valore.|  
|Ambito|Microsoft Edge|  
|Versione|4.6|  
|Tipo|Runtime|  
|API interessate|<xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=fullName>|  
|Analizzatori|CD0075B<br /><br /> CD0075A|  
  
<a name="diagnostic76"></a>   
## <a name="76-x509certificate2tostringbool-does-not-throw-now-when-net-cannot-handle-the-certificate"></a>76: X509Certificate2.ToString(bool) does not throw now when .NET cannot handle the certificate  
  
|||  
|-|-|  
|Dettagli|Nelle versioni precedenti questo metodo genere un'eccezione se viene passato il valore 'true' per il parametro verbose e sono presenti certificati installati non supportati da .NET Framework. Il metodo viene ora completato e restituisce una stringa valida che omette le parti inaccessibili del certificato.|  
|Suggerimento|È consigliabile aggiornare qualsiasi codice che dipende da X509Certificate2.ToString(bool), in modo da prevedere che la stringa restituita possa escludere alcuni dati del certificato (ad esempio la chiave pubblica, la chiave privata e le estensioni) in alcuni casi in cui l'API avrebbe precedentemente generato un'eccezione.|  
|Ambito|Microsoft Edge|  
|Versione|4.6|  
|Tipo|Runtime|  
|API interessate|<xref:System.Security.Cryptography.X509Certificates.X509Certificate2.ToString%28System.Boolean%29?displayProperty=fullName>|  
|Analizzatori|CD0076|  
  
<a name="diagnostic77"></a>   
## <a name="77-reflection-objects-can-no-longer-be-passed-from-managed-code-to-out-of-process-dcom-clients"></a>77: Reflection objects can no longer be passed from managed code to out-of-process DCOM clients  
  
|||  
|-|-|  
|Dettagli|Gli oggetti di reflection non possono essere più passati dal codice gestito ai client DCOM out-of-process. Sono interessati i tipi seguenti:<br /><br /> Assembly<br /><br /> MemberInfo e i tipi derivati, inclusi FieldInfo, MethodInfo, Type e TypeInfo<br /><br /> MethodBody<br /><br /> Modulo<br /><br /> ParameterInfo.<br /><br /> Le chiamate a `IMarshal` per l'oggetto restituiscono `E_NOINTERFACE`.|  
|Suggerimento|Aggiornare il codice di marshalling in modo che funzioni con oggetti non di reflection|  
|Ambito|Secondario|  
|Versione|4.6|  
|Tipo|Runtime|  
|Analizzatori|CD0077|  
  
<a name="diagnostic78"></a>   
## <a name="78-contentdisposition-datetimes-returns-slightly-different-string"></a>78: ContentDisposition DateTimes returns slightly different string  
  
|||  
|-|-|  
|Dettagli|Le rappresentazioni di stringa di ContentDisposition sono state aggiornate, a partire dalla versione 4.6, in modo da rappresentare sempre il componente dell'ora di un valore DateTime con due cifre. Questo comportamento è conforme a [RFC822](http://www.ietf.org/rfc/rfc0822.txt) e [RFC2822](http://www.ietf.org/rfc/rfc2822.txt). Ne consegue che `ContentDisposition.ToString` restituisce una stringa leggermente diversa nella versione 4.6 negli scenari in cui uno degli elementi di tempo della disposizione precede le 10.00. Si noti che i valori di ContentDisposition vengono a volte serializzati convertendoli in stringhe, pertanto è necessario verificare qualsiasi operazione ContentDisposition.ToString, la serializzazione o le chiamate di GetHashCode.|  
|Suggerimento|Non dare per scontato che le rappresentazioni di stringa di ContentDisposition da versioni diverse di .NET Framework vengano confrontate correttamente. Se possibile, riconvertire le stringhe in ContentDisposition prima di eseguire un confronto.|  
|Ambito|Secondario|  
|Versione|4.6|  
|Tipo|Runtime|  
|API interessate|<xref:System.Net.Mime.ContentDisposition.GetHashCode?displayProperty=fullName><br /><br /> <xref:System.Net.Mime.ContentDisposition.ToString?displayProperty=fullName>|  
|Analizzatori|CD0078|  
  
<a name="diagnostic82"></a>   
## <a name="82-workflowdesignerload-doesnt-remove-symbol-property"></a>82: WorkflowDesigner.Load doesn't remove symbol property  
  
|||  
|-|-|  
|Dettagli|Se si usa .NET Framework 4.5 come destinazione in Progettazione flussi di lavoro e si carica un flusso di lavoro 3.5 riallocato con il metodo WorkflowDesigner.Load(), viene generata un'eccezione XamlDuplicateMemberException durante il salvataggio del flusso di lavoro.|  
|Suggerimento|Questo bug si manifesta solo quando si seleziona .NET Framework 4.5 come destinazione in Progettazione flussi di lavoro, quindi è possibile evitarlo impostando `WorkflowDesigner.Context.Services.GetService<DesignerConfigurationService>().TargetFrameworkName` su .NET Framework 4.0.<br /><br /> In alternativa, il problema può essere evitato usando il metodo [WorkflowContext.Load(string)](https://msdn.microsoft.com/library/ee425926\(v=vs.110\).aspx) per caricare il flusso di lavoro, invece di [WorkflowDesigner.Load()](https://msdn.microsoft.com/library/ee403482\(v=vs.110\).aspx).|  
|Ambito|Principale|  
|Versione|4.5-4.5.2|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Activities.Presentation.WorkflowDesigner.Load?displayProperty=fullName>|  
|Analizzatori|CD0082|  
  
<a name="diagnostic83"></a>   
## <a name="83-sqlconnectionopen-fails-on-windows-7-with-non-ifs-winsock-bsp-or-lsp-present"></a>83: SqlConnection.Open fails on Windows 7 with non-IFS Winsock BSP or LSP present  
  
|||  
|-|-|  
|Dettagli|SqlConnection.Open e OpenAsync hanno esito negativo in .NET Framework 4.5 se in esecuzione in un computer Windows 7 in cui sono presenti un provider LSP o BSP Winsock non IFS.<br /><br /> Per determinare se è installato un provider LSP o BSP non-IFS, usare il comando `netsh WinSock Show Catalog` ed esaminare ogni elemento `Winsock Catalog Provider Entry` restituito. Se per il valore Service Flags è impostato il bit `0x20000`, il provider usa handle IFS e funzionerà correttamente. Se il bit `0x20000` non è impostato, si tratta di un LSP o BSP non-IFS.|  
|Suggerimento|Questo bug è stato risolto in .NET Framework 4.5.2, pertanto può essere evitato eseguendo l'aggiornamento di .NET Framework. In alternativa, è possibile evitarlo rimuovendo qualsiasi provider LSP Winsock non-IFS installato.|  
|Ambito|Secondario|  
|Versione|4.5-4.5.2|  
|Tipo|Runtime|  
|API interessate|<xref:System.Data.SqlClient.SqlConnection.Open?displayProperty=fullName><br /><br /> <xref:System.Data.SqlClient.SqlConnection.OpenAsync%28System.Threading.CancellationToken%29?displayProperty=fullName>|  
|Analizzatori|CD0083|  
  
<a name="diagnostic84"></a>   
## <a name="84-icommandcanexecutechanged-event-behaviour-changed-in-net-45"></a>84: ICommand.CanExecuteChanged event behaviour changed in .NET 4.5  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4.5, un CanExecuteChangedEvent viene ignorato a meno che il mittente dell'evento non sia lo stesso oggetto di quello che ha generato l'evento. Questo bug è stato risolto con gli aggiornamenti di manutenzione di .NET Framework 4.5.|  
|Suggerimento|Questo bug è stato risolto nelle service release di .NET Framework 4.5, quindi può essere evitato assicurandosi che .NET Framework sia aggiornato oppure eseguendo l'aggiornamento a .NET Framework 4.5.1. In alternativa, è possibile modificare il codice dell'applicazione che usa ICommand per assicurarsi che il mittente quando viene generato un comando CanExecuteChanged sia lo stesso dell'oggetto che genera l'evento.|  
|Ambito|Secondario|  
|Versione|4.5-4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Input.ICommand.CanExecuteChanged?displayProperty=fullName>|  
|Analizzatori|CD0084|  
  
<a name="diagnostic85"></a>   
## <a name="85-some-net-apis-cause-first-chance-handled-entrypointnotfoundexceptions"></a>85: Some .NET APIs cause first chance (handled) EntryPointNotFoundExceptions  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4.5, un numero limitato di metodi .NET ha iniziato a generare eccezioni EntryPointNotFoundException first-chance. Queste eccezioni sono gestite all'interno di .NET Framework, ma possono interrompere l'automazione dei test che non si aspettano eccezioni first-chance. Queste stesse API causano errori in alcuni scenari di ApiVerifier con HighVersionLie abilitato.|  
|Suggerimento|È possibile evitare questo bug eseguendo l'aggiornamento a .NET Framework 4.5.1. In alternativa, è possibile aggiornare l'automazione dei test in modo che non si interrompa in corrispondenza della prima EntryPointNotFoundException first-chance.|  
|Ambito|Microsoft Edge|  
|Versione|4.5-4.5.1|  
|Tipo|Runtime|  
|API interessate|<xref:System.Diagnostics.Debug.Assert%28System.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Diagnostics.Debug.Assert%28System.Boolean%2CSystem.String%29?displayProperty=fullName><br /><br /> <xref:System.Diagnostics.Debug.Assert%28System.Boolean%2CSystem.String%2CSystem.String%29?displayProperty=fullName><br /><br /> <xref:System.Diagnostics.Debug.Assert%28System.Boolean%2CSystem.String%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName><br /><br /> <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%29?displayProperty=fullName>|  
|Analizzatori|CD0085|  
  
<a name="diagnostic86"></a>   
## <a name="86-scrolling-a-wpf-treeview-or-grouped-listbox-in-a-virtualizingstackpanel-can-cause-a-hang"></a>86: Scrolling a WPF TreeView or grouped ListBox in a VirtualizingStackPanel can cause a hang  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4.5, lo scorrimento di un controllo TreeView WPF in un pannello Stack virtualizzato può causare blocchi se sono presenti margini nel viewport (tra gli elementi nel controllo TreeView, ad esempio, o in un elemento ItemsPresenter). In alcuni casi, inoltre, elementi di dimensioni diverse nella visualizzazione possono causare instabilità anche se non sono presenti margini.|  
|Suggerimento|È possibile evitare questo bug eseguendo l'aggiornamento a .NET Framework 4.5.1. In alternativa, i margini possono essere rimossi dalle raccolte di visualizzazioni (ad esempio TreeView) all'interno di pannelli Stack virtualizzati, se tutti gli elementi contenuti sono della stessa dimensione.|  
|Ambito|Principale|  
|Versione|4.5-4.5.1|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Controls.VirtualizingPanel.SetIsVirtualizing%28System.Windows.DependencyObject%2CSystem.Boolean%29?displayProperty=fullName>|  
|Analizzatori|CD0086<br /><br /> CD0086|  
  
<a name="diagnostic89"></a>   
## <a name="89-typeisassignablefrom-returns-wrong-result-for-generic-variables-with-constraints"></a>89: Type.IsAssignableFrom returns wrong result for generic variables with constraints  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4.5, Type.IsAssignableFrom restituisce erroneamente `false` in tutti i casi per alcuni tipi generici con vincoli.|  
|Suggerimento|Questo problema è stato risolto in un aggiornamento di manutenzione. Per risolvere questo problema, aggiornare .NET Framework 4.5 o eseguire l'aggiornamento a .NET Framework 4.5.1 o versioni successive. In alternativa, evitare di usare IsAssignableFrom con tipi generici che hanno vincoli su parametri generici. Le API reflection possono essere usate come alternativa.|  
|Ambito|Secondario|  
|Versione|4.5-4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Type.IsAssignableFrom%28System.Type%29?displayProperty=fullName>|  
|Analizzatori|CD0089<br /><br /> CD0089|  
  
<a name="diagnostic91"></a>   
## <a name="91-entityframework-60-loads-very-slowly-in-apps-launched-from-visual-studio"></a>91: EntityFramework 6.0 loads very slowly in apps launched from Visual Studio  
  
|||  
|-|-|  
|Dettagli|L'avvio di un'app da Visual Studio 2013 che usa EntityFramework 6.0 può essere molto lento.|  
|Suggerimento|Questo problema è risolto in EntityFramework 6.0.2. Aggiornare EntityFramework per evitare il problema di prestazioni.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0091|  
  
<a name="diagnostic92"></a>   
## <a name="92-multi-line-aspnet-textbox-spacing-changed-when-using-antixssencoder"></a>92: Multi-line ASP.Net TextBox spacing changed when using AntiXSSEncoder  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4.0 vengono inserite righe aggiuntive tra le righe di una casella di testo a più righe durante il postback, se si usa `AntiXSSEncoder`. In .NET Framework 4.5 queste interruzioni di riga aggiuntive non vengono incluse, ma solo se l'app Web è destinata a .NET 4.5|  
|Suggerimento|Tenere presente che nelle app Web 4.0 ridestinate a .NET 4.5, le caselle di testo a più righe possono essere migliorate in modo che non vengano più inserite interruzioni di riga aggiuntive. Se non è auspicabile, l'app può avere il comportamento precedente quando viene eseguita in .NET Framework 4.5 usando .NET Framework 4.0 come destinazione.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0092|  
  
<a name="diagnostic95"></a>   
## <a name="95-concurrentqueuettrypeek-can-return-an-erroneous-null-via-its-out-parameter"></a>95: ConcurrentQueue\<T>.TryPeek can return an erroneous null via its out parameter  
  
|||  
|-|-|  
|Dettagli|In alcuni scenari multithread, `ConcurentQueue<T>.TryPeek` può restituire true, ma popolare il parametro di output con un valore null, anziché il valore corretto, restituito.|  
|Suggerimento|Questo problema è risolto in .NET Framework 4.5.1. L'aggiornamento a questa versione di .NET Framework consentirà di risolvere il problema.|  
|Ambito|Principale|  
|Versione|4.5-4.5.1|  
|Tipo|Runtime|  
|API interessate|<xref:System.Collections.Concurrent.ConcurrentQueue%601.TryPeek%28%600%40%29?displayProperty=fullName>|  
|Analizzatori|CD0095|  
  
<a name="diagnostic98"></a>   
## <a name="98-multiple-items-in-a-single-tablelayoutpanel-cell-may-be-rearranged"></a>98: Multiple items in a single TableLayoutPanel cell may be rearranged  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4.5, se più elementi vengono inseriti nella stessa cella di TableLayoutPanel, potrebbero essere visualizzati in un ordine diverso rispetto a .NET Framework 4.0.|  
|Suggerimento|Questo comportamento è stato ripristinato in un aggiornamento di manutenzione per .NET Framework 4.5. Per risolvere questo problema, aggiornare .NET Framework 4.5 o eseguire l'aggiornamento a .NET Framework 4.5.1 o versioni successive. In alternativa, evitare il caso ambiguo di più elementi nella stessa cella di TableLayourPanel.|  
|Ambito|Secondario|  
|Versione|4.5-4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Forms.TableLayoutControlCollection.Add%28System.Windows.Forms.Control%2CSystem.Int32%2CSystem.Int32%29?displayProperty=fullName>|  
|Analizzatori|CD0098|  
  
<a name="diagnostic100"></a>   
## <a name="100-foreach-iterator-variable-is-now-scoped-within-the-iteration-so-closure-capturing-semantics-are-different-in-c5"></a>100: Foreach iterator variable is now scoped within the iteration, so closure capturing semantics are different (in C#5)  
  
|||  
|-|-|  
|Dettagli|A partire da C# 5 (Visual Studio 2012), le variabili iteratore foreach hanno ambito limitato all'interno dell'iterazione. Ciò può causare interruzioni se codice dipende dal fatto che le variabili non siano incluse nella chiusura di foreach. Il sintomo di questa modifica è che una variabile iteratore passata a un delegato verrà gestita come avente il valore esistente al momento della creazione del delegato, anziché il valore esistente al momento della chiamata del delegato.|  
|Suggerimento|Idealmente, è consigliabile aggiornare il codice in modo che tenga conto del nuovo comportamento del compilatore. Se è richiesta la semantica precedente, la variabile iteratore può essere sostituita con una variabile separata che viene inserita in modo esplicito all'esterno dell'ambito del ciclo.|  
|Ambito|Principale|  
|Versione|4.5|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0100|  
  
<a name="diagnostic101"></a>   
## <a name="101-htmltextwriter-does-not-render-br-element-correctly"></a>101: HtmlTextWriter does not render \`<br/\>` element correctly  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.6, la chiamata di `HtmlTextWriter.RenderBeginTag()` e `HtmlTextWriter.RenderEndTag()` con un elemento `<BR />` inserirà correttamente solo un `<BR />` (invece di due)|  
|Suggerimento|Se un'app dipende dal tag `<BR />` aggiuntivo, il metodo `HtmlTextWriter.RenderBeginTag()` deve essere chiamato una seconda volta. Si noti che questa modifica di comportamento influisce solo sulle app destinate a .NET Framework 4.6, quindi è possibile in alternativa selezionare una versione precedente di .NET Framework come destinazione per ottenere il comportamento precedente.|  
|Ambito|Microsoft Edge|  
|Versione|4.6|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Web.UI.HtmlTextWriter.RenderBeginTag%28System.String%29?displayProperty=fullName><br /><br /> <xref:System.Web.UI.HtmlTextWriter.RenderBeginTag%28System.Web.UI.HtmlTextWriterTag%29?displayProperty=fullName>|  
|Analizzatori|CD0101|  
  
<a name="diagnostic104"></a>   
## <a name="104-calling-itemsrefresh-on-a-wpf-listbox-listview-or-datagrid-with-items-selected-can-cause-duplicate-items-to-appear-in-the-element"></a>104: Calling Items.Refresh on a WPF ListBox, ListView, or DataGrid with items selected can cause duplicate items to appear in the element  
  
|||  
|-|-|  
|Dettagli|In .NET Framework 4.5, la chiamata di ListBox.Items.Refresh dal codice mentre sono presenti elementi selezionati in un controllo ListBox può causare la duplicazione degli elementi selezionati nell'elenco. Si verifica un problema simile con ListView e DataGrid. Questo problema è risolto in .NET Framework 4.6.|  
|Suggerimento|Questo problema può essere evitato deselezionando gli elementi a livello di codice prima della chiamata di Refresh, per poi selezionarli di nuovo dopo il completamento della chiamata. In alternativa, questo problema è stato corretto in .NET Framework 4.6 e può essere risolto eseguendo l'aggiornamento a tale versione di .NET Framework.|  
|Ambito|Secondario|  
|Versione|4.5-4.6|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Data.CollectionView.Refresh?displayProperty=fullName>|  
|Analizzatori|CD0104|  
  
<a name="diagnostic105"></a>   
## <a name="105-etw-eventlisteners-do-not-capture-events-from-providers-with-explicit-keywords-like-the-tpl-provider"></a>105: ETW EventListeners do not capture events from providers with explicit keywords (like the TPL provider)  
  
|||  
|-|-|  
|Dettagli|Gli EventListener ETW con una maschera di parole chiave vuota non acquisiscono correttamente gli eventi dai provider con parole chiave esplicite. In .NET Framework 4.5, il provider TPL ha iniziato a fornire parole chiave esplicite e ha causato questo problema. In .NET Framework 4.6, gli EventListener sono stati aggiornati e non presentano più questo problema.|  
|Suggerimento|Per risolvere questo problema, sostituire le chiamate a EnableEvents (eventSource, level) con chiamate all'overload di EnableEvents che specifica in modo esplicito la maschera "qualsiasi parola chiave" da usare: `EnableEvents(eventSource, level, unchecked((EventKeywords)0xFFFFffffFFFFffff))`.<br /><br /> In alternativa, questo problema è stato corretto in .NET Framework 4.6 e può essere risolto eseguendo l'aggiornamento a tale versione di .NET Framework.|  
|Ambito|Microsoft Edge|  
|Versione|4.5-4.6|  
|Tipo|Runtime|  
|API interessate|<xref:System.Diagnostics.Tracing.EventListener.EnableEvents%28System.Diagnostics.Tracing.EventSource%2CSystem.Diagnostics.Tracing.EventLevel%29?displayProperty=fullName>|  
|Analizzatori|CD0105|  
  
<a name="diagnostic109"></a>   
## <a name="109-building-an-entity-framework-edmx-with-visual-studio-2013-can-fail-with-error-msb4062-if-using-the-entitydeploysplit-or-entityclean-tasks"></a>109: Building an Entity Framework edmx with Visual Studio 2013 can fail with error MSB4062 if using the EntityDeploySplit or EntityClean tasks  
  
|||  
|-|-|  
|Dettagli|Gli strumenti di MSBuild 12.0 (inclusi in Visual Studio 2013) hanno modificato i percorsi dei file msbuild, invalidando i vecchi file di destinazioni di Entity Framework. Il risultato è che le attività `EntityDeploySplit` e `EntityClean` hanno esito negativo perché non sono in grado di trovare `Microsoft.Data.Entity.Build.Tasks.dll`. Si noti che questo problema è causato da una modifica del set di strumenti (msbuild/VS) e non da una modifica di .NET Framework. Si verificherà solo quando si aggiornano gli strumenti di sviluppo, e non aggiornando semplicemente .NET Framework.|  
|Suggerimento|I file di destinazioni di Entity Framework sono stati corretti per supportare il nuovo layout msbuild a partire da .NET Framework 4.6. L'aggiornamento a tale versione di .NET Framework consentirà di risolvere questo problema. In alternativa, è possibile usare [questa](http://stackoverflow.com/a/24249247/131944) soluzione alternativa per applicare una patch ai file di destinazioni direttamente.|  
|Ambito|Principale|  
|Versione|4.5.1-4.6|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0109|  
  
<a name="diagnostic111"></a>   
## <a name="111-xsd-schema-validation-now-correctly-detects-violations-of-unique-constraints-if-compound-keys-are-used-and-one-key-is-empty"></a>111: XSD Schema validation now correctly detects violations of unique constraints if compound keys are used and one key is empty  
  
|||  
|-|-|  
|Dettagli|Le versioni di .NET Framework precedenti alla 4.6 includono un bug a causa del quale la convalida XSD non rileva vincoli univoci per le chiavi composte se una delle chiavi è vuota. Questo problema è stato corretto in .NET Framework 4.6. La convalida sarà più corretta, ma è possibile che la convalida di alcuni file XML abbia esito negativo, diversamente da quanto accadeva in precedenza.|  
|Suggerimento|Se è necessario usare la convalida .NET Framework 4.0 meno restrittiva, l'applicazione da convalidare può essere destinata alla versione 4.5 (o versioni precedenti) di .NET Framework. In caso di ridestinazione alla versione .NET 4.6, tuttavia, è necessario rivedere il codice per assicurarsi che non sia prevista la convalida per le chiavi composte duplicate, come descritto nella descrizione di questo problema.|  
|Ambito|Microsoft Edge|  
|Versione|4.6|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0111|  
  
<a name="diagnostic112"></a>   
## <a name="112-calling-attributegetcustomattributes-on-an-indexer-property-no-longer-throws-ambiguousmatchexception-if-the-ambiguity-can-be-resolved-by-indexs-type"></a>112: Calling Attribute.GetCustomAttributes on an indexer property no longer throws AmbiguousMatchException if the ambiguity can be resolved by index's type  
  
|||  
|-|-|  
|Dettagli|Prima di .NET Framework 4.6, la chiamata di `GetCustomAttribute(s)` su una proprietà indicizzatore diversa da un'altra proprietà solo per il tipo di indice genera una eccezione `AmbiguousMatchException`. A partire da .NET Framework 4.6, gli attributi della proprietà verranno restituiti correttamente.|  
|Suggerimento|Tenere presente che GetCustomAttribute funzionerà più frequentemente. Se un'app dipende da `AmbiguousMatchException` nelle versioni precedenti, è ora necessario usare la reflection per cercare in modo esplicito più indicizzatori.|  
|Ambito|Microsoft Edge|  
|Versione|4.6|  
|Tipo|Runtime|  
|API interessate|<xref:System.Attribute.GetCustomAttribute%28System.Reflection.MemberInfo%2CSystem.Type%29?displayProperty=fullName><br /><br /> <xref:System.Attribute.GetCustomAttribute%28System.Reflection.MemberInfo%2CSystem.Type%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Attribute.GetCustomAttributes%28System.Reflection.MemberInfo%29?displayProperty=fullName><br /><br /> <xref:System.Attribute.GetCustomAttributes%28System.Reflection.MemberInfo%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Attribute.GetCustomAttributes%28System.Reflection.MemberInfo%2CSystem.Type%29?displayProperty=fullName><br /><br /> <xref:System.Attribute.GetCustomAttributes%28System.Reflection.MemberInfo%2CSystem.Type%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttribute%28System.Reflection.MemberInfo%2CSystem.Type%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttribute%28System.Reflection.MemberInfo%2CSystem.Type%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttribute%60%601%28System.Reflection.MemberInfo%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttribute%60%601%28System.Reflection.MemberInfo%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttributes%28System.Reflection.MemberInfo%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttributes%28System.Reflection.MemberInfo%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttributes%28System.Reflection.MemberInfo%2CSystem.Type%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttributes%28System.Reflection.MemberInfo%2CSystem.Type%2CSystem.Boolean%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttributes%60%601%28System.Reflection.MemberInfo%29?displayProperty=fullName><br /><br /> <xref:System.Reflection.CustomAttributeExtensions.GetCustomAttributes%60%601%28System.Reflection.MemberInfo%2CSystem.Boolean%29?displayProperty=fullName>|  
|Analizzatori|CD0112|  
  
<a name="diagnostic113"></a>   
## <a name="113-intermittently-unable-to-scroll-to-bottom-item-in-itemscontrols-like-listbox-and-datagrid-when-using-custom-datatemplates"></a>113: Intermittently unable to scroll to bottom item in ItemsControls (like ListBox and DataGrid) when using custom DataTemplates  
  
|||  
|-|-|  
|Dettagli|In alcuni casi, a causa di un bug in .NET Framework 4.5 i controlli ItemsControl (come ListBox, ComboBox, DataGrid e così via) non scorrono fino all'elemento inferiore quando si usano DataTemplate personalizzati. Lo scorrimento funzionerà se si esegue un secondo tentativo dopo uno scorrimento verso l'alto.|  
|Suggerimento|Questo problema è stato corretto in .NET Framework 4.5.2 e può essere risolto eseguendo l'aggiornamento a tale versione di .NET Framework o a una versione successiva. In alternativa, gli utenti possono trascinare le barre di scorrimento fino agli elementi finali di queste raccolte, ma potrebbe essere necessario provare due volte per completare l'operazione correttamente.|  
|Ambito|Secondario|  
|Versione|4.5-4.5.2|  
|Tipo|Runtime|  
|Analizzatori|CD0113|  
  
<a name="diagnostic114"></a>   
## <a name="114-glyphruncomputeinkboundingbox-and-formattedtextextent-return-different-values-beginning-in-net-45"></a>114: GlyphRun.ComputeInkBoundingBox() and FormattedText.Extent return different values beginning in .NET 4.5  
  
|||  
|-|-|  
|Dettagli|Sono stati apportati miglioramenti a GlyphRun.ComputeInkBoundingBox() e FormattedText.Extent in .NET Framework 4.5 per risolvere i problemi a causa dei quali i rettangoli di selezione sono troppo piccoli per i glifi contenuti in alcuni casi in .NET Framework 4.0. Ne consegue che alcuni rettangoli di selezione sono più grandi a partire da .NET Framework 4.5 e quindi si noteranno alcune piccole differenze nel layout dell'interfaccia utente.|  
|Suggerimento|Tenere presente che le dimensioni di alcuni rettangoli di selezione con glifi sono aumentate. Queste modifiche consentiranno in genere di migliorare la presentazione e l'hit testing per i rettangoli, ma se si preferisce il comportamento precedente alla versione .NET 4.5, è possibile sceglierlo in modo esplicito aggiungendo la voce seguente al file app.config:<br /><br /> `<appsettings> <add key="IncludeAllInkInBoundingBox" value="false"> </appsettings>`|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Media.GlyphRun.ComputeInkBoundingBox?displayProperty=fullName><br /><br /> <xref:System.Windows.Media.FormattedText.Extent?displayProperty=fullName>|  
|Analizzatori|CD0114|  
  
<a name="diagnostic124"></a>   
## <a name="124-calling-datagridcommitedit-from-a-celleditending-handler-drops-focus"></a>124: Calling DataGrid.CommitEdit from a CellEditEnding handler drops focus  
  
|||  
|-|-|  
|Dettagli|La chiamata di DataGrid.CommitEdit da uno dei gestori di eventi CellEditEnding di DataGrid causa la perdita dello stato attivo per DataGrid.|  
|Suggerimento|Questo bug è stato risolto in .NET Framework 4.5.2, pertanto può essere evitato eseguendo l'aggiornamento di .NET Framework. In alternativa, è possibile evitarlo selezionando di nuovo in modo esplicito DataGrid dopo la chiamata di CommitEdit.|  
|Ambito|Microsoft Edge|  
|Versione|4.5-4.5.2|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.Controls.DataGrid.CommitEdit?displayProperty=fullName><br /><br /> <xref:System.Windows.Controls.DataGrid.CommitEdit%28System.Windows.Controls.DataGridEditingUnit%2CSystem.Boolean%29?displayProperty=fullName>|  
|Analizzatori|CD0124|  
  
<a name="diagnostic125"></a>   
## <a name="125-aspnet-mvc-now-escapes-spaces-in-strings-passed-in-via-route-parameters"></a>125: ASP.NET MVC now escapes spaces in strings passed in via route parameters  
  
|||  
|-|-|  
|Dettagli|Per conformità allo standard RFC 2396, vengono ora usati caratteri di escape per gli spazi nei percorsi di route durante il popolamento dei parametri di azione da una route. Pertanto, mentre `/controller/action/some data` in precedenza corrispondeva alla route `/controller/action/{data}` e forniva il parametro dati `some data`, ora fornisce invece `some%20data`.|  
|Suggerimento|È necessario aggiornare il codice per rimuovere i caratteri di escape dai parametri stringa da una route. Se è necessario l'URI originale, è possibile accedervi con l'API Request.RequestUri.OriginalString.|  
|Ambito|Secondario|  
|Versione|4.5.2|  
|Tipo|Runtime|  
|API interessate|[System.Web.Http.RouteAttribute](https://msdn.microsoft.com/library/system.web.http.routeattribute(v=vs.118).aspx)|  
|Analizzatori|CD0125|  
  
<a name="diagnostic127"></a>   
## <a name="127-vbnet-no-longer-supports-partial-namespace-qualification-for-systemwindows-apis"></a>127: VB.NET no longer supports partial namespace qualification for System.Windows APIs  
  
|||  
|-|-|  
|Dettagli|A partire da .NET 4.5.2, i progetti VB.NET non possono specificare API System.Windows con spazi dei nomi parzialmente qualificati. Ad esempio, un riferimento a `Windows.Forms.DialogResult` avrà esito negativo. Il codice deve invece fare riferimento al nome completo (`System.Windows.Forms.DialogResult`) o importare lo spazio dei nomi specifico e fare semplicemente riferimento a `DialogResult`.|  
|Suggerimento|È consigliabile aggiornare il codice in modo che faccia riferimento alle API `System.Windows` tramite nomi semplici (e importare lo spazio dei nomi rilevante) o con nomi completi.|  
|Ambito|Secondario|  
|Versione|4.5.2|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0127|  
  
<a name="diagnostic129"></a>   
## <a name="129-two-way-data-binding-to-a-property-with-a-non-public-setter-is-not-supported"></a>129: Two-way data-binding to a property with a non-public setter is not supported  
  
|||  
|-|-|  
|Dettagli|Il data binding per una proprietà senza un setter pubblico non è mai stata uno scenario supportato. A partire da .NET Framework 4.5.1, questo scenario genererà un'eccezione InvalidOperationException. Si noti che la nuova eccezione verrà generata soltanto per le app destinate specificamente a .NET Framework 4.5.1. Per le app destinate a .NET Framework 4.5, la chiamata sarà consentita. Se l'app non è destinata a una versione specifica di .NET Framework, l'associazione verrà considerata unidirezionale.|  
|Suggerimento|È consigliabile aggiornare l'app per usare l'associazione unidirezionale o esporre pubblicamente il setter della proprietà. In alternativa, è possibile destinare l'app a .NET Framework 4.5 per ottenere il comportamento precedente.|  
|Ambito|Secondario|  
|Versione|4.5.1|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Windows.Data.BindingMode?displayProperty=fullName>|  
|Analizzatori|CD0129|  
  
<a name="diagnostic130"></a>   
## <a name="130-marshalsizeof-and-marshalptrtostructure-overloads-break-dynamic-code"></a>130: Marshal.SizeOf and Marshal.PtrToStructure overloads break dynamic code  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.5.1, l'associazione dinamica per i metodi `Marshal.SizeOf` o `Marshal.PtrToStructure` (ad esempio, tramite Windows PowerShell, IronPython o la parola chiave dynamic di C#) può causare eccezioni `MethodInvocationExceptions` perché sono stati aggiunti nuovi overload di questi metodi che potrebbero risultare ambigui per i motori di script.|  
|Suggerimento|Aggiornare gli script per indicare chiaramente quale overload deve essere usato. Questa operazione può essere eseguita in genere tramite il cast esplicito dei parametri di tipo dei metodi su `System.Type`. Vedere [questo collegamento](https://support.microsoft.com/kb/2909958/) per altri dettagli ed esempi per risolvere il problema.|  
|Ambito|Secondario|  
|Versione|4.5.1|  
|Tipo|Runtime|  
|Analizzatori|CD0130|  
  
<a name="diagnostic131"></a>   
## <a name="131-previewlostkeyboardfocus-is-called-repeatedly-if-its-handler-shows-a-windows-forms-message-box"></a>131: PreviewLostKeyboardFocus is called repeatedly if its handler shows a Windows Forms message box  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.5, la chiamata di `System.Windows.Forms.MessageBox.Show` da un gestore `UIElement.PreviewLostKeyboardFocus` causerà la riattivazione del gestore alla chiusura della finestra di messaggio, con un potenziale ciclo infinito di finestre di messaggio.|  
|Suggerimento|Esistono due modi per risolvere l'errore:<br /><br /> Può essere evitato chiamando `System.Windows.MessageBox.Show` invece di `System.Windows.Forms.MessageBox.Show`.<br /><br /> Può essere evitato visualizzando la finestra di messaggio da un gestore eventi `LostKeyboardFocus`, anziché un gestore eventi `PreviewLostKeyboardFocus`.|  
|Ambito|Microsoft Edge|  
|Versione|4.5|  
|Tipo|Runtime|  
|API interessate|<xref:System.Windows.ContentElement.PreviewLostKeyboardFocus?displayProperty=fullName><br /><br /> <xref:System.Windows.IInputElement.PreviewLostKeyboardFocus?displayProperty=fullName><br /><br /> <xref:System.Windows.UIElement.PreviewLostKeyboardFocus?displayProperty=fullName><br /><br /> <xref:System.Windows.UIElement3D.PreviewLostKeyboardFocus?displayProperty=fullName>|  
|Analizzatori|CD0131|  
  
<a name="diagnostic133"></a>   
## <a name="133-a-concurrentdictionary-serialized-in-net-45-with-netdatacontractserializer-cannot-be-deserialized-by-net-451-or-452"></a>133: A ConcurrentDictionary serialized in .NET 4.5 with NetDataContractSerializer cannot be deserialized by .NET 4.5.1 or 4.5.2  
  
|||  
|-|-|  
|Dettagli|A causa di modifiche interne del tipo, gli oggetti `System.Collections.Concurrent.ConcurrentDictionary` serializzati con .NET Framework 4.5 tramite `NetDataContractSerializer` non possono essere deserializzati in .NET Framework 4.5.1 o in .NET Framework 4.5.2.<br /><br /> Si noti che funziona l'operazione in direzione opposta, ovvero la serializzazione con .NET Framework 4.5.x e la deserializzazione con .NET Framework 4.5. Analogamente, tutte le operazioni di serializzazione tra versioni 4.x funzionano con .NET Framework 4.6.<br /><br /> Il problema non interessa la serializzazione e la deserializzazione con una sola versione di .NET Framework.|  
|Suggerimento|Se è necessario serializzare e deserializzare un oggetto ConcurrentDictionary tra .NET Framework 4.5 e .NET Framework 4.5.1/4.5.2, usare un serializzatore alternativo come il serializzatore DataContractSerializer o BinaryFormatter invece di NetDataContractSerializer.<br /><br /> In alternativa, dato che questo problema è stato corretto in .NET Framework 4.6 e possibile risolverlo eseguendo l'aggiornamento a tale versione di .NET Framework.|  
|Ambito|Secondario|  
|Versione|4.5.1-4.6|  
|Tipo|Runtime|  
|Analizzatori|CD0133|  
  
<a name="diagnostic134"></a>   
## <a name="134-persian-calendar-now-uses-the-hijri-solar-algorithm"></a>134: Persian calendar now uses the Hijri solar algorithm  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.6, la classe PersianCalendar usa l'algoritmo solare Hijri. La conversione di date tra il calendario PersianCalendar e altri calendari può produrre risultati leggermente diversi a partire da .NET Framework 4.6 per le date precedenti al 1800 o successive al 2023 (calendario gregoriano).<br /><br /> Inoltre, `PersianCalendar.MinSupportedDateTime` è ora `March 22, 0622 instead of March 21, 0622`.|  
|Suggerimento|Tenere presente che alcune date precedenti o successive potrebbero essere leggermente diverse quando si usa PersianCalendar in .NET 4.6. Inoltre, quando si serializzano le date tra processi che possono essere eseguiti in versioni diverse di .NET Framework, evitare di archiviarle come stringhe di data PersianCalendar, perché tali valori potrebbero essere diversi.|  
|Ambito|Secondario|  
|Versione|4.6|  
|Tipo|Runtime|  
|API interessate|<xref:System.Globalization.PersianCalendar?displayProperty=fullName>|  
|Analizzatori|CD0134|  
  
<a name="diagnostic138"></a>   
## <a name="138-calling-createdefaultauthorizationcontext-with-a-null-argument-has-changed"></a>138: Calling CreateDefaultAuthorizationContext with a null argument has changed  
  
|||  
|-|-|  
|Dettagli|L'implementazione dell'oggetto AuthorizationContext restituito da una chiamata al metodo `CreateDefaultAuthorizationContext(IList<IAuthorizationPolicy>)` con un argomento authorizationPolicies è cambiata in .NET Framework 4.6.|  
|Suggerimento|In rari casi, le app WCF che usano l'autenticazione personalizzata possono riscontrare differenze di comportamento. In questi casi è possibile ripristinare il comportamento precedente in due modi diversi:<br /><br /> Ricompilare l'app per destinarla a una versione precedente rispetto a .NET Framework 4.6. Per i servizi ospitati in IIS, usare l'elemento \<httpRuntime targetFramework="x.x" /> per destinare l'app a una versione precedente di .NET Framework.<br /><br /> Aggiungere la riga seguente alla sezione `<appSettings>` del file app.config: `<add key="appContext.SetSwitch:Switch.System.IdentityModel.EnableCachedEmptyDefaultAuthorizationContext" value="true" />`|  
|Ambito|Secondario|  
|Versione|4.6|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.IdentityModel.Policy.AuthorizationContext.CreateDefaultAuthorizationContext%28System.Collections.Generic.IList%7BSystem.IdentityModel.Policy.IAuthorizationPolicy%7D%29?displayProperty=fullName>|  
|Analizzatori|CD0138|  
  
<a name="diagnostic141"></a>   
## <a name="141-wpf-treeviewitem-must-be-used-within-a-treeview"></a>141: WPF TreeViewItem must be used within a TreeView  
  
|||  
|-|-|  
|Dettagli|È stata introdotta una modifica nella versione 4.5 che limita l'utilizzo di elementi TreeViewItem all'esterno di TreeView. Il problema può presentarsi nelle condizioni seguenti:<br /><br /> L'elemento padre visivo di TreeViewItem non è un pannello. (L'elemento padre di un TreeViewItem generato per un TreeView sarà un pannello)<br /><br /> TreeViewItem è un discendente di un VirtualizingStackPanel che funge da "host di elementi" per un controllo elenco (ListBox, DataGrid, ListView e così via). La virtualizzazione non deve essere abilitata.<br /><br /> VirtualizingStackPanel prevede lo scorrimento per elementi (`ScrollUnit="Item"`).<br /><br /> Qualcuno chiama `VirtualizingStackPanel.MakeVisible(v)` per scorrere fino a un elemento `v` e visualizzarlo. Questa operazione può essere eseguita in modo esplicito o implicito in diversi modi. Probabilmente il modo più comune è il semplice clic su `v` per spostare lo stato attivo della tastiera sull'elemento.<br /><br /> La catena elemento padre visivo da `v` a VirtualizingStackPanel passa attraverso TreeViewItem.<br /><br /> In altre parole, questo si verifica quando si usa un TreeViewItem all'esterno di un TreeView e l'utente fa clic su un discendente di TreeViewItem per visualizzarlo. Se non vi sono discendenti attivabili per TreeViewItem, non si noterà mai il problema. Un esempio di situazione in cui si verifica questo problema è quando un TreeViewItem corrisponde alla radice di un DataTemplate.  Quando si verifica il problema, viene generata un'eccezione InvalidCastException all'interno del framework WPF.|  
|Suggerimento|Verrà reso disponibile un hotfix per questo problema.|  
|Ambito|Secondario|  
|Versione|4.5|  
|Tipo|Runtime|  
|Analizzatori|CD0141|  
  
<a name="diagnostic143"></a>   
## <a name="143-x509certificateclaimsetfindclaims-considers-all-claimtypes"></a>143: X509CertificateClaimSet.FindClaims Considers All claimTypes  
  
|||  
|-|-|  
|Dettagli|Nelle app destinate a .NET Framework 4.6.1, se un set di attestazioni X509 viene inizializzato da un certificato con più voci DNS nel proprio campo SAN, il metodo FindClaims cerca di stabilire una corrispondenza con l'argomento claimType con tutte le voci DNS.<br /><br /> Per le app destinate a versioni precedenti di .NET Framework, il metodo FindClaims cerca di stabilire una corrispondenza con l'argomento claimType solo con l'ultima voce DNS.|  
|Suggerimento|Questa modifica riguarda solo le applicazioni destinate a .NET Framework 4.6.1. Questa modifica potrebbe essere disabilitata (o abilitata se la destinazione è una versione precedente alla 4.6.1) con l'opzione di compatibilità [DisableMultipleDNSEntries](https://msdn.microsoft.com/library/mt620030%28v=vs.110%29.aspx).|  
|Ambito|Secondario|  
|Versione|4.6.1|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%28System.String%2CSystem.String%29?displayProperty=fullName>|  
|Analizzatori|CD0143|  
  
<a name="diagnostic144"></a>   
## <a name="144-applicationfiltermessage-no-longer-throws-for-re-entrant-implementations-of-imessagefilterprefiltermessage"></a>144: Application.FilterMessage no longer throws for re-entrant implementations of IMessageFilter.PreFilterMessage  
  
|||  
|-|-|  
|Dettagli|Prima di .NET Framework 4.6.1, la chiamata di Application.FilterMessage con IMessageFilter.PreFilterMessage che chiama AddMessageFilter o RemoveMessageFilter (che chiama anche Application.DoEvents) causa un'eccezione IndexOutOfRangeException.<br /><br /> A partire dalle applicazioni destinate a .NET Framework 4.6.1, questa eccezione non viene più generata e si possono usare filtri rientranti come descritto in precedenza.|  
|Suggerimento|Tenere presente che Application.FilterMessage non genererà più un'eccezione per il comportamento IMessageFilter.PreFilterMessage rientrante descritto sopra. Questo problema riguarda solo le applicazioni destinate a .NET Framework 4.6.1.<br /><br /> Le app destinate a .NET Framework 4.6.1 possono rifiutare esplicitamente questa modifica (o le app destinate a versioni precedenti possono accettarla in modo esplicito) usando l'opzione di compatibilità [DontSupportReentrantFilterMessage](https://msdn.microsoft.com/library/mt620032%28v=vs.110%29.aspx).|  
|Ambito|Microsoft Edge|  
|Versione|4.6.1|  
|Tipo|Ridestinazione:|  
|API interessate|<xref:System.Windows.Forms.Application.FilterMessage%28System.Windows.Forms.Message%40%29?displayProperty=fullName>|  
|Analizzatori|CD0144|  
  
<a name="diagnostic145"></a>   
## <a name="145-currentculture-is-not-preserved-across-wpf-dispatcher-operations"></a>145: CurrentCulture is not preserved across WPF Dispatcher operations  
  
|||  
|-|-|  
|Dettagli|A partire da .NET Framework 4.6, le modifiche apportate a CurrentCulture o CurrentUICulture all'interno di un [Dispatcher](https://msdn.microsoft.com/library/system.windows.threading.dispatcher%28v=vs.110%29.aspx) andranno perdute al termine dell'operazione del dispatcher. In modo analogo, le modifiche apportate a CurrentCulture o CurrentUICulture all'esterno di un'operazione di Dispatcher potrebbero non essere disponibili quando viene eseguita l'operazione.<br /><br /> In pratica questo significa che le modifiche apportate a CurrentCulture e CurrentUICulture potrebbero non essere trasferite tra i callback dell'interfaccia utente di WPF e altro codice in un'applicazione WPF.<br /><br /> Ciò è dovuto a una modifica in [ExecutionContext](https://msdn.microsoft.com/library/system.threading.executioncontext%28v=vs.110%29.aspx) che causa l'archiviazione di CurrentCulture e CurrentUICulture nel contesto di esecuzione a partire dalle app destinate a .NET Framework 4.6. Le operazioni del dispatcher WPF archiviano il contesto di esecuzione usato per avviare l'operazione e ripristinano il contesto precedente dopo il completamento dell'operazione. Dato che CurrentCulture e CurrentUICulture fanno ora parte di tale contesto, le modifiche di questi elementi all'interno di un'operazione del dispatcher non vengono mantenute all'esterno dell'operazione.|  
|Suggerimento|Le app interessate da questa modifica possono risolvere il problema archiviando i valori CurrentCulture o CurrentUICulture desiderati in un campo e controllando che siano impostati i valori corretti di CurrentCulture e CurrentUICulture in tutti i corpi delle operazioni del dispatcher (inclusi i gestori di callback degli eventi dell'interfaccia utente). In alternativa, dato che la modifica di ExecutionContext sottostante questa modifica WPF influisce solo sulle app destinate a .NET Framework 4.6 o versione successiva, è possibile evitare il problema destinando le app a .NET Framework 4.5.2.|  
|Ambito|Secondario|  
|Versione|4.6|  
|Tipo|Ridestinazione:|  
|Analizzatori|CD0145|
