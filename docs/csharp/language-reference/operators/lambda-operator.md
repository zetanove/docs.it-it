---
title: =&gt; Operatore (Riferimenti per C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- =>_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- lambda operator [C#]
- => operator [C#]
- lambda expressions [C#], => operator
ms.assetid: 8c899251-dafa-4594-bec7-243b39072880
caps.latest.revision: 21
author: BillWagner
ms.author: wiwagn
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a75967e61d2c674e87e321de1fb6e4062cca4f19
ms.lasthandoff: 03/13/2017

---
# <a name="gt-operator-c-reference"></a>=&gt; Operatore (Riferimenti per C#)
Il token `=>` viene chiamato operatore lambda. Viene usato nelle *espressioni lambda* per separare le variabili di input sul lato sinistro dal corpo dell'espressione lambda da quelle sul lato destro. Le espressioni lambda sono espressioni inline simili ai metodi anonimi ma più flessibili. Vengono usate ampiamente nelle query LINQ espresse nella sintassi del metodo. Per altre informazioni, vedere [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
 Nell'esempio seguente vengono illustrate due modalità per individuare e visualizzare la lunghezza della stringa più breve in una matrice di stringhe. La prima parte dell'esempio applica un'espressione lambda (`w => w.Length`) a ogni elemento della matrice`words` e usa quindi il metodo <xref:System.Linq.Enumerable.Min%2A> per individuare la lunghezza minima. La seconda parte dell'esempio mostra invece una soluzione più lunga che usa la sintassi della query per eseguire la stessa operazione.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
## <a name="remarks"></a>Note  
 L'operatore `=>` ha la stessa priorità dell'operatore di assegnazione (`=`) e si associa all'operando a destra.  
  
 È possibile specificare il tipo di variabile di input in modo esplicito o consentendo al compilatore di dedurlo; in entrambi i casi, la variabile è fortemente tipizzata in fase di compilazione. Quando si specifica un tipo, è necessario racchiudere tra parentesi il nome del tipo e il nome della variabile, come illustrato nell'esempio seguente.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
## <a name="example"></a>Esempio  
 Nell'esempio riportato di seguito viene illustrato come scrivere un'espressione lambda per eseguire l'overload dell'operatore query standard <xref:System.Linq.Enumerable.Where%2A?displayProperty=fullName> che accetta due argomenti. Poiché l'espressione lambda contiene più di un parametro, i parametri devono essere racchiusi tra parentesi. Il secondo parametro, `index`, rappresenta l'indice dell'elemento corrente nella raccolta. L'espressione `Where` restituisce tutte le stringhe la cui lunghezza è minore rispetto alla loro posizione nell'indice nella matrice.  
  
```cs  
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
  
    // Output:  
    // Example that uses a lambda expression:  
    // five  
    // six  
    // seven  
    // eight  
    // nine  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)
