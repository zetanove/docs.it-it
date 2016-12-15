---
title: "Istruzione For Each...Next (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.ForEach"
  - "vb.ForEachNext"
  - "vb.Each"
  - "ForEachNext"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "cicli infiniti"
  - "Next (istruzione), For Each...Next"
  - "cicli senza termine"
  - "cicli (strutture), For Each...Next"
  - "cicli, senza termine"
  - "Each (parola chiave)"
  - "istruzioni, ripetizione"
  - "For Each (istruzioni)"
  - "raccolte, ripetizione di istruzioni"
  - "cicli, infiniti"
  - "istruzioni For Each...Next"
  - "For (parola chiave) [Visual Basic], istruzioni For Each...Next"
  - "Exit (istruzione), istruzioni For Each...Next"
  - "iterazione"
ms.assetid: ebce3120-95c3-42b1-b70b-fa7da40c75e2
caps.latest.revision: 56
caps.handback.revision: 56
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Istruzione For Each...Next (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consentono di ripetere un gruppo di istruzioni per ciascun elemento di una raccolta.  
  
## Sintassi  
  
```  
For Each element [ As datatype ] In group  
    [ statements ]  
    [ Continue For ]  
    [ statements ]  
    [ Exit For ]  
    [ statements ]  
Next [ element ]  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`element`|Obbligatorio nell'istruzione `For Each`.  Facoltativa nell'istruzione `Next`.  Variabile.  Utilizzata per scorrere gli elementi della raccolta.|  
|`datatype`|Obbligatorio se `element` non è già dichiarato.  Tipo di dati di `element`.|  
|`group`|Necessario.  Una variabile con un tipo che è un tipo di raccolta o un oggetto.  Fa riferimento alla raccolta sulla quale devono essere ripetute le `statements`.|  
|`statements`|Opzionale.  Una o più istruzioni tra `For Each` e `Next` che vengono eseguite su ciascun elemento incluso in `group`.|  
|`Continue For`|Opzionale.  Trasferisce il controllo all'inizio del ciclo `For Each`.|  
|`Exit For`|Opzionale.  Trasferisce il controllo all'esterno del ciclo `For Each`.|  
|`Next`|Necessario.  Termina la definizione del ciclo `For Each`.|  
  
## Esempio semplice  
 Utilizzare un ciclo `For Each`...`Next` quando si desidera ripetere un set di istruzioni per ciascun elemento di una raccolta o di una matrice.  
  
> [!TIP]
>  Con l'istruzione [Istruzione For...Next](../../../visual-basic/language-reference/statements/for-next-statement.md) è consigliabile associare ciascuna iterazione di un ciclo a una variabile di controllo e definire i valori iniziale e finale di tale variabile.  Tuttavia, quando si utilizzano di una raccolta, il concetto di valori iniziali e finali non è significativo e non si conosce il numero di elementi della raccolta dispone.  In questo tipo di evento, un ciclo di `For Each`…`Next` è spesso una scelta migliore.  
  
 Nell'esempio seguente, l'istruzione di `For Each`…`Next` scorrere tutti gli elementi di una raccolta di elenchi.  
  
 [!code-vb[VbVbalrStatements#121](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_1.vb)]  
  
 Per ulteriori esempi, vedere [Raccolte](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md) e [Matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
## Cicli annidati  
 È possibile annidare cicli `For Each` inserendo un ciclo all'interno dell'altro.  
  
 Nell'esempio seguente vengono illustrate delle strutture `For Each`…`Next` annidate.  
  
 [!code-vb[VbVbalrStatements#122](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_2.vb)]  
  
 Quando annidate cicli, ogni ciclo deve avere una variabile univoca di `element`.  
  
 È inoltre possibile annidare strutture di controllo di tipo diverso inserendole una all'interno dell'altra.  Per ulteriori informazioni, vedere [Nested Control Structures](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md).  
  
## L'uscita per e continua per  
 L'esecuzione di cause dell'istruzione [Per uscita](../../../visual-basic/language-reference/statements/exit-statement.md) per uscire dal ciclo di `For`…`Next` e il trasferisce il controllo all'istruzione che segue l'istruzione di `Next`.  
  
 Tramite l'istruzione `Continue For` il controllo viene trasferito immediatamente alla successiva iterazione del ciclo.  Per ulteriori informazioni, vedere [Continue Statement](../../../visual-basic/language-reference/statements/continue-statement.md).  
  
 Nell'esempio riportato di seguito viene illustrato come utilizzare le istruzioni `Continue For` e `Exit For`.  
  
 [!code-vb[VbVbalrStatements#123](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_3.vb)]  
  
 È possibile inserire un numero illimitato di istruzioni `Exit For` in un ciclo `For Each`.  Se utilizzata all'interno di cicli `For Each` annidati, l'istruzione `Exit For` consente l'uscita dal ciclo più interno e il trasferimento del controllo al livello di annidamento successivo superiore.  
  
 L'istruzione `Exit For` spesso viene utilizzata dopo la valutazione di una determinata condizione, ad esempio in una struttura `If`...`Then`...`Else`.  Si potrebbe decidere di utilizzare il controllo `Exit For` per le seguenti condizioni:  
  
-   La continuazione dell'iterazione non è necessaria oppure è impossibile.  Tale condizione potrebbe essere causata da un valore erroneo o da una richiesta di terminazione.  
  
-   Eccezione intercettata in un blocco `Try`...`Catch`...`Finally`.  È possibile utilizzare `Exit For` alla fine del blocco `Finally`.  
  
-   È presente un ciclo infinito, vale a dire un ciclo che può essere eseguito molte volte oppure all'infinito.  Se si rileva una simile condizione, è possibile utilizzare `Exit For` per interrompere l'esecuzione del ciclo.  Per ulteriori informazioni, vedere [Do...Loop Statement](../../../visual-basic/language-reference/statements/do-loop-statement.md).  
  
## Iteratori  
 Utilizzare *un iteratore* per eseguire un'iterazione personalizzata in una raccolta.  Un iteratore può essere una funzione o una funzione di accesso di `Get`.  Utilizza un'istruzione di `Yield` per restituire ogni elemento della raccolta uno alla volta.  
  
 Chiama un iteratore utilizzando un'istruzione di `For Each...Next`.  Ogni iterazione del ciclo `For Each` chiama l'iteratore.  Quando un'istruzione di `Yield` viene raggiunto l'iteratore, l'espressione nell'istruzione di `Yield` e viene restituita la posizione corrente nel codice vengono mantenute.  Alla successiva chiamata dell'iteratore, l'esecuzione verrà riavviata a partire da quella posizione.  
  
 Nell'esempio viene utilizzata una funzione di iteratore.  La funzione di iteratore ha un'istruzione di `Yield` presente in un ciclo di [Per… next](../../../visual-basic/language-reference/statements/for-next-statement.md).  Nel metodo di `ListEvenNumbers`, ogni iterazione del corpo dell'istruzione `For Each` crea una chiamata alla funzione di iteratore, che consente alla successiva istruzione di `Yield`.  
  
 [!code-vb[VbVbalrStatements#127](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_4.vb)]  
  
 Per ulteriori informazioni, vedere [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md), [Istruzione Yield](../../../visual-basic/language-reference/statements/yield-statement.md) e [Iterator](../../../visual-basic/language-reference/modifiers/iterator.md).  
  
## Implementazione tecnica  
 Quando un'istruzione di `For Each`…`Next` viene eseguita, Visual Basic valuta la raccolta solo una volta, prima che inizi il ciclo.  Se il blocco di istruzioni modifica `element` o `group`, tali modifiche non influiscono sull'iterazione del ciclo.  
  
 Dopo che tutti gli elementi della raccolta sono stati assegnati a `element`, il ciclo `For Each` si arresta e il controllo passa all'istruzione successiva all'istruzione `Next`.  
  
 Se `element` non è stato dichiarato fuori del ciclo, è necessario dichiararlo nell'istruzione di `For Each`.  È possibile dichiarare in modo esplicito il tipo dell'oggetto `element` tramite un'istruzione `As` oppure è possibile basarsi sull'inferenza dei tipi per assegnare il tipo.  In entrambi i casi, l'ambito dell'oggetto `element` è il corpo del ciclo.  Non è tuttavia possibile dichiarare `element` all'interno e all'esterno del ciclo.  
  
 Se lo si desidera, è possibile specificare `element` nell'istruzione `Next`.  Ciò consente di migliorare la leggibilità del programma, soprattutto se i cicli `For Each` sono annidati.  È necessario specificare la stessa variabile presente nell'istruzione `For Each` corrispondente.  
  
 Si potrebbe decidere di evitare di modificare il valore di `element` all'interno di un ciclo.  Tale operazione può rendere più difficile la lettura e il debug del codice.  Modificare il valore di `group` non influisce sulla raccolta o i relativi elementi, che siano stati determinati quando il ciclo viene immesso.  
  
 Quando si cicli di annidamento, se un'istruzione di `Next` di un livello di annidamento esterno viene visualizzato prima di `Next` di un livello interno, viene segnalato un errore.  Tuttavia, il compilatore può rilevare questo errore di sovrapposizione solo se si specifica `element` in ogni istruzione `Next`.  
  
 Se il codice dipende da scorrere una raccolta in un determinato ordine, un ciclo di `For Each`…`Next` non è la scelta ideale, a meno che non si conosca che le caratteristiche dell'oggetto enumerator essa esposte.  L'ordine di scorrimento non è determinato da Visual Basic, ma con il metodo di <xref:System.Collections.IEnumerator.MoveNext%2A> dell'oggetto enumerator.  Pertanto, potrebbe non essere possibile prevedere quale elemento della raccolta verrà restituito per primo in `element` o quale sarà l'elemento restituito dopo un determinato elemento.  È possibile ottenere risultati più affidabili utilizzando un struttura di ciclo diversa, ad esempio `For`...`Next` o `Do`...`Loop`..  
  
 Per i dati di tipo `element` è necessario specificare un tipo di dati in cui possa essere convertito il tipo di dati degli elementi di `group`.  
  
 Il tipo di dati di `group` deve essere un tipo di riferimento che fa riferimento a una raccolta o a una matrice che è enumerabile.  Nella maggior parte dei casi, ciò significa che `group` fa riferimento a un oggetto che implementa l'interfaccia <xref:System.Collections.IEnumerable> dello spazio dei nomi `System.Collections` oppure l'interfaccia <xref:System.Collections.Generic.IEnumerable%601> dello spazio dei nomi `System.Collections.Generic`.  `System.Collections.IEnumerable` definisce il metodo <xref:System.Collections.IEnumerable.GetEnumerator%2A>, il quale restituisce un oggetto enumeratore per la raccolta.  L'oggetto enumeratore implementa l'interfaccia `System.Collections.IEnumerator` dello spazio dei nomi `System.Collections` ed espone la proprietà <xref:System.Collections.IEnumerator.Current%2A> e i metodi <xref:System.Collections.IEnumerator.Reset%2A> e <xref:System.Collections.IEnumerator.MoveNext%2A> che verranno utilizzati per scorrere la raccolta.  
  
### Conversioni di restrizione  
 Quando l'oggetto `Option Strict` è impostato su `On`, le conversioni verso un tipo di dati più piccolo causano solitamente errori del compilatore.  In un'istruzione `For Each`, tuttavia, le conversioni dagli elementi nell'oggetto `group` all'oggetto `element` vengono valutate ed eseguite in fase di esecuzione e gli errori del compilatore causati da conversioni verso un tipo di dati più piccolo vengono eliminati.  
  
 Nell'esempio seguente, l'assegnazione di `m` come valore iniziale per `n` non viene compilato quando `Option Strict` si trova in quanto la conversione di `Long` a `Integer` è una conversione verso un tipo di dati più piccolo.  Nell'istruzione `For Each`, tuttavia, non viene segnalato alcun errore del compilatore, sebbene per l'assegnazione a `number` sia richiesta la stessa conversione da `Long` a `Integer`.  Nell'istruzione `For Each` in cui è contenuto un numero grande, si verifica un errore di run\-time quando il metodo <xref:Microsoft.VisualBasic.CompilerServices.Conversions.ToInteger%2A> viene applicato al numero grande.  
  
 [!code-vb[VbVbalrStatements#89](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_5.vb)]  
  
### Chiamate IEnumerator  
 All'avvio dell'esecuzione di un ciclo `For Each`...`Next`, in Visual Basic viene verificato che `group` faccia riferimento a un oggetto Collection valido.  In caso negativo, verrà generata un'eccezione.  In caso affermativo, vengono chiamati il metodo <xref:System.Collections.IEnumerator.MoveNext%2A> e la proprietà <xref:System.Collections.IEnumerator.Current%2A> dell'oggetto enumeratore per restituire il primo elemento.  Se tramite il metodo `MoveNext` viene indicato che non sono disponibili altri elementi, vale a dire che la raccolta è vuota, il ciclo `For Each` viene arrestato e il controllo passa all'istruzione successiva all'istruzione `Next`.  Altrimenti, `element` viene impostato sul primo elemento, quindi viene eseguito il blocco di istruzioni.  
  
 Ogni volta che rileva l'istruzione `Next`, Visual Basic torna all'istruzione `For Each`.  Vengono chiamati nuovamente il metodo `MoveNext` e la proprietà `Current` per restituire l'elemento successivo, quindi, in base al risultato, viene eseguito il blocco oppure viene arrestato il ciclo.  Questo processo continua finché il metodo `MoveNext` indica che non esistono altri elementi oppure finché non viene rilevata un'istruzione `Exit For`.  
  
 **Modifica della raccolta.** L'oggetto restituito da enumeratore <xref:System.Collections.IEnumerable.GetEnumerator%2A> in genere non consente di modificare la libreria aggiunta, eliminazione, sostituendo, o riordinando elementi.  Se si modifica la raccolta dopo aver iniziato un ciclo `For Each`...`Next`, l'oggetto enumeratore diventa non valido e con il tentativo successivo di accedere a un elemento si causa un'eccezione <xref:System.InvalidOperationException>.  
  
 Tuttavia, questo blocco di modifica non è determinato da [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], ma dall'implementazione dell'interfaccia di <xref:System.Collections.IEnumerable>.  È possibile implementare `IEnumerable` in modo da consentire le modifiche durante l'iterazione.  Se si intende eseguire tale modifica dinamica, accertarsi di avere un'adeguata conoscenza delle caratteristiche dell'implementazione di `IEnumerable` nella raccolta utilizzata.  
  
 **Modifica degli elementi di una raccolta.** La proprietà <xref:System.Collections.IEnumerator.Current%2A> dell'oggetto enumeratore è [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md) e restituisce una copia locale di ogni elemento della raccolta.  Pertanto non sarà possibile modificare gli elementi stessi in un ciclo `For Each`...`Next`.  Qualsiasi modifica apportata alle ha effetto solo sulla copia locale di `Current` e non vengono riflessi nella raccolta sottostante.  Se tuttavia un elemento è un tipo di riferimento, sarà possibile modificare i membri dell'istanza a cui esso punta.  Nell'esempio seguente viene modificato il membro di `BackColor` di ogni elemento di `thisControl`.  Non è possibile, tuttavia, modificare `thisControl` stesso.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 Nell'esempio precedente è possibile modificare il membro `BackColor` di ciascun elemento `thisControl` ma non è possibile modificare l'elemento `thisControl` stesso.  
  
 **Attraversamento di matrici.** Poiché la classe <xref:System.Array> implementa l'interfaccia <xref:System.Collections.IEnumerable>, tutte le matrici espongono il metodo <xref:System.Array.GetEnumerator%2A>.  Pertanto è possibile scorrere una matrice con un ciclo `For Each`...`Next`.  Tuttavia, gli elementi della matrice possono essere solo letti.  Non è possibile modificarli.  
  
## Esempio  
 Nell'esempio seguente vengono elencate tutte le cartelle nella directory C:\\ tramite la classe <xref:System.IO.DirectoryInfo>.  
  
 [!code-vb[VbVbalrStatements#124](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_6.vb)]  
  
## Esempio  
 Nell'esempio seguente viene illustrata una routine di ordinamento della raccolta.  Le istanze di base di esempio `Car` classe archiviate in <xref:System.Collections.Generic.List%601>.  La classe `Car` implementa l'interfaccia <xref:System.IComparable%601>, che richiede che il metodo <xref:System.IComparable%601.CompareTo%2A> venga implementato.  
  
 Ogni chiamata al metodo di <xref:System.IComparable%601.CompareTo%2A> effettua un'unica confronto utilizzato per l'ordinamento.  Il codice utente nel metodo `CompareTo` restituisce un valore per ogni confronto dell'oggetto corrente con un altro oggetto.  Il valore restituito è minore di zero se l'oggetto corrente è inferiore all'altro oggetto, maggiore di zero se l'oggetto corrente è superiore all'altro oggetto e zero se sono uguali.  Ciò consente di definire in codifica i criteri per maggiore di, minore di e il segno di uguale.  
  
 Nel metodo `ListCars`, l'istruzione `cars.Sort()` ordina l'elenco.  Questa chiamata al metodo <xref:System.Collections.Generic.List%601.Sort%2A> <xref:System.Collections.Generic.List%601> modo il metodo `CompareTo` venga chiamata automaticamente per gli oggetti `Car` in `List`.  
  
 [!code-vb[VbVbalrStatements#125](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_7.vb)]  
  
## Vedere anche  
 [Raccolte](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)   
 [Istruzione For...Next](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Loop Structures](../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [While...End While Statement](../../../visual-basic/language-reference/statements/while-end-while-statement.md)   
 [Do...Loop Statement](../../../visual-basic/language-reference/statements/do-loop-statement.md)   
 [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [Object Initializers: Named and Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [Collection Initializers](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)   
 [Matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md)