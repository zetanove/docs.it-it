---
title: Riferimenti per simboli e operatori (F#)
description: Riferimenti per simboli e operatori (F#)
keywords: visual f#, f#, programmazione funzionale
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: ab453800-d4d0-4a11-9d55-2b358d56af27
translationtype: Human Translation
ms.sourcegitcommit: 0a01ec92a90d99fafaacbd3f71f5177e5cf94a68
ms.openlocfilehash: 514dc37dce3df3f40ae99ce55772b0c4e8deb95f
ms.lasthandoff: 04/05/2017

---

# <a name="symbol-and-operator-reference"></a>Riferimenti per simboli e operatori

> [!NOTE]
I collegamenti di riferimento all'API in questo articolo portano a MSDN.  Il riferimento all'API in Microsoft Docs (docs.microsoft.com) non è completo.

Questo argomento include una tabella di simboli e operatori usati nel linguaggio F#.

## <a name="table-of-symbols-and-operators"></a>Tabella di simboli e operatori
Nella tabella seguente sono descritti i simboli usati nel linguaggio F#, vengono forniti collegamenti ad argomenti che contengono altre informazioni e una breve descrizione di alcuni degli usi del simbolo. I simboli sono elencati in base all'ordinamento del set di caratteri ASCII.

|Simbolo o operatore|Collegamenti|Descrizione|
|------------------|-----|-----------|
|`!`|[Celle di riferimento](../reference-cells.md)<br /><br />[Espressioni di calcolo](../computation-expressions.md)|<ul><li>Dereferenzia una cella di riferimento.<br /></li><li>Dopo una parola chiave indica una versione modificata del comportamento della parola chiave, controllato da un flusso di lavoro.<br /></li><ul/>|
|`!=`|Non applicabile.|<ul><li>Non usato in F#. Usare `<>` per le operazioni di disuguaglianza.<br /></li><ul/>|
|`"`|[Valori letterali](../literals.md)<br /><br />[Stringhe](../strings.md)|<ul><li>Delimita una stringa di testo.<br /></li><ul/>|
|`"""`|[Stringhe](../strings.md)|Delimita una stringa di testo letterale. È diverso da `@"..."` in quanto si può indicare un carattere di virgolette usando una virgoletta singola nella stringa.|
|`#`|[Direttive per il compilatore](../compiler-directives.md)<br /><br />[Tipi flessibili](../flexible-types.md)|<ul><li>Prefisso di una direttiva del preprocessore o del compilatore, ad esempio `#light`.<br /></li><li>Se usato con un tipo, indica un *tipo flessibile*, che fa riferimento a un tipo o a uno dei relativi tipi derivati.<br /></li><ul/>|
|`$`|Non sono disponibili altre informazioni.|<ul><li>Usato internamente per determinati nomi di variabile e funzione generati dal compilatore.<br /></li><ul/>|
|`%`|[Operatori aritmetici](arithmetic-operators.md)<br /><br />[Citazioni di codice](../code-quotations.md)|<ul><li>Calcola il modulo integer.<br /></li><li>Usato per lo splicing delle espressioni in citazioni di codice tipizzato.<br /></li><ul/>|
|`%%`|[Citazioni di codice](../code-quotations.md)|<ul><li>Usato per lo splicing delle espressioni in citazioni di codice non tipizzato.<br /></li><ul/>|
|`%?`|[Operatori nullable](nullable-operators.md)|<ul><li>Calcola il modulo di integer, quando la parte destra è un tipo nullable.<br /></li><ul/>|
|`&`|[Espressioni match](../match-expressions.md)|<ul><li>Calcola l'indirizzo di un valore modificabile, da usare quando si interagisce con altri linguaggi.<br /></li><li>Usato nei modelli AND.<br /></li><ul/>|
|`&&`|[Operatori booleani](boolean-operators.md)|<ul><li>Calcola l'operazione AND booleana.<br /></li><ul/>|
|`&&&`|[Operatori bit per bit](bitwise-operators.md)|<ul><li>Calcola l'operazione AND bit per bit.<br /></li><ul/>|
|`'`|[Valori letterali](../literals.md)<br /><br />[Generalizzazione automatica](../generics/automatic-generalization.md)|<ul><li>Delimita un valore letterale a carattere singolo.<br /></li><li>Indica un parametro di tipo generico.<br /></li><ul/>|
|<code>&#96;&#96;...&#96;&#96;</code>|Non sono disponibili altre informazioni.|<ul><li>Delimita un identificatore che altrimenti non sarebbe un identificatore valido, ad esempio una parola chiave del linguaggio.<br /></li><ul/>|
|`( )`|[Tipo di unità](../unit-type.md)|<ul><li>Rappresenta il singolo valore del tipo di unità.<br /></li><ul/>|
|`(...)`|[Tuple](../tuples.md)<br /><br />[Overload degli operatori](../operator-overloading.md)|<ul><li>Indica l'ordine in cui le espressioni vengono valutate.<br /></li><li>Delimita una tupla.<br /></li><li>Usato nelle definizioni degli operatori.<br /></li><ul/>|
|`(*...*)`||<ul><li>Delimita un commento che potrebbe estendersi su più righe.<br /></li><ul/>|
|<code>(&#124;...&#124;)</code>|[Criteri attivi](../active-patterns.md)|<ul><li>Delimita un criterio attivo. Chiamato anche *banana clip*.<br /></li><ul/>|
|`*`|[Operatori aritmetici](arithmetic-operators.md)<br /><br />[Tuple](../tuples.md)<br /><br />[Unità di misura](../units-of-measure.md)|<ul><li>Quando viene usato come operatore binario, moltiplica i lati sinistro e destro.<br /></li><li>Nei tipi, indica l'associazione in una tupla.<br /></li><li>Usato in unità di tipi di misura.<br /></li><ul/>|
|`*?`|[Operatori nullable](nullable-operators.md)|<ul><li>Moltiplica il lato sinistro e destro, quando il lato destro è un tipo nullable.<br /></li><ul/>|
|`**`|[Operatori aritmetici](arithmetic-operators.md)|<ul><li>Calcola l'operazione di elevamento a potenza (`x ** y` indica `x` alla potenza di `y`).<br /></li><ul/>|
|`+`|[Operatori aritmetici](arithmetic-operators.md)|<ul><li>Quando usato come operatore binario, aggiunge i lati sinistro e destro.<br /></li><li>Quando usato come operatore unario, indica una quantità positiva (formalmente, produce lo stesso valore con segno non modificato.)<br /></li><ul/>|
|`+?`|[Operatori nullable](nullable-operators.md)|<ul><li>Addiziona il lato sinistro e destro, quando il lato destro è un tipo nullable.<br /></li><ul/>|
|`,`|[Tuple](../tuples.md)|<ul><li>Separa gli elementi di una tupla o parametri di tipo.<br /></li><ul/>|
|`-`|[Operatori aritmetici](arithmetic-operators.md)|<ul><li>Quando usato come operatore binario, sottrae il lato destro dal lato sinistro.<br /></li><li>Quando usato come operatore unario, esegue un'operazione di negazione.<br /></li><ul/>|
|`-`|[Operatori nullable](nullable-operators.md)|<ul><li>Sottrae il lato destro dal lato sinistro, quando la parte destra è un tipo nullable.<br /></li><ul/>|
|`->`|[Funzioni](../functions/index.md)<br /><br />[Espressioni match](../match-expressions.md)|<ul><li>Nei tipi di funzione, delimita argomenti e valori restituiti.<br /></li><li>Produce un'espressione (nelle espressioni di sequenza); equivalente alla parola chiave `yield`.<br /></li><li>Usato nelle espressioni match<br /></li><ul/>|
|`.`|[Membri](../members/index.md)<br /><br />[Tipi primitivi](../primitive-types.md)|<ul><li>Accede a un membro e separa i singoli nomi in un nome completo.<br /></li><li>Consente di specificare un separatore decimale nei numeri a virgola mobile.<br /></li><ul/>|
|`..`|[Cicli: espressione `for...in`](../loops-for-in-expression.md)|<ul><li>Specifica un intervallo.<br /></li><ul/>|
|`.. ..`|[Cicli: espressione `for...in`](../loops-for-in-expression.md)|<ul><li>Specifica un intervallo con un incremento.<br /></li><ul/>|
|`.[...]`|[Matrici](../arrays.md)|<ul><li>Accede a un elemento di matrice.<br /></li><ul/>|
|`/`|[Operatori aritmetici](arithmetic-operators.md)<br /><br />[Unità di misura](../units-of-measure.md)|<ul><li>Divide il lato sinistro (numeratore) per il lato destro (denominatore).<br /></li><li>Usato in unità di tipi di misura.<br /></li><ul/>|
|`/?`|[Operatori nullable](nullable-operators.md)|<ul><li>Divide il lato sinistro dal lato destro, quando il lato destro è un tipo nullable.<br /></li><ul/>|
|`//`||<ul><li>Indica l'inizio di un commento a riga singola.<br /></li><ul/>|
|`///`|[Documentazione di XML](../xml-documentation.md)|<ul><li>Indica un commento XML.<br /></li><ul/>|
|`:`|[Funzioni](../functions/index.md)|<ul><li>In un'annotazione di tipo, separa un nome di parametro o membro dal relativo tipo.<br /></li><ul/>|
|`::`|[Elenchi](../lists.md)<br /><br />[Espressioni match](../match-expressions.md)|<ul><li>Crea un elenco. L'elemento sul lato sinistro viene aggiunto all'elenco sul lato destro.<br /></li><li>Usato nella corrispondenza tra modelli per separare le parti di un elenco.<br /></li><ul/>|
|`:=`|[Celle di riferimento](../reference-cells.md)|<ul><li>Assegna un valore a una cella di riferimento.<br /></li><ul/>|
|`:>`|[Cast e conversioni](../casting-and-conversions.md)|<ul><li>Converte un tipo in un tipo di livello superiore nella gerarchia.<br /></li><ul/>|
|`:?`|[Espressioni match](../match-expressions.md)|<ul><li>Restituisce `true` se il valore corrisponde al tipo specificato. In caso contrario, restituisce `false` (operatore di prova di tipo).<br /></li><ul/>|
|`:?>`|[Cast e conversioni](../casting-and-conversions.md)|<ul><li>Converte un tipo in un tipo di livello inferiore nella gerarchia.<br /></li><ul/>|
|`;`|[Sintassi dettagliata](../verbose-syntax.md)<br /><br />[Elenchi](../lists.md)<br /><br />[Record](../records.md)|<ul><li>Separa le espressioni (usate soprattutto nella sintassi dettagliata).<br /></li><li>Separa gli elementi di un elenco.<br /></li><li>Separa i campi di un record.<br /></li><ul/>|
|`<`|[Operatori aritmetici](arithmetic-operators.md)|<ul><li>Calcola l'operazione "minore di".<br /></li><ul/>|
|`<?`|[Operatori nullable](nullable-operators.md)|Calcola l'operazione "minore di", quando la parte destra è un tipo nullable.|
|`<<`|[Funzioni](../functions/index.md)|<ul><li>Compone due funzioni in ordine inverso. La seconda viene eseguita per prima (operatore di composizione inverso).<br /></li><ul/>|
|`<<<`|[Operatori bit per bit](bitwise-operators.md)|<ul><li>Sposta a sinistra i bit nella quantità sul lato sinistro indicata dal numero di bit specificato sul lato destro.<br /></li><ul/>|
|`<-`|[Valori](../values/index.md)|<ul><li>Assegna un valore a una variabile.<br /></li><ul/>|
|`<...>`|[Generalizzazione automatica](../generics/automatic-generalization.md)|<ul><li>Delimita i parametri di tipo.<br /></li><ul/>|
|`<>`|[Operatori aritmetici](arithmetic-operators.md)|<ul><li>Restituisce `true` se il lato sinistro non è uguale a quello destro; in caso contrario, restituisce false.<br /></li><ul/>|
|`<>?`|[Operatori nullable](nullable-operators.md)|<ul><li>Calcola l'operazione "diverso da" quando la parte destra è un tipo nullable.<br /></li><ul/>|
|`<=`|[Operatori aritmetici](arithmetic-operators.md)|<ul><li>Restituisce `true` se il lato sinistro è minore o uguale al lato destro; altrimenti restituisce `false`.<br /></li><ul/>|
|`<=?`|[Operatori nullable](nullable-operators.md)|<ul><li>Calcola l'operazione "minore o uguale a" quando la parte destra è un tipo nullable.<br /></li><ul/>|
|<code>&lt;&#124;</code>|[Funzioni](../functions/index.md)|<ul><li>Passa il risultato dell'espressione sul lato destro alla funzione sul lato sinistro (operatore pipe inverso).<br /></li><ul/>|
|<code>&lt;&#124;&#124;</code>|[Funzione Operators.&#40; &#60;&#124;&#124; &#41;&#60;'T1,'T2,'U&#62;](https://msdn.microsoft.com/visualfsharpdocs/conceptual/operators.%5b-%5bhh-%5d%5b%27t1%2c%27t2%2c%27u%5d-function-%5bfsharp%5d)|<ul><li>Passa la tupla di due argomenti sul lato destro alla funzione sul lato sinistro.<br /></li><ul/>|
|<code>&lt;&#124;&#124;&#124;</code>|[Funzione Operators.&#40; &#60;&#124;&#124;&#124; &#41;&#60;'T1,'T2,'T3,'U&#62;](https://msdn.microsoft.com/visualfsharpdocs/conceptual/operators.%5b-%5bhhh-%5d%5b%27t1%2c%27t2%2c%27t3%2c%27u%5d-function-%5bfsharp%5d)|<ul><li>Passa la tupla di tre argomenti sul lato destro alla funzione sul lato sinistro.<br /></li><ul/>|
|`<@...@>`|[Citazioni di codice](../code-quotations.md)|<ul><li>Delimita una citazione di codice tipizzato.<br /></li><ul/>|
|`<@@...@@>`|[Citazioni di codice](../code-quotations.md)|<ul><li>Delimita una citazione di codice non tipizzato.<br /></li><ul/>|
|`=`|[Operatori aritmetici](arithmetic-operators.md)|<ul><li>Restituisce `true` se il lato sinistro è uguale al lato destro; in caso contrario, restituisce `false`.<br /></li><ul/>|
|`=?`|[Operatori nullable](nullable-operators.md)|<ul><li>Calcola l'operazione "uguale a" quando la parte destra è un tipo nullable.<br /></li><ul/>|
|`==`|Non applicabile.|<ul><li>Non usato in F#. Usa `=` per le operazioni di uguaglianza.<br /></li><ul/>|
|`>`|[Operatori aritmetici](arithmetic-operators.md)|<ul><li>Restituisce `true` se il lato sinistro è maggiore del lato destro; in caso contrario, restituisce `false`.<br /></li><ul/>|
|`>?`|[Operatori nullable](nullable-operators.md)|<ul><li>Calcola l'operazione "maggiore di", quando la parte destra è un tipo nullable.<br /></li><ul/>|
|`>>`|[Funzioni](../functions/index.md)|<ul><li>Compone due funzioni (operatore di composizione diretto).<br /></li><ul/>|
|`>>>`|[Operatori bit per bit](bitwise-operators.md)|<ul><li>Sposta a destra i bit nella quantità sul lato sinistro indicata dal numero di posizioni specificato sul lato destro.<br /></li><ul/>|
|`>=`|[Operatori aritmetici](arithmetic-operators.md)|<ul><li>Restituisce `true` se il lato destro è maggiore o uguale al lato sinistro; in caso contrario, restituisce `false`.<br /></li><ul/>|
|`>=?`|[Operatori nullable](nullable-operators.md)|<ul><li>Calcola l'operazione "maggiore o uguale a" quando la parte destra è un tipo nullable.<br /></li><ul/>|
|`?`|[Parametri e argomenti](../parameters-and-arguments.md)|<ul><li>Specifica un argomento facoltativo.<br /></li><li>Usato come operatore per le chiamate di metodo e proprietà dinamiche. È necessario fornire un'implementazione personalizzata.<br /></li><ul/>|
|`? ... <- ...`|Non sono disponibili altre informazioni.|<ul><li>Usato come operatore per l'impostazione delle proprietà dinamiche. È necessario fornire un'implementazione personalizzata.<br /></li><ul/>|
|`?>=`, `?>`, `?<=`, `?<`, `?=`, `?<>`, `?+`, `?-`, `?*`, `?/`|[Operatori nullable](nullable-operators.md)|<ul><li>Equivalente per i corrispondenti operatori senza il prefisso ?, per cui un tipo nullable è a sinistra.<br /></li><ul/>|
|`>=?`, `>?`, `<=?`, `<?`, `=?`, `<>?`, `+?`, `-?`, `*?`, `/?`|[Operatori nullable](nullable-operators.md)|<ul><li>Equivalente per i corrispondenti operatori senza il suffisso ?, per cui un tipo nullable è a destra.<br /></li><ul/>|
|`?>=?`, `?>?`, `?<=?`, `?<?`, `?=?`, `?<>?`, `?+?`, `?-?`, `?*?`, `?/?`|[Operatori nullable](nullable-operators.md)|<ul><li>Equivalente per i corrispondenti operatori non racchiusi da punti interrogativi, dove entrambi i lati sono tipi nullable.<br /></li><ul/>|
|`@`|[Elenchi](../lists.md)<br /><br />[Stringhe](../strings.md)|<ul><li>Concatena due elenchi.<br /></li><li>Quando si trova prima di una stringa letterale, indica che la stringa deve essere interpretata alla lettera, senza interpretazione dei caratteri di escape.<br /></li><ul/>|
|`[...]`|[Elenchi](../lists.md)|<ul><li>Delimita gli elementi di un elenco.<br /></li><ul/>|
|<code>[&#124;...&#124;]</code>|[Matrici](../arrays.md)|<ul><li>Delimita gli elementi di una matrice.<br /></li><ul/>|
|`[<...>]`|[Attributi](../attributes.md)|<ul><li>Delimita un attributo.<br /></li><ul/>|
|`\`|[Stringhe](../strings.md)|<ul><li>Effettua l'escape del carattere successivo. Usato nei valori letterali di stringa e carattere.<br /></li><ul/>|
|`^`|[Parametri di tipo risolti staticamente](../generics/statically-resolved-type-parameters.md)<br /><br />[Stringhe](../strings.md)|<ul><li>Specifica i parametri di tipo che devono essere risolti in fase di compilazione, non in fase di esecuzione.<br /></li><li>Concatena le stringhe.<br /></li><ul/>|
|`^^^`|[Operatori bit per bit](bitwise-operators.md)|<ul><li>Calcola l'operazione di OR esclusivo bit per bit.<br /></li><ul/>|
|`_`|[Espressioni match](../match-expressions.md)<br /><br />[Generics](../generics/index.md)|<ul><li>Indica un modello di carattere jolly.<br /></li><li>Specifica un parametro generico anonimo.<br /></li><ul/>|
|<code>&#96;</code>|[Generalizzazione automatica](../generics/automatic-generalization.md)|<ul><li>Usato internamente per indicare un parametro di tipo generico.<br /></li><ul/>|
|`{...}`|[Sequenze](../sequences.md)<br /><br />[Record](../records.md)|<ul><li>Delimita le espressioni di sequenza e le espressioni di calcolo.<br /></li><li>Usato nelle definizioni dei record.<br /></li><ul/>|
|<code>&#124;</code>|[Espressioni match](../match-expressions.md)|<ul><li>Delimita singoli case di corrispondenza, singoli case di unione discriminata e valori di enumerazione.<br /></li><ul/>|
|<code>&#124;&#124;</code>|[Operatori booleani](boolean-operators.md)|<ul><li>Calcola l'operazione OR booleana.<br /></li><ul/>|
|<code>&#124;&#124;&#124;</code>|[Operatori bit per bit](bitwise-operators.md)|<ul><li>Calcola l'operazione OR bit per bit.<br /></li><ul/>|
|<code>&#124;></code>|[Funzioni](../functions/index.md)|<ul><li>Passa il risultato del lato sinistro alla funzione sul lato destro (operatore pipe diretto).<br /></li><ul/>|
|<code>&#124;&#124;></code>|[Funzione Operators.&#40; &#124;&#124;&#62; &#41;&#60;'T1,'T2,'U&#62;](https://msdn.microsoft.com/visualfsharpdocs/conceptual/operators.%5b-hh%5d-%5d%5b%27t1%2c%27t2%2c%27u%5d-function-%5bfsharp%5d)|<ul><li>Passa la tupla di due argomenti sul lato sinistro alla funzione sul lato destro.<br /></li><ul/>|
|<code>&#124;&#124;&#124;></code>|[Funzione Operators.&#40; &#124;&#124;&#124;&#62; &#41;&#60;'T1,'T2,'T3,'U&#62;](https://msdn.microsoft.com/visualfsharpdocs/conceptual/operators.%5b-hhh%5d-%5d%5b%27t1%2c%27t2%2c%27t3%2c%27u%5d-function-%5bfsharp%5d)|<ul><li>Passa la tupla di tre argomenti sul lato sinistro alla funzione sul lato destro.<br /></li><ul/>|
|`~~`|[Overload degli operatori](../operator-overloading.md)|<ul><li>Usato per dichiarare un overload per l'operatore di negazione unario.<br /></li><ul/>|
|`~~~`|[Operatori bit per bit](bitwise-operators.md)|<ul><li>Calcola l'operazione NOT bit per bit.<br /></li><ul/>|
|`~-`|[Overload degli operatori](../operator-overloading.md)|<ul><li>Usato per dichiarare un overload per l'operatore meno unario.<br /></li><ul/>|
|`~+`|[Overload degli operatori](../operator-overloading.md)|<ul><li>Usato per dichiarare un overload per l'operatore più unario.<br /></li><ul/>|

## <a name="operator-precedence"></a>Precedenza tra gli operatori
Nella tabella seguente viene illustrato l'ordine di precedenza degli operatori e altre parole chiave di espressioni nel linguaggio F#, in ordine dalla precedenza più bassa alla precedenza più elevata. È anche elencata l'associatività, se applicabile.

|Operatore|Associazione|
|--------|-------------|
|`as`|A destra|
|`when`|Destra|
|<code>&#124;</code> (barra verticale)|Sinistra|
|`;`|A destra|
|`let`|Non associativo|
|`function`, `fun`, `match`, `try`|Non associativo|
|`if`|Non associativo|
|`->`|A destra|
|`:=`|A destra|
|`,`|Non associativo|
|`or`, <code>&#124;&#124;</code>|Sinistra|
|`&`, `&&`|Sinistro|
|`:>`, `:?>`|Destra|
|`!=`*op*, `<`*op*, `>`*op*, `=`, <code>&#124;</code>*op*, `&`*op*, `&`<br /><br />(inclusi `<<<`, `>>>`, <code>&#124;&#124;&#124;</code>, `&&&`)|Sinistra|
|`^`*op*<br /><br />(incluso `^^^`)|Destra|
|`::`|Destra|
|`:?`|Non associativa|
|`-`*op*, `+`*op*|Si applica agli usi infissi di questi simboli|
|`*`*op*, `/`*op*, `%`*op*|Sinistra|
|`**`*op*|Destra|
|`f x` (applicazione di funzione)|Sinistra|
|<code>&#124;</code> (corrispondenza con il modello)|Destra|
|operatori di prefisso (`+`*op*, `-`*op*, `%`, `%%`, `&`, `&&`, `!`*op*, `~`*op*)|Sinistra|
|`.`|A sinistra|
|`f(x)`|Sinistra|
|`f<`*tipi*`>`|Sinistra|
F# supporta l'overload degli operatori personalizzati. Ciò significa che è possibile definire operatori personalizzati. Nella tabella precedente, *op* può essere qualsiasi sequenza valida (possibilmente vuota) di caratteri dell'operatore, predefinita o definita dall'utente. In questo modo, è possibile usare questa tabella per determinare la sequenza di caratteri da usare in modo che un operatore personalizzato raggiunga il livello di priorità desiderato. I caratteri `.` iniziali vengono ignorati quando il compilatore determina la precedenza.

## <a name="see-also"></a>Vedere anche
[Riferimenti per il linguaggio F#](../index.md)

[Overload degli operatori](../operator-overloading.md)

