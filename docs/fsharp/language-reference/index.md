---
title: Riferimenti per il linguaggio F#
description: Riferimenti per il linguaggio F#
keywords: visual f#, f#, programmazione funzionale
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: b1707be1-7b7c-4fdd-a717-d9c190bc5fb5
translationtype: Human Translation
ms.sourcegitcommit: 0a01ec92a90d99fafaacbd3f71f5177e5cf94a68
ms.openlocfilehash: e0b7058513b0487902b2a57b889e77df1abfef98
ms.lasthandoff: 04/05/2017

---

# <a name="f-language-reference"></a>Riferimenti per il linguaggio F#

Questa sezione è un riferimento al linguaggio F#, un linguaggio di programmazione multi-paradigma destinato alla piattaforma .NET. Il linguaggio F# supporta modelli di programmazione funzionali, orientati a oggetti e imperativi.


## <a name="f-tokens"></a>Token F#
La tabella seguente illustra gli argomenti di riferimento che includono tabelle di parole chiave, simboli e i valori letterali usati come token in F#.



|Titolo|Descrizione|
|-----|-----------|
|[Riferimento per parole chiave](keyword-reference.md)|Contiene collegamenti a informazioni su tutte le parole chiave del linguaggio F#.|
|[Riferimenti per simboli e operatori](symbol-and-operator-reference/index.md)|Include una tabella di simboli e operatori usati nel linguaggio F#.|
|[Valori letterali](literals.md)|Illustra la sintassi per i valori letterali in F# e come specificare informazioni sul tipo per i valori letterali F#.|

## <a name="f-language-concepts"></a>Concetti del linguaggio F#
La tabella seguente illustra gli argomenti di riferimento disponibili che descrivono i concetti del linguaggio.



