---
title: for (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- for
- for_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- for keyword [C#]
ms.assetid: 34041a40-2c87-467a-9ffb-a0417d8f67a8
caps.latest.revision: 39
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f2f32dd4bde376dd241cf168a4f034ba8f6e9b50
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="for-c-reference"></a>for (Riferimenti per C#)
Usando un ciclo `for`, è possibile eseguire ripetutamente un'istruzione o un blocco di istruzioni fino a quando un'espressione specificata restituisce `false`. Questo tipo di ciclo è utile per eseguire l'iterazione su matrici e per altre applicazioni in cui si conosce in anticipo quante volte il ciclo deve eseguire l'iterazione.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente il valore `i` viene scritto nella console e viene incrementato di 1 durante ogni iterazione del ciclo.  
  
 [!code-cs[csrefKeywordsIteration#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/for_1.cs)]  
  
 L'istruzione `for` nell'esempio precedente esegue le azioni seguenti.  
  
1.  Prima viene stabilito il valore iniziale della variabile `i`. Questo passaggio viene eseguito una sola volta, indipendentemente da quante volte viene ripetuto il ciclo. È possibile pensare all'inizializzazione come a un'operazione che viene eseguita all'esterno del processo di ciclo.  
  
2.  Per valutare la condizione (`i <= 5`), il valore di `i` viene confrontato con 5.  
  
    -   Se `i` è minore o uguale a 5, la condizione restituisce `true` e si verificano le azioni seguenti.  
  
        1.  L'istruzione `Console.WriteLine` nel corpo del ciclo visualizza il valore di `i`.  
  
        2.  Il valore di `i` viene incrementato di 1.  
  
        3.  Il ciclo ritorna all'inizio del passaggio 2 per valutare nuovamente la condizione.  
  
    -   Se `i` è maggiore di 5, la condizione restituisce `false` e si esce dal ciclo.  
  
 Si noti che, se il valore iniziale di `i` è maggiore di 5, il corpo del ciclo non viene eseguito neppure una volta.  
  
 Ogni istruzione `for` definisce le sezioni di inizializzatore, condizione e iteratore. In queste sezioni viene solitamente definito quante volte il ciclo esegue l'iterazione.  
  
```csharp  
for (initializer; condition; iterator)  
    body  
```  
  
 Gli scopi delle sezioni sono i seguenti.  
  
-   Nella sezione dell'inizializzatore vengono impostate le condizioni iniziali. Le istruzioni in questa sezione sono eseguite una sola volta, prima che inizi il ciclo. Questa sezione può contenere solo una delle due opzioni seguenti.  
  
    -   Dichiarazione e inizializzazione di una variabile di ciclo locale, come illustrato nel primo esempio (`int i = 1`). La variabile è locale rispetto al ciclo e non è possibile accedervi dall'esterno del ciclo.  
  
    -   Zero o più istruzioni, ricavate dal seguente elenco, separate da virgole.  
  
        -   Istruzione di [assegnazione](../../../csharp/language-reference/operators/assignment-operator.md)  
  
        -   Chiamata di un metodo  
  
        -   Espressione di [incremento](../../../csharp/language-reference/operators/increment-operator.md) in forma prefissa o suffissa, ad esempio `++i` o `i++`  
  
        -   Espressione di [decremento](../../../csharp/language-reference/operators/decrement-operator.md) in forma prefissa o suffissa, ad esempio `--i` o `i--`  
  
        -   Creazione di un oggetto con [new](../../../csharp/language-reference/keywords/new-operator.md)  
  
        -   Espressione [await](../../../csharp/language-reference/keywords/await.md)  
  
-   La sezione della condizione contiene un'espressione booleana valutata per determinare se uscire dal ciclo oppure ripeterlo.  
  
-   Nella sezione dell'iteratore viene definito cosa accade dopo ogni iterazione del corpo del ciclo. Questa sezione contiene zero o più delle espressioni di istruzioni seguenti, separate da virgole:  
  
    -   Istruzione di [assegnazione](../../../csharp/language-reference/operators/assignment-operator.md)  
  
    -   Chiamata di un metodo  
  
    -   Espressione di [incremento](../../../csharp/language-reference/operators/increment-operator.md) in forma prefissa o suffissa, ad esempio `++i` o `i++`  
  
    -   Espressione di [decremento](../../../csharp/language-reference/operators/decrement-operator.md) in forma prefissa o suffissa, ad esempio `--i` o `i--`  
  
    -   Creazione di un oggetto con [new](../../../csharp/language-reference/keywords/new-operator.md)  
  
    -   Espressione [await](../../../csharp/language-reference/keywords/await.md)  
  
-   Il corpo del ciclo è costituito da un'istruzione, un'istruzione vuota o un blocco di istruzioni, creato racchiudendo tra parentesi zero o più istruzioni.  
  
     È possibile interrompere un ciclo `for` con la parola chiave [break](../../../csharp/language-reference/keywords/break.md) oppure è possibile usare la parola chiave [continue](../../../csharp/language-reference/keywords/continue.md) per passare all'iterazione successiva. Si può uscire da un ciclo anche usando l'istruzione [goto](../../../csharp/language-reference/keywords/goto.md), [return](../../../csharp/language-reference/keywords/return.md) o [throw](../../../csharp/language-reference/keywords/throw.md).  
  
 Nel primo esempio di questo argomento viene illustrato il tipo di ciclo `for` più comune, che definisce le opzioni seguenti per le sezioni.  
  
-   L'inizializzatore dichiara e inizializza una variabile di ciclo locale, `i`, che conta le iterazioni del ciclo.  
  
-   La condizione confronta il valore della variabile del ciclo con il valore finale noto 5.  
  
-   Nella sezione dell'iteratore viene usata un'istruzione d'incremento in forma suffissa, `i++`, per calcolare ogni iterazione del ciclo.  
  
 L'esempio seguente illustra alcuni opzioni meno comuni: assegnazione di un valore a una variabile di ciclo esterno nella sezione dell'inizializzatore, chiamata del metodo `Console.WriteLine` nella sezione dell'inizializzatore e in quella dell'iteratore e modifica dei valori di due variabili nella sezione dell'iteratore.  
  
 [!code-cs[csrefKeywordsIteration#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/for_2.cs)]  
  
 Tutte le espressioni che definiscono un'istruzione `for` sono facoltative. Ad esempio, l'istruzione seguente crea un ciclo infinito.  
  
 [!code-cs[csrefKeywordsIteration#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/for_3.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [foreach, in](../../../csharp/language-reference/keywords/foreach-in.md)   
 [Istruzione for (C++)](https://docs.microsoft.com/cpp/cpp/for-statement-cpp)   
 [Istruzioni di iterazione](../../../csharp/language-reference/keywords/iteration-statements.md)
