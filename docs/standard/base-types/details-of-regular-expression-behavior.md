---
title: "Dettagli sul comportamento delle espressioni regolari | Microsoft Docs"
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
  - "espressioni regolari, comportamento"
  - "espressioni regolari di .NET Framework, comportamento"
ms.assetid: 0ee1a6b8-caac-41d2-917f-d35570021b10
caps.latest.revision: 27
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 27
---
# Dettagli sul comportamento delle espressioni regolari
Nel modulo di espressioni regolari di .NET Framework, un matcher di espressioni regolari di backtracking, è incorporato un modulo NFA \(Nondeterministic Finite Automaton\) tradizionale, quale quello utilizzato da Perl, Python, Emacs e Tcl.  Tale caratteristica lo distingue dai moduli di gestione di espressioni regolari DFA \(Deterministic Finite Automaton\) pure, più veloci ma soggetti a maggiori limitazioni, quali quelli di awk, egrep o lex.  Questa caratteristica lo distingue inoltre dai POSIX NFA, standardizzati ma più lenti.  Nella sezione riportata di seguito vengono descritti i tre tipi di motori per le espressioni regolari. Viene inoltre spiegato il motivo per cui le espressioni regolari in .NET Framework vengono implementate utilizzando un motore NFA tradizionale.  
  
## Vantaggi del motore NFA  
 Quando i motori DFA eseguono ricerche di corrispondenza, l'ordine di elaborazione è basato sulla stringa di input.  Il motore inizia l'elaborazione all'inizio della stringa di input e procede in sequenza per determinare se il carattere successivo corrisponde al modello di espressione regolare.  Tali motori sono in grado di garantire la corrispondenza della stringa più lunga possibile.  Poiché non esaminano mai due volte lo stesso carattere, i motori DFA non supportano il backtracking.  Poiché tuttavia un motore DFA contiene solo stati finiti, non è in grado di cercare le corrispondenze relative a criteri che includono backreference e, poiché non crea espansioni esplicite, non è in grado di catturare sottoespressioni.  
  
 A differenza dei motori DFA, quando i motori NFA tradizionali esaminano le corrispondenze con i criteri di ricerca, l'ordine di elaborazione è basato sul modello di espressione regolare.  Mentre elabora un particolare elemento di linguaggio, il motore utilizza un criterio greedy; ovvero, cerca la corrispondenza della porzione più ampia possibile della stringa di input.  Ma salva anche lo stato dopo aver determinato la corrispondenza di una sottoespressione.  Se non viene individuata alcuna corrispondenza, il motore sarà in grado di tornare a uno stato salvato in modo da tentare ulteriori corrispondenze.  Il processo in cui viene abbandonata una corrispondenza soddisfatta in una sottoespressione in modo da poter cercare anche le corrispondenze degli elementi di linguaggio successivi nell'espressione regolare è noto come *backtracking*.  I motori NFA utilizzano il backtracking per esaminare tutte le possibili espansioni di un'espressione regolare in un ordine specifico e accettare la prima corrispondenza.  Poiché un motore NFA tradizionale crea una specifica espansione dell'espressione regolare per una corrispondenza soddisfatta, è in grado di acquisire le corrispondenze di sottoespressioni e cercare le corrispondenze dei backreference.  Per effetto del backtracking, tuttavia, un motore NFA tradizionale può tornare sullo stesso identico stato più volte, se arriva a tale stato seguendo percorsi diversi.  Di conseguenza, nei casi peggiori si può assistere a rallentamenti di carattere esponenziale.  Poiché inoltre un motore NFA tradizionale accetta la prima corrispondenza trovata, è possibile che non individui altre corrispondenze potenzialmente più lunghe.  
  
 I moduli di gestione POSIX NFA sono simili ai moduli di gestione NFA tradizionali, con la sola eccezione che continuano il backtracking fino a maturare la certezza di aver trovato la corrispondenza più lunga.  Di conseguenza, un motore POSIX NFA è più lento di un motore NFA tradizionale. Inoltre, se si utilizza un motore POSIX NFA non è possibile favorire l'individuazione di una corrispondenza più breve rispetto a una più lunga modificando l'ordine di ricerca del backtracking.  
  
 I motori NFA tradizionali vengono preferiti dai programmatori, perché offrono maggiori possibilità di controllo sulla ricerca delle corrispondenze di stringhe rispetto ai motori DFA o POSIX NFA.  Sebbene nel caso peggiore possano risultare più lenti, possono essere impostati in modo da individuare le corrispondenze secondo una sequenza temporale lineare o polinomiale utilizzando criteri che riducano le ambiguità e limitino il backtracking.  In altre parole, sebbene i motori NFA costituiscano un compromesso tra potenza e flessibilità, nella maggioranza dei casi offrono prestazioni buone o almeno accettabili se un'espressione regolare è ben scritta ed evita casi in cui il backtracking degrada esponenzialmente le prestazioni.  
  
