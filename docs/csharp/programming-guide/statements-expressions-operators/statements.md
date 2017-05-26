---
title: Istruzioni (Guida per programmatori C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- statements [C#], about statements
- C# language, statements
ms.assetid: 901bcde7-87de-4e15-833c-f9cfd40c8ce3
caps.latest.revision: 28
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
ms.openlocfilehash: cfbd607f614bd8d287dd33f08dd47b12fa651ced
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="statements-c-programming-guide"></a>Istruzioni (Guida per programmatori C#)
Le azioni accettate da un programma vengono espresse in istruzioni. Le azioni comuni includono la dichiarazione di variabili, l'assegnazione di valori, le chiamate ai metodi, il ciclo delle raccolte e la creazione di rami tra blocchi di codice, a seconda di una data condizione. L'ordine in cui vengono le istruzioni eseguite in un programma viene chiamato "flusso di controllo" o "flusso di esecuzione". Il flusso di controllo può variare ogni volta che viene eseguito un programma, a seconda della reazione del programma all'input ricevuto in fase di esecuzione.  
  
 Un'istruzione può essere costituito da una singola riga di codice che termina con un punto e virgola o da una serie di istruzioni a riga singola in un blocco. Un blocco di istruzioni è racchiuso tra parentesi {} e può contenere blocchi annidati. Il codice seguente mostra due esempi di istruzioni a riga singola e un blocco di istruzioni a più righe:  
  
 [!code-cs[csProgGuideStatements#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_1.cs)]  
  
## <a name="types-of-statements"></a>Tipi di istruzioni  
 Nella tabella seguente sono elencati i vari tipi di istruzioni in C# e le parole chiave associate, con link ad argomenti contenenti maggiori informazioni:  
  
|Categoria|Parole chiave C#/note|  
|--------------|---------------------------|  
|Istruzioni di dichiarazione|Un'istruzione di dichiarazione introduce una nuova variabile o costante. Una dichiarazione di variabile può facoltativamente assegnare un valore alla variabile. In una dichiarazione di costante, l'assegnazione è necessaria.<br /><br /> [!code-cs[csProgGuideStatements#23](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_2.cs)]|  
|Istruzioni di espressione|Le istruzioni di espressione che calcolano un valore devono archiviare il valore in una variabile.<br /><br /> [!code-cs[csProgGuideStatements#24](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_3.cs)]|  
|[Istruzioni di selezione](../../../csharp/language-reference/keywords/selection-statements.md)|Le istruzioni di selezione consentono di creare un ramo tra le diverse sezioni di codice, in base a una o più condizioni specificate. Per altre informazioni, vedere i seguenti argomenti:<br /><br /> [if](../../../csharp/language-reference/keywords/if-else.md), [else](../../../csharp/language-reference/keywords/if-else.md), [switch](../../../csharp/language-reference/keywords/switch.md), [case](../../../csharp/language-reference/keywords/switch.md)|  
|[Istruzioni di iterazione](../../../csharp/language-reference/keywords/iteration-statements.md)|Le istruzioni di iterazione consentono di eseguire un ciclo tra le raccolte come matrici o eseguono ripetutamente lo stesso set di istruzioni finché non viene soddisfatta una condizione specificata. Per altre informazioni, vedere i seguenti argomenti:<br /><br /> [do](../../../csharp/language-reference/keywords/do.md), [for](../../../csharp/language-reference/keywords/for.md), [foreach](../../../csharp/language-reference/keywords/foreach-in.md), [in](../../../csharp/language-reference/keywords/foreach-in.md), [while](../../../csharp/language-reference/keywords/while.md)|  
|[Istruzioni di salto](../../../csharp/language-reference/keywords/jump-statements.md)|Le istruzioni di salto trasferiscono il controllo a un'altra sezione di codice. Per altre informazioni, vedere i seguenti argomenti:<br /><br /> [break](../../../csharp/language-reference/keywords/break.md), [continue](../../../csharp/language-reference/keywords/continue.md), [default](../../../csharp/language-reference/keywords/switch.md), [goto](../../../csharp/language-reference/keywords/goto.md), [return](../../../csharp/language-reference/keywords/return.md), [yield](../../../csharp/language-reference/keywords/yield.md)|  
|[Istruzioni di gestione delle eccezioni](../../../csharp/language-reference/keywords/exception-handling-statements.md)|Le istruzioni di gestione delle eccezioni consentono di recuperare condizioni eccezionali che si verificano in fase di esecuzione. Per altre informazioni, vedere i seguenti argomenti:<br /><br /> [throw](../../../csharp/language-reference/keywords/throw.md), [try-catch](../../../csharp/language-reference/keywords/try-catch.md), [try-finally](../../../csharp/language-reference/keywords/try-finally.md), [try-catch-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)|  
|[Checked e Unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md)|Le istruzioni Checked e Unchecked consentono di specificare se le operazioni numeriche possono provocare un overflow quando il risultato viene archiviato in una variabile troppo piccola per contenere il valore risultante. Per altre informazioni, vedere [checked](../../../csharp/language-reference/keywords/checked.md) e [unchecked](../../../csharp/language-reference/keywords/unchecked.md).|  
Istruzione `await`|Se si contrassegna un metodo con il modificatore [async](../../../csharp/language-reference/keywords/async.md), è possibile usare l'operatore [await](../../../csharp/language-reference/keywords/await.md) nel metodo. Quando il controllo raggiunge un'espressione `await` nel metodo asincrono, il controllo torna al chiamante e l'avanzamento nel metodo viene sospeso fino al completamento dell'attività attesa. Una volta completata l'attività, l'esecuzione del metodo può riprendere.<br /><br /> Per un esempio semplice, vedere la sezione "Metodi asincroni" in [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md). Per altre informazioni, vedere [Programmazione asincrona con async e await](../../../csharp/programming-guide/concepts/async/index.md).|  
|Istruzione `yield return`|Un iteratore esegue un'iterazione personalizzata su una raccolta, ad esempio un elenco o una matrice. Un iteratore usa l'istruzione [yield return](../../../csharp/language-reference/keywords/yield.md) per restituire un elemento per volta. Quando viene raggiunta un'istruzione `yield return`, la posizione corrente nel codice viene memorizzata. L'esecuzione viene riavviata a partire da quella posizione la volta successiva che viene chiamato l'iteratore.<br /><br /> Per altre informazioni, vedere [Iteratori](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7).|  
|Istruzione `fixed`|L'istruzione fixed impedisce che il Garbage Collector esegua la rilocazione di una variabile mobile. Per altre informazioni, vedere [fixed](../../../csharp/language-reference/keywords/fixed-statement.md).|  
|Istruzione `lock`|L'istruzione lock consente di limitare l'accesso ai blocchi di codice a un solo thread per volta. Per altre informazioni, vedere [lock](../../../csharp/language-reference/keywords/lock-statement.md).|  
|Istruzioni con etichetta|È possibile assegnare un'etichetta a un'istruzione e quindi usare la parola chiave [goto](../../../csharp/language-reference/keywords/goto.md) per passare all'istruzione con etichetta. Vedere l'esempio nell'argomento seguente.|  
|Istruzione vuota|L'istruzione vuota è costituita da un singolo punto e virgola. Non esegue alcuna operazione e può essere usata in posizioni in cui è richiesta un'istruzione ma non deve essere eseguita alcuna azione. Gli esempi seguenti illustrano due usi di un'istruzione vuota:<br /><br /> [!code-cs[csProgGuideStatements#25](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_4.cs)]|  
  
## <a name="embedded-statements"></a>Istruzioni incorporate  
 Alcune istruzioni, fra cui [do](../../../csharp/language-reference/keywords/do.md), [while](../../../csharp/language-reference/keywords/while.md), [for](../../../csharp/language-reference/keywords/for.md) e [foreach](../../../csharp/language-reference/keywords/foreach-in.md), dispongono sempre di un'istruzione incorporata che le segue. Questa istruzione incorporata può essere una singola istruzione o più istruzioni racchiuse tra parentesi {} in un blocco di istruzioni. Anche le istruzioni incorporate a riga singola possono essere racchiuse tra parentesi {}, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideStatements#26](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_5.cs)]  
  
 Un'istruzione incorporata non racchiusa tra parentesi {} non può essere un'istruzione di dichiarazione o un'istruzione con etichetta. Questa operazione è illustrata nell'esempio seguente:  
  
 [!code-cs[csProgGuideStatements#27](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_6.cs)]  
  
 Inserire l'istruzione incorporata in un blocco per correggere l'errore:  
  
 [!code-cs[csProgGuideStatements#28](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_7.cs)]  
  
## <a name="nested-statement-blocks"></a>Blocchi di istruzioni annidate  
 I blocchi di istruzioni possono essere annidati, come illustrato nel codice seguente:  
  
 [!code-cs[csProgGuideStatements#29](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_8.cs)]  
  
## <a name="unreachable-statements"></a>Istruzioni non raggiungibili  
 Se il compilatore determina che il flusso di controllo non può raggiungere mai una particolare istruzione in nessuna circostanza, genererà l'avviso CS0162, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideStatements#22](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_9.cs)]  
  
## <a name="related-sections"></a>Sezioni correlate  
  
-   [Parole chiave per le istruzioni](../../../csharp/language-reference/keywords/statement-keywords.md)  
  
-   [Espressioni](../../../csharp/programming-guide/statements-expressions-operators/expressions.md)  
  
-   [Operatori](../../../csharp/programming-guide/statements-expressions-operators/operators.md)  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)
