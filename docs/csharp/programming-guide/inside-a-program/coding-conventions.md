---
title: Convenzioni di codifica C# (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- coding conventions, C#
- Visual C#, coding conventions
- C# language, coding conventions
ms.assetid: f4f60de9-d49b-4fb6-bab1-20e19ea24710
caps.latest.revision: 32
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
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 85e113f66998157a69be3f1d9065a5c4c1117773
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="c-coding-conventions-c-programming-guide"></a>Convenzioni di codifica C# (Guida per programmatori C#)
La [specifica del linguaggio C#](http://go.microsoft.com/fwlink/?LinkId=199552) non definisce uno standard di codifica. Tuttavia, le linee guida riportate in questo argomento vengono usate da Microsoft per sviluppare gli esempi e la documentazione.  
  
 Le convenzioni di codifica hanno gli scopi seguenti:  
  
-   Creano un aspetto coerente per il codice in modo che chi legge possa concentrarsi sul contenuto, non sul layout.  
  
-   Consentono a chi legge di comprendere il codice più rapidamente, formulando presupposti basati sulle esperienze precedenti.  
  
-   Facilitano la copia, la modifica e la gestione del codice.  
  
-   Illustrano procedure consigliate di C#.  
  
## <a name="naming-conventions"></a>Convenzioni di denominazione  
  
-   Negli esempi brevi che non includono [direttive using](../../../csharp/language-reference/keywords/using-directive.md), usare qualifiche dello spazio dei nomi. Se si è certi che uno spazio dei nomi viene importato per impostazione predefinita in un progetto, non è necessario specificare in modo completo i nomi da tale spazio dei nomi. I nomi completi possono essere interrotti dopo un punto (.) se sono troppo lunghi per una singola riga, come illustrato nell'esempio seguente.  
  
     [!code-cs[csProgGuideCodingConventions#1](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_1.cs)]  
  
-   Non è necessario modificare i nomi degli oggetti creati usando gli strumenti di progettazione di Visual Studio per adattarli ad altre linee guida.  
  
## <a name="layout-conventions"></a>Convenzioni di layout  
 Un layout appropriato usa la formattazione per mettere in evidenza la struttura del codice e per facilitare la lettura del codice. Gli esempi Microsoft sono conformi alle convenzioni seguenti:  
  
-   Usare le impostazioni dell'Editor di codice predefinite (rientri intelligenti, rientri di quattro caratteri, tabulazioni salvate come spazi). Per altre informazioni, vedere [Opzioni, Editor di testo, C#, Formattazione](https://docs.microsoft.com/visualstudio/ide/reference/options-text-editor-csharp-formatting).  
  
-   Scrivere una sola istruzione per riga.  
  
-   Scrivere una sola dichiarazione per riga.  
  
-   Se le righe di continuazione non sono rientrate automaticamente, impostare un rientro con un punto di tabulazione (quattro spazi).  
  
-   Aggiungere almeno una riga vuota tra le definizioni di metodo e proprietà.  
  
-   Usare le parentesi per rendere visibili le clausole in un'espressione, come illustrato nel codice seguente.  
  
     [!code-cs[csProgGuideCodingConventions#2](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_2.cs)]  
  
## <a name="commenting-conventions"></a>Convenzioni relative ai commenti  
  
-   Posizionare il commento su una riga separata, non alla fine di una riga di codice.  
  
-   Iniziare il commento con una lettera maiuscola.  
  
-   Terminare il commento con un punto finale.  
  
-   Inserire uno spazio tra i delimitatori di commento (//) e il testo del commento, come illustrato nell'esempio seguente.  
  
     [!code-cs[csProgGuideCodingConventions#3](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_3.cs)]  
  
-   Non creare blocchi formattati di asterischi intorno ai commenti.  
  
## <a name="language-guidelines"></a>Linee guida della lingua  
 Nelle sezioni seguenti vengono descritte le procedure che il team C# deve seguire per preparare campioni ed esempi di codice.  
  
### <a name="string-data-type"></a>Tipo di dati String  
  
-   Usare l'operatore `+` per concatenare stringhe brevi, come illustrato nel codice seguente.  
  
     [!code-cs[csProgGuideCodingConventions#6](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_4.cs)]  
  
-   Per accodare stringhe nei cicli, specialmente quando si lavora con grandi quantità di testo, usare un oggetto <xref:System.Text.StringBuilder>.  
  
     [!code-cs[csProgGuideCodingConventions#7](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_5.cs)]  
  
### <a name="implicitly-typed-local-variables"></a>Variabili locali tipizzate in modo implicito  
  
-   Usare la [tipizzazione implicita](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md) per le variabili locali quando il tipo della variabile è ovvio dal lato destro dell'assegnazione o il tipo preciso non è importante.  
  
     [!code-cs[csProgGuideCodingConventions#8](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_6.cs)]  
  
-   Non usare [var](../../../csharp/language-reference/keywords/var.md) quando il tipo non è evidente dal lato destro dell'assegnazione.  
  
     [!code-cs[csProgGuideCodingConventions#9](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_7.cs)]  
  
-   Non basarsi sul nome della variabile per specificare il tipo della variabile. Potrebbe non essere corretto.  
  
     [!code-cs[csProgGuideCodingConventions#10](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_8.cs)]  
  
-   Evitare l'uso di `var` al posto di [dynamic](../../../csharp/language-reference/keywords/dynamic.md).  
  
-   Usare la tipizzazione implicita per determinare il tipo della variabile del ciclo nei cicli [for](../../../csharp/language-reference/keywords/for.md) e [foreach](../../../csharp/language-reference/keywords/foreach-in.md).  
  
     Nell'esempio seguente viene usata la tipizzazione implicita in un'istruzione `for`.  
  
     [!code-cs[csProgGuideCodingConventions#11](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_9.cs)]  
  
     Nell'esempio seguente viene usata la tipizzazione implicita in un'istruzione `foreach`.  
  
     [!code-cs[csProgGuideCodingConventions#12](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_10.cs)]  
  
### <a name="unsigned-data-type"></a>Tipi di dati non firmati  
  
-   In generale, usare `int` anziché tipi non firmati. L'utilizzo di `int` è comune in C# ed è più facile interagire con altre librerie, quando si usa `int`.  
  
### <a name="arrays"></a>Matrici  
  
-   Usare la sintassi concisa quando si inizializzano le matrici nella riga della dichiarazione.  
  
     [!code-cs[csProgGuideCodingConventions#13](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_11.cs)]  
  
### <a name="delegates"></a>Delegati  
  
-   Usare la sintassi concisa per creare istanze di un tipo delegato.  
  
     [!code-cs[csProgGuideCodingConventions#14](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_12.cs)]  
  
     [!code-cs[csProgGuideCodingConventions#15](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_13.cs)]  
  
### <a name="try-catch-and-using-statements-in-exception-handling"></a>Istruzioni try-catch e using nella gestione delle eccezioni  
  
-   Usare un'istruzione [try-catch](../../../csharp/language-reference/keywords/try-catch.md) per la gestione della maggior parte delle eccezioni.  
  
     [!code-cs[csProgGuideCodingConventions#16](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_14.cs)]  
  
-   Semplificare il codice usando l'[istruzione using](../../../csharp/language-reference/keywords/using-statement.md) di C#. Se si ha un'istruzione [try-finally](../../../csharp/language-reference/keywords/try-finally.md) in cui l'unico codice nel blocco `finally` è una chiamata al metodo <xref:System.IDisposable.Dispose%2A>, usare invece un'istruzione `using`.  
  
     [!code-cs[csProgGuideCodingConventions#17](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_15.cs)]  
  
### <a name="-and-124124-operators"></a>Operatori && e &#124;&#124;  
  
-   Per evitare eccezioni e migliorare le prestazioni ignorando i confronti non necessari, usare [&&](../../../csharp/language-reference/operators/conditional-and-operator.md) invece di [&](../../../csharp/language-reference/operators/and-operator.md) e [&#124;&#124;](../../../csharp/language-reference/operators/conditional-or-operator.md) invece di [&#124;](../../../csharp/language-reference/operators/or-operator.md) quando si eseguono confronti, come illustrato nell'esempio seguente.  
  
     [!code-cs[csProgGuideCodingConventions#18](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_16.cs)]  
  
### <a name="new-operator"></a>Operatore New  
  
-   Usare il modulo conciso della creazione dell'istanza di oggetto, con la tipizzazione implicita, come illustrato nella dichiarazione seguente.  
  
     [!code-cs[csProgGuideCodingConventions#19](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_17.cs)]  
  
     La riga precedente è equivalente alla dichiarazione seguente.  
  
     [!code-cs[csProgGuideCodingConventions#20](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_18.cs)]  
  
-   Usare gli inizializzatori di oggetto per semplificare la creazione di un oggetto.  
  
     [!code-cs[csProgGuideCodingConventions#21](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_19.cs)]  
  
### <a name="event-handling"></a>Gestione di eventi  
  
-   Se si definisce un gestore eventi che non è necessario rimuovere successivamente, usare un'espressione lambda.  
  
     [!code-cs[csProgGuideCodingConventions#22](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_20.cs)]  
  
     [!code-cs[csProgGuideCodingConventions#23](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_21.cs)]  
  
### <a name="static-members"></a>Membri static  
  
-   Chiamare i membri [static](../../../csharp/language-reference/keywords/static.md) usando il nome della classe: *ClassName.StaticMember*. Questa pratica rende più leggibile il codice semplificando l'accesso statico.  Non qualificare un membro statico definito in una classe base con il nome di una classe derivata.  Nonostante il codice venga compilato, la leggibilità del codice è fuorviante mentre il codice potrebbe essere interrotto in futuro, se si aggiunge un membro statico con lo stesso nome alla classe derivata.  
  
### <a name="linq-queries"></a>Query LINQ  
  
-   Usare nomi significativi per le variabili di query. Nell'esempio seguente viene usato `seattleCustomers` per i clienti che si trovano a Seattle.  
  
     [!code-cs[csProgGuideCodingConventions#25](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_22.cs)]  
  
-   Usare gli alias per assicurarsi che i nomi delle proprietà di tipi anonimi siano scritti correttamente in maiuscolo, usando la convenzione Pascal.  
  
     [!code-cs[csProgGuideCodingConventions#26](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_23.cs)]  
  
-   Rinominare le proprietà quando i nomi delle proprietà nel risultato potrebbero risultare ambigui. Ad esempio, se la query restituisce un nome cliente un ID del server di distribuzione, anziché lasciarli come `Name` e `ID` nei risultati, rinominarli per spiegare che `Name` è il nome di un cliente e `ID` è l'ID di un server di distribuzione.  
  
     [!code-cs[csProgGuideCodingConventions#27](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_24.cs)]  
  
-   Usare la tipizzazione implicita nella dichiarazione di variabili di query e variabili di intervallo.  
  
     [!code-cs[csProgGuideCodingConventions#25](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_22.cs)]  
  
-   Allineare le clausole di query sotto la clausola [from](../../../csharp/language-reference/keywords/from-clause.md), come illustrato negli esempi precedenti.  
  
-   Usare le clausole [where](../../../csharp/language-reference/keywords/where-clause.md) prima delle altre clausole di query, per garantire che le clausole di query successive agiscano su un set di dati ridotto e filtrato.  
  
     [!code-cs[csProgGuideCodingConventions#29](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_25.cs)]  
  
-   Usare più clausole `from` invece di una clausola [join](../../../csharp/language-reference/keywords/join-clause.md) per accedere a raccolte interne. Ad esempio, ogni raccolta di oggetti `Student` potrebbe contenere una raccolta di punteggi del test. Quando viene eseguita la query seguente, viene restituito ogni punteggio superiore a 90, e il cognome dello studente che ha ricevuto il punteggio.  
  
     [!code-cs[csProgGuideCodingConventions#30](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/coding-conventions_26.cs)]  
  
## <a name="security"></a>Sicurezza  
 Seguire le indicazioni in [Linee guida per la generazione di codice sicuro](../../../standard/security/secure-coding-guidelines.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Convenzioni di codifica di Visual Basic](../../../visual-basic/programming-guide/program-structure/coding-conventions.md)   
 [Linee guida per la generazione di codice sicuro](../../../standard/security/secure-coding-guidelines.md)