> [!NOTE]
>  Per informazioni sulla riduzione delle prestazioni causata da un utilizzo eccessivo del backtracking e sulle modalità di elaborazione di un'espressione regolare per risolvere tale problema, vedere [Backtracking](../../../docs/standard/base-types/backtracking-in-regular-expressions.md).  
  
## Funzionalità del modulo di .NET Framework  
 Per sfruttare i vantaggi offerti da un motore NFA tradizionale, nel motore delle espressioni regolari di .NET Framework è incluso un set completo di costrutti per consentire ai programmatori di impostare il motore di backtracking.  Tali costrutti possono essere utilizzati per velocizzare l'individuazione delle corrispondenze o per favorire specifiche espansioni rispetto ad altre.  
  
 Fra le altre funzionalità del motore delle espressioni regolari di .NET Framework è incluso quanto riportato di seguito.  
  
-   Quantificatori pigri: `??`, `*?`, `+?`, `{`*n*`,`*m*`}?`.  Questi costrutti indicano al motore del backtracking di cercare prima le corrispondenze nel numero minimo di ripetizioni.  Al contrario, i quantificatori onerosi ordinari cercano prima la corrispondenza nel numero massimo di ripetizioni.  Nell'esempio riportato di seguito vengono illustrate le differenze tra i due tipi.  Un'espressione regolare determina la corrispondenza di una frase che termina con un numero e un gruppo di acquisizione ha lo scopo di estrarre tale numero.  L'espressione regolare `.+(\d+)\.` include il quantificatore greedy `.+` che induce il motore delle espressioni regolari ad acquisire solo l'ultima cifra del numero.  Al contrario, l'espressione regolare `.+?(\d+)\.` include il quantificatore lazy `.+?` che induce il motore delle espressioni regolari ad acquisire il numero completo.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lazy1.cs#1)]
     [!code-vb[Conceptual.RegularExpressions.Design#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lazy1.vb#1)]  
  
     Le versioni greedy e lazy di questa espressione regolare sono definite come illustrato nella tabella riportata di seguito.  
  
    |Modello|Descrizione|  
    |-------------|-----------------|  
    |`.+` \(quantificatore greedy\)|Accetta la corrispondenza di almeno un'occorrenza di qualsiasi carattere.  Questo induce il motore delle espressioni regolari a considerare soddisfatta la corrispondenza dell'intera stringa e quindi a eseguire il backtracking come necessario per esaminare le corrispondenze con il resto del criterio.|  
    |`.+?` \(quantificatore lazy\)|Accetta la corrispondenza di almeno un'occorrenza di qualsiasi carattere, ma accetta la corrispondenza del minor numero possibile di caratteri.|  
    |`(\d+)`|Accetta la corrispondenza di almeno un carattere numerico e lo assegna al primo gruppo di acquisizione.|  
    |`\.`|Corrisponde a un punto.|  
  
     Per ulteriori informazioni sui quantificatori lazy, vedere [Quantificatori](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md).  
  
-   Lookahead positivo: `(?=`*subexpression*`)`.  Questa funzionalità consente al motore di backtracking di tornare alla stessa posizione del testo dopo aver individuato la corrispondenza di una sottoespressione.  Risulta utile per eseguire ricerche all'interno del testo verificando più criteri a partire dalla stessa posizione.  Ciò consente anche al motore di verificare che una sottostringa esista alla fine della ricerca di corrispondenza senza includere la sottostringa nel testo di cui è stata individuata la corrispondenza.  Nell'esempio riportato di seguito viene utilizzato il lookahead positivo per estrarre le parole in una frase che non sono seguite da simboli di punteggiatura.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lookahead1.cs#2)]
     [!code-vb[Conceptual.RegularExpressions.Design#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lookahead1.vb#2)]  
  
     L'espressione regolare `\b[A-Z]+\b(?=\P{P})` viene definita come illustrato nella tabella riportata di seguito.  
  
    |Modello|Descrizione|  
    |-------------|-----------------|  
    |`\b`|Inizia la corrispondenza sul confine di parola.|  
    |`[A-Z]+`|Accetta una o più corrispondenze di qualsiasi carattere alfabetico.  Poiché il metodo <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=fullName> viene richiamato con l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>, il confronto non rileva la distinzione tra maiuscole e minuscole.|  
    |`\b`|Termina la corrispondenza sul confine di parola.|  
    |`(?=\P{P})`|Esegue il lookahead per determinare se il carattere successivo è un simbolo di punteggiatura.  In caso contrario, il criterio di corrispondenza è soddisfatto.|  
  
     Per ulteriori informazioni sulle asserzioni per il lookahead positivo, vedere [Costrutti di raggruppamento](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
-   Lookahead negativo: `(?!`*subexpression*`)`.  Questa funzionalità aggiunge la capacità di considerare soddisfatta la corrispondenza di un'espressione solo se non viene individuata alcuna corrispondenza di una sottoespressione.  Ciò risulta particolarmente utile per abbreviare una ricerca, poiché è spesso più semplice formulare un'espressione relativa a un caso da eliminare che non un'espressione che individua i casi da includere.  È difficile, ad esempio, scrivere un'espressione per individuare le parole che non iniziano con "non".  Nell'esempio riportato di seguito viene utilizzato il lookahead negativo per escludere tali parole.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lookahead2.cs#3)]
     [!code-vb[Conceptual.RegularExpressions.Design#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lookahead2.vb#3)]  
  
     Il modello di espressione regolare `\b(?!non)\w+\b` viene definito come illustrato nella tabella seguente.  
  
    |Modello|Descrizione|  
    |-------------|-----------------|  
    |`\b`|Inizia la corrispondenza sul confine di parola.|  
    |`(?!non)`|Lookahead per verificare che la stringa corrente non inizi con "non".  In caso contrario, il criterio di corrispondenza non è soddisfatto.|  
    |`(\w+)`|Trova la corrispondenza di uno o più caratteri alfanumerici.|  
    |`\b`|Termina la corrispondenza sul confine di parola.|  
  
     Per ulteriori informazioni sulle asserzioni per il lookahead negativo, vedere [Costrutti di raggruppamento](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
-   Valutazione condizionale: `(?(`*expression*`)`*yes* `|` *no* `)` e `(?(`*name*`)`*yes* `|` *no* `)`, dove *expression* rappresenta una sottoespressione di cui cercare la corrispondenza, *name* rappresenta il nome di un gruppo di acquisizione, *yes* rappresenta la stringa di cui valutare la corrispondenza se è soddisfatta la corrispondenza di *expression* oppure *name* rappresenta un gruppo di acquisizione valido e non vuoto e *no* rappresenta la sottoespressione di cui valutare la corrispondenza se non è soddisfatta la corrispondenza di *expression* oppure *name* rappresenta un gruppo di acquisizione non vuoto e non valido.  Questa funzionalità consente al motore di eseguire ricerche utilizzando più di un modello alternativo, a seconda del risultato della valutazione di corrispondenza di una sottoespressione precedente o del risultato di un'asserzione di larghezza zero.  Ciò offre una forma più efficace di backreference che consente, ad esempio, di valutare la corrispondenza di una sottoespressione a seconda se la corrispondenza di una sottoespressione precedente è soddisfatta o meno.  L'espressione regolare illustrata nell'esempio riportato di seguito ricerca le corrispondenze di paragrafi destinati sia per uso pubblico che per uso interno.  I paragrafi destinati solo per uso interno iniziano con un tag `<PRIVATE>`.  Il modello di espressione regolare `^(?<Pvt>\<PRIVATE\>\s)?(?(Pvt)((\w+\p{P}?\s)+)|((\w+\p{P}?\s)+))\r?$` utilizza la valutazione condizionale per assegnare il contenuto dei paragrafi destinati per uso pubblico e per uso interno a gruppi di acquisizione separati.  Tali paragrafi possono quindi essere gestiti in modo diverso.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/conditional1.cs#4)]
     [!code-vb[Conceptual.RegularExpressions.Design#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/conditional1.vb#4)]  
  
     Il modello di espressione regolare viene definito come illustrato nella tabella riportata di seguito.  
  
    |Modello|Descrizione|  
    |-------------|-----------------|  
    |`^`|Inizia la ricerca di corrispondenza all'inizio di una riga.|  
    |`(?<Pvt>\<PRIVATE\>\s)?`|Accetta la corrispondenza di zero o un'occorrenza della stringa `<PRIVATE>` seguita da un carattere di spazio vuoto.  Assegna la corrispondenza a un gruppo di acquisizione denominato `Pvt`.|  
    |`(?(Pvt)((\w+\p{P}?\s)+)`|Se il gruppo di acquisizione `Pvt` esiste, accetta la corrispondenza di una o più occorrenze di uno o più caratteri alfanumerici seguiti da zero o un carattere separatore di punteggiatura seguito da un carattere di spazio vuoto.  Assegna la sottostringa al primo gruppo di acquisizione.|  
    |`&#124;((\w+\p{P}?\s)+))`|Se il gruppo di acquisizione `Pvt` non esiste, accetta la corrispondenza di una o più occorrenze di uno o più caratteri alfanumerici seguiti da zero o un carattere separatore di punteggiatura seguito da un carattere di spazio vuoto.  Assegna la sottostringa al terzo gruppo di acquisizione.|  
    |`\r?$`|Ricerca la corrispondenza alla fine di una riga o alla fine della stringa.|  
  
     Per ulteriori informazioni sulla valutazione condizionale, vedere [Costrutti di alternanza](../../../docs/standard/base-types/alternation-constructs-in-regular-expressions.md).  
  
-   Definizioni di gruppo di bilanciamento: `(?<`*name1*`-`*name2*`>` *subexpression*`)`.  Questa funzionalità consente al motore delle espressioni regolari di tenere traccia di costrutti annidati quali parentesi o parentesi quadre di apertura e chiusura.  Per un esempio, vedere [Costrutti di raggruppamento](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
-   Sottoespressioni non di backtracking, \(note anche come sottoespressioni greedy\): `(?>`*subexpression*`)`.  Questa funzionalità consente al motore di backtracking di garantire che una sottoespressione corrisponda solo alla prima corrispondenza trovata per tale sottoespressione, come se l'espressione fosse eseguita indipendentemente dall'espressione che la contiene.  Se non si utilizza questo costrutto, le ricerche di backtracking eseguite dall'espressione più estesa possono modificare il comportamento di una sottoespressione.  Ad esempio, l'espressione regolare `(a+)\w` determina la corrispondenza di uno o più caratteri "a", insieme a un carattere alfanumerico che segue la sequenza di caratteri "a", e assegna la sequenza di caratteri "a" al primo gruppo di acquisizione. Tuttavia, se anche il carattere finale della stringa di input è un carattere "a", l'elemento di linguaggio `\w` ne determinerà la corrispondenza e tale carattere non verrà incluso nel gruppo acquisito.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/nonbacktracking2.cs#7)]
     [!code-vb[Conceptual.RegularExpressions.Design#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/nonbacktracking2.vb#7)]  
  
     L'espressione regolare `((?>a+))\w` evita questo comportamento.  Poiché la corrispondenza di tutti i caratteri "a" consecutivi viene determinata senza backtracking, il primo gruppo di acquisizione include tutti i caratteri "a" consecutivi.  Se i caratteri "a" non sono seguiti da almeno un carattere diverso da "a", la corrispondenza non sarà soddisfatta.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/nonbacktracking1.cs#8)]
     [!code-vb[Conceptual.RegularExpressions.Design#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/nonbacktracking1.vb#8)]  
  
     Per ulteriori informazioni sulle sottoespressioni non di backtracking, vedere [Costrutti di raggruppamento](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
-   Corrispondenza da destra a sinistra, specificata fornendo l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> a un costruttore della classe <xref:System.Text.RegularExpressions.Regex> o al metodo corrispondente dell'istanza statica.  Questa funzionalità risulta utile quando si eseguono ricerche da destra verso sinistra invece che da sinistra verso destra oppure nei casi in cui è più efficiente iniziare la valutazione di corrispondenza dalla parte destra del criterio anziché dalla sinistra.  Come viene illustrato nell'esempio riportato di seguito, l'utilizzo della valutazione di corrispondenza da destra a sinistra può modificare il comportamento dei quantificatori greedy.  Nell'esempio riportato di seguito vengono eseguite due ricerche di una frase che termina con un numero.  La ricerca da sinistra a destra che utilizza il quantificatore greedy `+` determina la corrispondenza di una delle sei cifre nella frase, mentre la ricerca da destra a sinistra individua la corrispondenza di tutte le sei cifre.  Per una descrizione del modello di espressione regolare, vedere l'esempio che illustra i quantificatori lazy, precedentemente in questa sezione.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/rtl1.cs#6)]
     [!code-vb[Conceptual.RegularExpressions.Design#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/rtl1.vb#6)]  
  
     Per ulteriori informazioni sulla valutazione di corrispondenza da destra a sinistra, vedere [Opzioni di espressioni regolari](../../../docs/standard/base-types/regular-expression-options.md).  
  
-   Lookbehind positivo e negativo: `(?<=`*subexpression*`)` per lookbehind positivo e `(?<!`*subexpression*`)` per lookbehind negativo.  Questa funzionalità è simile a lookahead, discusso precedentemente in questo argomento.  Poiché il modulo di gestione delle espressioni regolari consente la corrispondenza completa da destra verso sinistra, le espressioni regolari consentono lookbehind illimitati.  Il lookbehind positivo e negativo può essere inoltre utilizzato per evitare l'annidamento di quantificatori quando la sottoespressione annidata è un superset di un'espressione esterna.  Le espressioni regolari con tali quantificatori annidati offrono spesso prestazioni insufficienti.  Nell'esempio riportato di seguito viene verificato se una stringa inizia e termina con un carattere alfanumerico e se qualsiasi altro carattere nella stringa appartiene a un subset più ampio.  Tale criterio costituisce una parte dell'espressione regolare utilizzata per convalidare indirizzi di posta elettronica; per ulteriori informazioni, vedere [Procedura: Verificare che le stringhe siano in formato di posta elettronica valido](../../../docs/standard/base-types/how-to-verify-that-strings-are-in-valid-email-format.md).  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lookbehind1.cs#5)]
     [!code-vb[Conceptual.RegularExpressions.Design#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lookbehind1.vb#5)]  
  
     L'espressione regolare `^[A-Z0-9]([-!#$%&'.*+/=?^`{}|~\w])*(?<=[A-Z0-9])$` viene definita come illustrato nella tabella riportata di seguito.  
  
    |Modello|Descrizione|  
    |-------------|-----------------|  
    |`^`|Inizia la valutazione di corrispondenza all'inizio della stringa.|  
    |`[A-Z0-9]`|Trovare la corrispondenza di qualsiasi carattere numerico o alfanumerico. Il confronto non rileva la distinzione tra maiuscole e minuscole.|  
    |`([-!#$%&'.*+/=?^`{}&#124;~\w])*`|Determina la corrispondenza di zero o più occorrenze di qualsiasi carattere alfanumerico o di uno qualsiasi dei seguenti caratteri: \-, \!, \#, $, %, &, ', ., \*, \+, \/, \=, ?, ^, \`, {, }, &#124; oppure ~.|  
    |`(?<=[A-Z0-9])`|Esegue il lookbehind al carattere precedente che deve essere numerico o alfanumerico. Il confronto non rileva la distinzione tra maiuscole e minuscole.|  
    |`$`|Terminare la corrispondenza alla fine della stringa.|  
  
     Per ulteriori informazioni sul lookbehind positivo e negativo, vedere [Costrutti di raggruppamento](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Backtracking](../../../docs/standard/base-types/backtracking-in-regular-expressions.md)|Vengono fornite informazioni sul modo in cui il backtracking di espressioni regolari si dirama per trovare corrispondenze alternative.|  
|[Compilazione e riutilizzo](../../../docs/standard/base-types/compilation-and-reuse-in-regular-expressions.md)|Vengono fornite informazioni sulla compilazione e il riutilizzo di espressioni regolari per accrescere le prestazioni.|  
|[Thread safety](../../../docs/standard/base-types/thread-safety-in-regular-expressions.md)|Vengono fornite informazioni sulla caratteristica thread\-safe delle espressioni regolari e sul momento consigliato per sincronizzare l'accesso agli oggetti di espressioni regolari.|  
|[Espressioni regolari di .NET Framework](../../../docs/standard/base-types/regular-expressions.md)|Viene fornita una panoramica dell'aspetto delle espressioni regolari relativo al linguaggio di programmazione.|  
|[Modello a oggetti delle espressioni regolari](../../../docs/standard/base-types/the-regular-expression-object-model.md)|Vengono forniti esempi di codice ed informazioni per illustrare l'utilizzo delle classi di espressioni regolari.|  
|[Esempi di espressioni regolari](../../../docs/standard/base-types/regular-expression-examples.md)|Vengono forniti gli esempi di codice che illustrano l'utilizzo delle espressioni regolari nelle applicazioni comuni.|  
|[Linguaggio di espressioni regolari \- Riferimento rapido](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)|Vengono fornite informazioni sui set di caratteri, di operatori e di costrutti utilizzabili per definire le espressioni regolari.|  
  
## Riferimento  
 <xref:System.Text.RegularExpressions?displayProperty=fullName>