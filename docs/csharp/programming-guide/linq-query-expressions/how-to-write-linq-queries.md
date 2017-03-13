---
redirect_url: /dotnet/articles/csharp/linq/write-linq-queries
caps.handback.revision: 25
---
# Procedura: scrivere query LINQ in C# #
In questo argomento vengono illustrate le tre modalità in cui è possibile scrivere una query [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] in C\#:  
  
1.  Uso della sintassi della query.  
  
2.  Uso della sintassi del metodo.  
  
3.  Uso di una combinazione di sintassi della query e sintassi del metodo.  
  
 Negli esempi seguenti vengono dimostrate alcune query semplici [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] utilizzando ogni approccio sopra elencato.  In generale, la regola prevede di utilizzare \(1\) ogni qualvolta è possibile e di utilizzare \(2\) e \(3\) ogni qualvolta è necessario.  
  
> [!NOTE]
>  Queste query operano su semplici raccolte in memoria. La sintassi di base, tuttavia, è identica a quella utilizzata in [!INCLUDE[vbtecdlinq](../../../csharp/includes/vbtecdlinq-md.md)] e [!INCLUDE[sqltecxlinq](../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)].  
  
## Esempio  
  
## Sintassi della query  
 Il modo consigliato per scrivere la maggior parte delle query è di utilizzare la *sintassi della query* per creare *espressioni di query*.  Nell'esempio seguente vengono illustrate tre espressioni di query.  La prima espressione di query dimostra come filtrare o limitare i risultati applicando le condizioni con una clausola `where`.  Restituisce tutti gli elementi nella sequenza di origine i cui valori sono maggiori di 7 o minori di 3.  La seconda espressione dimostra come ordinare i risultati restituiti.  La terza espressione dimostra come raggruppare i risultati secondo una chiave.  Questa query restituisce due gruppi basati sulla prima lettera della parola.  
  
 [!code-cs[csProgGuideLINQ#5](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-write-linq-queries_1.cs)]  
  
 Si noti che il tipo delle query è <xref:System.Collections.Generic.IEnumerable%601>.  Tutte queste query potrebbero essere scritte tramite `var`, come è illustrato nell'esempio seguente:  
  
 `var query = from num in numbers...`  
  
 In ogni esempio precedente, le query non vengono effettivamente eseguite finché non si scorre la variabile della query in un'istruzione `foreach`.  Per ulteriori informazioni, vedere la classe [Introduction to LINQ Queries \(C\#\)](../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md).  
  
## Esempio  
  
## Sintassi del metodo  
 Alcune operazioni di query devono essere espresse come chiamata al metodo.  I metodi di questo genere più comuni sono quelli che restituiscono valori numerici singleton, ad esempio <xref:System.Linq.Enumerable.Sum%2A>, <xref:System.Linq.Enumerable.Max%2A><xref:System.Linq.Enumerable.Min%2A>, <xref:System.Linq.Enumerable.Average%2A>e così via.  Questi metodi devono essere sempre chiamati per ultimi in qualsiasi query perché rappresentano un solo valore e non possono fungere da origine per un'operazione di query aggiuntiva.  Nell'esempio seguente viene illustrata una chiamata al metodo in un'espressione di query:  
  
 [!code-cs[csProgGuideLINQ#6](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-write-linq-queries_2.cs)]  
  
## Esempio  
 Gli eventuali parametri presenti nel metodo vengono specificati con il formato di un'espressione [lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md), come è illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideLINQ#7](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-write-linq-queries_3.cs)]  
  
 Tra le query precedenti, solo la numero 4 viene eseguita immediatamente,  perché restituisce un solo valore e non una raccolta <xref:System.Collections.Generic.IEnumerable%601> generica.  Il metodo stesso deve utilizzare `foreach` per calcolare il valore.  
  
 Ognuna delle query precedenti può essere scritta utilizzando la tipizzazione implicita con [var](../../../csharp/language-reference/keywords/var.md), come è illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideLINQ#8](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-write-linq-queries_4.cs)]  
  
## Esempio  
  
## Sintassi mista del metodo e della query  
 In questo esempio viene mostrato come utilizzare la sintassi del metodo sui risultati di una clausola query.  Racchiudere l'espressione di query nelle parentesi e quindi applicare l'operatore punto e chiamare il metodo.  Nell'esempio seguente, la query n. 7 restituisce un conteggio dei numeri il cui valore è compreso tra 3 e 7.  In generale, tuttavia, è meglio utilizzare una seconda variabile per archiviare il risultato della chiamata al metodo.  In questo modo, è meno probabile che la query venga confusa con i risultati della query.  
  
 [!code-cs[csProgGuideLINQ#9](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-write-linq-queries_5.cs)]  
  
 La query n. 7 viene eseguita immediatamente, perché restituisce un solo valore e non una raccolta.  
  
 La query precedente può essere scritta utilizzando la tipizzazione implicita con `var`, come segue:  
  
```  
var numCount = (from num in numbers...  
```  
  
 Può essere scritta nella sintassi del metodo come segue:  
  
```  
var numCount = numbers.Where(n => n < 3 || n > 7).Count();  
```  
  
 Può essere scritta utilizzando la tipizzazione esplicita, come segue:  
  
```  
int numCount = numbers.Where(n => n < 3 || n > 7).Count();  
```  
  
## Vedere anche  
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Walkthrough: Writing Queries in C\#](../../../csharp/programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Clausola where](../../../csharp/language-reference/keywords/where-clause.md)