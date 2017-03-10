---
title: "Lambda Expressions (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.LambdaFunction"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "functions [Visual Basic], lambda expressions"
  - "lambda expressions [Visual Basic]"
  - "expressions [Visual Basic], lambda"
  - "inline functions [Visual Basic]"
ms.assetid: 137064b0-3928-4bfa-ba71-c3f9cbd951e2
caps.latest.revision: 52
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 52
---
# Lambda Expressions (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un'*espressione lambda* è una funzione o subroutine senza nome che può essere utilizzata ovunque sia valido un delegato.  Le espressioni lambda possono essere funzioni o subroutine e possono trovarsi su una riga singola o su più righe.  È possibile passare valori dall'ambito corrente a un'espressione lambda.  
  
> [!NOTE]
>  Fa eccezione l''istruzione `RemoveHandler`.  Non è possibile passare un'espressione lambda in per il parametro del delegato di `RemoveHandler`.  
  
 È possibile creare espressioni lambda utilizzando la parola chiave `Function` o `Sub`, nello stesso modo in cui si crea una subroutine o una funzione standard.  Le espressioni lambda sono tuttavia incluse in un'istruzione.  
  
 Nell'esempio seguente viene illustrata un'espressione lambda che incrementa il proprio argomento e restituisce il valore.  Nell'esempio viene illustrata la sintassi delle espressioni lambda sia su una riga singola che su più righe per una funzione.  
  
 [!code-vb[VbVbalrLambdas#14](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class1.vb#14)]  
  
 Nell'esempio seguente viene illustrata un'espressione lambda che scrive un valore nella console.  Nell'esempio viene illustrata la sintassi delle espressioni lambda sia su una riga singola che su più righe per una subroutine.  
  
 [!code-vb[VbVbalrLambdas#15](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class1.vb#15)]  
  
 Si noti che negli esempi precedenti alle espressioni lambda è assegnato un nome di variabile.  Quando si fa riferimento alla variabile, si richiama l'espressione lambda.  È anche possibile dichiarare e richiamare contemporaneamente un'espressione lambda, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrLambdas#3](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class1.vb#3)]  
  
 Un'espressione lambda può essere restituita come valore di una chiamata di funzione \(come illustrato nell'esempio nella sezione [Contesto](#context) più avanti in questo argomento\) o passata come argomento a un parametro che accetta un tipo di delegato, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrLambdas#8](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class2.vb#8)]  
  
## Sintassi delle espressioni lambda  
 La sintassi di un'espressione lambda è simile a quella di una subroutine o di una funzione standard.  Le differenze sono le seguenti.  
  
-   Un'espressione lambda non possiede un nome.  
  
-   Le espressioni lambda non possono avere modificatori, ad esempio `Overloads` o `Overrides`.  
  
-   Le funzioni lambda su una riga singola non utilizzano una clausola `As` per designare il tipo restituito.  Invece, il tipo viene dedotto dal valore calcolato dal corpo dell'espressione lambda .  Ad esempio, se il corpo dell'espressione lambda è `cust.City = "London"`, il relativo tipo restituito è `Boolean`.  
  
-   Nelle funzioni lambda su più righe è possibile specificare un tipo restituito tramite una clausola `As` oppure omettere la clausola `As` in modo che il tipo restituito venga dedotto.  Quando la clausola `As` viene omessa per una funzione lambda su più righe, il tipo restituito viene dedotto come tipo dominante in tutte le istruzioni `Return` nella funzione lambda su più righe.  Il  *tipo dominante* è un tipo univoco allargare a tutti gli altri tipi.  Se questo tipo univoco non può essere determinato, il tipo dominante è il tipo univoco in cui possono restringersi tutti gli altri tipi nella matrice.  Se nessuno di questi tipi univoci può essere determinato, il tipo dominante è `Object`.  In questo caso, se `Option Strict` viene impostato su `On`, si verifica un errore del compilatore.  
  
     Ad esempio, se le espressioni fornito per la `Return` istruzione contengono i valori di tipo `Integer`, `Long`, e `Double`, la matrice risultante è di tipo `Double`.  Sia `Integer` che `Long` possono ampliarsi nel tipo `Double` e solo `Double`.  `Double` è pertanto il tipo dominante.  Per ulteriori informazioni, vedere [Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md).  
  
-   Il corpo di una funzione su una riga singola deve essere un'espressione che restituisce un valore e non un'istruzione.  Non vi è alcuna istruzione `Return` per le funzioni su una riga singola.  Il valore restituito dalla funzione su una riga singola è il valore dell'espressione nel corpo della funzione.  
  
-   Il corpo di una subroutine su una riga singola deve essere un'istruzione su una riga singola.  
  
-   Le funzioni e le subroutine su una riga singola non includono un'istruzione `End Function` o `End Sub`.  
  
-   È possibile specificare il tipo di dati di un parametro dell'espressione lambda utilizzando la parola chiave `As` oppure il tipo di dati del parametro può essere dedotto.  Tutti i parametri devono avere tipi di dati specificati oppure tutti devono essere dedotti.  
  
-   I parametri `Optional` e `Paramarray` non sono consentiti.  
  
-   Non sono permessi parametri generici.  
  
## Funzioni lambda Async  
 È possibile creare espressioni lambda e istruzioni che includono l'elaborazione asincrona utilizzando il [Async](../../../../visual-basic/language-reference/modifiers/async.md) e [Await Operator](../../../../visual-basic/language-reference/operators/await-operator.md) le parole chiave.  Ad esempio, nell'esempio di Windows Form contiene un gestore eventi che chiama e in attesa di un metodo asincrono, `ExampleMethodAsync`.  
  
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
  
 È possibile aggiungere lo stesso gestore eventi tramite una lambda asincrono in un [AddHandler Statement](../../../../visual-basic/language-reference/statements/addhandler-statement.md).  Per aggiungere questo gestore, aggiungere un `Async` modificatore prima l'elenco dei parametri lambda, come illustrato nell'esempio riportato di seguito.  
  
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
  
 Per ulteriori informazioni su come creare e utilizzare i metodi asincroni, vedere [Programmazione asincrona con Async e Await](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md).  
  
##  <a name="context"></a> Contesto  
 Un'espressione lambda condivide il contesto con l'ambito in cui è definita.  Dispone degli stessi diritti di accesso di qualsiasi codice scritto nell'ambito che la contiene.  È incluso l'accesso a variabili membro, funzioni e subroutine, `Me` e parametri e variabili locali nell'ambito che la contiene.  
  
 L'accesso a parametri e variabili locali nell'ambito che la contiene può essere esteso oltre la durata di tale ambito.  Finché un delegato che fa riferimento a un'espressione lambda non viene reso disponibile per la Garbage Collection, viene mantenuto l'accesso alle variabili nell'ambiente originale.  Nell'esempio seguente, la variabile `target` è locale per `makeTheGame`, il metodo nel quale viene definita l'espressione lambda `playTheGame`.  Si noti che l'espressione lambda restituita, assegnata a `takeAGuess` in `Main`, dispone ancora dell'accesso alla variabile locale `target`.  
  
 [!code-vb[VbVbalrLambdas#12](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class6.vb#12)]  
  
 Nell'esempio seguente viene illustrata l'ampia gamma di autorizzazioni di accesso dell'espressione lambda annidata.  Quando l'espressione lambda restituita viene eseguita da `Main` come `aDel`, accede a questi elementi:  
  
-   Un campo della classe in cui viene definito: `aField`  
  
-   Una proprietà della classe in cui viene definito: `aProp`  
  
-   Un parametro del metodo `functionWithNestedLambda` nel quale è definito: `level1`  
  
-   Una variabile locale di `functionWithNestedLambda`: `localVar`  
  
-   Un parametro dell'espressione lambda nella quale è annidata: `level2`  
  
 [!code-vb[VbVbalrLambdas#9](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class3.vb#9)]  
  
## Conversione a un tipo delegato  
 Un'espressione lambda può essere convertita implicitamente a un tipo delegato compatibile.  Per ulteriori informazioni sui requisiti generali per la compatibilità, vedere [Relaxed Delegate Conversion](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md).  Nell'esempio di codice seguente viene ad esempio illustrata un'espressione lambda che esegue in modo implicito la conversione a `Func(Of Integer, Boolean)` o a una firma del delegato corrispondente.  
  
 [!code-vb[VbVbalrLambdas#16](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class1.vb#16)]  
  
 Nell'esempio di codice seguente viene illustrata un'espressione lambda che esegue in modo implicito la conversione a `Sub(Of Double, String, Double)` o a una firma del delegato corrispondente.  
  
 [!code-vb[VbVbalrLambdas#23](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/class7.vb#23)]  
  
 Quando si assegnano espressioni lambda ai delegati o si passano come argomenti alle routine, è possibile specificare i nomi dei parametri ma omettere i relativi tipi di dati, consentendo di ottenere i tipi dal delegato.  
  
## Esempi  
  
-   Nell'esempio riportato di seguito viene definita un'espressione lambda che restituisce `True` se l'argomento nullable ha un valore assegnato e `False` se il relativo valore è `Nothing`.  
  
     [!code-vb[VbVbalrLambdas#4](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class1.vb#4)]  
  
-   Nell'esempio riportato di seguito viene definita un'espressione lambda che restituisce l'indice dell'ultimo elemento in una matrice.  
  
     [!code-vb[VbVbalrLambdas#5](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class1.vb#5)]  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Delegates](../../../../visual-basic/programming-guide/language-features/delegates/delegates.md)   
 [Function Statement](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub Statement](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Nullable Value Types](../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)   
 [How to: Pass Procedures to Another Procedure in Visual Basic](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)   
 [How to: Create a Lambda Expression](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-lambda-expression.md)   
 [Relaxed Delegate Conversion](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)