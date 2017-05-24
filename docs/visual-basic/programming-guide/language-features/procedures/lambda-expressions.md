---
title: Le espressioni lambda (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.LambdaFunction
dev_langs:
- VB
helpviewer_keywords:
- functions [Visual Basic], lambda expressions
- lambda expressions [Visual Basic]
- expressions [Visual Basic], lambda
- inline functions [Visual Basic]
ms.assetid: 137064b0-3928-4bfa-ba71-c3f9cbd951e2
caps.latest.revision: 52
author: dotnet-bot
ms.author: dotnetcontent
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e50593e76afecfe8807c3cb5bac479245d2feaef
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="lambda-expressions-visual-basic"></a>Espressioni lambda (Visual Basic)
Oggetto *espressione lambda* è una funzione o subroutine senza nome, che può essere utilizzato ovunque sia valido un delegato. Le espressioni lambda possono essere funzioni o subroutine e possono essere a riga singola o multiriga. È possibile passare valori dall'ambito corrente in un'espressione lambda.  
  
> [!NOTE]
>  Il `RemoveHandler` istruzione è un'eccezione. Non è possibile passare un'espressione lambda in per il parametro del delegato `RemoveHandler`.  
  
 Per creare espressioni lambda, utilizzare il `Function` o `Sub` (parola chiave), come se si crea una subroutine o una funzione standard. Tuttavia, le espressioni lambda sono inclusi in un'istruzione.  
  
 Nell'esempio seguente è un'espressione lambda che incrementa il proprio argomento e restituisce il valore. L'esempio mostra sia la sintassi delle espressioni lambda a riga singola e a più righe per una funzione.  
  
 [!code-vb[VbVbalrLambdas&#14;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_1.vb)]  
  
 Nell'esempio seguente è un'espressione lambda che scrive un valore nella console. L'esempio mostra sia la sintassi delle espressioni lambda a riga singola e a più righe di una subroutine.  
  
 [!code-vb[VbVbalrLambdas&#15;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_2.vb)]  
  
 Si noti che, negli esempi precedenti le espressioni lambda vengono assegnate un nome di variabile. Quando si fa riferimento alla variabile, richiamare l'espressione lambda. È anche possibile dichiarare e richiamare un'espressione lambda nello stesso momento, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrLambdas n.&3;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_3.vb)]  
  
 Un'espressione lambda può essere restituita come valore di una chiamata di funzione (come illustrato nell'esempio di [contesto](#context) sezione più avanti in questo argomento), o passato come argomento a un parametro che accetta un tipo delegato, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrLambdas n.&8;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_4.vb)]  
  
## <a name="lambda-expression-syntax"></a>Sintassi delle espressioni lambda  
 La sintassi di un'espressione lambda è simile a quello di una subroutine o una funzione standard. Le differenze sono come segue:  
  
-   Un'espressione lambda non ha un nome.  
  
-   Espressioni lambda non possono avere modificatori, ad esempio `Overloads` o `Overrides`.  
  
-   Le funzioni lambda a riga singola non utilizzano un `As` clausola per definire il tipo restituito. Al contrario, il tipo viene dedotto dal valore che restituisce il corpo dell'espressione lambda. Ad esempio, se il corpo dell'espressione lambda è `cust.City = "London"`, il tipo restituito `Boolean`.  
  
-   Nelle funzioni lambda su più righe, è possibile specificare un tipo restituito tramite un `As` clausola, oppure omettere il `As` clausola in modo che il tipo restituito viene dedotto. Quando il `As` clausola viene omessa per una funzione lambda su più righe, il tipo restituito viene considerato il tipo dominante da tutti i `Return` istruzioni nella funzione lambda su più righe. Il *tipo dominante* è un tipo univoco che possono ampliarsi tutti gli altri tipi. Se non è possibile determinare il tipo univoco, il tipo dominante è il tipo univoco possono restringersi tutti gli altri tipi nella matrice. Se nessuno di questi tipi univoci può essere determinato, il tipo dominante è `Object`. In questo caso, se `Option Strict` è impostato su `On`, si verifica un errore del compilatore.  
  
     Ad esempio, se le espressioni fornite per la `Return` istruzione contengono valori di tipo `Integer`, `Long`, e `Double`, la matrice risultante è di tipo `Double`. Entrambi `Integer` e `Long` ampliarsi `Double` e solo `Double`. `Double` è pertanto il tipo dominante. Per ulteriori informazioni, vedere [conversioni di ampliamento e restrizione](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md).  
  
-   Il corpo di una funzione a riga singola deve essere un'espressione che restituisce un valore, non un'istruzione. Non esiste alcun `Return` istruzione per le funzioni a riga singola. Il valore restituito dalla funzione a riga singola è il valore dell'espressione nel corpo della funzione.  
  
-   Il corpo di una subroutine a riga singola deve essere a riga singola istruzione.  
  
-   Funzioni a riga singola e le subroutine non includono un `End Function` o `End Sub` istruzione.  
  
-   È possibile specificare il tipo di dati di un parametro di espressione lambda con il `As` parola chiave o il tipo di dati del parametro può essere dedotto. Tutti i parametri devono avere specificato deve essere dedotto, tipi di dati o tutti.  
  
-   `Optional`e `Paramarray` i parametri non sono consentiti.  
  
-   Parametri generici non sono consentiti.  
  
## <a name="async-lambdas"></a>Espressioni lambda asincrone  
 È possibile creare con facilità le espressioni lambda e le istruzioni che includono l'elaborazione asincrona utilizzando il [Async](../../../../visual-basic/language-reference/modifiers/async.md) e [operatore Await](../../../../visual-basic/language-reference/operators/await-operator.md) parole chiave. Nell'esempio seguente di Windows Form è presente un gestore eventi che chiama e attende un metodo asincrono, `ExampleMethodAsync`.  
  
```vb  
Public Class Form1  
  
    Async Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click  
        ' ExampleMethodAsync returns a Task.  
        Await ExampleMethodAsync()  
        TextBox1.Text = vbCrLf & "Control returned to button1_Click."  
    End Sub  
  
    Async Function ExampleMethodAsync() As Task  
        ' The following line simulates a task-returning asynchronous process.  
        Await Task.Delay(1000)  
    End Function  
  
End Class  
```  
  
 È possibile aggiungere lo stesso gestore eventi utilizzando un'espressione lambda asincrona in un [AddHandler (istruzione)](../../../../visual-basic/language-reference/statements/addhandler-statement.md). Per aggiungere il gestore, aggiungere un modificatore `Async` prima dell'elenco di parametri lambda, come illustrato di seguito.  
  
```vb  
Public Class Form1  
  
    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load  
        AddHandler Button1.Click,   
            Async Sub(sender1, e1)  
                ' ExampleMethodAsync returns a Task.  
                Await ExampleMethodAsync()  
                TextBox1.Text = vbCrLf & "Control returned to Button1_ Click."  
            End Sub  
    End Sub  
  
    Async Function ExampleMethodAsync() As Task  
        ' The following line simulates a task-returning asynchronous process.  
        Await Task.Delay(1000)  
    End Function  
  
End Class  
```  
  
 Per ulteriori informazioni su come creare e utilizzare i metodi asincroni, vedere [la programmazione asincrona con Async e Await](../../../../visual-basic/programming-guide/concepts/async/index.md).  
  
##  <a name="context"></a>Contesto  
 Un'espressione lambda condivide il contesto con l'ambito entro il quale è definito. Include gli stessi diritti di accesso di qualsiasi codice scritto nell'ambito che lo contiene. Ciò include l'accesso a variabili membro, funzioni e subroutine, `Me`e i parametri e variabili locali all'interno dell'ambito contenitore.  
  
 Accesso alle variabili locali e i parametri nell'ambito che lo contiene può estendersi oltre la durata di tale ambito. Come un delegato che fa riferimento a un'espressione lambda non è disponibile a garbage collection, l'accesso alle variabili nell'ambiente originale viene mantenuto. Nell'esempio seguente, variabile `target` locale `makeTheGame`, il metodo in cui l'espressione lambda `playTheGame` è definito. Si noti che l'espressione lambda restituita, assegnata a `takeAGuess` in `Main`, può ancora accedere alla variabile locale `target`.  
  
 [!code-vb[VbVbalrLambdas&#12;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_5.vb)]  
  
 Nell'esempio seguente viene illustrato l'ampia gamma di diritti di accesso dell'espressione lambda annidata. Quando viene eseguita l'espressione lambda restituita da `Main` come `aDel`, accede a questi elementi:  
  
-   Un campo della classe in cui è definito:`aField`  
  
-   Una proprietà della classe in cui è definito:`aProp`  
  
-   Un parametro di metodo `functionWithNestedLambda`, in cui è definito:`level1`  
  
-   Una variabile locale di `functionWithNestedLambda`:`localVar`  
  
-   Un parametro dell'espressione lambda in cui è annidato:`level2`  
  
 [!code-vb[9 VbVbalrLambdas](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_6.vb)]  
  
## <a name="converting-to-a-delegate-type"></a>La conversione in un tipo delegato  
 Un'espressione lambda può essere convertita in modo implicito in un tipo delegato compatibile. Per informazioni sui requisiti generali per la compatibilità, vedere [conversione di tipo Relaxed del delegato](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md). Ad esempio, il codice seguente viene illustrata un'espressione lambda che converte in modo implicito in `Func(Of Integer, Boolean)` o una firma del delegato corrispondente.  
  
 [!code-vb[VbVbalrLambdas&#16;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_7.vb)]  
  
 Esempio di codice seguente viene illustrata un'espressione lambda che converte in modo implicito in `Sub(Of Double, String, Double)` o una firma del delegato corrispondente.  
  
 [!code-vb[VbVbalrLambdas&#23;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_8.vb)]  
  
 Quando si assegnano espressioni lambda ai delegati o passati come argomenti alle procedure, è possibile specificare i nomi di parametro ma omettere i tipi di dati, consentire i tipi di essere eseguite dal delegato.  
  
## <a name="examples"></a>Esempi  
  
-   Nell'esempio seguente viene definita un'espressione lambda che restituisce `True` se l'argomento nullable ha un valore assegnato e `False` se il valore è `Nothing`.  
  
     [!code-vb[VbVbalrLambdas n.&4;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_9.vb)]  
  
-   Nell'esempio seguente viene definita un'espressione lambda che restituisce l'indice dell'ultimo elemento in una matrice.  
  
     [!code-vb[VbVbalrLambdas n.&5;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_10.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Delegati](../../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [Istruzione Function](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub (istruzione)](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Tipi di valore nullable](../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)   
 [Procedura: passare una routine a un'altra routine in Visual Basic](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)   
 [Procedura: creare un'espressione Lambda](./how-to-create-a-lambda-expression.md)   
 [Conversione di tipo relaxed del delegato](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)

