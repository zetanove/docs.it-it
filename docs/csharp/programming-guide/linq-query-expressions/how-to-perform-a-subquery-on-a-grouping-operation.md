---
redirect_url: /dotnet/articles/csharp/linq/perform-a-subquery-on-a-grouping-operation
caps.handback.revision: 15
---
# Procedura: eseguire una sottoquery su un&#39;operazione di raggruppamento (Guida per programmatori C#)
In questo argomento sono illustrati due modi diversi per creare una query che ordina i dati di origine in gruppi e quindi esegue una sottoquery su ogni singolo gruppo.  La tecnica di base in ogni esempio consiste nel raggruppare gli elementi di origine utilizzando una *continuazione* denominata `newGroup` e generando quindi una nuova sottoquery a fronte di `newGroup`.  Questa sottoquery viene eseguita a fronte di ogni nuovo gruppo creato dalla query esterna.  Si noti che in questo particolare esempio l'output finale non è un gruppo, ma una sequenza semplice di tipi anonimi.  
  
 Per ulteriori informazioni su come eseguire il raggruppamento, vedere [Clausola group](../../../csharp/language-reference/keywords/group-clause.md).  
  
 Per ulteriori informazioni sulle continuazioni, vedere [into](../../../csharp/language-reference/keywords/into.md).  Nell'esempio seguente viene utilizzata una struttura di dati in memoria come origine dati, ma gli stessi principi sono validi per qualsiasi tipo di origine dati di [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)].  
  
## Esempio  
 [!code-cs[csProgGuideLINQ#23](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-perform-a-subquery-on-a-grouping-operation_1.cs)]  
  
## Compilazione del codice  
 In questo esempio sono contenuti i riferimenti a oggetti definiti nell'applicazione di esempio in [Procedura: eseguire query in una raccolta di oggetti](../../../csharp/programming-guide/linq-query-expressions/how-to-query-a-collection-of-objects.md).  Per compilare ed eseguire questo metodo, incollarlo nella classe `StudentClass` in tale applicazione e aggiungervi una chiamata dal metodo `Main`.  
  
 Quando si adatta questo metodo alla propria applicazione, ricordare che LINQ richiede la versione 3.5 di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] e che il progetto deve contenere un riferimento a System.Core.dll e una direttiva using per System.Linq.  I tipi LINQ to SQL, LINQ to XML e LINQ to DataSet richiedono direttive using e riferimenti aggiuntivi.  Per ulteriori informazioni, vedere [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md).  
  
## Vedere anche  
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)