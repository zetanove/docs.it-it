---
title: Per ogni corso... Istruzione successiva (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.ForEach
- vb.ForEachNext
- vb.Each
- ForEachNext
dev_langs:
- VB
helpviewer_keywords:
- infinite loops
- Next statement, For Each...Next
- endless loops
- loop structures, For Each...Next
- loops, endless
- Each keyword
- instructions, repeating
- For Each statement
- collections, instruction repetition
- loops, infinite
- For Each...Next statements
- For keyword [Visual Basic], For Each...Next statements
- Exit statement, For Each...Next statements
- iteration
ms.assetid: ebce3120-95c3-42b1-b70b-fa7da40c75e2
caps.latest.revision: 56
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e0173877fa4a57da76fd774d70ce63d2beda23ad
ms.lasthandoff: 03/13/2017

---
# <a name="for-eachnext-statement-visual-basic"></a>Istruzione For Each...Next (Visual Basic)
Ripete un gruppo di istruzioni per ogni elemento in una raccolta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
For Each element [ As datatype ] In group  
    [ statements ]  
    [ Continue For ]  
    [ statements ]  
    [ Exit For ]  
    [ statements ]  
Next [ element ]  
```  
  
## <a name="parts"></a>Parti  
  
|Termine|Definizione|  
|---|---|  
|`element`|Obbligatorio nel `For Each` istruzione. Facoltativo nel `Next` istruzione. Variabile. Utilizzato per scorrere gli elementi della raccolta.|  
|`datatype`|Obbligatorio se `element` non è già stato dichiarato. Tipo di dati di `element`.|  
|`group`|Obbligatorio. Una variabile con un tipo che è un tipo di raccolta o un oggetto. Fa riferimento alla raccolta in cui il `statements` devono essere ripetute.|  
|`statements`|Facoltativo. Uno o più istruzioni tra `For Each` e `Next` eseguiti su ogni elemento `group`.|  
|`Continue For`|Facoltativo. Trasferisce il controllo all'inizio di `For Each` ciclo.|  
|`Exit For`|Facoltativo. Trasferisce il controllo fuori il `For Each` ciclo.|  
|`Next`|Obbligatorio. Termina la definizione di `For Each` ciclo.|  
  
## <a name="simple-example"></a>Esempio semplice  
 Use a `For Each`... `Next` ciclo quando si desidera ripetere un set di istruzioni per ogni elemento di una raccolta o una matrice.  
  
> [!TIP]
>  A [For... Istruzione successiva](../../../visual-basic/language-reference/statements/for-next-statement.md) funziona bene quando è possibile associare ogni iterazione di un ciclo a una variabile di controllo e determinare i valori iniziale e finale della variabile. Tuttavia, quando si utilizzano una raccolta, il concetto di valori iniziale e finale non è significativo e non necessariamente conoscere quanti elementi disponibili. In tal caso, un `For Each`... `Next` ciclo è spesso una scelta migliore.  
  
 Nell'esempio seguente, il `For Each`...`Next` istruzione scorre tutti gli elementi di una raccolta di elenco.  
  
 [!code-vb[VbVbalrStatements&#121;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_1.vb)]  
  
 Per ulteriori esempi, vedere [raccolte](http://msdn.microsoft.com/library/e76533a9-5033-4a0b-b003-9c2be60d185b) e [matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
## <a name="nested-loops"></a>Nested Loops  
 È possibile annidare `For Each` cicli inserendo un ciclo all'interno di un altro.  
  
 Nell'esempio seguente viene nidificata `For Each`...`Next` strutture.  
  
 [!code-vb[VbVbalrStatements&#122;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_2.vb)]  
  
 Quando si annida cicli, ogni ciclo deve essere associato un unico `element` variabile.  
  
 È inoltre possibile annidare tipi diversi di strutture di controllo all'interno di altro. Per ulteriori informazioni, vedere [strutture di controllo nidificate](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md).  
  
## <a name="exit-for-and-continue-for"></a>Per uscire e continua per  
 Il [Exit For](../../../visual-basic/language-reference/statements/exit-statement.md) causa l'esecuzione uscire dall'istruzione di `For`...`Next` ciclo e trasferisce il controllo all'istruzione che segue il `Next` istruzione.  
  
 Il `Continue For` istruzione trasferisce il controllo immediatamente all'iterazione successiva del ciclo. Per ulteriori informazioni, vedere [istruzione Continue](../../../visual-basic/language-reference/statements/continue-statement.md).  
  
 Nell'esempio seguente viene illustrato come utilizzare il `Continue For` e `Exit For` istruzioni.  
  
 [!code-vb[123 VbVbalrStatements](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_3.vb)]  
  
 È possibile inserire un numero qualsiasi di `Exit For` istruzioni in un `For Each` ciclo. Se utilizzato all'interno di cicli `For Each` cicli, `Exit For` di chiudere il controllo più interno di ciclo e i trasferimenti al successivo livello superiore di nidificazione dell'esecuzione.  
  
 `Exit For`viene spesso utilizzata dopo una versione di valutazione di una determinata condizione, ad esempio, in un `If`... `Then`... `Else` struttura. È consigliabile utilizzare `Exit For` per le condizioni seguenti:  
  
-   Continuando a eseguire l'iterazione è necessaria o impossibile. Ciò potrebbe dipendere da un valore errato o una richiesta di terminazione.  
  
-   Viene generata un'eccezione un `Try`... `Catch`... `Finally`. È possibile utilizzare `Exit For` alla fine del `Finally` blocco.  
  
-   Esiste un ciclo infinito, ovvero un ciclo che potrebbe essere eseguito un numero elevato o persino infinito di volte. Se si rileva questa condizione, è possibile utilizzare `Exit For` per interrompere il ciclo. Per ulteriori informazioni, vedere [si... Istruzione di ciclo](../../../visual-basic/language-reference/statements/do-loop-statement.md).  
  
## <a name="iterators"></a>Iteratori  
 Si utilizza un *iteratore* per eseguire un'iterazione personalizzata su una raccolta. Un iteratore può essere una funzione o un `Get` della funzione di accesso. Viene utilizzato un `Yield` istruzione per la restituzione di ogni elemento della raccolta uno alla volta.  
  
 Viene chiamato un iteratore utilizzando un `For Each...Next` istruzione. Ogni iterazione del `For Each` ciclo chiama l'iteratore. Quando un `Yield` nell'iteratore, l'espressione viene raggiunta l'istruzione di `Yield` istruzione viene restituita, e viene mantenuta la posizione corrente nel codice. L'esecuzione viene ripresa a partire da quella posizione la volta successiva che viene chiamato l'iteratore.  
  
 Nell'esempio seguente viene utilizzata una funzione iteratore. La funzione iteratore dispone di un `Yield` istruzione all'interno di un [per... Avanti](../../../visual-basic/language-reference/statements/for-next-statement.md) ciclo. Nel `ListEvenNumbers` (metodo), ogni iterazione del `For Each` corpo dell'istruzione crea una chiamata alla funzione iteratore, che procede alla successiva `Yield` istruzione.  
  
 [!code-vb[127 VbVbalrStatements](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_4.vb)]  
  
 Per ulteriori informazioni, vedere [iteratori](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7), [istruzione Yield](../../../visual-basic/language-reference/statements/yield-statement.md), e [iteratore](../../../visual-basic/language-reference/modifiers/iterator.md).  
  
## <a name="technical-implementation"></a>Implementazione tecnica  
 Quando un `For Each`...`Next` istruzione viene eseguita, Visual Basic restituisce solo una volta, prima viene avviato il ciclo di raccolta. Se il blocco di istruzioni `element` o `group`, queste modifiche non influiscono sull'iterazione del ciclo.  
  
 Quando tutti gli elementi nella raccolta sono stati assegnati a `element`, `For Each` ciclo si interrompe e il controllo passa all'istruzione che segue il `Next` istruzione.  
  
 Se `element` non è stata dichiarata all'esterno di questo ciclo, è necessario dichiararla nel `For Each` istruzione. È possibile dichiarare il tipo di `element` in modo esplicito utilizzando un `As` istruzione oppure è possibile basarsi sull'inferenza per assegnare il tipo. In entrambi i casi, l'ambito di `element` è il corpo del ciclo. Tuttavia, non è possibile dichiarare `element` all'esterno e all'interno del ciclo.  
  
 È possibile specificare facoltativamente `element` nel `Next` istruzione. Per migliorare la leggibilità del programma, soprattutto se sono presenti annidati `For Each` cicli. È necessario specificare la stessa variabile come quella visualizzata corrispondenti `For Each` istruzione.  
  
 È possibile evitare di modificare il valore di `element` all'interno di un ciclo. Questa operazione può rendere più difficile da leggere e il debug del codice. Modifica del valore di `group` non influenza la raccolta o i relativi elementi, quali sono stati definiti durante il ciclo è stato immesso prima.  
  
 Quando si sono cicli nidificati, se un `Next` viene rilevata un'istruzione di un livello di annidamento esterno prima di `Next` di un livello interno, il compilatore segnala un errore. Tuttavia, il compilatore può rilevare questo errore di sovrapposizione solo se si specifica `element` in ogni `Next` istruzione.  
  
 Se il codice dipende dall'attraversamento di una raccolta in un ordine particolare, un `For Each`... `Next` ciclo non è la scelta migliore, a meno che non si conoscano le caratteristiche dell'oggetto enumeratore esposto dall'insieme. L'ordine di attraversamento non è determinato da Visual Basic, ma dal <xref:System.Collections.IEnumerator.MoveNext%2A>metodo dell'oggetto enumeratore.</xref:System.Collections.IEnumerator.MoveNext%2A> Pertanto, potrebbe essere in grado di prevedere quale elemento della raccolta è il primo a essere restituiti in `element`, o che è in attesa di essere restituito dopo un determinato elemento. È possibile ottenere risultati più affidabili utilizzando una struttura di ciclo diversa, ad esempio `For`... `Next` or `Do`... `Loop`.  
  
 Il tipo di dati `element` deve essere in modo che il tipo di dati degli elementi di `group` può essere convertito a esso.  
  
 Tipo di dati di `group` deve essere un tipo di riferimento che fa riferimento a una raccolta o una matrice che è enumerabile. In genere ciò significa che `group` fa riferimento a un oggetto che implementa il <xref:System.Collections.IEnumerable>interfaccia della `System.Collections` dello spazio dei nomi o <xref:System.Collections.Generic.IEnumerable%601>interfaccia del `System.Collections.Generic` dello spazio dei nomi.</xref:System.Collections.Generic.IEnumerable%601> </xref:System.Collections.IEnumerable> `System.Collections.IEnumerable`definisce il <xref:System.Collections.IEnumerable.GetEnumerator%2A>metodo, che restituisce un oggetto enumeratore per la raccolta.</xref:System.Collections.IEnumerable.GetEnumerator%2A> L'oggetto enumeratore implementa il `System.Collections.IEnumerator` interfaccia del `System.Collections` dello spazio dei nomi ed espone il <xref:System.Collections.IEnumerator.Current%2A>proprietà e il <xref:System.Collections.IEnumerator.Reset%2A>e <xref:System.Collections.IEnumerator.MoveNext%2A>metodi.</xref:System.Collections.IEnumerator.MoveNext%2A> </xref:System.Collections.IEnumerator.Reset%2A> </xref:System.Collections.IEnumerator.Current%2A> Visual Basic utilizzati per scorrere la raccolta.  
  
### <a name="narrowing-conversions"></a>Conversioni verso un tipo di dati più piccolo  
 Quando `Option Strict` è impostato su `On`, le conversioni causano in genere gli errori del compilatore. In un `For Each` istruzione, tuttavia, le conversioni da elementi di `group` a `element` vengono valutate ed eseguite in fase di esecuzione, mentre vengono eliminati gli errori del compilatore causati da conversioni di restrizione.  
  
 Nell'esempio seguente, l'assegnazione di `m` come valore iniziale per `n` non viene compilato quando `Option Strict` si trova in quanto la conversione di un `Long` per un `Integer` è una conversione di restrizione. Nel `For Each` istruzione, tuttavia, nessun errore del compilatore è segnalato, anche se l'assegnazione al `number` richiede la stessa conversione da `Long` a `Integer`. Nel `For Each` si verifica un errore di run-time di istruzione che contiene un numero elevato, quando <xref:Microsoft.VisualBasic.CompilerServices.Conversions.ToInteger%2A>viene applicato per il numero di grandi dimensioni.</xref:Microsoft.VisualBasic.CompilerServices.Conversions.ToInteger%2A>  
  
 [!code-vb[VbVbalrStatements&#89;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_5.vb)]  
  
### <a name="ienumerator-calls"></a>Chiamate di IEnumerator  
 Quando l'esecuzione di un `For Each`... `Next` ciclo viene avviato, viene verificato che `group` fa riferimento a un oggetto collection valido. In caso contrario viene generata un'eccezione. In caso contrario, chiama il <xref:System.Collections.IEnumerator.MoveNext%2A>(metodo) e <xref:System.Collections.IEnumerator.Current%2A>proprietà dell'oggetto enumeratore per restituire il primo elemento.</xref:System.Collections.IEnumerator.Current%2A> </xref:System.Collections.IEnumerator.MoveNext%2A> Se `MoveNext` non indica che è presente alcun elemento successivo, ovvero, se la raccolta è vuota, il `For Each` ciclo si interrompe e il controllo passa all'istruzione che segue il `Next` istruzione. In caso contrario, Visual Basic imposta `element` il primo elemento e viene eseguito il blocco di istruzioni.  
  
 Ogni volta che Visual Basic rileva il `Next` istruzione restituisce il `For Each` istruzione. Chiama nuovamente `MoveNext` e `Current` per restituire l'elemento successivo e anche in questo caso, viene eseguito il blocco oppure viene arrestato il ciclo in base al risultato. Questo processo continua fino a `MoveNext` non indica che è presente alcun elemento successivo o `Exit For` viene rilevata un'istruzione.  
  
 **Modifica della raccolta.** L'oggetto enumeratore restituito da <xref:System.Collections.IEnumerable.GetEnumerator%2A>in genere non è possibile modificare la raccolta mediante l'aggiunta, eliminazione, sostituzione o il riordino di elementi.</xref:System.Collections.IEnumerable.GetEnumerator%2A> Se si modifica la raccolta dopo aver iniziato un `For Each`... `Next` ciclo, l'oggetto enumeratore viene invalidato e al successivo tentativo di accedere a un elemento comporta un <xref:System.InvalidOperationException>(eccezione).</xref:System.InvalidOperationException>  
  
 Tuttavia, il blocco delle modifiche non è determinato dalla [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], ma piuttosto dall'implementazione del <xref:System.Collections.IEnumerable>interfaccia.</xref:System.Collections.IEnumerable> È possibile implementare `IEnumerable` in modo che le modifiche durante l'iterazione. Se si prevede di eseguire tale modifica dinamica, assicurarsi di comprendere le caratteristiche del `IEnumerable` implementazione per la raccolta in uso.  
  
 **Modifica di elementi della raccolta.** Il <xref:System.Collections.IEnumerator.Current%2A>è di proprietà dell'oggetto enumeratore [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md), e restituisce una copia locale di ogni elemento della raccolta.</xref:System.Collections.IEnumerator.Current%2A> Ciò significa che non è possibile modificare gli elementi in un `For Each`... `Next` loop. Le eventuali modifiche apportate influenzano solo la copia locale di `Current` e non sono riflesse nell'insieme sottostante. Tuttavia, se un elemento è un tipo di riferimento, è possibile modificare i membri dell'istanza a cui fa riferimento. Nell'esempio seguente viene modificato il `BackColor` membro di ogni `thisControl` elemento. Tuttavia, non è possibile, modificare `thisControl` stesso.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 Nell'esempio precedente è possibile modificare il `BackColor` membro di ogni `thisControl` elemento, è possibile modificare `thisControl` stesso.  
  
 **Attraversamento di matrici.** Poiché il <xref:System.Array>implementa il <xref:System.Collections.IEnumerable>interfaccia, tutte le matrici espongono il <xref:System.Array.GetEnumerator%2A>(metodo).</xref:System.Array.GetEnumerator%2A> </xref:System.Collections.IEnumerable> </xref:System.Array> Ciò significa che è possibile scorrere una matrice con un `For Each`... `Next` loop. Tuttavia, è possibile leggere solo gli elementi della matrice. È possibile modificarle.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono elencate tutte le cartelle nella directory c:\. utilizzando la <xref:System.IO.DirectoryInfo>classe.</xref:System.IO.DirectoryInfo>  
  
 [!code-vb[VbVbalrStatements&#124;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_6.vb)]  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra una procedura per ordinare una raccolta. Nell'esempio consente di ordinare le istanze di un `Car` (classe) che vengono archiviati in un <xref:System.Collections.Generic.List%601>.</xref:System.Collections.Generic.List%601> Il `Car` implementa il <xref:System.IComparable%601>interfaccia, che è necessario che il <xref:System.IComparable%601.CompareTo%2A>metodo essere implementato.</xref:System.IComparable%601.CompareTo%2A> </xref:System.IComparable%601>  
  
 Ogni chiamata al <xref:System.IComparable%601.CompareTo%2A>metodo effettua un confronto singolo che viene utilizzato per l'ordinamento.</xref:System.IComparable%601.CompareTo%2A> Codice scritto dall'utente di `CompareTo` il metodo restituisce un valore per ogni confronto dell'oggetto corrente con un altro oggetto. Il valore restituito è minore di zero se l'oggetto corrente è inferiore all'altro oggetto, maggiore di zero se l'oggetto corrente è superiore all'altro oggetto e zero se sono uguali. In questo modo è possibile definire nel codice i criteri di maggiore, minore e uguale.  
  
 Nel `ListCars` (metodo), il `cars.Sort()` istruzione Ordina l'elenco. Questa chiamata al <xref:System.Collections.Generic.List%601.Sort%2A>metodo il <xref:System.Collections.Generic.List%601>fa sì che il `CompareTo` metodo da chiamare automaticamente per il `Car` gli oggetti il `List`.</xref:System.Collections.Generic.List%601> </xref:System.Collections.Generic.List%601.Sort%2A>  
  
 [!code-vb[&#125; VbVbalrStatements](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_7.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolte](http://msdn.microsoft.com/library/e76533a9-5033-4a0b-b003-9c2be60d185b)   
 [For... Next (istruzione)](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Cicli (strutture)](../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [While... End While (istruzione)](../../../visual-basic/language-reference/statements/while-end-while-statement.md)   
 [Eseguire l'operazione... Istruzione di ciclo](../../../visual-basic/language-reference/statements/do-loop-statement.md)   
 [Ampliamento e restrizione conversioni](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [Inizializzatori di oggetto: Tipi denominati e anonimi](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [Inizializzatori di insieme](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)   
 [Matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md)
