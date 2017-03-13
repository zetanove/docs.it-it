---
redirect_url: /dotnet/articles/csharp/linq/create-a-nested-group
caps.handback.revision: 12
---
# Procedura: creare un gruppo annidato (Guida per programmatori C#)
Nell'esempio seguente viene illustrato come creare gruppi annidati in un'espressione di query [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)].  Ogni gruppo creato in base all'anno studentesco o al livello di istruzione viene quindi suddiviso ulteriormente in gruppi basati sui nomi degli utenti.  
  
## Esempio  
 [!code-cs[csProgGuideLINQ#24](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-create-a-nested-group_1.cs)]  
  
 Si noti che sono necessari tre cicli `foreach` annidati per scorrere gli elementi interni di un gruppo annidato.  
  
## Compilazione del codice  
 In questo esempio sono contenuti i riferimenti a oggetti definiti nell'applicazione di esempio in [Procedura: eseguire query in una raccolta di oggetti](../../../csharp/programming-guide/linq-query-expressions/how-to-query-a-collection-of-objects.md).  Per compilare ed eseguire questo metodo, incollarlo nella classe `StudentClass` in tale applicazione e aggiungervi una chiamata dal metodo `Main`.  
  
 Quando si adatta questo metodo alla propria applicazione, ricordare che LINQ richiede la versione 3.5 di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] e che il progetto deve contenere un riferimento a System.Core.dll e una direttiva using per System.Linq.  I tipi LINQ to SQL, LINQ to XML e LINQ to DataSet richiedono direttive using e riferimenti aggiuntivi.  Per ulteriori informazioni, vedere [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md).  
  
## Vedere anche  
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)