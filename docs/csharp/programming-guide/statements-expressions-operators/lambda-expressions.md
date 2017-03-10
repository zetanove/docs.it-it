---
title: "Espressioni lambda (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2017-03-03"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "espressioni lambda [C#]"
  - "variabili esterne [C#]"
  - "lambda (istruzione) [C#]"
  - "lambda (espressione) [C#]"
  - "espressioni [C#], lambda"
ms.assetid: 57e3ba27-9a82-4067-aca7-5ca446b7bf93
caps.latest.revision: 64
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 64
---
# Espressioni lambda (Guida per programmatori C#)
Un'espressione lambda è una [funzione anonima](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md) che è possibile utilizzare per creare [delegati](../../../csharp/programming-guide/delegates/using-delegates.md) o tipi di [alberi delle espressioni](../Topic/Expression%20Trees%20\(C%23%20and%20Visual%20Basic\).md). Mediante le espressioni lambda è possibile scrivere funzioni locali che possono essere passate come argomenti o restituite come valore delle chiamate di funzione. Le espressioni lambda sono particolarmente utili per la scrittura delle espressioni di query LINQ.  
  
 Per creare un'espressione lambda, specificare gli eventuali parametri di input a sinistra dell'operatore lambda [\=\>](../../../csharp/language-reference/operators/lambda-operator.md) e inserire l'espressione o il blocco di istruzioni dall'altra parte. Ad esempio, l'espressione lambda `x => x * x` specifica un parametro denominato `x` e restituisce il valore di `x` al quadrato. È possibile assegnare questa espressione a un tipo di delegato, come illustrato nell'esempio riportato di seguito:  
  
```c#  
delegate int del(int i);  
static void Main(string[] args)  
{  
    del myDelegate = x => x * x;  
    int j = myDelegate(5); //j = 25  
}  
```  
  
 Per creare un tipo di albero delle espressioni:  
  
```c#  
using System.Linq.Expressions;  
  
namespace ConsoleApplication1  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            Expression<del> myET = x => x * x;  
        }  
    }  
}  
```  
  
 L'operatore `=>` ha la stessa precedenza dell' assegnazione \(`=`\) e [prevede l'associazione all'operando di destra](../../../csharp/programming-guide/statements-expressions-operators/operators.md) \(vedere la sezione "Associazione" dell'articolo sugli operatori\).  
  
 Le espressioni lambda vengono utilizzate nelle query [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] basate sul metodo come argomenti dei metodi di operatori di query standard, quali <xref:System.Linq.Enumerable.Where%2A>.  
  
 Quando si utilizza la sintassi basata sul metodo per chiamare il metodo <xref:System.Linq.Enumerable.Where%2A> nella classe <xref:System.Linq.Enumerable>, come in [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] to Objects e [!INCLUDE[sqltecxlinq](../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)], il parametro è un tipo <xref:System.Func%602?displayProperty=fullName> delegato. Un'espressione lambda è il modo più pratico per creare tale delegato. Quando, ad esempio, si chiama lo stesso metodo nella classe <xref:System.Linq.Queryable?displayProperty=fullName>, come in [!INCLUDE[vbtecdlinq](../../../csharp/includes/vbtecdlinq-md.md)], il tipo di parametro sarà <xref:System.Linq.Expressions.Expression?displayProperty=fullName>\<Func\>, dove Func è qualsiasi delegato Func con un massimo di sedici parametri di input. Un'espressione lambda rappresenta quindi un modo rapido per costruire tale albero delle espressioni. Mediante le espressioni lambda, le chiamate `Where` risultano simili anche se in realtà il tipo di oggetto creato dall'espressione lambda è diverso.  
  
 Nell'esempio precedente si noti che la firma del delegato ha un parametro di input tipizzato in modo implicito di tipo `int` e restituisce un oggetto `int`. L'espressione lambda può essere convertita in un delegato di tale tipo poiché dispone anche di un parametro di input \(`x`\) e di un valore restituito che il compilatore può convertire in modo implicito nel tipo `int`. L'inferenza dei tipi viene illustrata più dettagliatamente nelle sezioni seguenti. Quando il delegato viene richiamato tramite un parametro di input pari a 5, restituisce un risultato di 25.  
  
 Non è possibile utilizzare le espressioni lambda sul lato sinistro dell'operatore [is](../../../csharp/language-reference/keywords/is.md) o [as](../../../csharp/language-reference/keywords/as.md).  
  
 Tutte le restrizioni che si applicano ai metodi anonimi si applicano anche alle espressioni lambda. Per altre informazioni, vedere [Metodi anonimi](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md).  
  
## Espressioni lambda  
 Un'espressione lambda con un'espressione sul lato destro dell'operatore \=\> è denominata *lambda espressione*. Queste espressioni vengono usate spesso nella costruzione di [Strutture ad albero dell'espressione](../Topic/Expression%20Trees%20\(C%23%20and%20Visual%20Basic\).md). Un'espressione lambda dell'espressione restituisce il risultato dell'espressione e ha il formato di base seguente:  
  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
 Le parentesi sono facoltative solo se l'espressione lambda ha un parametro di input; in caso contrario sono obbligatorie. Due o più parametri di input vengono separati da virgole e racchiusi tra parentesi:  
  
