---
title: "Cast e conversioni di tipi (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "cast [C#]"
  - "conversioni [C#], tipo"
  - "conversione di tipi [C#]"
  - "conversione di tipi di dati [C#]"
  - "conversioni numeriche [C#]"
  - "conversione di tipi [C#]"
ms.assetid: 568df58a-d292-4b55-93ba-601578722878
caps.latest.revision: 52
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 52
---
# Cast e conversioni di tipi (Guida per programmatori C#)
Poiché il codice C\# viene tipizzato in modo statico in fase di compilazione, una variabile dichiarata non può essere nuovamente dichiarata o utilizzata per archiviare valori di un altro tipo a meno che il tipo non sia convertibile nel tipo della variabile.  Ad esempio, non esiste alcuna conversione da un intero a una stringa arbitraria.  Pertanto, dopo avere dichiarato `i` come intero, non è possibile assegnare a esso la stringa "Hello", come mostrato nel codice seguente.  
  
```c#  
int i;  
i = "Hello"; // Error: "Cannot implicitly convert type 'string' to 'int'"  
```  
  
 Tuttavia, copiare un valore in una variabile o in un parametro di metodo di un altro tipo potrebbe essere talvolta necessario.  Ad esempio, è possibile che si disponga di una variabile integer che è necessario passare a un metodo il cui parametro è tipizzato come `double` oppure che sia necessario assegnare una variabile di classe a una variabile di un tipo di interfaccia.  Questi tipi di operazioni sono detti *conversioni di tipi*.  In C\#, è possibile eseguire i tipi di conversioni seguenti:  
  
-   **Conversioni implicite**: non è richiesta alcuna sintassi speciale perché la conversione è indipendente dai tipi e nessun dato viene perso.  Gli esempi includono le conversioni da tipi integrali più piccoli a più grandi e le conversioni da classi derivate a classi di base.  
  
-   **Conversioni esplicite \(cast\)**: le conversioni esplicite richiedono un operatore di cast.  Il cast è obbligatoria quando le informazioni potrebbero andare perdute durante la conversione o quando la conversione potrebbe non riuscire per altri motivi. Gli esempi tipici includono la conversione numerica in un tipo con meno precisione o un intervallo più piccolo e la conversione di un'istanza di una classe base in una classe derivata.  
  
-   **Conversioni definite dall'utente**: le conversioni definite dall'utente vengono eseguite da metodi speciali che è possibile definire per attivare le conversioni esplicite e implicite fra tipi personalizzati privi di relazione classe di base\-classe derivata.  Per ulteriori informazioni, vedere [Operatori di conversione](../../../csharp/programming-guide/statements-expressions-operators/conversion-operators.md).  
  
-   **Conversioni con le classi di supporto**: per eseguire la conversione tra tipi non compatibili, ad esempio numeri interi e oggetti <xref:System.DateTime?displayProperty=fullName> o stringhe esadecimali e matrici di byte, è possibile utilizzare la classe <xref:System.BitConverter?displayProperty=fullName>, la classe <xref:System.Convert?displayProperty=fullName> e i metodi `Parse` dei tipi numerici incorporati, ad esempio <xref:System.Int32.Parse%2A?displayProperty=fullName>.  Per ulteriori informazioni, vedere [Procedura: convertire una matrice di byte in un Integer](../../../csharp/programming-guide/types/how-to-convert-a-byte-array-to-an-int.md), [Procedura: convertire una stringa in un numero](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md) e [Procedura: eseguire la conversione tra stringhe esadecimali e tipi numerici](../../../csharp/programming-guide/types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md).  
  
## Conversioni implicite  
 Per i tipi numerici incorporati, una conversione implicita può essere eseguita quando il valore da archiviare può essere adattato alla variabile senza essere troncato o arrotondato.  Ad esempio, una variabile di tipo [long](../../../csharp/language-reference/keywords/long.md) \(intero a 8 byte\) è in grado di archiviare qualsiasi valore archiviabile in un tipo [int](../../../csharp/language-reference/keywords/int.md) \(4 byte su un computer a 32 bit\).  Nell'esempio seguente, il compilatore converte implicitamente il valore a destra in un tipo `long` prima di assegnarlo a `bigNum`.  
  
 [!code-cs[csProgGuideTypes#34](../../../csharp/programming-guide/nullable-types/codesnippet/csharp/casting-and-type-convers_1.cs)]  
  
 Per un elenco completo delle conversioni numeriche implicite, vedere [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
 Per i tipi riferimento, esiste sempre una conversione implicita da una classe a una delle relative classi di base o interfacce dirette o indirette.  Non è necessaria alcuna sintassi speciale perché una classe derivata contiene sempre tutti i membri di una classe di base.  
  
```  
Derived d = new Derived();  
Base b = d; // Always OK.  
```  
  
## Conversioni esplicite  
 Tuttavia, se una conversione non può essere eseguita senza un rischio di perdita di informazioni, il compilatore richiede che si esegua una conversione esplicita, chiamata *cast*.  Il cast è un modo di informare in modo esplicito il compilatore che si intende eseguire la conversione e che si è consapevoli che potrebbe verificarsi una perdita di dati.  Per eseguire un cast, specificare il tipo di destinazione del cast in parentesi davanti al valore o alla variabile da convertire.  Il seguente programma esegue il cast di [double](../../../csharp/language-reference/keywords/double.md) su [int](../../../csharp/language-reference/keywords/int.md).  Se il cast non è presente, il programma non verrà compilato.  
  
 [!code-cs[csProgGuideTypes#2](../../../csharp/programming-guide/nullable-types/codesnippet/csharp/casting-and-type-convers_2.cs)]  
  
 Per un elenco delle conversioni numeriche esplicite consentite, vedere [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md).  
  
 Per i tipi riferimento, un cast esplicito è richiesto se è necessario eseguire la conversione da un tipo di base a un tipo derivato:  
  
```c#  
// Create a new derived type.  
Giraffe g = new Giraffe();  
  
// Implicit conversion to base type is safe.  
Animal a = g;  
  
// Explicit conversion is required to cast back  
// to derived type. Note: This will compile but will  
// throw an exception at run time if the right-side  
// object is not in fact a Giraffe.  
Giraffe g2 = (Giraffe) a;  
```  
  
 Un'operazione cast tra tipi riferimento non modifica il tipo in fase di esecuzione dell'oggetto sottostante, ma modifica solo il tipo del valore utilizzato come riferimento a tale oggetto.  Per ulteriori informazioni, vedere [Polimorfismo](../../../csharp/programming-guide/classes-and-structs/polymorphism.md).  
  
## Eccezioni di conversione di tipi in fase di esecuzione  
 In alcune conversioni di tipi riferimento, il compilatore non è in grado di determinare se un cast sarà valido.  È possibile che un'operazione di cast compilata correttamente non riesca in fase di esecuzione.  Come mostrato nell'esempio seguente, un cast di tipo che non riesce in fase di esecuzione provoca la generazione di <xref:System.InvalidCastException>.  
  
 [!code-cs[csProgGuideTypes#41](../../../csharp/programming-guide/nullable-types/codesnippet/csharp/casting-and-type-convers_3.cs)]  
  
 Il linguaggio C\# fornisce gli operatori [is](../../../csharp/language-reference/keywords/is.md) e [as](../../../csharp/language-reference/keywords/as.md) per consentire di verificare la compatibilità prima di eseguire un cast.  Per ulteriori informazioni, vedere [Procedura: eseguire il cast sicuro tramite gli operatori as e is](../../../csharp/programming-guide/types/how-to-safely-cast-by-using-as-and-is-operators.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Capitoli del libro rappresentati  
 [Ulteriori informazioni sulle variabili](http://go.microsoft.com/fwlink/?LinkId=221230) in [Visual c\# 2010 iniziale](http://go.microsoft.com/fwlink/?LinkId=221214)  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tipi](../../../csharp/programming-guide/types/index.md)   
 [Operatore \(\)](../../../csharp/language-reference/operators/invocation-operator.md)   
 [esplicita](../../../csharp/language-reference/keywords/explicit.md)   
 [impliciti](../../../csharp/language-reference/keywords/implicit.md)   
 [Operatori di conversione](../../../csharp/programming-guide/statements-expressions-operators/conversion-operators.md)   
 [Generalized Type Conversion](../Topic/Generalized%20Type%20Conversion.md)   
 [Exported Type Conversion](http://msdn.microsoft.com/it-it/1dfe55f4-07a2-4b61-aabf-a8cf65783a6b)   
 [Procedura: convertire una stringa in un numero](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md)