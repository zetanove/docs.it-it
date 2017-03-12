---
redirect_url: /dotnet/articles/csharp/linq/perform-grouped-joins
caps.handback.revision: 23
---
# Procedura: eseguire dei join raggruppati (Guida per programmatori C#)
Il join di gruppo è utile per produrre strutture di dati gerarchiche.  Abbina ogni elemento della prima raccolta con un set di elementi correlati della seconda raccolta.  
  
 Ad esempio, una classe o una tabella del database relazionale denominata Student potrebbe contenere due campi: Id e Name.  Un'altra classe o tabella del database relazionale denominata Course potrebbe contenere due campi: StudentId e CourseTitle.  Un join di gruppo di queste due origini dati, basato sulla corrispondenza di Student.Id e Course.StudentId, raggrupperebbe ogni studente con una raccolta di oggetti Course \(che può essere vuota\).  
  
> [!NOTE]
>  Ogni elemento della prima raccolta viene visualizzata nel set di risultati di un join di gruppo indipendentemente dal fatto che gli elementi correlati vengano trovati nella seconda raccolta.  Nel caso in cui non venga trovato alcun elemento correlato, la sequenza di elementi correlati per tale elemento è vuota.  Il selettore del risultato ha pertanto accesso a ogni elemento della prima raccolta.  È diverso dal selettore del risultato in un join non di gruppo, che non può accedere a elementi della prima raccolta che non hanno corrispondenza nella seconda raccolta.  
  
 Nel primo esempio di questo argomento viene illustrato come eseguire un join di gruppo.  Nel secondo esempio viene illustrato come utilizzare un join di gruppo per creare elementi XML.  
  
## Esempio  
  
### Esempio di join di gruppo  
 Nell'esempio seguente viene eseguito un join di gruppo di oggetti di tipo `Person` e `Pet` basato su `Person` corrispondente alla proprietà `Pet.Owner`.  Diversamente da un join non di gruppo, che produrrebbe una coppia di elementi per ogni corrispondenza, il join di gruppo produce un solo oggetto risultante per ogni elemento della prima raccolta, che in questo esempio è un oggetto `Person`.  Gli elementi corrispondenti della seconda raccolta, che in questo esempio sono oggetti `Pet`, vengono raggruppati in una raccolta.  La funzione del selettore del risultato crea infine un tipo anonimo per ogni corrispondenza costituita da `Person.FirstName` e una raccolta di oggetti `Pet`.  
  
 [!code-cs[CsLINQProgJoining#5](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/Joins/joins.cs#5)]  
  
## Esempio  
  
### Esempio di join di gruppo per la creazione di XML  
 I join di gruppo sono ideali per la creazione di XML tramite [!INCLUDE[sqltecxlinq](../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)].  L'esempio seguente è analogo a quello precedente tranne per il fatto che, invece di creare tipi anonimi, la funzione del selettore del risultato crea elementi XML che rappresentano gli oggetti uniti in join.  Per ulteriori informazioni su [!INCLUDE[sqltecxlinq](../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)], vedere [LINQ to XML](../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md).  
  
 [!code-cs[CsLINQProgJoining#6](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/Joins/joins.cs#6)]  
  
## Compilazione del codice  
  
-   Creare un nuovo progetto  **Applicazione console**  in [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)].  
  
-   Aggiungere un riferimento a System.Core.dll e a System.Xml.Linq.dll se non vi è già fatto riferimento.  
  
-   Includere gli spazi dei nomi <xref:System.Linq> e <xref:System.Xml.Linq>.  
  
-   Copiare e incollare il codice dall'esempio nel file program.cs, sotto il metodo `Main`.  Aggiungere una riga di codice al metodo `Main` per chiamare il metodo in cui è stata eseguita l'operazione Incolla.  
  
-   Eseguire il programma.  
  
## Vedere anche  
 <xref:System.Linq.Enumerable.Join%2A>   
 <xref:System.Linq.Enumerable.GroupJoin%2A>   
 [Join Operations](../../../visual-basic/programming-guide/concepts/linq/join-operations.md)   
 [Procedura: eseguire degli inner join](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md)   
 [Procedura: Eseguire i left outer join](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-left-outer-joins.md)   
 [LINQ to XML](../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md)   
 [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)