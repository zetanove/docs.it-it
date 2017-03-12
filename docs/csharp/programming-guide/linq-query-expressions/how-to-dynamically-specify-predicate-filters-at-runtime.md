---
redirect_url: /dotnet/articles/csharp/linq/dynamically-specify-predicate-filters-at-runtime
caps.handback.revision: 22
---
# Procedura: specificare dinamicamente i filtri dei predicati in fase di esecuzione (Guida per programmatori C#)
In alcuni casi non è possibile sapere quanti predicati sia necessario applicare agli elementi di origine nella clausola `where` fino alla fase di esecuzione.  Per specificare in modo dinamico più filtri dei predicati è possibile utilizzare il metodo <xref:System.Linq.Enumerable.Contains%2A>, come illustrato nell'esempio seguente.  L'esempio viene costruito in due modi.  Prima, il progetto viene eseguito filtrando i valori forniti nel programma.  Quindi il progetto viene nuovamente eseguito utilizzando l'input fornito in fase di esecuzione.  
  
### Per eseguire il filtraggio utilizzando il metodo Contains  
  
1.  Aprire una nuova applicazione console in Visual Studio.  Denominarla `PredicateFilters`.  
  
2.  Copiare la classe `StudentClass` da [Procedura: eseguire query in una raccolta di oggetti](../../../csharp/programming-guide/linq-query-expressions/how-to-query-a-collection-of-objects.md) e incollarla nello spazio dei nomi `PredicateFilters` sotto la classe `Program`.  `StudentClass` fornisce un elenco di oggetti `Student`.  
  
3.  Impostare come commento il metodo `Main` in `StudentClass`.  
  
4.  Sostituire la classe `Program` con il codice seguente.  
  
     [!code-cs[csProgGuideLINQ#26](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csrefLINQHowTos.cs#26)]  
  
5.  Aggiungere la riga seguente al metodo `Main` nella classe `DynamicPredicates`, sotto la dichiarazione di `ids`.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
6.  Premere F5 per eseguire il progetto.  
  
7.  In una finestra del prompt dei comandi verrà visualizzato il seguente output:  
  
     Garcia: 114  
  
     O'Donnell: 112  
  
     Omelchenko: 111  
  
8.  Il passaggio successivo consiste nell'eseguire nuovamente il progetto, questa volta utilizzando l'input immesso in fase di esecuzione anziché la matrice `ids`.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **PredicateFilters**, quindi scegliere **Proprietà**.  
  
9. Fare clic sulla scheda **Debug**.  
  
10. Nella finestra **Argomenti della riga di comando** digitare 122, 117, 120 e 115 separati da spazi: `122 117 120 115`.  Quando il progetto viene eseguito, tali valori diventano elementi di `args`, il parametro del metodo `Main`.  
  
11. Modificare `QueryByID(ids)` con `QueryByID(args)` nel metodo `Main`.  
  
12. Premere F5 per eseguire il progetto.  
  
13. In una finestra del prompt dei comandi verrà visualizzato il seguente output:  
  
     Adams: 120  
  
     Feng: 117  
  
     Garcia: 115  
  
     Tucker: 122  
  
### Per eseguire il filtraggio utilizzando un'istruzione switch  
  
1.  È possibile utilizzare un'istruzione `switch` per scegliere tra le query alternative predefinite.  Nell'esempio seguente, `studentQuery` utilizza una clausola `where` diversa a seconda dell'anno scolastico specificato in fase di esecuzione.  
  
2.  Copiare il seguente metodo e incollarlo nella classe `DynamicPredicates`.  
  
     [!code-cs[csProgGuideLINQ#27](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csrefLINQHowTos.cs#27)]  
  
3.  Nella finestra **Argomenti della riga di comando** sostituire i numeri di ID della procedura precedente con un valore intero compreso tra 1 e 4.  
  
4.  Nel metodo `Main` sostituire la chiamata a `QueryByID` con la seguente chiamata, che consente di inviare il primo elemento dalla matrice `args` come relativo argomento: `QueryByYear(args[0])`.  
  
5.  Premere F5 per eseguire il progetto.  
  
### Per utilizzare questo metodo nelle applicazioni  
  
-   Quando si adatta questo metodo a un'applicazione, ricordare che LINQ richiede la versione 3.5 o 4 di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] e che il progetto deve contenere un riferimento a System.Core.dll e una direttiva `using` per `System.Linq`.  I tipi LINQ to SQL, LINQ to XML e LINQ to DataSet richiedono direttive `using` e riferimenti aggiuntivi.  Per ulteriori informazioni, vedere [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md).  
  
## Vedere anche  
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Clausola where](../../../csharp/language-reference/keywords/where-clause.md)