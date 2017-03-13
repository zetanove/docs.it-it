---
redirect_url: /dotnet/articles/csharp/programming-guide/main-and-command-args/
caps.handback.revision: 30
---
# Main() e argomenti della riga di comando (Guida per programmatori C#)
Il metodo  `Main` costituisce il punto di ingresso di un'applicazione console C\# o di un'applicazione Windows.  Librerie e servizi non richiedono un metodo `Main` come punto di ingresso.  All'avvio dell'applicazione, `Main` è il primo metodo richiamato.  
  
 In un programma C\# può esistere un solo punto di ingresso.  Se si dispone di più di una classe con un metodo `Main`, è necessario compilare il programma con l'opzione del compilatore **\/main** per specificare quale metodo `Main` per utilizzare come punto di ingresso.  Per ulteriori informazioni, vedere la classe [\/main \(Specify Location of Main Method\)](../../../csharp/language-reference/compiler-options/main-compiler-option.md).  
  
 [!code-cs[csProgGuideMain#17](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/main-and-command-line-arguments_1.cs)]  
  
## Panoramica  
  
-   Il metodo `Main` è il punto di ingresso di un programma EXE, ovvero il punto in cui il controllo del programma inizia e termina.  
  
-   `Main` viene dichiarato all'interno di una classe o di uno struct.  `Main` deve essere [statico](../../../csharp/language-reference/keywords/static.md) e non deve essere [pubblico](../../../csharp/language-reference/keywords/public.md).  Nell'esempio precedente, riceve l'accesso predefinito di [privato](../../../csharp/language-reference/keywords/private.md).\) Non è necessario che la classe o la struttura che lo contiene sia statica.  
  
-   `Main` può avere un tipo restituito `void` o `int`.  
  
-   Il metodo `Main` può essere dichiarato con o senza un parametro `string[]` contenente gli argomenti della riga di comando.  Quando si utilizza [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] per creare applicazioni Windows Form, è possibile aggiungere il parametro manualmente o utilizzare la classe <xref:System.Environment> per ottenere gli argomenti della riga di comando.  I parametri vengono letti come argomenti della riga di comando a indice zero. Diversamente da c e C\+\+, il nome del programma non viene considerato il primo argomento della riga di comando.  
  
## Argomenti della sezione  
  
-   [Argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/command-line-arguments.md)  
  
-   [Procedura: visualizzare gli argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)  
  
-   [Procedura: accedere agli argomenti della riga di comando utilizzando foreach](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)  
  
-   [Valori restituiti da Main\(\)](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Command\-line Building With csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [Contenuto di un programma C\#](../../../csharp/programming-guide/inside-a-program/index.md)   
 [\<paveover\>C\# Sample Applications](http://msdn.microsoft.com/it-it/9a9d7aaa-51d3-4224-b564-95409b0f3e15)