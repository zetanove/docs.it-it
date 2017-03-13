---
title: "Istruzione For...Next (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Step"
  - "vb.Next"
  - "vb.To"
  - "vb.for"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "cicli infiniti"
  - "Next (parola chiave), istruzioni For...Next"
  - "For (parola chiave) [Visual Basic], istruzioni For...Next"
  - "Step (parola chiave), istruzioni For...Next"
  - "overload degli operatori, istruzione For...Next"
  - "To (parola chiave), istruzioni For...Next"
  - "cicli senza termine"
  - "cicli, senza termine"
  - "istruzioni, ripetizione"
  - "Next (istruzione), For...Next"
  - "For...Next (istruzioni)"
  - "cicli (strutture), For...Next"
  - "cicli, infiniti"
  - "Exit (istruzione), istruzioni For...Next"
  - "For (istruzione)"
ms.assetid: f5fc0d51-67ce-4c36-9f09-31c9a91c94e9
caps.latest.revision: 64
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 64
---
# Istruzione For...Next (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consentono di ripetere un gruppo di istruzioni per il numero di volte specificato.  
  
## Sintassi  
  
```  
For counter [ As datatype ] = start To end [ Step step ]  
    [ statements ]  
    [ Continue For ]  
    [ statements ]  
    [ Exit For ]  
    [ statements ]  
Next [ counter ]  
```  
  
## Parti  
  