<CodeContentPlaceHolder>3</CodeContentPlaceHolder>  
 Talvolta è difficile o impossibile che il compilatore deduca i tipi di input. In tal caso, è possibile specificare i tipi in modo esplicito come illustrato nell'esempio seguente:  
  
<CodeContentPlaceHolder>4</CodeContentPlaceHolder>  
 Specificare zero parametri di input con parentesi vuote:  
  
<CodeContentPlaceHolder>5</CodeContentPlaceHolder>  
 Si noti che nell'esempio precedente il corpo di un'espressione lambda dell'espressione può essere costituito da una chiamata al metodo. Tuttavia, se si creano alberi delle espressioni valutati al di fuori di .NET Framework, ad esempio in SQL Server, non è consigliabile utilizzare chiamate al metodo nelle espressioni lambda. I metodi non avranno alcun significato all'esterno del contesto di .NET Common Language Runtime.  
  
## Espressioni lambda dell'istruzione  
 Un'espressione lambda dell'istruzione è simile a un'espressione lambda dell'espressione con la differenza che l'istruzione o le istruzioni sono racchiuse tra parentesi graffe:  
  
<CodeContentPlaceHolder>6</CodeContentPlaceHolder>  
 Il corpo di un'espressione lambda dell'istruzione può essere costituito da un numero qualsiasi di istruzioni, sebbene in pratica generalmente non ce ne siano più di due o tre.  
  
<CodeContentPlaceHolder>7</CodeContentPlaceHolder>  
 Le espressioni lambda dell'istruzione, come i metodi anonimi, non possono essere utilizzate per creare alberi delle espressioni.  
  
## Espressioni lambda asincrone  
 È facile creare istruzioni ed espressioni lambda che includono l'elaborazione asincrona utilizzando le parole chiave [async](../../../csharp/language-reference/keywords/async.md) e [await](../../../csharp/language-reference/keywords/await.md). Nell'esempio seguente di Windows Form è presente un gestore eventi che chiama e attende un metodo asincrono, `ExampleMethodAsync`.  
  
<CodeContentPlaceHolder>8</CodeContentPlaceHolder>  
 È possibile aggiungere lo stesso gestore eventi utilizzando un'espressione lambda asincrona. Per aggiungere il gestore, aggiungere un modificatore `async` prima dell'elenco di parametri lambda, come illustrato di seguito.  
  
