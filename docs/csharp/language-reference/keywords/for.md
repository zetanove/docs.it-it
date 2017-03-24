---
title: "for (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "for"
  - "for_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "for (parola chiave) [C#]"
ms.assetid: 34041a40-2c87-467a-9ffb-a0417d8f67a8
caps.latest.revision: 39
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 39
---
# for (Riferimenti per C#)
Utilizzando un ciclo `for`, è possibile eseguire più volte un'istruzione o un blocco di istruzioni fino a quando un'espressione specificata non risulta essere in `false`.  Questo tipo di ciclo è utile per la ripetizione su matrici e ad altre applicazioni in cui si conosce in anticipo quante volte il ciclo per scorrere.  
  
## Esempio  
 Nell'esempio seguente, il valore `i` viene scritto nella console e viene incrementato da 1 durante ogni iterazione del ciclo.  
  
 [!code-cs[csrefKeywordsIteration#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/for_1.cs)]  
  
 L'istruzione `for` nell'esempio precedente vengono eseguite le seguenti azioni.  
  
1.  Innanzitutto, il valore iniziale `i` variabile viene stabilito.  Questo passaggio si verifica solo una volta, indipendentemente dal numero di volte le ripetizioni del ciclo.  È possibile pensare a questa inizializzazione come esterno verificanteti il processo di ciclo.  
  
2.  Per valutare la condizione \(`i <= 5`\), il valore `i` viene confrontato a 5.  
  
    -   Se `i` è minore o uguale a 5, la condizione restituisce a `true`e si verificano le seguenti operazioni.  
  
        1.  L'istruzione `Console.WriteLine` nel corpo del ciclo visualizzare il valore `i`.  
  
        2.  Il valore `i` viene incrementato da 1.  
  
        3.  Restituisce il cicloinizio del passaggio 2 valutare nuovamente la condizione.  
  
    -   Se `i` è maggiore di 5, la condizione restituisce a `false`e uscire dal ciclo.  
  
 Si noti che, se il valore iniziale `i` è maggiore di 5, il corpo del ciclo non funziona anche una volta.  
  
 Ogni istruzione `for` definisce un inizializzatore, la condizione e le sezioni di iteratore.  Queste sezioni in genere determinare quante volte il ciclo scorre.  
  
```c#  
for (initializer; condition; iterator)  
    body  
```  
  
 Le sezioni hanno gli scopi seguenti.  
  
-   La sezione dell'inizializzatore imposta le condizioni iniziali.  Le istruzioni in questa sezione solo quando l'esecuzione, prima di immettere il ciclo.  La sezione può contenere solo una delle due opzioni.  
  
    -   La dichiarazione e l'inizializzazione di una variabile di circuito locale, come nel primo esempio viene illustrato \(`int i = 1`\).  La variabile è locale al ciclo e non può essere eseguito dall'esterno del ciclo.  
  
    -   Zero o più expressons di istruzione dall'elenco, separati da virgole.  
  
        -   Istruzione di[assegnazione](../../../csharp/language-reference/operators/assignment-operator.md)  
  
        -   chiamata di un metodo  
  
        -   preceduti o aggiungere alla fine dell'espressione [incremento](../../../csharp/language-reference/operators/increment-operator.md), come `++i` o `i++`  
  
        -   preceduti o aggiungere alla fine dell'espressione [decremento](../../../csharp/language-reference/operators/decrement-operator.md), come `--i` o `i--`  
  
        -   creazione di un oggetto utilizzando [new](../../../csharp/language-reference/keywords/new-operator.md)  
  
        -   espressione di[attendere](../../../csharp/language-reference/keywords/await.md)  
  
-   La sezione di condizione contiene un'espressione booleana che viene valutata per determinare se il ciclo deve essere chiusa o deve essere ancora.  
  
-   La sezione di iteratore definisce si verifica dopo ogni iterazione del corpo del ciclo.  La sezione di iteratore contiene zero o più delle espressioni di istruzione, separati da virgole:  
  
    -   Istruzione di[assegnazione](../../../csharp/language-reference/operators/assignment-operator.md)  
  
    -   chiamata di un metodo  
  
    -   preceduti o aggiungere alla fine dell'espressione [incremento](../../../csharp/language-reference/operators/increment-operator.md), come `++i` o `i++`  
  
    -   preceduti o aggiungere alla fine dell'espressione [decremento](../../../csharp/language-reference/operators/decrement-operator.md), come `--i` o `i--`  
  
    -   creazione di un oggetto utilizzando [new](../../../csharp/language-reference/keywords/new-operator.md)  
  
    -   espressione di[attendere](../../../csharp/language-reference/keywords/await.md)  
  
-   Il corpo del ciclo è costituita da un'istruzione, un'istruzione vuoto, o un blocco di istruzioni, creati racchiudendo zero o più istruzioni tra parentesi graffe.  
  
     È possibile uscire da un ciclo `for` utilizzando la parola chiave [interruzione](../../../csharp/language-reference/keywords/break.md), oppure è possibile passare all'iterazione successiva utilizzando la parola chiave [continuare](../../../csharp/language-reference/keywords/continue.md).  È inoltre possibile uscire dal ciclo utilizzando [di avanzamento](../../../csharp/language-reference/keywords/goto.md), [ritorno](../../../csharp/language-reference/keywords/return.md), l'istruzione o [generare](../../../csharp/language-reference/keywords/throw.md).  
  
 Il primo esempio di questo argomento viene illustrato il tipo più comune del ciclo `for`, che opera le opzioni seguenti per le sezioni.  
  
-   L'inizializzatore dichiara e inizializza una variabile di circuito locale, `i`, che gestisce un conteggio di iterazioni del ciclo.  
  
-   I controlli di condizione il valore della variabile del ciclo in base a un valore finale noto, 5.  
  
-   La sezione di iteratore utilizza un'istruzione di incremento suffisso, `i++`, corrispondente a ogni iterazione del ciclo.  
  
 Nell'esempio seguente vengono illustrate diverse scelte meno comuni: assegnare un valore a una variabile esterna del ciclo nella sezione di inizializzazione, richiamando il metodo `Console.WriteLine` nell'inizializzatore che le sezioni iteratori e modificare i valori di due variabili nella sezione di iteratore.  
  
 [!code-cs[csrefKeywordsIteration#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/for_2.cs)]  
  
 Tutte le espressioni che definiscono un'istruzione `for` sono facoltative.  Ad esempio, l'istruzione seguente viene creato un ciclo infinito.  
  
 [!code-cs[csrefKeywordsIteration#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/for_3.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [foreach, in](../../../csharp/language-reference/keywords/foreach-in.md)   
 [Istruzione for \(C\+\+\)](/visual-cpp/cpp/for-statement-cpp)   
 [Istruzioni di iterazione](../../../csharp/language-reference/keywords/iteration-statements.md)