|Parte|Descrizione|  
|-----------|-----------------|  
|`counter`|Obbligatorio nell'istruzione `For`.  Variabile numerica.  Variabile di controllo disponibile per il ciclo.  Per ulteriori informazioni, vedere [Argomento Counter](#BKMK_Counter) più avanti in questo argomento.|  
|`datatype`|Opzionale.  Tipo di dati di `counter`.  Per ulteriori informazioni, vedere [Argomento Counter](#BKMK_Counter) più avanti in questo argomento.|  
|`start`|Necessario.  Espressione numerica.  Valore iniziale di `counter`.|  
|`end`|Necessario.  Espressione numerica.  Valore finale di `counter`.|  
|`step`|Opzionale.  Espressione numerica.  Valore dell'incremento di `counter` a ogni iterazione del ciclo.|  
|`statements`|Opzionale.  Una o più istruzioni inserite tra `For` e `Next` ed eseguite per il numero di volte specificato.|  
|`Continue For`|Opzionale.  Consente di trasferire il controllo all'iterazione del ciclo successiva.|  
|`Exit For`|Opzionale.  Trasferisce il controllo all'esterno del ciclo `For`.|  
|`Next`|Necessario.  Termina la definizione del ciclo `For`.|  
  
> [!NOTE]
>  La parola chiave di `To` viene utilizzata in questa istruzione per specificare l'intervallo per il contatore.  È inoltre possibile utilizzare la parola chiave in [Select...Case Statement](../../../visual-basic/language-reference/statements/select-case-statement.md) e nelle dichiarazioni di matrice.  Per ulteriori informazioni sulle dichiarazioni di matrice, vedere [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md).  
  
## Esempi semplici  
 Utilizzare una struttura di `For`…`Next` quando si desidera riprodurre un insieme di istruzioni per il numero di volte specificato.  
  
 Nell'esempio seguente, la variabile di `index` inizia con un valore di 1 e viene incrementata a ogni iterazione del ciclo, terminando dopo che il valore di intervalli di 5. `index`.  
  
 [!code-vb[VbVbalrStatements#111](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-next-statement_1.vb)]  
  
 Nell'esempio seguente, la variabile di `number` inizia a 2 e viene ridotta di 0,25 per ogni iterazione del ciclo, terminando dopo che il valore di 0 intervalli di `number`.  L'argomento di `Step` di `-.25` ridurre il valore di 0,25 per ogni iterazione del ciclo.  
  
 [!code-vb[VbVbalrStatements#112](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-next-statement_2.vb)]  
  
> [!TIP]
>  Funzionamento di [Do...Loop Statement](../../../visual-basic/language-reference/statements/do-loop-statement.md) o di [While...End While Statement](../../../visual-basic/language-reference/statements/while-end-while-statement.md) scaturiscono quando non si conosce in anticipo quante volte per eseguire le istruzioni del ciclo.  Se invece si prevede di eseguire il ciclo per un numero specifico di volte, si consiglia di utilizzare `For`...`Next`.  Il numero di iterazioni viene definito la prima volta che si entra nel ciclo.  
  
## Cicli annidati  
 È possibile annidare cicli `For` inserendo un ciclo all'interno dell'altro.  Nell'esempio seguente vengono illustrate le strutture `For`...`Next` annidate con diversi valori di incremento.  Il ciclo esterno consente di creare una stringa per ogni iterazione del ciclo.  Nel ciclo interno, per ogni iterazione del ciclo viene ridotta una variabile del contatore di cicli.  
  
 [!code-vb[VbVbalrStatements#113](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-next-statement_3.vb)]  
  
 Quando i cicli di annidamento, ogni ciclo deve essere una variabile univoca di `counter`.  
  
 È inoltre possibile annidare strutture di controllo di tipo diverso inserendole una all'interno dell'altra.  Per ulteriori informazioni, vedere [Nested Control Structures](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md).  
  
## L'uscita per e continua per  
 L'istruzione di `Exit For` immediatamente chiude il ciclo di `For`…`Next` e il trasferisce il controllo all'istruzione che segue l'istruzione di `Next`.  
  
 Tramite l'istruzione `Continue For` il controllo viene trasferito immediatamente alla successiva iterazione del ciclo.  Per ulteriori informazioni, vedere [Continue Statement](../../../visual-basic/language-reference/statements/continue-statement.md).  
  
 Nell'esempio riportato di seguito viene illustrato l'utilizzo delle istruzioni `Continue For` e `Exit For`.  
  
 [!code-vb[VbVbalrStatements#115](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-next-statement_4.vb)]  
  
 È possibile inserire un numero illimitato di istruzioni `Exit For` in un ciclo `For`…`Next`.  Se utilizzata all'interno di cicli `For`…`Next` annidati, l'istruzione `Exit For` consente l'uscita dal ciclo più interno e il trasferimento del controllo al livello di annidamento successivo superiore.  
  
 `Exit For` viene spesso utilizzato dopo la valutazione di una determinata condizione, ad esempio in una struttura di `If`…`Then`…`Else` \).  Si potrebbe decidere di utilizzare il controllo `Exit For` per le seguenti condizioni:  
  
-   La continuazione dell'iterazione non è necessaria oppure è impossibile.  Un valore errato o una richiesta di chiusura potrebbe creare tale condizione.  
  
-   Un'istruzione di `Try`…`Catch`…`Finally` intercetta un'eccezione.  È possibile utilizzare `Exit For` alla fine del blocco `Finally`.  
  
-   È un ciclo infinito, un ciclo che esegua un grande o addirittura numero di volte infinito.  Se si rileva una simile condizione, è possibile utilizzare `Exit For` per interrompere l'esecuzione del ciclo.  Per ulteriori informazioni, vedere [Do...Loop Statement](../../../visual-basic/language-reference/statements/do-loop-statement.md).  
  
## Implementazione tecnica  
 Quando viene avviato un ciclo `For`...`Next`, in Visual Basic vengono restituiti `start`, `end` e `step`.  Visual Basic valuta questi valori solo attualmente e quindi assegnato `start` a `counter`.  Prima che il blocco di istruzioni funzioni, Visual Basic e `counter` a `end`.  Se `counter` è ancora maggiore del valore di `end` o più piccolo se `step` è negativo\), il ciclo di `For` termina e il controllo passa all'istruzione che segue l'istruzione di `Next`.  In caso contrario, il blocco di istruzioni viene eseguito.  
  
 Ogni volta che Visual Basic incontra l'istruzione `Next`, incrementa il valore di `counter` di `step` e torna all'istruzione `For`.  La variabile `counter` viene nuovamente confrontata con il valore `end` e in base al risultato viene eseguito di nuovo il blocco oppure viene effettuata l'uscita dal ciclo.  Il processo continua finché `counter` non passa `end` oppure non si raggiunge un'istruzione `Exit For`.  
  
 Il ciclo non si interrompe finché `counter` non ha passato `end`.  Se `counter` è uguale a `end`, il ciclo continua.  Il confronto che determina se eseguire il blocco è `counter` \<\=`end` se `step` è positivo e `counter` \>\= `end` se `step` è negativo.  
  
 Se si modifica il valore di `counter` mentre in un ciclo, il codice può essere più difficile da leggere e debug.  Modificando il valore di `start`, `end`, o `step` non influisce sui valori di iterazione che siano stati determinati quando il ciclo viene immesso.  
  
 Se annidate i cicli, il compilatore segnala un errore se rileva l'istruzione di `Next` di un livello di annidamento esterno prima dell'istruzione di `Next` di un livello interno.  Tuttavia, il compilatore può rilevare questo errore di sovrapposizione solo se si specifica `counter` in ogni istruzione `Next`.  
  
### Argomento step  
 Dal valore di `step`, che può essere positivo o negativo,  Questo parametro consente l'elaborazione del ciclo nella seguente tabella:  
  
|**Valore di Step**|**Il ciclo verrà eseguito se**|  
|------------------------|------------------------------------|  
|Positivo o zero|`counter` \<\= `end`|  
|Negativo|`counter` \>\= `end`|  
  
 Il valore predefinito di `step` è 1.  
  
###  <a name="BKMK_Counter"></a> Argomento Counter  
 La tabella riportata di seguito indica se `counter` definisce una nuova variabile locale limitata all'intero ciclo di `For…Next`.  Questa scelta dipende da `datatype` è presente e se `counter` è già definito.  
  
|È `datatype` presente?|`counter` è già definito?|Risultato \(se `counter` definisce una nuova variabile locale limitata all'intero ciclo di `For...Next` \)|  
|----------------------------|-------------------------------|----------------------------------------------------------------------------------------------------------------|  
|No|Sì|No, perché `counter` è già definito.  Se l'ambito di `counter` non è locale alla routine, un avviso in fase di compilazione si verifica.|  
|No|No|Sì.  Il tipo di dati viene dedotto da `start`, da `end`e da espressioni di `step`.  Per informazioni sull'inferenza del tipo, vedere [Option Infer Statement](../../../visual-basic/language-reference/statements/option-infer-statement.md) e [Local Type Inference](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).|  
|Sì|Sì|Sì, ma solo se la variabile esistente di `counter` è definita all'esterno della routine.  La variabile rimane separata.  Se l'ambito di una variabile esistente di `counter` è locale alla routine, un errore in fase di compilazione si verifica.|  
|Sì|No|Sì.|  
  
 Il tipo di dati di `counter` determina il tipo dell'iterazione, che deve essere uno dei seguenti tipi:  
  
-   Oggetto `Byte`, `SByte`, `UShort`, `Short`, `UInteger`, `Integer`, `ULong`, `Long`, `Decimal`, `Single` o `Double`.  
  
-   Enumerazione che viene dichiarata tramite un'[Enum Statement](../../../visual-basic/language-reference/statements/enum-statement.md).  
  
-   Oggetto `Object`.  
  
-   Tipo `T` che dispone dei seguenti operatori, dove `B` è un tipo che può essere utilizzato in un'espressione `Boolean`.  
  
     `Public Shared Operator >= (op1 As T, op2 As T) As B`  
  
     `Public Shared Operator <= (op1 As T, op2 As T) As B`  
  
     `Public Shared Operator - (op1 As T, op2 As T) As T`  
  
     `Public Shared Operator + (op1 As T, op2 As T) As T`  
  
 È possibile specificare la variabile di `counter` nell'istruzione di `Next`.  Questa sintassi consente di migliorare la leggibilità del programma, specialmente se sono presenti cicli annidati di di `For`.  È necessario specificare la variabile visualizzato nell'istruzione corrispondente di `For`.  
  
 Tramite le espressioni `start`, `end` e `step` è possibile restituire qualsiasi tipo di dati ampliabile al tipo di `counter`.  Se si utilizza un tipo definito per `counter`, potrebbe essere necessario definire l'operatore di conversione di `CType` per convertire i tipi di `start`, di `end`, o di `step` al tipo di `counter`.  
  
## Esempio  
 Nell'esempio seguente vengono rimossi tutti gli elementi da un elenco generico.  Anziché [Istruzione For Each...Next](../../../visual-basic/language-reference/statements/for-each-next-statement.md), nell'esempio viene illustrata un'istruzione di `For`…`Next` che scorre in ordine decrescente.  L'esempio utilizza questa tecnica perché il metodo di `removeAt` determina gli elementi dopo l'elemento rimosso a un valore di indice più basso.  
  
 [!code-vb[VbVbalrStatements#114](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-next-statement_5.vb)]  
  
## Esempio  
 L'esempio seguente consente di scorrere un'enumerazione che viene dichiarata utilizzando [Enum Statement](../../../visual-basic/language-reference/statements/enum-statement.md).  
  
 [!code-vb[VbVbalrStatements#116](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-next-statement_6.vb)]  
  
## Esempio  
 Nell'esempio seguente, la classe dei parametri dell'istruzione dispone di overload degli operatori per gli operatori `+`, `-`, `>=` e `<=`.  
  
 [!code-vb[VbVbalrStatements#117](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-next-statement_7.vb)]  
  
## Vedere anche  
 <xref:System.Collections.Generic.List%601>   
 [Loop Structures](../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [While...End While Statement](../../../visual-basic/language-reference/statements/while-end-while-statement.md)   
 [Do...Loop Statement](../../../visual-basic/language-reference/statements/do-loop-statement.md)   
 [Nested Control Structures](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Exit Statement](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [Raccolte](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)