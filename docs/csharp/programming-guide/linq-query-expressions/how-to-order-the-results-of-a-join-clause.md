---
redirect_url: /dotnet/articles/csharp/linq/order-the-results-of-a-join-clause
caps.handback.revision: 6
---
# Procedura: ordinare i risultati di una clausola join (Guida per programmatori C#)
In questo esempio viene illustrato come ordinare i risultati di un'operazione di join.  Notare che l'ordinamento viene eseguito dopo l'operazione di join.  In genere, sebbene sia possibile, non è consigliabile utilizzare la clausola `orderby` con una o più sequenze di origine prima dell'operazione join.  Alcuni provider [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] potrebbero non mantenere tale ordinamento dopo l'operazione join.  
  
## Esempio  
 Questa query crea un join di gruppo e quindi ordina i gruppi in base all'elemento categoria che è ancora nell'ambito.  Nell'inizializzatore di tipi anonimi una sottoquery ordina tutti gli elementi corrispondenti della sequenza di prodotti.  
  
 [!code-cs[csProgGuideLINQ#81](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-order-the-results-of-a-join-clause_1.cs)]  
  
## Compilazione del codice  
  
-   Creare un progetto [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)] per .NET Framework versione 3.5.  Per impostazione predefinita, il progetto include un riferimento a System.Core.dll e una direttiva `using` per lo spazio dei nomi System.Linq.  
  
-   Copiare il codice nel progetto.  
  
-   Premere F5 per compilare ed eseguire il programma.  
  
-   Premere un tasto per chiudere la finestra della console.  
  
## Vedere anche  
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Clausola orderby](../../../csharp/language-reference/keywords/orderby-clause.md)   
 [Clausola join](../../../csharp/language-reference/keywords/join-clause.md)   
 [Join Operations](../../../visual-basic/programming-guide/concepts/linq/join-operations.md)