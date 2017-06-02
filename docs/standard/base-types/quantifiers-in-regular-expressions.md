---
title: "Quantificatori in espressioni regolari | Microsoft Docs"
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
  - "espressioni regolari, quantificatori"
  - "metacaratteri, quantificatori"
  - "quantificatori di corrispondenza minima"
  - "quantificatori in espressioni regolari"
  - "espressioni regolari di .NET Framework, quantificatori"
  - "quantificatori"
  - "quantificatori lenti"
ms.assetid: 36b81212-6511-49ed-a8f1-ff080415312f
caps.latest.revision: 22
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 22
---
# Quantificatori in espressioni regolari
I quantificatori specificano il numero di istanze di un carattere, un gruppo o una classe di caratteri che devono essere presenti nell'input affinché venga trovata una corrispondenza.  Nella tabella seguente sono elencati i quantificatori supportati da .NET Framework.  
  
|Quantificatore greedy|Quantificatore lazy|Descrizione|  
|---------------------------|-------------------------|-----------------|  
|`*`|`*?`|Ottiene zero o più volte una corrispondenza.|  
|`+`|`+?`|Ottiene una corrispondenza una o più volte.|  
|`?`|`??`|Ottiene zero o una volta una corrispondenza.|  
|`{` *n* `}`|`{` *n* `}?`|Ottiene una corrispondenza esatta *n* volte.|  
|`{` *n* `,}`|`{` *n* `,}?`|Trova corrispondenze per almeno *n* volte.|  
|`{` *n* `,` *m* `}`|`{` *n* `,` *m* `}?`|Trova corrispondenza da *n* a *m* volte.|  
  
 Le quantità `n` e `m` sono costanti integer.  In genere, i quantificatori sono greedy: fanno in modo che il motore delle espressioni regolari individui corrispondenze per il maggior numero possibile di occorrenze di modelli specifici.  L'aggiunta del carattere `?` a un quantificatore lo rende lazy; fa in modo che il motore delle espressioni regolari trovi il minor numero possibile di corrispondenze.  Per una descrizione della differenza tra quantificatore greedy e lazy, vedere la sezione [Quantificatore greedy e lazy](#Greedy) riportata più avanti in questo argomento.  
  
> [!IMPORTANT]
>  Annidare i quantificatori \(ad esempio, come nel modello di espressione regolare `(a*)*`\) può aumentare il numero dei confronti che il motore delle espressioni regolari deve eseguire, come funzione esponenziale del numero di caratteri nella stringa di input.  Per ulteriori informazioni su tale comportamento e relative soluzioni alternative, vedere [Backtracking](../../../docs/standard/base-types/backtracking-in-regular-expressions.md).  
  
## Quantificatori delle espressioni regolari  
 Nelle seguenti sezioni vengono elencati i quantificatori supportati dalle espressioni regolari di .NET Framework.  
  
> [!NOTE]
>  Se i caratteri \*, \+, ?, { e } sono presenti in un criterio di espressione regolare, il motore delle espressioni regolari li interpreta come quantificatori o parte di costrutti del quantificatore a meno che siano inclusi in una [classe di caratteri](../../../docs/standard/base-types/character-classes-in-regular-expressions.md).  Per interpretare questi caratteri come caratteri letterali esterni a una classe di caratteri, è necessario utilizzare caratteri di escape preceduti da una barra rovesciata.  Ad esempio, in un criterio di espressione regolare la stringa `\*` viene interpretata come un carattere letterale asterisco \("\*"\).  
  
