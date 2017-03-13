---
redirect_url: /dotnet/articles/csharp/programming-guide/exceptions/
caps.handback.revision: 33
---
# Eccezioni e gestione delle eccezioni (Guida per programmatori C#)
Le funzionalità di gestione delle eccezioni del linguaggio C\# consentono di gestire situazioni impreviste o eccezionali che si verificano durante l'esecuzione di un programma.  Nella gestione delle eccezioni vengono utilizzate le parole chiave `try`, `catch` e `finally` per tentare di eseguire azioni che potrebbero non riuscire, per gestire gli errori quando lo si ritiene opportuno e per pulire successivamente le risorse.  Le eccezioni possono essere generate da Common Language Runtime \(CLR\), da librerie .NET Framework o di altri produttori o dal codice dell'applicazione.  Le eccezioni vengono create tramite la parola chiave `throw`.  
  
 In molti casi, un'eccezione può essere generata non da un metodo chiamato direttamente dal codice, ma da un altro metodo più in basso nello stack di chiamate.  In questa situazione, CLR rimuoverà lo stack, alla ricerca di un metodo con un blocco `catch` per il tipo di eccezione specifico ed eseguirà il primo blocco `catch` di questo tipo trovato.  Se non trova un blocco `catch` appropriato nello stack di chiamate, terminerà il processo e visualizzerà un messaggio all'utente.  
  
 In questo esempio un metodo verifica la presenza di una divisione per zero e rileva l'errore.  Senza la gestione delle eccezioni, il programma verrebbe chiuso con un errore simile al seguente: **DivideByZeroException non è stata gestita**.  
  
 [!code-cs[csProgGuideExceptions#18](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/exceptions-and-exception-handling_1.cs)]  
  
## Cenni preliminari sulle eccezioni  
 Le eccezioni dispongono delle seguenti proprietà:  
  
-   Le eccezioni sono tipi che derivano tutti da `System.Exception`.  
  
-   Utilizzare un blocco `try` intorno alle istruzioni che potrebbero generare eccezioni.  
  
-   Quando si verifica un'eccezione nel blocco `try`, il flusso di controllo passa al primo gestore eccezioni associato presente in qualsiasi punto dello stack di chiamate.  Per la definizione di un gestore eccezioni, in C\# viene utilizzata la parola chiave `catch`.  
  
-   Se per una determinata eccezione non sono presenti gestori, l'esecuzione del programma verrà interrotta con un messaggio di errore.  
  
-   Non rilevare un'eccezione a meno che non sia possibile gestirla e lasciare l'applicazione in uno stato conosciuto.  Se si rileva `System.Exception`, effettuarne una nuova generazione utilizzando la parola chiave `throw` alla fine del blocco `catch`.  
  
-   Se un blocco `catch` definisce una variabile di eccezione, è possibile utilizzarla per ottenere ulteriori informazioni sul tipo di eccezione che si è verificata.  
  
-   Le eccezioni possono essere generate in modo esplicito da un programma mediante la parola chiave `throw`.  
  
-   Gli oggetti eccezione contengono informazioni dettagliate sull'errore, ad esempio lo stato dello stack di chiamate e una descrizione dell'errore.  
  
-   Il codice in un blocco `finally` viene eseguito anche se viene generata un'eccezione.  Utilizzare un blocco `finally` per rilasciare risorse, ad esempio per chiudere qualsiasi flusso o file aperto nel blocco `try`.  
  
-   Le eccezioni gestite in .NET Framework vengono implementate nel meccanismo di gestione delle eccezioni strutturata in Win32.  Per ulteriori informazioni, vedere [Gestione strutturata delle eccezioni](/visual-cpp/cpp/structured-exception-handling-c-cpp) e [A Crash Course on the Depths of Win32 Structured Exception Handling](http://go.microsoft.com/fwlink/?LinkId=119654) \(il contenuto potrebbe essere in inglese\).  
  
## Sezioni correlate  
 Per ulteriori informazioni sulle eccezioni e sulla relativa gestione, vedere i seguenti argomenti:  
  
-   [Utilizzo di eccezioni](../../../csharp/programming-guide/exceptions/using-exceptions.md)  
  
-   [Gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exception-handling.md)  
  
-   [Creazione e generazione di eccezioni](../../../csharp/programming-guide/exceptions/creating-and-throwing-exceptions.md)  
  
-   [Eccezioni generate dal compilatore](../../../csharp/programming-guide/exceptions/compiler-generated-exceptions.md)  
  
-   [Procedura: gestire un'eccezione utilizzando Try\/Catch](../../../csharp/programming-guide/exceptions/how-to-handle-an-exception-using-try-catch.md)  
  
-   [Procedura: eseguire codice di pulitura mediante finally](../../../csharp/programming-guide/exceptions/how-to-execute-cleanup-code-using-finally.md)  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 <xref:System.SystemException>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [throw](../../../csharp/language-reference/keywords/throw.md)   
 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [try...finally](../../../csharp/language-reference/keywords/try-finally.md)   
 [try...catch...finally](../../../csharp/language-reference/keywords/try-catch-finally.md)   
 [Eccezioni](../Topic/Handling%20and%20Throwing%20Exceptions.md)   
 [Gerarchia delle eccezioni](../Topic/Exception%20Hierarchy.md)   
 [Scrittura di codice affidabile .NET](http://go.microsoft.com/fwlink/?LinkId=112400)   
 [minidump per le eccezioni specifiche](http://go.microsoft.com/fwlink/?LinkId=112408)