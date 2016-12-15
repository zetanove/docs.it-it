---
title: "Operatore =&gt; (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "=>_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "lambda (operatore) [C#]"
  - "=> (operatore) (C#)"
  - "espressioni lambda [C#], => (operatore)"
ms.assetid: 8c899251-dafa-4594-bec7-243b39072880
caps.latest.revision: 21
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Operatore =&gt; (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il token `=>` è chiamato l'operatore lambda.  Viene utilizzato nelle *espressioni lambda* per separare le variabili di input sul lato sinistro dal corpo della lambda sul lato destro.  Le espressioni lambda sono espressioni in linea simili ai metodi anonimi, ma più flessibili. Vengono utilizzate spesso nelle query LINQ espresse in sintassi del metodo.  Per ulteriori informazioni, vedere [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
 Nell'esempio seguente vengono illustrate due modalità per individuare e visualizzare la lunghezza di più breve stringa in una matrice di stringhe.  La prima parte dell'esempio viene applicata un'espressione lambda \(`w => w.Length`\) a ogni elemento della matrice di `words` quindi utilizzato il metodo di <xref:System.Linq.Enumerable.Min%2A> per trovare la lunghezza.  Per il confronto, la seconda parte dell'esempio viene illustrata una soluzione più lunga che la sintassi della query per eseguire la stessa operazione.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
## Note  
 L'operatore `=>` ha la stessa precedenza dell'operatore di assegnazione \(`=`\) e prevede l'associazione all'operando di destra.  
  
 È possibile specificare il tipo della variabile di input in modo esplicito oppure lasciare che il compilatore dedurlo; in entrambi i casi, la variabile è fortemente tipizzata in fase di compilazione.  Quando si specifica un tipo, è necessario racchiudere il nome del tipo e il nome della variabile tra parentesi, come illustrato di seguito.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
## Esempio  
 Di seguito viene illustrato come scrivere un'espressione lambda per l'overload di <xref:System.Linq.Enumerable.Where%2A?displayProperty=fullName> degli operatori di query standard che accetta due argomenti.  Poiché l'espressione lambda dispone di più di un parametro, i parametri devono essere racchiusi tra parentesi.  Il secondo parametro, `index`, rappresenta l'indice dell'elemento corrente nella raccolta.  L'espressione di `Where` restituisce tutte le stringhe delle lunghezze inferiori alla posizione di indice nella matrice.  
  
```c#  
static void Main(string[] args)  
{  
    string[] digits = { "zero", "one", "two", "three", "four", "five",   
            "six", "seven", "eight", "nine" };  
  
    Console.WriteLine("Example that uses a lambda expression:");  
    var shortDigits = digits.Where((digit, index) => digit.Length < index);  
    foreach (var sD in shortDigits)  
    {  
        Console.WriteLine(sD);  
    }  
  
    // Compare the following code, which arrives at the same list of short  
    // digits but takes more work to get there.  
    Console.WriteLine("\nExample that uses a for loop:");  
    List<string> shortDigits2 = new List<string>();  
    for (var i = 0; i < digits.Length; i++)  
    {  
        if (digits[i].Length < i)  
            shortDigits2.Add(digits[i]);  
    }  
  
    foreach (var d in shortDigits2)  
    {  
        Console.WriteLine(d);  
    }  
    // Output:  
    // Example that uses a lambda expression:  
    // five  
    // six  
    // seven  
    // eight  
    // nine  
  
    // Example that uses a for loop:  
    // five  
    // six  
    // seven  
    // eight  
    // nine  
}  
```  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)