<CodeContentPlaceHolder>9</CodeContentPlaceHolder>  
 Per altre informazioni su come creare e usare metodi asincroni, vedere [Programmazione asincrona con Async e Await](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Espressioni lambda con operatori di query standard  
 Molti operatori di query standard hanno un parametro di input il cui tipo è uno della famiglia <xref:System.Func%602> di delegati generici. Questi delegati utilizzano parametri di tipo per definire il numero e i tipi di parametri di input e il tipo restituito del delegato. I delegati `Func` sono molto utili per incapsulare le espressioni definite dall'utente applicate a ogni elemento in un set di dati di origine. Considerare ad esempio il seguente tipo delegato:  
  
```c#  
public delegate TResult Func<TArg0, TResult>(TArg0 arg0)  
```  
  
 È possibile creare un'istanza del delegato come `Func<int,bool> myFunc` dove `int` è un parametro di input e `bool` è il valore restituito. Il valore restituito è sempre specificato nell'ultimo parametro di tipo.`Func<int, string, bool>` definisce un delegato con due parametri di input, `int` e `string`, e un tipo restituito `bool`. Quando viene richiamato, il delegato `Func` seguente restituisce true o false per indicare se il parametro di input è uguale a 5:  
  
```c#  
Func<int, bool> myFunc = x => x == 5;  
bool result = myFunc(4); // returns false of course  
```  
  
 È inoltre possibile fornire un'espressione lambda quando il tipo di argomento è `Expression<Func>`, ad esempio negli operatori di query standard definiti in System.Linq.Queryable. Quando si specifica un argomento `Expression<Func>`, l'espressione lambda viene compilata in un albero delle espressioni.  
  
 Di seguito viene illustrato un operatore di query standard, il metodo <xref:System.Linq.Enumerable.Count%2A>:  
  
```c#  
int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };  
int oddNumbers = numbers.Count(n => n % 2 == 1);  
```  
  
 Il compilatore è in grado di dedurre il tipo del parametro di input oppure è possibile specificarlo in modo esplicito. Questa espressione lambda particolare conta i numeri interi \(`n`\) che divisi per due danno il resto di 1.  
  
 La seguente riga di codice produce una sequenza che contiene tutti gli elementi presenti nella matrice `numbers` che si trovano a sinistra di 9, che rappresenta il primo numero della sequenza che non soddisfa la condizione:  
  
```c#  
var firstNumbersLessThan6 = numbers.TakeWhile(n => n < 6);  
```  
  
 In questo esempio viene illustrato come specificare più parametri di input racchiudendoli tra parentesi. Il metodo restituisce tutti gli elementi presenti nella matrice di numeri finché non viene rilevato un numero il cui valore è inferiore alla relativa posizione. Non confondere l'operatore lambda \(`=>`\) con l'operatore Greater Than o Equals \(`>=`\).  
  
```c#  
var firstSmallNumbers = numbers.TakeWhile((n, index) => n >= index);  
```  
  
## Inferenza dei tipi nelle espressioni lambda  
 Quando si scrivono le espressioni lambda, spesso non occorre specificare un tipo per i parametri di input in quanto il compilatore è in grado di dedurlo in base al corpo dell'espressione lambda, al tipo delegato del parametro e ad altri fattori, come descritto nella specifica del linguaggio C\#. Per la maggior parte degli operatori di query standard, il primo input è il tipo degli elementi nella sequenza di origine. Pertanto se si esegue una query su un oggetto `IEnumerable<Customer>`, si deduce che la variabile di input sia un oggetto `Customer`, ovvero che si dispone dell'accesso ai relativi metodi e proprietà:  
  
```c#  
customers.Where(c => c.City == "London");  
```  
  
 Di seguito sono riportate le regole generali per le espressioni lambda:  
  
-   L'espressione lambda deve contenere lo stesso numero di parametri del tipo delegato.  
  
-   Ogni parametro di input nell'espressione lambda deve essere convertibile in modo implicito nel parametro del delegato corrispondente.  
  
-   Il valore restituito dell'espressione lambda, se presente, deve essere convertibile in modo implicito nel tipo restituito del delegato.  
  
 Si noti che le espressioni lambda non hanno un tipo poiché Common Type System non ha alcun concetto intrinseco di "espressione lambda". In alcuni casi, tuttavia, può essere utile fare riferimento in modo informale al "tipo" di un'espressione lambda. In questi casi, per tipo si intende il tipo delegato o il tipo <xref:System.Linq.Expressions.Expression> in cui viene convertita l'espressione lambda.  
  
## Ambito delle variabili nelle espressioni lambda  
 Le espressioni lambda possono fare riferimento alle *variabili esterne* \(vedere [Metodi anonimi](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)\) presenti nell'ambito del metodo che definisce la funzione lambda o nell'ambito del tipo che contiene l'espressione lambda. Le variabili acquisite in questo modo vengono archiviate per poter essere utilizzate nell'espressione lambda anche se le variabili diventano esterne all'ambito e vengono sottoposte a Garbage Collection. Una variabile esterna deve essere assegnata prima di poter essere utilizzata in un'espressione lambda. Nell'esempio seguente vengono illustrate queste regole:  
  
```c#  
delegate bool D();  
delegate bool D2(int i);  
  
class Test  
{  
    D del;  
    D2 del2;  
    public void TestMethod(int input)  
    {  
        int j = 0;  
        // Initialize the delegates with lambda expressions.  
        // Note access to 2 outer variables.  
        // del will be invoked within this method.  
        del = () => { j = 10;  return j > input; };  
  
        // del2 will be invoked after TestMethod goes out of scope.  
        del2 = (x) => {return x == j; };  
  
        // Demonstrate value of j:  
        // Output: j = 0   
        // The delegate has not been invoked yet.  
        Console.WriteLine("j = {0}", j);        // Invoke the delegate.  
        bool boolResult = del();  
  
        // Output: j = 10 b = True  
        Console.WriteLine("j = {0}. b = {1}", j, boolResult);  
    }  
  
    static void Main()  
    {  
        Test test = new Test();  
        test.TestMethod(5);  
  
        // Prove that del2 still has a copy of  
        // local variable j from TestMethod.  
        bool result = test.del2(10);  
  
        // Output: True  
        Console.WriteLine(result);  
  
        Console.ReadKey();  
    }  
}  
  
```  
  
 Le regole seguenti si applicano all'ambito delle variabili nelle espressioni lambda:  
  
-   Una variabile acquisita non sarà sottoposta a Garbage Collection finché il delegato a cui fa riferimento non diventa idoneo per il Garbage Collection.  
  
-   Le variabili introdotte all'interno di un'espressione lambda non sono visibili nel metodo esterno.  
  
-   Un'espressione lambda non può acquisire direttamente un parametro `ref` o `out` da un metodo contenitore.  
  
-   Un'istruzione return in un'espressione lambda non causa la restituzione del metodo contenitore.  
  
-   Un'espressione lambda non può contenere un'istruzione `goto`, `break` o `continue`, inclusa nella funzione lambda se la destinazione dell'istruzione jump è esterna al blocco. È altresì errato inserire all'esterno del blocco della funzione lambda un'istruzione jump se la destinazione è interna al blocco.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Capitoli del libro rappresentati  
 [Delegates, Events, and Lambda Expressions](http://go.microsoft.com/fwlink/?LinkId=195395) \(Delegati, eventi ed espressioni lambda\) in [C\# 3.0 Cookbook, Third Edition: More than 250 solutions for C\# 3.0 programmers](http://go.microsoft.com/fwlink/?LinkId=195369)  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Metodi anonimi](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)   
 [is](../../../csharp/language-reference/keywords/is.md)   
 [Strutture ad albero dell'espressione](../Topic/Expression%20Trees%20\(C%23%20and%20Visual%20Basic\).md)   
 [Esempi C\# di Visual Studio 2008 \(vedere i file di query di esempio LINQ e il programma XQuery\)](http://code.msdn.microsoft.com/Visual-Studio-2008-C-d295cdba)   
 [Recursive lambda expressions \(Espressioni lambda ricorsive\)](http://go.microsoft.com/fwlink/?LinkId=112395)