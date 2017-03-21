---
title: Funzione Statement (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Function
dev_langs:
- VB
helpviewer_keywords:
- procedures, creating
- Function procedures, Function statement syntax
- functions [Visual Basic], function procedures
- ParamArray keyword, Function statements
- Private keyword, Function statements
- declarations, procedures
- procedures, declaration
- Public keyword, in Function statement
- ByVal keyword, Function statements
- procedures, recursive
- Implements keyword, Function statements
- procedures, returning values
- Exit statement, in Function procedures
- recursive procedures
- As keyword, in Function statement
- Optional keyword, Function statements
- Function statement
- Visual Basic code, Function procedures
- procedures, function
- ByRef keyword, Function statements
- Friend keyword, Function statements
- End keyword, Function statements
- Handles keyword, Function statements
ms.assetid: a4497077-0f46-4ede-a27f-9e8670df52b9
caps.latest.revision: 62
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: af87477f81fab8406d726ebc8c81260b371d71c8
ms.lasthandoff: 03/13/2017

---
# <a name="function-statement-visual-basic"></a>Istruzione Function (Visual Basic)
Dichiara il nome, parametri e il codice che definiscono un `Function` procedura.  
  
## <a name="syntax"></a>Sintassi  
  
```  
[ <attributelist> ] [ accessmodifier ] [ proceduremodifiers ] [ Shared ] [ Shadows ] [ Async | Iterator ]  
Function name [ (Of typeparamlist) ] [ (parameterlist) ] [ As returntype ] [ Implements implementslist | Handles eventlist ]  
    [ statements ]  
    [ Exit Function ]  
    [ statements ]  
End Function  
```  
  
## <a name="parts"></a>Parti  
  
-   `attributelist`  
  
     Facoltativo. Vedere [elenco attributi](attribute-list.md).  
  
-   `accessmodifier`  
  
     Facoltativo. Può essere uno dei seguenti:  
  
    -   [Public](../../../visual-basic/language-reference/modifiers/public.md)  
  
    -   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)  
  
    -   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
    -   [Private](../../../visual-basic/language-reference/modifiers/private.md)  
  
    -   `Protected Friend`  
  
     Vedere [livelli in Visual Basic di accesso](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
-   `proceduremodifiers`  
  
     Facoltativo. Può essere uno dei seguenti:  
  
    -   [Overload](../../../visual-basic/language-reference/modifiers/overloads.md)  
  
    -   [Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)  
  
    -   [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)  
  
    -   [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)  
  
    -   [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)  
  
    -   `MustOverride Overrides`  
  
    -   `NotOverridable Overrides`  
  
-   `Shared`  
  
     Facoltativo. Vedere [condivisi](../../../visual-basic/language-reference/modifiers/shared.md).  
  
-   `Shadows`  
  
     Facoltativo. Vedere [ombreggiature](../../../visual-basic/language-reference/modifiers/shadows.md).  
  
-   `Async`  
  
     Facoltativo. Vedere [Async](../../../visual-basic/language-reference/modifiers/async.md).  
  
-   `Iterator`  
  
     Facoltativo. Vedere [iteratore](../../../visual-basic/language-reference/modifiers/iterator.md).  
  
-   `name`  
  
     Obbligatorio. Nome della routine. Vedere [dichiarati i nomi degli elementi](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
-   `typeparamlist`  
  
     Facoltativo. Elenco di parametri di tipo per una procedura generica. Vedere [digitare elenco](type-list.md).  
  
-   `parameterlist`  
  
     Facoltativo. Elenco di nomi di variabili locali che rappresentano i parametri di questa procedura. Vedere [elenco parametri](parameter-list.md).  
  
-   `returntype`  
  
     Obbligatorio se `Option Strict` è `On`. Tipo di dati del valore restituito da questa procedura.  
  
-   `Implements`  
  
     Facoltativo. Indica che questa procedura viene implementato uno o più `Function` procedure, ognuna definita in un'interfaccia implementata dalla classe o struttura che contiene questa procedura. Vedere [implementa istruzione](implements-statement.md).  
  
-   `implementslist`  
  
     Necessario se si fornisce `Implements`. Elenco delle routine `Function` implementate.  
  
     `implementedprocedure [ , implementedprocedure ... ]`  
  
     Ogni `implementedprocedure` presenta la sintassi e le parti seguenti:  
  
     `interface.definedname`  
  
    |Parte|Descrizione|  
    |---|---|  
    |`interface`|Obbligatorio. Nome di un'interfaccia implementata da questa procedura contenente classe o struttura.|  
    |`definedname`|Obbligatorio. Nome mediante il quale la routine viene definita in `interface`.|  
  
-   `Handles`  
  
     Facoltativo. Indica che questa procedura può gestire uno o più eventi specifici. Vedere [gestisce](handles-clause.md).  
  
-   `eventlist`  
  
     Necessario se si fornisce `Handles`. Elenco di eventi gestiti dalla routine.  
  
     `eventspecifier [ , eventspecifier ... ]`  
  
     Ogni `eventspecifier` presenta la sintassi e le parti seguenti:  
  
     `eventvariable.event`  
  
    |Parte|Descrizione|  
    |---|---|  
    |`eventvariable`|Obbligatorio. Variabile oggetto dichiarata con il tipo di dati della classe o struttura che genera l'evento.|  
    |`event`|Obbligatorio. Nome dell'evento gestito dalla routine.|  
  
-   `statements`  
  
     Facoltativo. Blocco di istruzioni da eseguire all'interno di questa procedura.  
  
-   `End Function`  
  
     Termina la definizione di questa procedura.  
  
## <a name="remarks"></a>Note  
 Tutto il codice eseguibile deve essere all'interno di una routine. Ogni procedura, a sua volta, viene dichiarata all'interno di una classe, una struttura o un modulo che viene definito la classe, struttura o un modulo che lo contiene.  
  
 Per restituire un valore al codice chiamante, utilizzare un `Function` procedura; in caso contrario, utilizzare un `Sub` procedura.  
  
## <a name="defining-a-function"></a>Definizione di una funzione  
 È possibile definire un `Function` procedura solo a livello di modulo. Pertanto, il contesto della dichiarazione per una funzione deve essere una classe, una struttura, un modulo o un'interfaccia e non può essere un file di origine, uno spazio dei nomi, una routine o un blocco. Per ulteriori informazioni, vedere [contesti delle dichiarazioni e livelli di accesso predefinito](declaration-contexts-and-default-access-levels.md).  
  
 `Function`Per impostazione predefinita le procedure per l'accesso pubblico. È possibile regolare i livelli di accesso con i modificatori di accesso.  
  
 Oggetto `Function` routine consente di dichiarare il tipo di dati del valore che restituisce la procedura. È possibile specificare qualsiasi tipo di dati o il nome di un'enumerazione, una struttura, una classe o un'interfaccia. Se non si specifica il `returntype` , la procedura restituisce `Object`.  
  
 Se la routine utilizza il `Implements` (parola chiave), classe o struttura deve inoltre disporre un `Implements` istruzione che segue immediatamente il `Class` o `Structure` istruzione. Il `Implements` istruzione deve includere ogni interfaccia specificata in `implementslist`. Tuttavia, il nome con cui si definisce un'interfaccia di `Function` (in `definedname`) non deve corrispondere al nome di questa procedura (in `name`).  
  
> [!NOTE]
>  È possibile utilizzare espressioni lambda per definire espressioni di funzione inline. Per ulteriori informazioni, vedere [espressione di funzione](../../../visual-basic/language-reference/operators/function-expression.md) e [le espressioni Lambda](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
## <a name="returning-from-a-function"></a>Restituzione da una funzione  
 Quando il `Function` procedure restituisce al codice chiamante, l'esecuzione continua con l'istruzione che segue l'istruzione che ha chiamato la routine.  
  
 Per restituire un valore di una funzione, è possibile assegnare il valore per il nome della funzione o includerlo in un `Return` istruzione.  
  
 Il `Return` istruzione contemporaneamente assegna il valore restituito ed esce dalla funzione, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrStatements&#24;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/function-statement_1.vb)]  
  
 Nell'esempio seguente assegna il valore restituito per il nome della funzione `myFunction` e quindi utilizza il `Exit Function` istruzione per la restituzione.  
  
 [!code-vb[VbVbalrStatements&#23;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/function-statement_2.vb)]  
  
 Il `Exit Function` e `Return` istruzioni uscire immediatamente da un `Function` procedura. Un numero qualsiasi di `Exit Function` e `Return` istruzioni possono trovarsi in qualsiasi punto della procedura, ed è possibile combinare `Exit Function` e `Return` istruzioni.  
  
 Se si utilizza `Exit Function` senza assegnare un valore a `name`, la procedura restituisce il valore predefinito per il tipo di dati specificato in `returntype`. Se `returntype` non è specificato, la stored procedure restituisce `Nothing`, ovvero il valore predefinito per `Object`.  
  
## <a name="calling-a-function"></a>Chiamata di una funzione  
 Si chiama un `Function` procedure utilizzando il nome, seguito dall'elenco di argomenti racchiuso tra parentesi, in un'espressione. È possibile omettere le parentesi solo se non si specificano argomenti. Tuttavia, il codice è più leggibile se si includono sempre le parentesi.  
  
 Si chiama un `Function` procedura simile a quello di chiamare qualsiasi libreria funzione, ad esempio `Sqrt`, `Cos`, o `ChrW`.  
  
 È inoltre possibile chiamare una funzione utilizzando il `Call` (parola chiave). In tal caso, il valore restituito viene ignorato. Utilizzare il `Call` (parola chiave) non è consigliata nella maggior parte dei casi. Per ulteriori informazioni, vedere [istruzione Call](call-statement.md).  
  
 Visual Basic vengono a volte riorganizzate espressioni aritmetiche per aumentare l'efficienza interna. Per questo motivo, è consigliabile utilizzare un `Function` procedure in un'espressione aritmetica se la funzione modifica il valore delle variabili nella stessa espressione.  
  
## <a name="async-functions"></a>Funzioni asincrone  
 Il *Async* funzionalità consente di richiamare le funzioni asincrone senza utilizzare callback esplicito o suddividere manualmente il codice in più funzioni o espressioni lambda.  
  
 Se si contrassegna una funzione con la [Async](../../../visual-basic/language-reference/modifiers/async.md) modificatore, è possibile utilizzare il [Await](../../../visual-basic/language-reference/operators/await-operator.md) operatore della funzione. Quando il controllo raggiunge un `Await` espressione il `Async` funzione, il controllo ritorna al chiamante e lo stato di avanzamento nella funzione viene sospesa fino al completamento dell'attività di attesa. Una volta completata l'attività, è possibile riprendere esecuzione nella funzione.  
  
> [!NOTE]
>  Un `Async` procedura restituisce al chiamante quando rileva il primo oggetto atteso che non è ancora completo o raggiunge la fine della `Async` procedura, qualunque si verifichi prima.  
  
 Un `Async` funzione può avere un tipo restituito <xref:System.Threading.Tasks.Task%601>o <xref:System.Threading.Tasks.Task>.</xref:System.Threading.Tasks.Task> </xref:System.Threading.Tasks.Task%601> Un esempio di un `Async` funzione che dispone di un tipo restituito di <xref:System.Threading.Tasks.Task%601>viene fornito di seguito.</xref:System.Threading.Tasks.Task%601>  
  
 Un `Async` funzione non può dichiarare [ByRef](../../../visual-basic/language-reference/modifiers/byref.md) parametri.  
  
 Oggetto [Sub (istruzione)](sub-statement.md) può anche essere contrassegnato con il `Async` modificatore. Viene utilizzato principalmente per i gestori eventi, in cui non può essere restituito un valore. Un `Async``Sub` procedura non può essere atteso e il chiamante di un `Async``Sub` procedura non può intercettare le eccezioni generate dalla `Sub` procedura.  
  
 Per ulteriori informazioni su `Async` funzioni, vedere [la programmazione asincrona con Async e Await](../../../visual-basic/programming-guide/concepts/async/index.md), [flusso di controllo in programmi asincroni](../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md), e [Async restituire tipi](../../../visual-basic/programming-guide/concepts/async/async-return-types.md).  
  
## <a name="iterator-functions"></a>Funzioni di iteratore  
 Un *iteratore* funzione esegue un'iterazione personalizzata su una raccolta, ad esempio un elenco o una matrice. Utilizza una funzione iteratore di [Yield](yield-statement.md) istruzione per restituire un elemento alla volta. Quando un [Yield](yield-statement.md) viene raggiunta l'istruzione, viene memorizzata la posizione corrente nel codice. L'esecuzione viene riavviata da quella posizione la volta successiva che viene chiamata la funzione iteratore.  
  
 Un iteratore viene chiamato dal codice client utilizzando un [For Each... Avanti](for-each-next-statement.md) istruzione.  
  
 Il tipo restituito di una funzione iteratore può essere <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator>, o <xref:System.Collections.Generic.IEnumerator%601>.</xref:System.Collections.Generic.IEnumerator%601> </xref:System.Collections.IEnumerator> </xref:System.Collections.Generic.IEnumerable%601> </xref:System.Collections.IEnumerable>  
  
 Per altre informazioni, vedere [Iteratori](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la `Function` istruzione per dichiarare il nome, parametri e il codice che formano il corpo di un `Function` procedura. Il `ParamArray` modificatore consente alla funzione di accettare un numero variabile di argomenti.  
  
 [!code-vb[VbVbalrStatements&#25;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/function-statement_3.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente richiama la funzione dichiarata nell'esempio precedente.  
  
 [!code-vb[&#26; VbVbalrStatements](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/function-statement_4.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente, `DelayAsync` è un `Async``Function` che presenta un tipo restituito di <xref:System.Threading.Tasks.Task%601>.</xref:System.Threading.Tasks.Task%601> `DelayAsync` ha un'istruzione `Return` che restituisce un numero intero. Pertanto la dichiarazione della funzione di `DelayAsync` deve avere un tipo restituito di `Task(Of Integer)`. Poiché il tipo restituito è `Task(Of Integer)`, la valutazione di `Await` espressione `DoSomethingAsync` produce un numero intero. Questa funzionalità viene illustrata questa istruzione: `Dim result As Integer = Await delayTask`.  
  
 Il `startButton_Click` procedura è un esempio di un `Async Sub` procedura. Poiché `DoSomethingAsync` è un `Async` (funzione), l'attività per la chiamata a `DoSomethingAsync` deve essere atteso, come illustrato di seguito l'istruzione seguente: `Await DoSomethingAsync()`. Il `startButton_Click``Sub` procedura deve essere definita con la `Async` modificatore perché contiene un `Await` espressione.  
  
 [!code-vb[csAsyncMethod n.&1;](../../../csharp/programming-guide/classes-and-structs/codesnippet/VisualBasic/function-statement_5.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Sub (istruzione)](sub-statement.md)   
 [Routine di funzione](../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Elenco di parametri](parameter-list.md)   
 [Dim (istruzione)](dim-statement.md)   
 [Istruzione Call](call-statement.md)   
 [Of](of-clause.md)   
 [Matrici di parametri](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [Procedura: utilizzare una classe generica](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)   
 [Le procedure di risoluzione](../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [Espressioni lambda](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [Espressione di funzione](../../../visual-basic/language-reference/operators/function-expression.md)
