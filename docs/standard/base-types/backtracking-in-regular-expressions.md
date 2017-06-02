---
title: "Backtracking nelle espressioni regolari | Microsoft Docs"
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
  - "espressioni regolari di .NET framework, backtracking"
  - "criteri di corrispondenza alternativi"
  - "criteri di corrispondenza facoltativi"
  - "ricerca con espressioni regolari, backtracking"
  - "corrispondenza al modello con espressioni regolari, backtracking"
  - "backtracking"
  - "espressioni regolari [.NET framework], backtracking"
  - "stringhe [.NET Framework], espressioni regolari"
  - "analisi di testo con espressioni regolari, backtracking"
ms.assetid: 34df1152-0b22-4a1c-a76c-3c28c47b70d8
caps.latest.revision: 20
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# Backtracking nelle espressioni regolari
<a name="top"></a> Il backtracking si verifica quando un modello di espressione regolare contiene [quantificatori](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md) facoltativi o [costrutti di alternanza](../../../docs/standard/base-types/alternation-constructs-in-regular-expressions.md) e il motore delle espressioni regolari torna a uno stato salvato in precedenza per continuare la ricerca di una corrispondenza. Il backtracking è fondamentale per la potenza delle espressioni regolari. Consente alle espressioni di essere potenti e flessibili e di cercare una corrispondenza di modelli molto complessi. Questa tecnica presenta tuttavia anche alcuni svantaggi. Il backtracking spesso è il fattore più importante che influisce sulle prestazioni del motore delle espressioni regolari. Fortunatamente, lo sviluppatore è in grado di controllare il comportamento del motore delle espressioni regolari e il modo in cui viene utilizzato il backtracking. In questo argomento viene illustrato il funzionamento del backtracking e il modo in cui può essere controllato.  
  