### Ottiene zero o più volte una corrispondenza: \*  
 Il quantificatore `*` trova zero o più corrispondenze con l'elemento precedente.  È equivalente al quantificatore `{0,}`.  `*` è un quantificatore greedy il cui equivalente lazy è `*?`.  
  
 Questa espressione regolare viene illustrata nell'esempio seguente.  Delle nove cifre della stringa di input, cinque corrispondono al modello e quattro \(`95`, `929`, `9129` e `9919`\) no.  
  
 [!code-csharp[RegularExpressions.Quantifiers#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#1)]
 [!code-vb[RegularExpressions.Quantifiers#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#1)]  
  
 Il modello di espressione regolare viene definito come illustrato nella tabella riportata di seguito.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\b`|Iniziare dal confine di una parola.|  
|`91*`|Corrisponde a un "9" seguito da zero o più caratteri "1".|  
|`9*`|Corrisponde a zero o più caratteri "9".|  
|`\b`|Terminare al confine di una parola.|  
  
### Ottiene una corrispondenza una o più volte: \+  
 Il quantificatore `+` trova una o più corrispondenze con l'elemento precedente.  Equivale a `{1,}`.  `+` è un quantificatore greedy il cui equivalente lazy è `+?`.  
  
 Ad esempio, l'espressione regolare `\ban+\w*?\b` tenta di trovare una corrispondenza con intere parole che iniziano con la lettera `a` seguita da una o più istanze della lettera `n`.  Questa espressione regolare viene illustrata nell'esempio seguente.  L'espressione regolare trova una corrispondenza con le parole `an`, `annual`, `announcement` e `antique`, mentre correttamente non la trova con `autumn` e `all`.  
  
 [!code-csharp[RegularExpressions.Quantifiers#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#2)]
 [!code-vb[RegularExpressions.Quantifiers#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#2)]  
  
 Il modello di espressione regolare viene definito come illustrato nella tabella riportata di seguito.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\b`|Iniziare dal confine di una parola.|  
|`an+`|Corrisponde a una "a" seguita da uno o più caratteri "n".|  
|`\w*?`|Ottiene zero o più volte la corrispondenza di un carattere alfanumerico, ma il minor numero di volte possibile.|  
|`\b`|Terminare al confine di una parola.|  
  
### Ottiene zero o una volta una corrispondenza: ?  
 Il quantificatore `?` trova zero o una corrispondenza con l'elemento precedente.  Equivale a `{0,1}`.  `?` è un quantificatore greedy il cui equivalente lazy è `??`.  
  
 Ad esempio, l'espressione regolare `\ban?\b` tenta di trovare una corrispondenza con intere parole che iniziano con la lettera `a` seguita da zero o più istanze della lettera `n`.  In altri termini, tenta di trovare una corrispondenza con le parole `a` e `an`.  Questa espressione regolare viene illustrata nell'esempio seguente.  
  
 [!code-csharp[RegularExpressions.Quantifiers#3](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#3)]
 [!code-vb[RegularExpressions.Quantifiers#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#3)]  
  
 Il modello di espressione regolare viene definito come illustrato nella tabella riportata di seguito.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\b`|Iniziare dal confine di una parola.|  
|`an?`|Corrisponde a una "a" seguita da zero o un carattere "n".|  
|`\b`|Terminare al confine di una parola.|  
  
### Ottiene una corrispondenza esatta n volte: {n}  
 Il quantificatore `{`*n*`}` corrisponde all'elemento precedente esattamente *n* volte, dove *n* è qualsiasi numero intero.  `{`*n*`}` è un quantificatore greedy il cui equivalente lazy è `{`*n*`}?`.  
  
 Ad esempio, l'espressione regolare `\b\d+\,\d{3}\b` tenta di trovare una corrispondenza con un limite di parola seguito da una o più cifre decimali seguite da tre cifre decimali seguite da un limite di parola.  Questa espressione regolare viene illustrata nell'esempio seguente.  
  
 [!code-csharp[RegularExpressions.Quantifiers#4](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#4)]
 [!code-vb[RegularExpressions.Quantifiers#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#4)]  
  
 Il modello di espressione regolare viene definito come illustrato nella tabella riportata di seguito.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\b`|Iniziare dal confine di una parola.|  
|`\d+`|Corrisponde a una o più cifre decimali.|  
|`\,`|Corrisponde a una virgola.|  
|`\d{3}`|Corrisponde a tre cifre decimali.|  
|`\b`|Terminare al confine di una parola.|  
  
### Ottiene una corrispondenza per almeno n volte: {n,}  
 Il quantificatore `{`*n*`,}` corrisponde all'elemento precedente almeno *n* volte, dove *n* è qualsiasi numero intero.  `{`*n*`,}` è un quantificatore greedy il cui equivalente lazy è `{`*n*`}?`.  
  
 Ad esempio, l'espressione regolare `\b\d{2,}\b\D+` tenta di trovare una corrispondenza con un limite di parola seguito da almeno due cifre seguite da un limite di parola e da un carattere non numerico.  Questa espressione regolare viene illustrata nell'esempio seguente.  L'espressione regolare non trova corrispondenza con la frase `"7 days"` perché contiene solo uno cifra decimale, ma trova corrispondenza con le frasi `"10 weeks and 300 years"`.  
  
 [!code-csharp[RegularExpressions.Quantifiers#5](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#5)]
 [!code-vb[RegularExpressions.Quantifiers#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#5)]  
  
 Il modello di espressione regolare viene definito come illustrato nella tabella riportata di seguito.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\b`|Iniziare dal confine di una parola.|  
|`\d{2,}`|Corrisponde almeno a due cifre decimali.|  
|`\b`|Trovare la corrispondenza di un confine di parola.|  
|`\D+`|Corrisponde almeno a una cifra non decimale.|  
  
### Corrispondenza tra n e m volte: {n,m}  
 Il quantificatore `{`*n*`,`*m*`}` corrisponde all'elemento precedente almeno *n* volte, ma non più di *m* volte, dove *n* e *m* sono numeri interi.  `{`*n*`,`*m*`}` è un quantificatore greedy il cui equivalente lazy è `{`*n*`,`*m*`}?`.  
  
 Nell'esempio riportato di seguito, l'espressione regolare `(00\s){2,4}` tenta di trovare una corrispondenza tra due e quattro occorrenze di due cifre zero seguite da uno spazio.  Si noti che la parte finale della stringa di input include il modello cinque volte anziché il massimo di quattro.  Tuttavia, solo la parte iniziale della sottostringa \(fino allo spazio e alla quinta coppia di zero\) corrisponde al modello dell'espressione regolare.  
  
 [!code-csharp[RegularExpressions.Quantifiers#6](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#6)]
 [!code-vb[RegularExpressions.Quantifiers#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#6)]  
  
### Ottiene zero o più volte una corrispondenza \(Corrispondenza Lazy\): \*?  
 Il quantificatore `*?` corrisponde all'elemento che lo precede zero o più volte, ma il numero minimo di volte possibile.  Si tratta di un quantificatore lazy omologo del quantificatore greedy `*`.  
  
 Nell'esempio riportato di seguito, l'espressione regolare `\b\w*?oo\w*?\b` corrisponde a tutte le parole che contengono la stringa `oo`.  
  
 [!code-csharp[RegularExpressions.Quantifiers#7](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#7)]
 [!code-vb[RegularExpressions.Quantifiers#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#7)]  
  
 Il modello di espressione regolare viene definito come illustrato nella tabella riportata di seguito.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\b`|Iniziare dal confine di una parola.|  
|`\w*?`|Corrisponde a zero o più caratteri alfanumerici, ma al minor numero di caratteri possibile.|  
|`oo`|Corrisponde alla stringa "oo".|  
|`\w*?`|Corrisponde a zero o più caratteri alfanumerici, ma al minor numero di caratteri possibile.|  
|`\b`|Fine sul confine di parola.|  
  
### Ottiene una corrispondenza una o più volte \(Corrispondenza Lazy\): \+?  
 Il quantificatore `+?` corrisponde all'elemento che lo precede una o più volte, ma il numero minimo di volte possibile.  Si tratta di un quantificatore lazy omologo del quantificatore greedy `+`.  
  
 Ad esempio, l'espressione regolare `\b\w+?\b` corrisponde a uno o più caratteri separati da limiti di parola.  Questa espressione regolare viene illustrata nell'esempio seguente.  
  
 [!code-csharp[RegularExpressions.Quantifiers#8](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#8)]
 [!code-vb[RegularExpressions.Quantifiers#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#8)]  
  
### Ottiene zero o una volta una corrispondenza \(Corrispondenza Lazy\): ??  
 Il quantificatore `??` corrisponde all'elemento che lo precede zero o una volta, ma il numero minimo di volte possibile.  Si tratta di un quantificatore lazy omologo del quantificatore greedy `?`.  
  
 Ad esempio, l'espressione regolare `^\s*(System.)??Console.Write(Line)??\(??` tenta di far corrispondere le stringhe "Console.Write" o "Console.WriteLine".  La stringa può includere anche "System." prima di "Console" e può essere seguita da una parentesi aperta.  La stringa deve trovarsi all'inizio di una riga, anche se può essere preceduta da uno spazio vuoto.  Questa espressione regolare viene illustrata nell'esempio seguente.  
  
 [!code-csharp[RegularExpressions.Quantifiers#9](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#9)]
 [!code-vb[RegularExpressions.Quantifiers#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#9)]  
  
 Il modello di espressione regolare viene definito come illustrato nella tabella riportata di seguito.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`^`|Corrisponde all'inizio del flusso di input.|  
|`\s*`|Trovare la corrispondenza di zero o più spazi vuoti.|  
|`(System.)??`|Corrisponde a zero o a un'occorrenza della stringa "System.".|  
|`Console.Write`|Corrispondere stringa "Console.Write".|  
|`(Line)??`|Corrispondere zero o una occorrenza della stringa "Line".|  
|`\(??`|Corrisponde a zero o a un'occorrenza della parentesi di apertura.|  
  
### Ottiene una corrispondenza esatta n volte \(Corrispondenza Lazy\): {n}?  
 Il quantificatore `{`*n*`}?` corrisponde all'elemento precedente esattamente `n` volte, dove *n* è qualsiasi numero intero.  Si tratta di un quantificatore lazy omologo del quantificatore greedy `{`*n*`}+`.  
  
 Nell'esempio riportato di seguito, l'espressione regolare `\b(\w{3,}?\.){2}?\w{3,}?\b` viene utilizzata per identificare un indirizzo di sito Web.  Corrisponde a "www.microsoft.com" e "msdn.microsoft.com", ma non corrisponde a "sitoweb" o "azienda.com".  
  
 [!code-csharp[RegularExpressions.Quantifiers#10](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#10)]
 [!code-vb[RegularExpressions.Quantifiers#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#10)]  
  
 Il modello di espressione regolare viene definito come illustrato nella tabella riportata di seguito.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\b`|Iniziare dal confine di una parola.|  
|`(\w{3,}?\.)`|Corrisponde ad almeno 3 caratteri alfanumerici, ma al minor numero di caratteri possibile, seguiti da un punto.  Primo gruppo di acquisizione.|  
|`(\w{3,}?\.){2}?`|Ottiene due volte la corrispondenza per il modello nel primo gruppo, ma il minor numero di volte possibile.|  
|`\b`|Termina la corrispondenza sul confine di parola.|  
  
### Ottiene una corrispondenza per almeno n volte \(Corrispondenza Lazy\): {n,}?  
 Il quantificatore `{`*n*`,}?` corrisponde all'elemento precedente almeno `n` volte, dove *n* è qualsiasi numero intero, ma il minor numero di volte possibile.  Si tratta di un quantificatore lazy omologo del quantificatore greedy `{`*n*`,}`.  
  
 Vedere l'esempio relativo al quantificatore `{`*n*`}?` nella sezione precedente per un'illustrazione.  L'espressione regolare nell'esempio utilizza il quantificatore `{`*n*`,}` per ottenere una corrispondenza con una stringa costituita da almeno tre caratteri seguiti da un punto.  
  
### Corrispondenza tra n e m volte \(Corrispondenza Lazy\): {n, m}?  
 Il quantificatore `{`*n*`,`*m*`}?` corrisponde all'elemento precedente tra `n` e `m` volte, dove *n* e *m* sono numeri interi, ma il minor numero di volte possibile.  Si tratta di un quantificatore lazy omologo del quantificatore greedy `{`*n*`,`*m*`}`.  
  
 Nel seguente esempio, l'espressione regolare `\b[A-Z](../../../amples/snippets/visualbasic/VS_Snippets_Remoting/SoapAttributes1/VB/s.vb){1,10}?[.!?]` corrisponde alle frasi che contengono da una a dieci parole.  Corrisponde a tutte le frasi nella stringa di input ad eccezione di una singola frase che contenga 18 parole.  
  
 [!code-csharp[RegularExpressions.Quantifiers#12](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers/cs/Quantifiers1.cs#12)]
 [!code-vb[RegularExpressions.Quantifiers#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers/vb/Quantifiers1.vb#12)]  
  
 Il modello di espressione regolare viene definito come illustrato nella tabella riportata di seguito.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\b`|Iniziare dal confine di una parola.|  
|`[A-Z]`|Corrisponde a un carattere maiuscolo da A a Z.|  
|`(\w*\s+)`|Corrisponde a zero o più caratteri alfanumerici, seguiti da uno o più spazi vuoti.  Si tratta del primo gruppo di acquisizione.|  
|`{1,10}?`|Ottiene da 1 a 10 volte la corrispondenza con il modello precedente, ma il minor numero di volte possibile.|  
|`[.!?]`|Corrisponde a uno dei caratteri di punteggiatura ".", "\!" o "?".|  
  
<a name="Greedy"></a>   
## Quantificatore greedy e lazy  
 Diversi quantificatori sono disponibili in due versioni:  
  
-   Una versione greedy.  
  
     Un quantificatore greedy tenta di trovare una corrispondenza con un elemento il numero massimo di volte possibile.  
  
-   Una versione non\-greedy \(o lazy\).  
  
     Un quantificatore non greedy tenta di trovare una corrispondenza con un elemento il numero minimo di volte possibile.  È possibile trasformare un quantificatore greedy in un quantificatore lazy aggiungendo semplicemente un `?`.  
  
 Considerare un'espressione regolare semplice progettata per estrarre le ultime quattro cifre da una stringa di numeri, ad esempio il numero di una carta di credito.  La versione dell'espressione regolare che utilizza il quantificatore greedy `*` è `\b.*([0-9]{4})\b`.  Tuttavia, se una stringa contiene due numeri, l'espressione regolare corrisponde soltanto alle ultime quattro cifre del secondo numero, come illustrato nell'esempio seguente.  
  
 [!code-csharp[RegularExpressions.Quantifiers.Greedy#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers.Greedy/cs/Greedy.cs#1)]
 [!code-vb[RegularExpressions.Quantifiers.Greedy#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers.Greedy/vb/Greedy.vb#1)]  
  
 L'espressione regolare non riesce a trovare una corrispondenza con il primo numero perché il quantificatore `*` tenta di trovare una corrispondenza con l'elemento precedente il numero massimo di volte possibile nell'intera stringa, quindi trova la corrispondenza alla fine della stringa.  
  
 Non si tratta del comportamento previsto.  È invece possibile utilizzare il quantificatore lazy `*?` ``  per estrarre cifre da entrambi numeri, come illustrato nell'esempio seguente.  
  
 [!code-csharp[RegularExpressions.Quantifiers.Greedy#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Quantifiers.Greedy/cs/Greedy.cs#2)]
 [!code-vb[RegularExpressions.Quantifiers.Greedy#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Quantifiers.Greedy/vb/Greedy.vb#2)]  
  
 Nella maggior parte dei casi, le espressioni regolari con quantificatori greedy e lazy restituiscono le stesse corrispondenze.  In genere restituiscono risultati diversi se utilizzate con il carattere jolly, metacarattere `.`, che corrisponde a qualsiasi carattere.  
  
## Quantificatori e corrispondenze vuote  
 I quantificatori `*`, `+` e `{`*n*`,`*m*`}` e le controparti lazy non si ripetono mai dopo una corrispondenza vuota quando è stato trovato il numero minimo di acquisizioni.  Questa regola impedisce ai quantificatori di fornire cicli infiniti su corrispondenze di sottoespressioni vuote quando il numero massimo di acquisizioni di gruppo possibili è infinito o prossimo a tale valore.  
  
 Ad esempio, nel codice seguente viene illustrato il risultato di una chiamata al metodo <xref:System.Text.RegularExpressions.Regex.Match%2A?displayProperty=fullName> con il modello di espressione regolare `(a?)*`, che corrisponde a zero o una occorrenza del carattere "a" per 0 o più volte.  Si noti che il singolo gruppo di acquisizione acquisisce ogni "a", nonché <xref:System.String.Empty?displayProperty=fullName>, ma non esiste una seconda corrispondenza vuota, perché la prima corrispondenza vuota induce il quantificatore a non essere ripetuto.  
  
 [!code-csharp[RegularExpressions.Quantifiers.EmptyMatch#1](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.quantifiers.emptymatch/cs/emptymatch1.cs#1)]
 [!code-vb[RegularExpressions.Quantifiers.EmptyMatch#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.quantifiers.emptymatch/vb/emptymatch1.vb#1)]  
  
 Per visualizzare la differenza pratica tra un gruppo di acquisizione che definisce un numero minimo e uno massimo di acquisizioni e uno che definisce un numero fisso di acquisizioni, considerare i modelli di espressione regolare `(a\1|(?(1)\1)){0,2}` e `(a\1|(?(1)\1)){2}`.  Entrambe le espressioni regolari sono costituite da un singolo gruppo di acquisizione, che viene definito nel modo illustrato nella tabella seguente.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`(a\1`|Far corrispondere "a" con il valore del primo gruppo acquisito…|  
|`&#124;(?(1)`|… o eseguire il test per verificare se è stato definito il gruppo acquisito per primo. \(Notare che il costrutto `(?(1)` non definisce un gruppo di acquisizione\).|  
|`\1))`|Se il primo gruppo acquisito esiste, fargli corrispondere il suo valore.  Se il gruppo non esiste, corrisponderà a <xref:System.String.Empty?displayProperty=fullName>.|  
  
 La prima espressione regolare tenta di far corrispondere questo modello tra zero e due volte; la seconda esattamente due volte.  Poiché il primo modello raggiunge il numero minimo di didascalie con la prima didascalia di <xref:System.String.Empty?displayProperty=fullName>, non ripete mai il tentativo di far corrispondere `a\1`; il quantificatore di `{0,2}` consente solo corrispondenze vuote nell'ultima iterazione.  Al contrario, la seconda espressione regolare non corrisponde a "a" poiché valuta `a\1` una seconda volta; il numero minimo di iterazioni, ovvero 2, impone la ripetizione del modulo di gestione dopo una corrispondenza vuota.  
  
 [!code-csharp[RegularExpressions.Quantifiers.EmptyMatch#2](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.quantifiers.emptymatch/cs/emptymatch4.cs#2)]
 [!code-vb[RegularExpressions.Quantifiers.EmptyMatch#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.quantifiers.emptymatch/vb/emptymatch4.vb#2)]  
  
## Vedere anche  
 [Linguaggio di espressioni regolari \- Riferimento rapido](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)   
 [Backtracking](../../../docs/standard/base-types/backtracking-in-regular-expressions.md)