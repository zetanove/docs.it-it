---
title: "Code Contracts | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "Code contracts"
ms.assetid: 84526045-496f-489d-8517-a258cf76f040
caps.latest.revision: 15
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 15
---
# Code Contracts
I contratti di codice consentono di specificare precondizioni, postcondizioni e invarianti dell'oggetto nel codice.  Le precondizioni sono requisiti da soddisfare quando si accede a un metodo o a una proprietà.  Le postcondizioni descrivono le aspettative al momento dell'uscita dal codice del metodo o della proprietà.  Le invarianti dell'oggetto descrivono lo stato previsto per una classe in stato integro.  
  
 I contratti di codice includono classi che consentono di contrassegnare il codice, un analizzatore statico per l'analisi in fase di compilazione e un analizzatore di runtime.  Le classi per i contratti di codice sono disponibili nello spazio dei nomi <xref:System.Diagnostics.Contracts>.  
  
 I vantaggi dei contratti di codice includono:  
  
-   Test migliorati: i contratti di codice consentono la verifica statica, il controllo di runtime e la generazione di documentazione.  
  
-   Strumenti di test automatici: è possibile usare i contratti di codice per generare unit test più significativi eliminando gli argomenti di test inutili che non soddisfano le precondizioni.  
  
-   Verifica statica: lo strumento di controllo statico può rilevare eventuali violazioni dei contratti senza eseguire il programma.  Verifica la presenza di contratti impliciti, ad esempio dereferenziazioni null e limiti di matrici, e di contratti espliciti.  
  