> [!NOTE]
>  In generale, un motore NFA \(Nondeterministic Finite Automaton\) come il motore delle espressioni regolari di .NET Framework affida la responsabilità della creazione di espressioni regolari efficienti e veloci allo sviluppatore.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
-   [Confronto lineare senza backtracking](#linear_comparison_without_backtracking)  
  
-   [Backtracking con quantificatori facoltativi o costrutti di alternanza](#backtracking_with_optional_quantifiers_or_alternation_constructs)  
  
-   [Backtracking con quantificatori facoltativi annidati](#backtracking_with_nested_optional_quantifiers)  
  
-   [Controllo del backtracking](#controlling_backtracking)  
  
<a name="linear_comparison_without_backtracking"></a>   
## Confronto lineare senza backtracking  
 Se un modello di espressione regolare non contiene quantificatori facoltativi o costrutti di alternanza, il motore delle espressioni regolari viene eseguito in un tempo lineare, ovvero dopo che il motore delle espressioni regolari trova una corrispondenza tra il primo elemento del linguaggio del modello e il testo della stringa di input, prova a trovare una corrispondenza tra l'elemento del linguaggio successivo del modello e il carattere o il gruppo di caratteri successivi della stringa di input. Il processo continua finché la ricerca della corrispondenza non avrà esito positivo o negativo. In entrambi i casi, il motore delle espressioni regolari avanza di un carattere alla volta nella stringa di input.  
  
 Nell'esempio seguente viene illustrato questo concetto. L'espressione regolare `e{2}\w\b` cerca due occorrenze della lettera "e", seguite da qualsiasi carattere alfanumerico, seguito da un confine di parola.  
  
 [!code-csharp[Conceptual.RegularExpressions.Backtracking#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/cs/backtracking1.cs#1)]
 [!code-vb[Conceptual.RegularExpressions.Backtracking#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/vb/backtracking1.vb#1)]  
  
 Benché questa espressione regolare includa il quantificatore `{2}`, viene valutata in modo lineare. Il motore delle espressioni regolari non esegue il backtracking perché `{2}` non è un quantificatore facoltativo, ma specifica un numero esatto e non un numero variabile di volte in cui trovare la corrispondenza della sottoespressione precedente. Di conseguenza, il motore delle espressioni regolari tenta di trovare una corrispondenza tra il modello di espressione regolare e la stringa di input come illustrato nella tabella seguente.  
  
|Operazione|Posizione nel modello|Posizione nella stringa|Risultato|  
|----------------|---------------------------|-----------------------------|---------------|  
|1|h|"needing a reed" \(indice 0\)|Nessuna corrispondenza.|  
|2|h|"eeding a reed" \(indice 1\)|Possibile corrispondenza.|  
|3|e{2}|"eding a reed" \(indice 2\)|Possibile corrispondenza.|  
|4|\\w|"ding a reed" \(indice 3\)|Possibile corrispondenza.|  
|5|\\b|"ing a reed" \(indice 4\)|Possibile corrispondenza non riuscita.|  
|6|h|"eding a reed" \(indice 2\)|Possibile corrispondenza.|  
|7|e{2}|"ding a reed" \(indice 3\)|Possibile corrispondenza non riuscita.|  
|8|h|"ding a reed" \(indice 3\)|La corrispondenza ha esito negativo.|  
|9|h|"ing a reed" \(indice 4\)|Nessuna corrispondenza.|  
|10|h|"ng a reed" \(indice 5\)|Nessuna corrispondenza.|  
|11|h|"g a reed" \(indice 6\)|Nessuna corrispondenza.|  
|12|h|" a reed" \(indice 7\)|Nessuna corrispondenza.|  
|13|h|"a reed" \(indice 8\)|Nessuna corrispondenza.|  
|14|h|" reed" \(indice 9\)|Nessuna corrispondenza.|  
|15|h|"reed" \(indice 10\)|Nessuna corrispondenza.|  
|16|h|"eed" \(indice 11\)|Possibile corrispondenza.|  
|17|e{2}|"ed" \(indice 12\)|Possibile corrispondenza.|  
|18|\\w|"d" \(indice 13\)|Possibile corrispondenza.|  
|19|\\b|"" \(indice 14\)|Corrispondenza.|  
  
 Se un modello di espressione regolare non include quantificatori facoltativi o costrutti di alternanza, il numero massimo di confronti necessari per trovare una corrispondenza tra il modello di espressione regolare e la stringa di input equivale approssimativamente al numero di caratteri della stringa di input. In questo caso, l'espressione regolare utilizza 19 confronti per identificare le possibili corrispondenze nella stringa di 13 caratteri.  In altre parole, il motore delle espressioni regolari viene eseguito in un tempo quasi lineare se non contiene quantificatori facoltativi o costrutti di alternanza.  
  
 [Torna all'inizio](#top)  
  
<a name="backtracking_with_optional_quantifiers_or_alternation_constructs"></a>   
## Backtracking con quantificatori facoltativi o costrutti di alternanza  
 Quando un'espressione regolare include quantificatori facoltativi o costrutti di alternanza, la valutazione della stringa di input non è più lineare. La corrispondenza dei modelli con un motore NFA è determinata dagli elementi del linguaggio nell'espressione regolare e non dai caratteri con cui trovare una corrispondenza nella stringa di input. Il motore delle espressioni regolari prova pertanto a trovare una piena corrispondenza con le sottoespressioni facoltative o alternative. Quando avanza all'elemento del linguaggio successivo nella sottoespressione e la corrispondenza ha esito negativo, il motore delle espressioni regolari può abbandonare una parte della corrispondenza esatta e tornare a uno stato salvato in precedenza al fine di trovare una corrispondenza tra l'intera espressione regolare e la stringa di input. Questo processo di tornare a uno stato salvato in precedenza per trovare una corrispondenza è noto come backtracking.  
  
 Si consideri, ad esempio, il modello di espressione regolare `.*(es)` che cerca una corrispondenza con i caratteri "es" e tutti i caratteri che li precedono. Come illustrato nell'esempio seguente, se la stringa di input è "Essential services are provided by regular expressions.", il modello cerca una corrispondenza con l'intera stringa fino ai caratteri "es" in "expressions" compresi.  
  
 [!code-csharp[Conceptual.RegularExpressions.Backtracking#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/cs/backtracking2.cs#2)]
 [!code-vb[Conceptual.RegularExpressions.Backtracking#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/vb/backtracking2.vb#2)]  
  
 A tale scopo, il motore delle espressioni regolari utilizza il backtracking come segue:  
  
-   Trova la corrispondenza di `.*`, ovvero di zero, uno o più occorrenze di qualsiasi carattere, con l'intera stringa di input.  
  
-   Tenta di trovare una corrispondenza di "e" nel modello di espressione regolare. Tuttavia, nella stringa di input non sono presenti altri caratteri di cui cercare una corrispondenza.  
  
-   Esegue il backtracking fino all'ultima corrispondenza esatta, "Essential services are provided by regular expressions", e tenta di trovare una corrispondenza di "e" con il punto alla fine della frase. La corrispondenza ha esito negativo.  
  
-   Continua a eseguire il backtracking fino a una corrispondenza esatta precedente, un carattere alla volta, finché la sottostringa temporaneamente corrispondente non è "Essential services are provided by regular expr". Confronta quindi la "e" nel modello con la seconda "e" in "expressions" e trova una corrispondenza.  
  
-   Confronta la "s" nel modello con la "s" che segue il carattere "e" corrispondente \(la prima "s" in "expressions"\). La corrispondenza ha esito positivo.  
  
 Quando si utilizza il backtracking, la ricerca di una corrispondenza tra il modello di espressione regolare e la stringa di input, con una lunghezza pari a 55 caratteri, richiede 67 operazioni di confronto. È interessante notare che se nel modello di espressione regolare venisse incluso un quantificatore lazy, .`*?(es)`, la ricerca di una corrispondenza dell'espressione regolare richiederebbe ulteriori confronti. In questo caso, anziché eseguire il backtracking dalla fine della stringa fino alla "r" in "expressions", il motore delle espressioni regolari dovrà eseguire il backtracking fino all'inizio della stringa per trovare una corrispondenza di "Es" richiedendo 113 confronti. In genere, se un modello di espressione regolare include un singolo costrutto di alternanza o un singolo quantificatore facoltativo, il numero di operazioni di confronto necessarie per trovare una corrispondenza del modello è più del doppio rispetto al numero di caratteri della stringa di input.  
  
 [Torna all'inizio](#top)  
  
<a name="backtracking_with_nested_optional_quantifiers"></a>   
## Backtracking con quantificatori facoltativi annidati  
 Il numero di operazioni di confronto necessarie per trovare una corrispondenza di un modello di espressione regolare può aumentare in modo esponenziale se il modello include un numero elevato di costrutti di alternanza, se include costrutti di alternanza annidati o se include sopratutto quantificatori facoltativi annidati. Il modello di espressione regolare `^(a+)+$`, ad esempio, è progettato per cercare una corrispondenza con una stringa completa contenente uno o più caratteri "a". Nell'esempio vengono fornite due stringhe di input di lunghezza identica, ma solo la prima stringa corrisponde al modello. La classe <xref:System.Diagnostics.Stopwatch?displayProperty=fullName> viene utilizzata per determinare il tempo richiesto dall'operazione di corrispondenza.  
  
 [!code-csharp[Conceptual.RegularExpressions.Backtracking#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/cs/backtracking3.cs#3)]
 [!code-vb[Conceptual.RegularExpressions.Backtracking#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/vb/backtracking3.vb#3)]  
  
 Come illustrato nell'output dell'esempio, il motore delle espressioni regolari ha impiegato il doppio del tempo per rilevare che una stringa di input non corrisponde al modello rispetto al tempo impiegato per identificare una stringa corrispondente. Ciò è dovuto al fatto che una corrispondenza negativa rappresenta sempre lo scenario peggiore. Il motore delle espressioni regolari deve utilizzare l'espressione regolare per seguire tutti i percorsi possibili nei dati prima di poter concludere che la corrispondenza è negativa e le parentesi annidate creano molti percorsi aggiuntivi nei dati. Il motore delle espressioni regolari conclude che la seconda stringa non corrisponde al modello effettuando le operazioni seguenti:  
  
-   Verifica di essere all'inizio della stringa, quindi cerca una corrispondenza tra i primi cinque caratteri della stringa e il modello `a+`. Determina quindi che non esistono altri gruppi di caratteri "a" nella stringa. Infine, verifica la fine della stringa. Poiché nella stringa rimane un ulteriore carattere, la corrispondenza ha esito negativo. La corrispondenza non riuscita richiede 9 confronti. Il motore delle espressioni regolari salva inoltre le informazioni di stato dalle relative corrispondenze di "a" \(che chiameremo corrispondenza 1\), "aa" \(corrispondenza 2\), "aaa" \(corrispondenza 3\) e "aaaa" \(corrispondenza 4\).  
  
-   Torna alla corrispondenza 4 salvata in precedenza. Determina che esiste un altro carattere "a" da assegnare a un gruppo acquisito aggiuntivo. Infine, verifica la fine della stringa. Poiché nella stringa rimane un ulteriore carattere, la corrispondenza ha esito negativo. La corrispondenza non riuscita richiede 4 confronti. Fino a questo momento sono stati eseguiti complessivamente 13 confronti.  
  
-   Torna alla corrispondenza 3 salvata in precedenza. Determina che esistono sono altri due caratteri "a" da assegnare a un gruppo acquisito aggiuntivo. Tuttavia, il test di fine della stringa ha esito negativo. Torna quindi alla corrispondenza 3 e tenta di trovare una corrispondenza degli altri due caratteri "a" nei due gruppi acquisiti aggiuntivi. Il test di fine della stringa ha ancora esito negativo. Le corrispondenza non riuscite richiedono 12 confronti. Fino a questo punto, sono stati eseguiti complessivamente 25 confronti.  
  
 Il confronto della stringa di input con l'espressione regolare continua in questo modo fino a quando il motore delle espressioni regolari non ha tentato tutte le combinazioni di corrispondenze possibili, concludendo infine che non vi è alcuna corrispondenza. A causa dei quantificatori annidati, questo confronto è un'operazione O\(2<sup>n</sup>\) o un'operazione esponenziale, dove *n* è il numero di caratteri nella stringa di input. Ciò significa che nei casi peggiori una stringa di input di 30 caratteri richiede circa 1.073.741.824 confronti e una stringa di input di 40 caratteri richiede circa 1.099.511.627.776 confronti. Se si utilizzano stringhe di queste lunghezze o di lunghezze ancora maggiore, i metodi delle espressioni regolari possono richiedere una quantità di tempo eccessiva per il completamento quando elaborano un input che non corrisponde al modello di espressione regolare.  
  
 [Torna all'inizio](#top)  
  
<a name="controlling_backtracking"></a>   
## Controllo del backtracking  
 Il backtracking consente di creare espressioni regolari potenti e flessibili. Tuttavia, come illustrato nella sezione precedente, insieme a questi vantaggi si ottiene una notevole riduzione delle prestazioni. Per evitare un utilizzo eccessivo del backtracking, è necessario definire un intervallo di timeout quando si crea un'istanza di un oggetto <xref:System.Text.RegularExpressions.Regex> o si chiama un metodo di espressione regolare statica corrispondente. Questo è discusso nella sezione seguente. Inoltre, .NET Framework supporta tre elementi del linguaggio delle espressioni regolari che limitano o evitano del tutto l'utilizzo del backtracking e che supportano le espressioni regolari complesse senza o con una minima riduzione delle prestazioni: [sottoespressioni non di backtracking](#Nonbacktracking), [asserzioni lookbehind](#Lookbehind) e [asserzioni lookahead](#Lookahead). Per altre informazioni su ogni elemento del linguaggio, vedere [Costrutti di raggruppamento](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
<a name="Timeout"></a>   
### Definizione di un intervallo di timeout  
 A partire da [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], è possibile impostare un valore di timeout che rappresenta l'intervallo più lungo, il motore delle espressioni regolari cercherà una singola corrispondenza prima che abbandoni il tentativo e genererà un'eccezione <xref:System.Text.RegularExpressions.RegexMatchTimeoutException>. Specificare l'intervallo di timeout fornendo un valore <xref:System.TimeSpan> al costruttore <xref:System.Text.RegularExpressions.Regex.%23ctor%28System.String%2CSystem.Text.RegularExpressions.RegexOptions%2CSystem.TimeSpan%29?displayProperty=fullName> per instanziare espressioni regolari. Inoltre, ogni metodo statico di criteri di ricerca ha un overload con un parametro <xref:System.TimeSpan> che consente di specificare un valore di timeout. Per impostazione predefinita, l'intervallo di timeout viene impostato su <xref:System.Text.RegularExpressions.Regex.InfiniteMatchTimeout?displayProperty=fullName> e il motore delle espressioni regolari non ha timeout.  
  
> [!IMPORTANT]
>  È consigliabile impostare sempre un intervallo di timeout se l'espressione regolare si basa sul backtracking.  
  
 Un'eccezione <xref:System.Text.RegularExpressions.RegexMatchTimeoutException> indica che il motore delle espressioni regolari non è in grado di trovare una corrispondenza nell'intervallo di timeout specificato, ma non indica che l'eccezione è stata generata. Il motivo può essere l'utilizzo eccessivo del backtracking, ma è anche possibile che l'intervallo di timeout sia stato impostato troppo basso dato il carico di sistema al momento in cui l'eccezione è stata generata. Quando si gestisce l'eccezione, è possibile scegliere di ignorare ulteriori corrispondenze con la stringa di input o aumentare l'intervallo di timeout e ritentare l'operazione corrispondente.  
  
 Ad esempio, il codice seguente chiama il costruttore <xref:System.Text.RegularExpressions.Regex.%23ctor%28System.String%2CSystem.Text.RegularExpressions.RegexOptions%2CSystem.TimeSpan%29?displayProperty=fullName> per creare un'istanza di un oggetto <xref:System.Text.RegularExpressions.Regex> con un valore di timeout di un secondo. Il modello di espressione regolare `(a+)+$`, che corrisponde a uno o più sequenze di uno o più caratteri "a" alla fine di una riga, è soggetto all'utilizzo eccessivo del backtracking. Se <xref:System.Text.RegularExpressions.RegexMatchTimeoutException> viene generato, l'esempio aumenta il valore di timeout fino a un intervallo massimo di tre secondi. Successivamente, ignora il tentativo di corrispondere al modello.  
  
 [!code-csharp[System.Text.RegularExpressions.Regex.ctor#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.text.regularexpressions.regex.ctor/cs/ctor1.cs#1)]
 [!code-vb[System.Text.RegularExpressions.Regex.ctor#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.text.regularexpressions.regex.ctor/vb/ctor1.vb#1)]  
  
<a name="Nonbacktracking"></a>   
### Sottoespressione non di backtracking  
 L'elemento del linguaggio `(?>` *sottoespressione*`)` evita l'uso del backtracking in una sottoespressione. È utile per non incorrere nei problemi di prestazioni associati alle corrispondenze non riuscite.  
  
 Nell'esempio seguente vengono illustrati i miglioramenti nelle prestazioni con i quantificatori annidati quando non si utilizza il backtracking. Viene calcolato il tempo impiegato dal motore delle espressioni regolari per determinare che una stringa di input non corrisponde a due espressioni regolari. La prima espressione regolare utilizza il backtracking per tentare di trovare una corrispondenza con una stringa contenente una o più occorrenze di una o più cifre esadecimali seguite da due punti, seguiti da una o più cifre esadecimali, seguite da un doppio due punti. La seconda espressione regolare è identica alla prima, con la differenza che il backtracking è disabilitato. Come illustrato nell'output dell'esempio, il miglioramento delle prestazioni derivante dalla disabilitazione del backtracking è significativo.  
  
 [!code-csharp[Conceptual.RegularExpressions.Backtracking#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/cs/backtracking4.cs#4)]
 [!code-vb[Conceptual.RegularExpressions.Backtracking#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/vb/backtracking4.vb#4)]  
  
<a name="Lookbehind"></a>   
### Asserzioni lookbehind  
 .NET Framework include due elementi del linguaggio, `(?<=`*sottoespressione*`)` e `(?<!`*sottoespressione*`)`, che trovano il carattere o i caratteri precedenti nella stringa di input. Entrambi gli elementi del linguaggio sono asserzioni di larghezza zero, ovvero determinano se il carattere o i caratteri che precedono immediatamente il carattere corrente possono essere trovati da *sottoespressione*, senza avanzamento o backtracking.  
  
 `(?<=` *sottoespressione* `)` è un'asserzione lookbehind positiva, ovvero il carattere o i caratteri prima della posizione corrente devono corrispondere a *sottoespressione*.`(?<!`*sottoespressione*`)` è un'asserzione lookbehind negativa, ovvero il carattere o i caratteri prima della posizione corrente non devono corrispondere a *sottoespressione*. Le asserzioni lookbehind positive e negative sono entrambe particolarmente utili quando *sottoespressione* è un subset della sottoespressione precedente.  
  
 Nell'esempio seguente vengono utilizzati due modelli di espressione regolare equivalenti per verificare il nome utente in un indirizzo di posta elettronica. Il primo modello è soggetto a una riduzione delle prestazioni a causa di un utilizzo eccessivo del backtracking. Il secondo modello modifica la prima espressione regolare sostituendo un quantificatore annidato con un'asserzione lookbehind positiva. Nell'output dell'esempio viene visualizzato il tempo di esecuzione del metodo <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=fullName>.  
  
 [!code-csharp[Conceptual.RegularExpressions.Backtracking#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/cs/backtracking5.cs#5)]
 [!code-vb[Conceptual.RegularExpressions.Backtracking#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/vb/backtracking5.vb#5)]  
  
 Il primo criterio di espressione regolare, `^[0-9A-Z]([-.\w]*[0-9A-Z])*@`, è definito nel modo illustrato nella tabella seguente.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`^`|Inizia la ricerca della corrispondenza all'inizio della stringa.|  
|`[0-9A-Z]`|Trova la corrispondenza di un carattere alfanumerico. Poiché il metodo <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=fullName> viene richiamato con l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>, il confronto non rileva la distinzione tra maiuscole e minuscole.|  
|`[-.\w]*`|Trova la corrispondenza di zero, una o più occorrenze di un trattino, un punto o un carattere alfanumerico.|  
|`[0-9A-Z]`|Trova la corrispondenza di un carattere alfanumerico.|  
|`([-.\w]*[0-9A-Z])*`|Trova la corrispondenza di zero o più occorrenze della combinazione di zero o più trattini, punti o caratteri alfanumerici seguiti da un carattere alfanumerico. Equivale al primo gruppo di acquisizione.|  
|`@`|Trova la corrispondenza di una chiocciola \("@"\).|  
  
 Il secondo criterio di espressione regolare, `^[0-9A-Z][-.\w]*(?<=[0-9A-Z])@`, usa un'asserzione lookbehind positiva e viene definito come illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`^`|Inizia la ricerca della corrispondenza all'inizio della stringa.|  
|`[0-9A-Z]`|Trova la corrispondenza di un carattere alfanumerico. Poiché il metodo <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=fullName> viene richiamato con l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>, il confronto non rileva la distinzione tra maiuscole e minuscole.|  
|`[-.\w]*`|Trova la corrispondenza di zero o più occorrenze di un trattino, un punto o un carattere alfanumerico.|  
|`(?<=[0-9A-Z])`|Esegue la ricerca dell'ultimo carattere corrispondente e continua la ricerca della corrispondenza se si tratta di un carattere alfanumerico. Si noti che i caratteri alfanumerici sono un subset del set costituito da punti, trattini e tutti i caratteri alfanumerici.|  
|`@`|Trova la corrispondenza di una chiocciola \("@"\).|  
  
<a name="Lookahead"></a>   
### Asserzioni lookahead  
 .NET Framework include due elementi del linguaggio, `(?=`*sottoespressione*`)` e `(?!`*sottoespressione*`)`, che trovano il carattere o i caratteri successivi nella stringa di input. Entrambi gli elementi del linguaggio sono asserzioni di larghezza zero, ovvero determinano se il carattere o i caratteri che seguono immediatamente il carattere corrente possono essere trovati da *sottoespressione*, senza avanzamento o backtracking.  
  
 `(?=` *sottoespressione* `)` è un'asserzione lookahead positiva, ovvero il carattere o i caratteri dopo la posizione corrente devono corrispondere a *sottoespressione*.`(?!`*sottoespressione*`)` è un'asserzione lookahead negativa, ovvero il carattere o i caratteri dopo la posizione corrente non devono corrispondere a *sottoespressione*. Le asserzioni lookahead positive e negative sono entrambe particolarmente utili quando *sottoespressione* è un subset della sottoespressione successiva.  
  
 Nell'esempio seguente vengono utilizzati due modelli di espressione regolare equivalenti per verificare un nome di tipo completo. Il primo modello è soggetto a una riduzione delle prestazioni a causa di un utilizzo eccessivo del backtracking. Il secondo modello modifica la prima espressione regolare sostituendo un quantificatore annidato con un'asserzione lookahead positiva. Nell'output dell'esempio viene visualizzato il tempo di esecuzione del metodo <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=fullName>.  
  
 [!code-csharp[Conceptual.RegularExpressions.Backtracking#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/cs/backtracking6.cs#6)]
 [!code-vb[Conceptual.RegularExpressions.Backtracking#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/vb/backtracking6.vb#6)]  
  
 Il primo criterio di espressione regolare, `^(([A-Z]\w*)+\.)*[A-Z]\w*$`, è definito nel modo illustrato nella tabella seguente.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`^`|Inizia la ricerca della corrispondenza all'inizio della stringa.|  
|`([A-Z]\w*)+\.`|Trova la corrispondenza di un carattere alfabetico \(A\-Z\) seguito da zero o più caratteri alfanumerici una o più volte seguiti da un punto. Poiché il metodo <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=fullName> viene richiamato con l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>, il confronto non rileva la distinzione tra maiuscole e minuscole.|  
|`(([A-Z]\w*)+\.)*`|Trova la corrispondenza del modello precedente zero o più volte.|  
|`[A-Z]\w*`|Trova la corrispondenza di un carattere alfabetico seguito da zero o più caratteri alfanumerici.|  
|`$`|Termina la ricerca della corrispondenza alla fine della stringa di input.|  
  
 Il secondo criterio di espressione regolare, `^((?=[A-Z])\w+\.)*[A-Z]\w*$`, usa un'asserzione lookahead positiva e viene definito come illustrato nella tabella seguente.  
  
|Criterio|Descrizione|  
|--------------|-----------------|  
|`^`|Inizia la ricerca della corrispondenza all'inizio della stringa.|  
|`(?=[A-Z])`|Esegue la ricerca fino primo carattere e continua la ricerca della corrispondenza se si tratta di un carattere alfabetico \(A\-Z\). Poiché il metodo <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=fullName> viene richiamato con l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>, il confronto non rileva la distinzione tra maiuscole e minuscole.|  
|`\w+\.`|Trova la corrispondenza di uno o più caratteri alfanumerici seguiti da un punto.|  
|`((?=[A-Z])\w+\.)*`|Trova la corrispondenza del modello di uno o più caratteri alfanumerici seguiti da un punto zero o più volte. Il carattere alfanumerico iniziale deve essere alfabetico.|  
|`[A-Z]\w*`|Trova la corrispondenza di un carattere alfabetico seguito da zero o più caratteri alfanumerici.|  
|`$`|Termina la ricerca della corrispondenza alla fine della stringa di input.|  
  
 [Torna all'inizio](#top)  
  
## Vedere anche  
 [Espressioni regolari di .NET Framework](../../../docs/standard/base-types/regular-expressions.md)   
 [Linguaggio di espressioni regolari \- Riferimento rapido](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)   
 [Quantificatori](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md)   
 [Costrutti di alternanza](../../../docs/standard/base-types/alternation-constructs-in-regular-expressions.md)   
 [Costrutti di raggruppamento](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)