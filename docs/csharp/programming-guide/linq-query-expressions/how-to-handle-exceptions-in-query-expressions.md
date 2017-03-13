---
redirect_url: /dotnet/articles/csharp/linq/handle-exceptions-in-query-expressions
caps.handback.revision: 15
---
# Procedura: gestire le eccezioni nelle espressioni di query (Guida per programmatori C#)
È possibile chiamare qualsiasi metodo nel contesto di un'espressione di query.  Si consiglia, tuttavia, di non chiamare qualsiasi metodo in un'espressione di query che può creare un effetto collaterale, quale la modifica del contenuto dell'origine dati o la generazione di un'eccezione.  In questo esempio viene illustrato come evitare la generazione di eccezioni quando si chiamano metodi in un'espressione di query senza violare le linee guida di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] generali sulla gestione delle eccezioni.  Tali linee guida stabiliscono che è accettabile intercettare un'eccezione specifica quando è evidente il motivo per cui verrà generata in un contesto specificato.  Per ulteriori informazioni, vedere [Suggerimenti per le eccezioni](../Topic/Best%20Practices%20for%20Exceptions.md).  
  
 Nell'esempio finale viene illustrato come gestire tali casi quando è necessario generare un'eccezione durante l'esecuzione di una query.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come spostare codice di gestione dell'eccezione al di fuori di un'espressione di query.  Questa operazione è possibile solo quando il metodo non dipende da qualsiasi variabile locale per la query.  
  
 [!code-cs[csProgGuideLINQ#10](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-handle-exceptions-in-query-expressions_1.cs)]  
  
## Esempio  
 In alcuni casi, la migliore risposta a un'eccezione generata dall'interno di una query potrebbe essere l'arresto immediato dell'esecuzione della query.  Nell'esempio seguente viene illustrato come gestire le eccezioni che potrebbero essere generate all'interno di un corpo di query.  Si presuma che `SomeMethodThatMightThrow` possa potenzialmente causare un'eccezione che richiede l'arresto dell'esecuzione della query.  
  
 Si noti che il blocco `try` racchiude il ciclo `foreach` e non la query stessa,  in quanto il ciclo `foreach` è il punto in corrispondenza del quale la query viene effettivamente eseguita.  Per ulteriori informazioni, vedere la classe [Introduction to LINQ Queries \(C\#\)](../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md).  
  
 [!code-cs[csProgGuideLINQ#12](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-handle-exceptions-in-query-expressions_2.cs)]  
  
## Compilazione del codice  
  
-   Creare un progetto [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)] per .NET Framework versione 3.5.  Per impostazione predefinita, il progetto include un riferimento a System.Core.dll e una direttiva `using` per lo spazio dei nomi System.Linq.  
  
-   Copiare il codice nel progetto.  
  
-   Premere F5 per compilare ed eseguire il programma.  
  
 Premere un tasto per chiudere la finestra della console.  
  
## Vedere anche  
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)