-   Documentazione di riferimento: il generatore di documentazione integra i file di documentazione XML esistenti con le informazioni sul contratto.  Sono disponibili anche dei fogli di stile che è possibile usare con [Sandcastle](http://go.microsoft.com/fwlink/?LinkID=169253) in modo che le pagine della documentazione generate contengano sezioni relative ai contratti.  
  
 I contratti possono essere usati immediatamente da tutti i linguaggi di .NET Framework; non è necessario scrivere un parser o un compilatore speciale.  Un componente aggiuntivo di Visual Studio consente di specificare il livello di analisi dei contratti di codice da eseguire.  Gli analizzatori possono confermare che i contratti sono formalmente corretti \(controllo del tipo e risoluzione dei nomi\) e possono produrre un form compilato dei contratti nel formato MSIL \(Microsoft Intermediate Language\).  La funzionalità di creazione dei contratti in Visual Studio consente di usare IntelliSense standard fornito dallo strumento.  
  
 La maggior parte dei metodi nella classe dei contratti sono compilati in modo condizionale; in altre parole, il compilatore genera chiamate a questi metodi solo quando si definisce un simbolo speciale, CONTRACTS\_FULL, tramite la direttiva `#define`.  CONTRACTS\_FULL consente di scrivere contratti nel codice senza usare le direttive `#ifdef`; è possibile produrre build diverse, alcune con contratti e altre senza.  
  
 Per gli strumenti e le istruzioni dettagliate per l'uso dei contratti di codice, vedere [Contratti di codice](http://go.microsoft.com/fwlink/?LinkId=152461) sul sito Web DevLabs di MSDN.  
  
## Preconditions  
 È possibile esprimere delle precondizioni usando il metodo <xref:System.Diagnostics.Contracts.Contract.Requires%2A?displayProperty=fullName>.  Le precondizioni specificano lo stato nel momento in cui viene richiamato un metodo.  In genere, vengono usate per specificare valori di parametro validi.  Tutti i membri menzionati nelle precondizioni devono essere accessibili almeno quanto il metodo stesso; in caso contrario, la precondizione potrebbe non essere compresa da tutti i chiamanti di un metodo.  La condizione non deve avere effetti collaterali.  Il comportamento in fase di esecuzione delle precondizioni con errori è determinato dall'analizzatore di runtime.  
  
 Ad esempio, la precondizione seguente indica che il parametro `x` non deve essere null.  
  
 `Contract.Requires( x != null );`  
  
 Se il codice deve generare una particolare eccezione in caso di errore di una precondizione, è possibile usare l'overload generico di <xref:System.Diagnostics.Contracts.Contract.Requires%2A> come descritto di seguito.  
  
 `Contract.Requires<ArgumentNullException>( x != null, "x" );`  
  
### Istruzioni Requires legacy  
 Gran parte del codice include la convalida dei parametri sotto forma di codice `if`\-`then`\-`throw`.  Gli strumenti dei contratti riconoscono queste istruzioni come precondizioni nei casi seguenti:  
  
-   Le istruzioni vengono visualizzate prima di qualsiasi altra istruzione in un metodo.  
  
-   L'intero set di istruzioni è seguito da una chiamata al metodo <xref:System.Diagnostics.Contracts.Contract> esplicita, ad esempio una chiamata al metodo <xref:System.Diagnostics.Contracts.Contract.Requires%2A>, <xref:System.Diagnostics.Contracts.Contract.Ensures%2A>, <xref:System.Diagnostics.Contracts.Contract.EnsuresOnThrow%2A> o <xref:System.Diagnostics.Contracts.Contract.EndContractBlock%2A>.  
  
 Quando le istruzioni `if`\-`then`\-`throw` vengono visualizzate in questo formato, gli strumenti le riconoscono come istruzioni `requires` legacy.  Se la sequenza `if`\-`then`\-`throw` non è seguita da altri contratti, terminare il codice con il metodo <xref:System.Diagnostics.Contracts.Contract.EndContractBlock%2A?displayProperty=fullName>.  
  
```  
if ( x == null ) throw new ...  
Contract.EndContractBlock(); // All previous "if" checks are preconditions  
```  
  
 La condizione nel test precedente è una precondizione negata.  La precondizione effettiva sarebbe `x != null`. Una precondizione negata è altamente limitata: deve essere scritta come mostrato nell'esempio precedente, quindi non deve contenere clausole `else` e il corpo della clausola `then` deve essere un'unica istruzione `throw`.  Il test `if` è soggetto a regole di purezza e visibilità \(vedere [Linee guida di utilizzo](#usage_guidelines)\), ma l'espressione `throw` è soggetta solo a regole di purezza.  Tuttavia, il tipo dell'eccezione generata deve essere visibile quanto il metodo in cui si verifica il contratto.  
  
## Postconditions  
 Le postcondizioni sono contratti per lo stato di un metodo nel momento in cui termina.  La postcondizione viene controllata appena prima dell'uscita da un metodo.  Il comportamento in fase di esecuzione delle postcondizioni con errori viene determinato dall'analizzatore di runtime.  
  
 Diversamente dalle precondizioni, le postcondizioni possono fare riferimento a membri con visibilità inferiore.  Un client potrebbe non essere in grado di comprendere o usare alcune delle informazioni espresse da una postcondizione tramite uno stato privato, tuttavia ciò non influisce sulla capacità del client di usare il metodo correttamente.  
  
### Postcondizioni standard  
 È possibile esprimere postcondizioni standard con il metodo <xref:System.Diagnostics.Contracts.Contract.Ensures%2A>.  Le postcondizioni esprimono una condizione che deve essere `true` quando il metodo termina regolarmente.  
  
 `Contract.Ensures( this .F > 0 );`  
  
### Postcondizioni eccezionali  
 Le postcondizioni eccezionali sono postcondizioni che devono essere `true` quando una particolare eccezione viene generata da un metodo.  È possibile specificare queste postcondizioni tramite il metodo <xref:System.Diagnostics.Contracts.Contract.EnsuresOnThrow%2A?displayProperty=fullName>, come mostrato nell'esempio seguente.  
  
 `Contract.EnsuresOnThrow<T>( this.F > 0 );`  
  
 L'argomento è la condizione che deve essere `true` quando viene generata un'eccezione che corrisponde a un sottotipo di `T`.  
  
 Alcuni tipi di eccezione sono difficili da usare in una postcondizione eccezionale.  Ad esempio, l'uso del tipo <xref:System.Exception> per `T` richiede che il metodo garantisca la condizione indipendentemente dal tipo di eccezione generato, anche se si tratta di un overflow dello stack o di un'altra eccezione impossibile da controllare.  Le postcondizioni eccezionali devono essere usate solo per eccezioni specifiche che potrebbero essere generate quando viene chiamato un membro, ad esempio quando viene generata un'eccezione <xref:System.InvalidTimeZoneException> per una chiamata al metodo <xref:System.TimeZoneInfo>.  
  
### Postcondizioni speciali  
 I seguenti metodi possono essere usati solo all'interno di postcondizioni:  
  
-   È possibile fare riferimento ai valori restituiti dai metodi nelle postcondizioni usando l'espressione `Contract. Result<T>()`, dove `T` viene sostituito dal tipo restituito del metodo.  Quando il compilatore non è in grado di dedurre il tipo, è necessario fornirlo in modo esplicito.  Il compilatore C\#, ad esempio, non è in grado di dedurre i tipi per i metodi che non accettano argomenti, pertanto richiede la seguente postcondizione: `Contract.Ensures(0 < Contract.Result<int>())`. I metodi con un tipo restituito `void` non possono fare riferimento a `Contract. Result<T>()` nelle relative postcondizioni.  
  
-   Un valore di prestato in una postcondizione fa riferimento al valore di un'espressione all'inizio di un metodo o di una proprietà.  Usa l'espressione `Contract.OldValue<T>(e)`, dove `T` è il tipo di `e`.  È possibile omettere l'argomento di tipo generico quando il compilatore è in grado di dedurre il tipo.  Il compilatore C\#, ad esempio, deduce sempre il tipo poiché accetta un argomento. Esistono diverse restrizioni relative a quanto può accadere in `e` e i contesti nei quali può essere visualizzata un'espressione Old.  Un'espressione Old non può contenere un'altra espressione Old.  In particolare, un'espressione Old deve fare riferimento a un valore esistente nello stato di precondizione del metodo.  In altre parole, deve essere un'espressione valutabile finché la precondizione del metodo resta `true`.  Di seguito sono riportate diverse istanze di questa regola.  
  
    -   Il valore deve esistere nello stato di precondizione del metodo.  Per fare riferimento a un campo in un oggetto, le precondizioni devono garantire che tale oggetto sia sempre non null.  
  
    -   Non è possibile fare riferimento al valore restituito del metodo in un'espressione Old:  
  
        ```  
        Contract.OldValue(Contract.Result<int>() + x) // ERROR  
        ```  
  
    -   Non è possibile fare riferimento a parametri `out` in un'espressione Old.  
  
    -   Un'espressione Old non può dipendere dalla variabile associata di un quantificatore se l'intervallo del quantificatore dipende dal valore restituito del metodo:  
  
        ```  
        Contract. ForAll (0,Contract. Result<int>(),  
        i => Contract.OldValue(xs[i]) > 3 ); // ERROR  
        ```  
  
    -   Un'espressione Old non può fare riferimento al parametro del delegato anonimo in una chiamata a <xref:System.Diagnostics.Contracts.Contract.ForAll%2A> o <xref:System.Diagnostics.Contracts.Contract.Exists%2A> a meno che non venga usata come indicizzatore o argomento di una chiamata al metodo:  
  
        ```  
        Contract. ForAll (0, xs .Length, i => Contract.OldValue(xs[i]) > 3); // OK  
        Contract. ForAll (0, xs .Length, i => Contract.OldValue(i) > 3 ); // ERROR  
        ```  
  
    -   Un'espressione Old non può verificarsi nel corpo di un delegato anonimo se il valore dell'espressione dipende da uno dei parametri del delegato, a meno che quest'ultimo non sia un argomento del metodo <xref:System.Diagnostics.Contracts.Contract.ForAll%2A> o <xref:System.Diagnostics.Contracts.Contract.Exists%2A>:  
  
        ```  
        Method( ... (T t) => Contract.OldValue(... t ...) ... ); // ERROR  
        ```  
  
    -   I parametri `Out` presentano un problema in quanto i contratti vengono visualizzati prima del corpo del metodo e la maggior parte dei compilatori non consente riferimenti ai parametri `out` nelle postcondizioni.  Per risolvere il problema, la classe <xref:System.Diagnostics.Contracts.Contract> fornisce il metodo <xref:System.Diagnostics.Contracts.Contract.ValueAtReturn%2A> che consente una postcondizione basata su un parametro `out`.  
  
        ```  
        public void OutParam(out int x) f  
        Contract.Ensures(Contract.ValueAtReturn(out x) == 3);  
        x = 3;  
        ```  
  
         Come per il metodo <xref:System.Diagnostics.Contracts.Contract.OldValue%2A>, è possibile omettere il parametro di tipo generico quando il compilatore è in grado di dedurre il tipo.  Il rewriter del contratto sostituisce la chiamata al metodo con il valore del parametro `out`.  Il metodo <xref:System.Diagnostics.Contracts.Contract.ValueAtReturn%2A> può essere visualizzato solo nelle postcondizioni.  L'argomento del metodo deve essere un parametro `out` o un campo del parametro `out` di una struttura.  Quest'ultimo è utile anche in caso di riferimento a campi nella postcondizione di un costruttore della struttura.  
  
        > [!NOTE]
        >  Attualmente, gli strumenti di analisi dei contratti di codice non verificano se i parametri `out` vengono inizializzati correttamente e ne ignorano la menzione nella postcondizione.  Quindi, nell'esempio precedente, se la riga dopo il contratto avesse usato il valore `x` anziché assegnare un numero intero, un compilatore non avrebbe generato l'errore corretto.  Tuttavia, in una build in cui il simbolo del preprocessore CONTRACTS\_FULL non viene definito \(ad esempio ``  una build di rilascio\), il compilatore genererà un errore.  
  
## Invarianti  
 Le invarianti dell'oggetto sono condizioni che devono essere true per ogni istanza di una classe quando l'oggetto è visibile a un client.  Esprimono le condizioni con le quali l'oggetto viene considerato corretto.  
  
 I metodi invarianti vengono contrassegnati ai fini dell'identificazione con l'attributo <xref:System.Diagnostics.Contracts.ContractInvariantMethodAttribute>.  I metodi invarianti non devono contenere codice, fatta eccezione per una sequenza di chiamate al metodo <xref:System.Diagnostics.Contracts.Contract.Invariant%2A>, ognuna delle quali specifica una singola invariante, come mostrato nell'esempio seguente.  
  
```  
[ContractInvariantMethod]  
protected void ObjectInvariant ()   
{  
Contract.Invariant ( this.y >= 0 );  
Contract.Invariant ( this.x > this.y );  
...  
}  
```  
  
 Le invarianti vengono definite in modo condizionale dal simbolo del preprocessore CONTRACTS\_FULL.  Durante il controllo in fase di esecuzione, le invarianti vengono controllate alla fine di ogni metodo pubblico.  Se un'invariante menziona un metodo pubblico nella stessa classe, il controllo dell'invariante che avverrebbe normalmente alla fine di tale metodo viene disabilitato.  Al contrario, il controllo viene eseguito solo alla fine della chiamata al metodo più esterna in quella classe.  Ciò avviene anche se la classe viene immessa di nuovo a causa di una chiamata a un metodo in un'altra classe.  L'eventuale presenza di finalizzatori di oggetti o di metodi che implementano il metodo <xref:System.IDisposable.Dispose%2A> non viene verificata nelle invarianti.  
  
<a name="usage_guidelines"></a>   
## Linee guida di utilizzo  
  
### Ordine dei contratti  
 La tabella seguente mostra l'ordine degli elementi da usare per la scrittura di contratti del metodo.  
  
|||  
|-|-|  
|`If-then-throw statements`|Precondizioni pubbliche compatibili con le versioni precedenti|  
|<xref:System.Diagnostics.Contracts.Contract.Requires%2A>|Tutte le precondizioni pubbliche.|  
|<xref:System.Diagnostics.Contracts.Contract.Ensures%2A>|Tutte le postcondizioni pubbliche \(normali\).|  
|<xref:System.Diagnostics.Contracts.Contract.EnsuresOnThrow%2A>|Tutte le postcondizioni pubbliche eccezionali.|  
|<xref:System.Diagnostics.Contracts.Contract.Ensures%2A>|Tutte le postcondizioni private\/interne \(normali\).|  
|<xref:System.Diagnostics.Contracts.Contract.EnsuresOnThrow%2A>|Tutte le postcondizioni private\/interne eccezionali.|  
|<xref:System.Diagnostics.Contracts.Contract.EndContractBlock%2A>|Se si usano le precondizioni di stile `if`\-`then`\-`throw` senza altri contratti, inserire una chiamata a <xref:System.Diagnostics.Contracts.Contract.EndContractBlock%2A> per indicare che tutti i controlli if precedenti sono precondizioni.|  
  
<a name="purity"></a>   
### Purezza  
 Tutti i metodi chiamati all'interno di un contratto devono essere puri; in altre parole, non devono aggiornare stati preesistenti.  Un metodo puro può modificare gli oggetti creati in seguito all'accesso al metodo stesso.  
  
 Gli strumenti dei contratti di codice presuppongono che i seguenti elementi di codice siano puri:  
  
-   Metodi contrassegnati con <xref:System.Diagnostics.Contracts.PureAttribute>.  
  
-   Tipi contrassegnati con <xref:System.Diagnostics.Contracts.PureAttribute> \(l'attributo si applica a tutti i metodi del tipo\).  
  
-   Funzioni di accesso get della proprietà.  
  
-   Operatori \(metodi statici i cui nomi iniziano con "op" e che hanno uno o due parametri e un tipo restituito non void\).  
  
-   Tutti i metodi il cui nome completo inizia con "System.Diagnostics.Contracts.Contract", "System.String", "System.IO.Path" o "System.Type".  
  
-   Tutti i delegati richiamati, purché al tipo del delegato venga attribuito <xref:System.Diagnostics.Contracts.PureAttribute>.  I tipi del delegato <xref:System.Predicate%601?displayProperty=fullName> e <xref:System.Comparison%601?displayProperty=fullName> sono considerati puri.  
  
<a name="visibility"></a>   
### Visibilità  
 Tutti i membri menzionati in un contratto devono essere visibili almeno quanto il metodo in cui vengono visualizzati.   Un campo privato, ad esempio, non può essere menzionato in una precondizione per un metodo pubblico; i client non possono convalidare un simile contratto prima di chiamare il metodo.  Tuttavia, se il campo è contrassegnato con <xref:System.Diagnostics.Contracts.ContractPublicPropertyNameAttribute>, è esente da queste regole.  
  
## Esempio  
 L'esempio seguente mostra l'uso dei contratti di codice.  
  
 [!code-csharp[ContractExample#1](../../../samples/snippets/csharp/VS_Snippets_CLR/contractexample/cs/program.cs#1)]
 [!code-vb[ContractExample#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/contractexample/vb/program.vb#1)]