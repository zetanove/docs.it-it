---
title: "Variabili locali tipizzate in modo implicito (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "variabili locali tipizzate in modo implicito [C#]"
  - "var [C#]"
ms.assetid: b9218fb2-ef5d-4814-8a8e-2bc29b0bbc9b
caps.latest.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 23
---
# Variabili locali tipizzate in modo implicito (Guida per programmatori C#)
Alle variabili locali può essere fornite un "tipo" dedotto di `var` anziché un tipo esplicito.  La parola chiave `var` indica al compilatore di dedurre il tipo della variabile dall'espressione sul lato destro dell'istruzione di inizializzazione.  Il tipo dedotto può essere un tipo incorporato, un tipo anonimo, un tipo definito dall'utente o un tipo definito nella libreria di classi .NET Framework.  Per ulteriori informazioni su come inizializzare matrici con `var`, vedere [Matrici tipizzate in modo implicito](../../../csharp/programming-guide/arrays/implicitly-typed-arrays.md).  
  
 Negli esempi seguenti sono illustrati svariati modi con cui le variabili locali possono essere dichiarate con `var`:  
  
 [!code-cs[csProgGuideLINQ#43](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csRef30LangFeatures_2.cs#43)]  
  
 È importante comprendere che la parola chiave `var` non significa "variant" e che non indica che la variabile è debolmente tipizzata o è ad associazione tardiva.  Significa semplicemente che il compilatore determina e assegna il tipo più adatto.  
  
 È possibile utilizzare la parola chiave `var` nei seguenti contesti:  
  
-   Su variabili locali \(variabili dichiarate nell'ambito del metodo\) come illustrato nell'esempio precedente.  
  
-   In un'istruzione di inizializzazione [for](../../../csharp/language-reference/keywords/for.md).  
  
    ```  
    for(var x = 1; x < 10; x++)  
    ```  
  
-   In un'istruzione di inizializzazione [foreach](../../../csharp/language-reference/keywords/foreach-in.md).  
  
    ```  
    foreach(var item in list){...}  
    ```  
  
-   In un'istruzione [using](../../../csharp/language-reference/keywords/using-statement.md).  
  
    ```  
    using (var file = new StreamReader("C:\\myfile.txt")) {...}  
    ```  
  
 Per ulteriori informazioni, vedere [Procedura: utilizzare variabili e matrici locali tipizzate in modo implicito in un'espressione di query](../../../csharp/programming-guide/classes-and-structs/how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression.md).  
  
## var e tipi anonimi  
 In molti casi l'utilizzo di `var` è facoltativo ed è solo una convenzione sintattica.  Tuttavia, quando una variabile viene inizializzata con un tipo anonimo è necessario dichiararla come `var`, se si deve accedere alle proprietà dell'oggetto in un momento successivo.  Si tratta di uno scenario comune nelle espressioni di query [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)].  Per ulteriori informazioni, vedere [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md).  
  
 Dalla prospettiva del codice sorgente, un tipo anonimo non dispone di nome.  Se una variabile di query è stata inizializzata con `var`, l’unico modo per accedere alle proprietà nella sequenza di oggetti restituita è utilizzare `var` come tipo della variabile di iterazione nell’istruzione `foreach`.  
  
 [!code-cs[csProgGuideLINQ#44](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csRef30LangFeatures_2.cs#44)]  
  
## Note  
 Le restrizioni seguenti si applicano alle dichiarazioni di variabili tipizzate in modo implicito:  
  
-   `var` può essere utilizzata solo quando una variabile locale viene dichiarata e inizializzata nella stessa istruzione. La variabile non può essere inizializzata su null, su un gruppo di metodi o una funzione anonima.  
  
-   Non è possibile utilizzare `var` nei campi nell'ambito della classe.  
  
-   Le variabili dichiarate utilizzando `var` non possono essere utilizzate nell'espressione di inizializzazione.  In altre parole, questa espressione è valida`: int i = (i = 20);` ma produce un errore in fase di compilazione: `var i = (i = 20);`  
  
-   Non è possibile inizializzare più variabili tipizzate in modo implicito nella stessa istruzione.  
  
-   Se un tipo denominato `var` rientra nell’ambito, la parola chiave `var` risolverà in tale nome di tipo e non verrà trattata come parte di una dichiarazione di variabile locale tipizzata in modo implicito.  
  
 `var` può inoltre risultare utile con le espressioni di query in cui è difficile determinare con esattezza il tipo costruito della variabile della query,  ad esempio con il raggruppamento e l'ordinamento di operazioni.  
  
 La parola chiave `var` può essere utile anche quando il tipo specifico della variabile risulta difficile da digitare con la tastiera, è ovvio o non migliora la leggibilità del codice.  `var` è utile in tal senso ad esempio con i tipi generici annidati, quali quelli utilizzati con le operazioni di gruppo.  Nella query seguente, il tipo della variabile della query è `IEnumerable<IGrouping<string, Student>>`.  Purché ciò sia chiaro a tutti coloro che devono gestire il codice, l'utilizzo della tipizzazione implicita per ragioni di praticità e brevità non costituisce un problema.  
  
 [!code-cs[cscsrefQueryKeywords#13](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Group.cs#13)]  
  
 L'utilizzo di `var`, tuttavia, può quanto meno rendere più difficoltosa la comprensione del codice per gli altri sviluppatori.  Nella documentazione di C\# `var` viene pertanto in genere utilizzata solo quando è necessario.  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Matrici tipizzate in modo implicito](../../../csharp/programming-guide/arrays/implicitly-typed-arrays.md)   
 [Procedura: utilizzare variabili e matrici locali tipizzate in modo implicito in un'espressione di query](../../../csharp/programming-guide/classes-and-structs/how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression.md)   
 [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [Inizializzatori di oggetto e di raccolta](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)   
 [var](../../../csharp/language-reference/keywords/var.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [for](../../../csharp/language-reference/keywords/for.md)   
 [foreach, in](../../../csharp/language-reference/keywords/foreach-in.md)   
 [Istruzione using](../../../csharp/language-reference/keywords/using-statement.md)