|Titolo|Descrizione|
|-----|-----------|
|[Funzioni](functions/index.md)|Le funzioni sono l'unità fondamentale di esecuzione di un programma in qualsiasi linguaggio di programmazione. Come negli altri linguaggi, una funzione F# ha un nome, può avere parametri e accettare argomenti e ha un corpo. F# supporta anche i costrutti di programmazione funzionale, ad esempio l'uso di funzioni come valori, l'uso di funzioni senza nome nelle espressioni, composizione di funzioni per creare nuove funzioni, funzioni sottoposte a currying e la definizione implicita di funzioni attraverso l'applicazione parziale di argomenti di funzioni.|
|[Tipi F#](fsharp-types.md)|Descrive i tipi usati in F# e come sono denominati e descritti i tipi F#.|
|[Inferenza di tipi](type-inference.md)|Descrive come il compilatore F# deduce i tipi di valori, le variabili, i parametri e i valori restituiti.|
|[Generalizzazione automatica](generics/automatic-generalization.md)|Descrive costrutti generici in F#.|
|[Ereditarietà](inheritance.md)|Descrive l'ereditarietà usata per modellare la relazione "is-a", o la definizione dei sottotipi nella programmazione orientata agli oggetti.|
|[Membri](members/index.md)|Descrive i membri dei tipi di oggetto F#.|
|[Parametri e argomenti](Parameters-and-Arguments.md)|Descrive il supporto di linguaggio per la definizione dei parametri e il passaggio di argomenti a funzioni, metodi e proprietà. Include informazioni su come passare valori in base al riferimento.|
|[Overload degli operatori](operator-overloading.md)|Descrive come eseguire l'overload di operatori aritmetici in una classe o in un tipo di record e a livello globale.|
|[Cast e conversioni](casting-and-conversions.md)|Descrive il supporto per le conversioni di tipo in F#.|
|[Controllo di accesso](access-control.md)|Descrive il controllo di accesso in F#. Il controllo di accesso implica la dichiarazione che i client sono in grado di usare determinati elementi di programma, ad esempio tipi, metodi, funzioni e così via.|
|[Criteri di ricerca](pattern-matching.md)|Descrive i modelli, che rappresentano le regole per la trasformazione dei dati di input usati nel linguaggio F# per estrarre i dati di confronto con un modello, decomporre i dati nelle parti costituenti o estrarre informazioni dai dati in vari modi.|
|[Criteri attivi](active-patterns.md)|Descrive i modelli attivi. I modelli attivi consentono di definire partizioni denominate che suddividono i dati di input. È possibile usare i criteri attivi per decomporre i dati in modo personalizzato per ogni partizione.|
|[Asserzioni](assertions.md)|Descrive l'espressione `assert`, che è una funzionalità di debug che è possibile usare per verificare un'espressione. In caso di errore in modalità Debug, un'asserzione genera una finestra di dialogo di errore di sistema.|
|[Gestione delle eccezioni](exception-handling/index.md)|Contiene informazioni sul supporto di gestione delle eccezioni nel linguaggio F#.|
|[Attributi](attributes.md)|Descrive gli attributi, che abilitano i metadati da applicare a un costrutto di programmazione.|
|[Gestione delle risorse: parola chiave `use` ](resource-management-the-use-keyword.md)|Descrive le parole chiave `use` e `using`, che possono controllare l'inizializzazione e il rilascio delle risorse.|
|[Spazi dei nomi](namespaces.md)|Descrive il supporto degli spazi dei nomi in F#. Uno spazio dei nomi consente di organizzare il codice in aree di funzionalità correlate perché consente di collegare un nome a un raggruppamento di elementi di programma.|
|[Moduli](modules.md)|Descrive i moduli. Un modulo F# è un raggruppamento di codice F#, ad esempio valori, tipi e valori di funzioni, in un programma F#. Il codice di raggruppamento nei moduli consente di tenere insieme il codice correlato e consente di evitare conflitti di nome nel programma.|
|[Dichiarazioni di importazione: parola chiave `open`](import-declarations-the-open-keyword.md)|Descrive il funzionamento di `open`. Una dichiarazione di importazione specifica un modulo o uno spazio dei nomi ai cui elementi è possibile fare riferimento senza usare un nome completo.|
|[Firme](signatures.md)|Descrive le firme e i file delle firme. Un file della firma contiene informazioni sulle firme pubbliche di un set di elementi del programma F#, ad esempio i tipi, gli spazi dei nomi e i moduli. Può essere usato per specificare l'accessibilità di questi elementi del programma.|
|[Documentazione di XML](xml-documentation.md)|Descrive il supporto per generare file di documentazione per i commenti ai documenti XML, noti anche come commenti a barra tripla. È possibile produrre documentazione dai commenti di codice in F# come in altri linguaggi .NET.|
|[Sintassi dettagliata](verbose-syntax.md)|Descrive la sintassi per i costrutti F# quando la sintassi leggera non è abilitata. La sintassi dettagliata è indicata dalla direttiva `#light "off"` che si trova nella parte superiore del file di codice.|

## <a name="f-types"></a>Tipi F#
La tabella seguente illustra gli argomenti di riferimento disponibili che descrivono i tipi supportati dal linguaggio F#.



|Titolo|Descrizione|
|-----|-----------|
|[Valori](values/index.md)|Descrive i valori, ovvero quantità non modificabili che hanno un tipo specifico. I valori possono essere numeri interi o a virgola mobile, caratteri o testo, elenchi, sequenze, matrici, tuple, unioni discriminate, record, tipi di classe o valori di funzioni.|
|[Tipi primitivi](primitive-types.md)|Descrive i tipi primitivi fondamentali usati nel linguaggio F#. Specifica anche i tipi .NET corrispondenti e i valori minimi e massimi per ogni tipo.|
|[Tipo di unità](unit-type.md)|Descrive il tipo `unit`, ovvero un tipo che indica l'assenza di un valore specifico. Il tipo `unit` ha un solo valore, che funge da segnaposto quando nessun altro valore è presente o necessario.|
|[Stringhe](strings.md)|Descrive le stringhe in F#. Il tipo `string` rappresenta un testo non modificabile come sequenza di caratteri Unicode. `string` è un alias per `System.String` in .NET Framework.|
|[Tuple](tuples.md)|Descrive le tuple, ovvero un raggruppamento di valori senza nome, ma ordinati, di tipi potenzialmente diversi.|
|[Tipi di raccolta F#](fsharp-collection-types.md)|Panoramica dei tipi di raccolte funzionali di F#, inclusi i tipi per matrici, elenchi, sequenze (seq), mappe e set.|
|[Elenchi](lists.md)|Descrive elenchi. Un elenco in F# è una serie ordinata e non modificabile di elementi dello stesso tipo.|
|[Opzioni](options.md)|Descrive il tipo di opzione. Un'opzione in F# viene usata quando un valore può esistere o meno. Un'opzione ha un tipo sottostante e può contenere un valore di tale tipo o nessun valore.|
|[Sequenze](sequences.md)|Descrive le sequenze. Una sequenza è una serie logica di elementi dello stesso tipo. Gli elementi individuali di una sequenza vengono calcolati solo se necessario, pertanto la rappresentazione potrebbe essere minore di quella indicata da un conteggio di elementi letterali.|
|[Matrici](arrays.md)|Descrive matrici. Le matrici sono sequenze di dimensioni fisse, in base zero, o modificabili di elementi di dati consecutivi dello stesso tipo.|
|[Record](records.md)|Descrive record. I record rappresentano aggregazioni semplici di valori denominati, facoltativamente con membri.|
|[Unioni discriminate](discriminated-unions.md)|Descrive le unioni discriminate, che offrono supporto per i valori che possono essere uno dei vari casi denominati con tipi e i valori potenzialmente diversi.|
|[Enumerazioni](enumerations.md)|Descrive le enumerazioni, che sono tipi che hanno un set definito di valori denominati. È possibile usarle in sostituzione ai valori letterali per rendere il codice più leggibile e gestibile.|
|[Celle di riferimento](reference-cells.md)|Descrive le celle di riferimento, che sono punti di archiviazione che consentono di creare variabili modificabili con una semantica di riferimento.|
|[Abbreviazioni dei tipi](type-abbreviations.md)|Descrive le abbreviazioni dei tipi, che sono nomi alternativi per i tipi.|
|[Classi](classes.md)|Descrive le classi, che sono tipi che rappresentano oggetti che possono avere proprietà, metodi ed eventi.|
|[Strutture](structures.md)|Descrive strutture, che sono tipi di oggetti compatti che possono essere più efficaci di una classe per i tipi che hanno una quantità piccola di dati e un comportamento semplice.|
|[Interfacce](interfaces.md)|Descrive le interfacce, che specificano set di membri correlati implementati da altre classi.|
|[Classi astratte](abstract-classes.md)|Descrive le classi astratte, ovvero classi che lasciano alcuni o tutti i membri non implementati, in modo che l'implementazione possa essere effettuata dalle classi derivate.|
|[Estensioni di tipo](type-extensions.md)|Descrive le estensioni di tipo, che consentono di aggiungere nuovi membri a un tipo di oggetto definito in precedenza.|
|[Tipi flessibili](flexible-types.md)|Descrive i tipi flessibili. Un'annotazione di tipo flessibile indica che un parametro, una variabile o un valore ha un tipo compatibile con il tipo specificato, in cui la compatibilità viene determinata dalla posizione in una gerarchia orientata agli oggetti di classi o interfacce.|
|[Delegati](delegates.md)|Descrive i delegati, che rappresentano una chiamata di funzione come oggetto.|
|[Unità di misura](units-of-measure.md)|Descrive le unità di misura. I valori a virgola mobile in F# possono avere unità di misura associate, che sono in genere usate per indicare lunghezza, volume, massa e così via.|
|[Provider di tipi](../tutorials/type-providers/index.md)|Descrive il tipo e offre collegamenti alle procedure dettagliate sull'uso dei provider di tipo predefinito per accedere ai database e ai servizi Web.|

## <a name="f-expressions"></a>Espressioni F#
La tabella seguente elenca gli argomenti che descrivono le espressioni F#.

|Titolo|Descrizione|
|-----|-----------|
|[Espressioni condizionali: `if...then...else`](conditional-expressions-if-then-else.md)|Descrive l'espressione `if...then...else`, che esegue diversi rami di codice e restituisce un valore diverso in base all'espressione booleana specificata.|
|[Espressioni match](match-expressions.md)|Descrive l'espressione `match`, che consente il controllo del branching basato sul confronto di un'espressione con un set di modelli.|
|[Cicli: espressione `for...to`](loops-for-to-expression.md)|Descrive l'espressione `for...to`, che viene usata per eseguire l'iterazione di un ciclo sopra un intervallo di valori di una variabile di ciclo.|
|[Cicli: espressione `for...in`](loops-for-in-expression.md)|Descrive l'espressione `for...in`, un costrutto di ciclo usato per eseguire l'iterazione sopra le corrispondenze di un modello in una raccolta enumerabile, ad esempio un'espressione di intervallo, una sequenza, un elenco, una matrice o un altro costrutto che supporta l'enumerazione.|
|[Cicli: espressione `while...do`](loops-while-do-expression.md)|Descrive l'espressione `while...do`, usata per l'esecuzione iterativa (ciclo) quando una specifica condizione di verifica è true.|
|[Espressioni di oggetto](object-expressions.md)|Descrive le espressioni di oggetto, ovvero le espressioni che creano nuove istanze di un tipo di oggetto creato dinamicamente, di un tipo di oggetto anonimo basato su un tipo di base, un'interfaccia o un set di interfacce esistenti.|
|[Calcoli differiti](lazy-computations.md)|Descrive i calcoli differiti, ovvero calcoli che non vengono eseguiti immediatamente, ma solo quando il risultato è effettivamente necessario.|
|[Espressioni di calcolo](computation-expressions.md)|Descrive le espressioni di calcolo in F#, che specificano una sintassi efficiente per la scrittura di calcoli che possono essere ordinati in sequenza e combinati tramite costrutti di flusso di controllo e associazioni. Possono essere usati per specificare una sintassi efficiente per *monads*, ovvero una funzionalità di programmazione funzionale che può essere usata per gestire i dati, il controllo e gli effetti collaterali nei programmi funzionali. Un solo tipo di espressione di calcolo, ovvero il flusso di lavoro asincrono, offre supporto per i calcoli paralleli e asincroni. Per altre informazioni, vedere [Flussi di lavoro asincroni](asynchronous-workflows.md).|
|[Flussi di lavoro asincroni](asynchronous-workflows.md)|Descrive i flussi di lavoro asincroni, una funzionalità del linguaggio che consente di scrivere codice asincrono in modo molto simile a quello normale in cui si scrive codice sincrono.|
|[Citazioni di codice](code-quotations.md)|Descrive le citazioni di codice, una funzionalità del linguaggio che consente di generare e usare espressioni di codice F# a livello di codice.|
|[Espressioni di query](query-expressions.md)|Descrive le espressioni di query, una funzionalità del linguaggio che implementa LINQ per F# e consente di scrivere query su un'origine dati o una raccolta enumerabile.|

## <a name="compiler-supported-constructs"></a>Costrutti supportati dal compilatore
La tabella seguente elenca argomenti che descrivono costrutti speciali supportati dal compilatore.

|Argomento|Descrizione|
|-----|-----------|
|[Opzioni del compilatore](compiler-options.md)|Descrive le opzioni della riga di comando per il compilatore F#.|
|[Direttive per il compilatore](compiler-directives.md)|Descrive le direttive del preprocessore e del compilatore.|
|[Identificatori riga, file e percorso di origine](source-line-file-path-identifiers.md)|Descrive gli identificatori `__LINE__`, `__SOURCE_DIRECTORY__` e `__SOURCE_FILE__`, che sono valori predefiniti che consentono di accedere al numero della riga d'origine, alla directory e al nome file nel codice.|

## <a name="see-also"></a>Vedere anche
[Visual F#](../index.md)
