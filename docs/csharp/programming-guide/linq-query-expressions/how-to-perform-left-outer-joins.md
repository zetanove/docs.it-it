---
redirect_url: /dotnet/articles/csharp/linq/perform-left-outer-joins
caps.handback.revision: 23
---
# Procedura: Eseguire i left outer join (Guida per programmatori C#)
Un left outer join è un join nel quale viene restituito ogni elemento della prima raccolta, indipendentemente dal fatto che disponga di elementi correlati nella seconda raccolta.  È possibile utilizzare [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] per eseguire un left outer join chiamando il metodo di <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> sui risultati di un join di gruppo.  
  
## Esempio  
 Nell'esempio seguente viene dimostrato come utilizzare il metodo <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> sui risultati di un join di gruppo per eseguire un left outer join.  
  
 Il primo passaggio nella produzione di un left outer join di due raccolte consiste nell'esecuzione di un inner join utilizzando un join di gruppo.  Per ulteriori informazioni su questo processo, vedere [Procedura: eseguire degli inner join](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md). In questo esempio, l'elenco di oggetti di `Person` è unito tramite inner join all'elenco di oggetti di `Pet` basati su un oggetto di `Person` che corrisponde `Pet.Owner`.  
  
 Il secondo passaggio consiste nell'includere ogni elemento della prima raccolta \(di sinistra\) nel set di risultati anche se tale elemento non ha corrispondenze nella raccolta di destra.  Questa operazione viene eseguita chiamando <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> su ogni sequenza di elementi corrispondenti dal join di gruppo.  In questo esempio, <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> viene chiamato a ogni sequenza di associare gli oggetti di `Pet`.  Il metodo restituisce una raccolta che contiene un solo valore predefinito, se la sequenza di associare gli oggetti di `Pet` è vuota per qualsiasi oggetto di `Person`, assicurando pertanto che ogni oggetto di `Person` è rappresentato nella raccolta di risultati.  
  
> [!NOTE]
>  Il valore predefinito per un tipo di riferimento è `null`; pertanto, i controlli di esempio per un riferimento Null prima di accedere a ogni elemento di ogni raccolta di `Pet`.  
  
 [!code-cs[CsLINQProgJoining#7](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/how-to-perform-left-outer-joins_1.cs)]  
  
## Compilazione del codice  
  
-   Creare un nuovo progetto Applicazione console in [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)].  
  
-   Aggiungere un riferimento a System.Core.dll, se non è già presente un riferimento.  
  
-   Includere lo spazio dei nomi <xref:System.Linq>.  
  
-   Copiare e incollare il codice nell'esempio nel file program.cs, nel metodo di `Main` nella classe di `Program`.  Aggiungere una riga di codice al metodo di `Main` per chiamare il metodo di `LeftOuterJoinExample`.  
  
-   Eseguire il programma.  
  
## Vedere anche  
 <xref:System.Linq.Enumerable.Join%2A>   
 <xref:System.Linq.Enumerable.GroupJoin%2A>   
 [Join Operations](../../../visual-basic/programming-guide/concepts/linq/join-operations.md)   
 [Procedura: eseguire degli inner join](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md)   
 [Procedura: eseguire dei join raggruppati](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-grouped-joins.md)   
 [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)