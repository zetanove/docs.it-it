---
title: "Istruzioni (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, istruzioni"
  - "istruzioni [C#], informazioni"
ms.assetid: 901bcde7-87de-4e15-833c-f9cfd40c8ce3
caps.latest.revision: 28
caps.handback.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Istruzioni (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Le azioni eseguite dal programma vengono espresse nelle istruzioni.  Azioni comuni includono: dichiarazioni di variabili, assegnazione di valori, chiamate di metodi, scorrimento in ciclo di raccolte e creazione di rami su uno o un altro blocco di codice, a seconda di una condizione specificata.  L'ordine in cui le istruzioni vengono eseguite in un programma, viene chiamato: flusso di controllo o flusso di esecuzione.  Il flusso di controllo può variare ogni volta che viene eseguito un programma, a seconda di come il programma reagisce agli input ricevuti in fase di esecuzione.  
  
 Un'istruzione può essere costituita da una sola riga di codice che termina in un punto e virgola o da una serie di istruzioni a riga singola in un blocco.  Un blocco di istruzioni è racchiuso fra parentesi {} e può contenere blocchi annidati.  Nel codice seguente vengono mostrati due esempi di istruzioni a riga singola e un blocco di istruzioni su più righe:  
  
 [!code-cs[csProgGuideStatements#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_1.cs)]  
  
## Tipi di istruzioni  
 Nella tabella seguente vengono elencati i vari tipi di istruzioni in C\# e le parole chiave associate, con i collegamenti ad argomenti che includono ulteriori informazioni:  
  
|Category|Parole chiave C\# \/ note|  
|--------------|-------------------------------|  
|Istruzioni di dichiarazione|Un'istruzione di dichiarazione introduce una nuova variabile o costante.  Una dichiarazione di variabile può facoltativamente assegnare un valore alla variabile stessa.  In una dichiarazione di costante, l'assegnazione è obbligatoria.<br /><br /> [!code-cs[csProgGuideStatements#23](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_2.cs)]|  
|Istruzioni di espressione|Le istruzioni di espressione che calcolano un valore, devono memorizzare tale valore in una variabile.<br /><br /> [!code-cs[csProgGuideStatements#24](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_3.cs)]|  
|[Istruzioni di selezione](../../../csharp/language-reference/keywords/selection-statements.md)|Le istruzioni di selezione consentono di creare un ramo a sezioni diverse di codice, in base a una o più condizioni specifiche.  Per ulteriori informazioni, vedere i seguenti argomenti:<br /><br /> [if](../../../csharp/language-reference/keywords/if-else.md), [else](../../../csharp/language-reference/keywords/if-else.md), [switch](../../../csharp/language-reference/keywords/switch.md), [case](../../../csharp/language-reference/keywords/switch.md)|  
|[Istruzioni di iterazione](../../../csharp/language-reference/keywords/iteration-statements.md)|Le istruzioni di iterazione consentono di eseguire un ciclo in raccolte come matrici, o di eseguire ripetutamente lo stesso insieme di istruzioni fino a che non è stata soddisfatta una condizione specificata.  Per ulteriori informazioni, vedere i seguenti argomenti:<br /><br /> [do](../../../csharp/language-reference/keywords/do.md), [for](../../../csharp/language-reference/keywords/for.md), [foreach](../../../csharp/language-reference/keywords/foreach-in.md), [in](../../../csharp/language-reference/keywords/foreach-in.md), [while](../../../csharp/language-reference/keywords/while.md)|  
|[Istruzioni di spostamento](../../../csharp/language-reference/keywords/jump-statements.md)|Le istruzioni di spostamento trasferiscono il controllo a un'altra sezione di codice.  Per ulteriori informazioni, vedere i seguenti argomenti:<br /><br /> [break](../../../csharp/language-reference/keywords/break.md), [continue](../../../csharp/language-reference/keywords/continue.md), [default](../../../csharp/language-reference/keywords/switch.md), [goto](../../../csharp/language-reference/keywords/goto.md), [return](../../../csharp/language-reference/keywords/return.md), [yield](../../../csharp/language-reference/keywords/yield.md)|  
|[Istruzioni di gestione delle eccezioni](../../../csharp/language-reference/keywords/exception-handling-statements.md)|Le istruzioni di gestione delle eccezioni consentono all'applicazione di rispondere correttamente a condizioni eccezionali verificatesi in fase di esecuzione.  Per ulteriori informazioni, vedere i seguenti argomenti:<br /><br /> [throw](../../../csharp/language-reference/keywords/throw.md), [try\-catch](../../../csharp/language-reference/keywords/try-catch.md), [try\-finally](../../../csharp/language-reference/keywords/try-finally.md), [try\-catch\-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)|  
|[Istruzioni checked e unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md)|Le istruzioni checked e unchecked consentono di specificare se le operazioni numeriche possono provocare un overflow quando il risultato viene memorizzato in una variabile troppo piccola per contenere il valore risultante.  Per ulteriori informazioni, vedere [checked](../../../csharp/language-reference/keywords/checked.md) e [unchecked](../../../csharp/language-reference/keywords/unchecked.md).|  
|Istruzione `await`.|Se si contrassegna un metodo con il modificatore [async](../../../csharp/language-reference/keywords/async.md), è possibile utilizzare l'operatore [attendere](../../../csharp/language-reference/keywords/await.md) nel metodo.  Quando il controllo raggiunge un'espressione `await` nel metodo async, il controllo torna il chiamante e lo stato di avanzamento nel metodo viene sospeso finché l'attività attesa non completi.  Quando l'attività è stata completata, l'esecuzione può riattivare il metodo.<br /><br /> Per un esempio, vedere la sezione “metodi di Async„ [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md).  Per ulteriori informazioni, vedere [Programmazione asincrona con Async e Await](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md).|  
|Istruzione `yield return`.|Un iteratore esegue un'iterazione personalizzata in una raccolta, come un elenco o una matrice.  Un iteratore utilizza l'istruzione [prestazioni](../../../csharp/language-reference/keywords/yield.md) per restituire ogni elemento uno alla volta.  Quando un'istruzione `yield return` viene raggiunto, la posizione corrente nel codice viene memorizzata.  L'esecuzione viene riavviata da quella posizione all'iteratore verrà chiamato alla successiva.<br /><br /> Per ulteriori informazioni, vedere [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md).|  
|Istruzione `fixed`.|L'istruzione fixed impedisce che il Garbage Collector esegua la rilocazione di una variabile mobile.  Per ulteriori informazioni, vedere [fixed](../../../csharp/language-reference/keywords/fixed-statement.md).|  
|Istruzione `lock`.|L'istruzione lock consente di limitare l'accesso a blocchi di codice a un solo thread alla volta.  Per ulteriori informazioni, vedere [lock](../../../csharp/language-reference/keywords/lock-statement.md).|  
|Istruzioni con etichetta|È possibile assegnare un'etichetta a un'istruzione e utilizzare quindi la parola chiave [goto](../../../csharp/language-reference/keywords/goto.md) per passare all'istruzione con etichetta.  \(Vedere l'esempio nella riga seguente\).|  
|Istruzione vuota|L'istruzione vuota è costituita da un solo punto e virgola.  Non esegue alcuna operazione e può essere utilizzata dove è richiesta un'istruzione ma non deve essere eseguita alcuna azione.  Negli esempi seguenti vengono illustrati due utilizzi per un'istruzione vuota:<br /><br /> [!code-cs[csProgGuideStatements#25](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_4.cs)]|  
  
## Istruzioni incorporate  
 Alcune istruzioni, fra cui [do](../../../csharp/language-reference/keywords/do.md), [while](../../../csharp/language-reference/keywords/while.md), [for](../../../csharp/language-reference/keywords/for.md) e [foreach](../../../csharp/language-reference/keywords/foreach-in.md), sono sempre seguite da un'istruzione incorporata.  Questa istruzione incorporata può essere costituita da una sola istruzione o da più istruzioni racchiuse fra parentesi {} in un blocco di istruzioni.  Anche le istruzioni incorporate a riga singola possono essere racchiuse fra parentesi {}, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideStatements#26](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_5.cs)]  
  
 Un'istruzione incorporata non racchiusa tra parentesi {} non può essere un'istruzione di dichiarazione o un'istruzione con etichetta,  come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideStatements#27](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_6.cs)]  
  
 Inserire l'istruzione incorporata in un blocco per correggere l'errore:  
  
 [!code-cs[csProgGuideStatements#28](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_7.cs)]  
  
## Blocchi di istruzioni annidati  
 I blocchi di istruzioni possono essere annidati, come illustrato nel codice seguente:  
  
 [!code-cs[csProgGuideStatements#29](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_8.cs)]  
  
## Istruzioni non eseguibili  
 Se il compilatore determina che il flusso del controllo non può raggiungere mai una particolare istruzione in qualsiasi circostanza, produrrà l'avviso CS0162, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideStatements#22](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/statements_9.cs)]  
  
## Sezioni correlate  
  
-   [Parole chiave per le istruzioni](../../../csharp/language-reference/keywords/statement-keywords.md)  
  
-   [Espressioni](../../../csharp/programming-guide/statements-expressions-operators/expressions.md)  
  
-   [Operatori](../../../csharp/programming-guide/statements-expressions-operators/operators.md)  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)