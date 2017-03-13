---
redirect_url: /dotnet/articles/csharp/linq/group-query-results
caps.handback.revision: 19
---
# Procedura: raggruppare i risultati di una query (Guida per programmatori C#)
Il raggruppamento è una delle funzionalità più potenti di [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)].  Nell'esempio riportato di seguito viene illustrato come raggruppare i dati con diverse modalità:  
  
-   In base a una singola proprietà.  
  
-   In base alla prima lettera di una proprietà di stringa.  
  
-   In base a un intervallo numerico calcolato.  
  
-   In base al predicato booleano o altra espressione.  
  
-   In base a una chiave composta.  
  
 Le ultime due query proiettano inoltre i risultati in un tipo anonimo nuovo che contiene solo il nome e il cognome dello studente.  Per ulteriori informazioni, vedere [Clausola group](../../../csharp/language-reference/keywords/group-clause.md).  
  
## Esempio  
 In tutti gli esempi di questo argomento vengono utilizzate le classi di supporto e le origini dati seguenti.  
  
 [!code-cs[csProgGuideLINQ#15](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-group-query-results_1.cs)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come raggruppare elementi di origine utilizzando una sola proprietà dell'elemento come chiave di gruppo.  In questo caso, la chiave è un oggetto `string`, il cognome dello studente.  È anche possibile utilizzare una sottostringa per la chiave.  L'operazione di raggruppamento utilizza l'operatore di confronto di uguaglianza predefinito per il tipo.  
  
 Incollare il metodo seguente nella classe `StudentClass`.  Cambiare l'istruzione di chiamata nel metodo `Main` in `sc.GroupBySingleProperty()`.  
  
 [!code-cs[csProgGuideLINQ#17](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-group-query-results_2.cs)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come raggruppare elementi di origine utilizzando uno strumento diverso da una proprietà dell'oggetto per la chiave di gruppo.  In questo esempio la chiave è la prima lettera del cognome dello studente.  
  
 Incollare il metodo seguente nella classe `StudentClass`.  Cambiare l'istruzione di chiamata nel metodo `Main` in `sc.GroupBySubstring()`.  
  
 [!code-cs[csProgGuideLINQ#18](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-group-query-results_3.cs)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come raggruppare elementi di origine utilizzando un intervallo numerico come chiave di gruppo.  La query proietta quindi i risultati in un tipo anonimo che contiene solo il nome e il cognome e l'intervallo percentile al quale appartiene lo studente.  Viene utilizzato un tipo anonimo perché non è necessario utilizzare l'oggetto `Student` completo per visualizzare i risultati.  `GetPercentile` è una funzione di supporto che consente di calcolare un percentile basato sul voto medio dello studente.  Il metodo restituisce un Integer compreso tra 0 e 10.  
  
 [!code-cs[csProgGuideLINQ#50](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-group-query-results_4.cs)]  
  
 Incollare il metodo seguente nella classe `StudentClass`.  Cambiare l'istruzione di chiamata nel metodo `Main` in `sc.GroupByRange()`.  
  
 [!code-cs[csProgGuideLINQ#19](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-group-query-results_5.cs)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come raggruppare elementi di origine utilizzando un'espressione di confronto booleana.  In questo esempio l'espressione booleana consente di verificare se il voto medio degli esami di uno studente è maggiore di 75.  Come negli esempi precedenti, i risultati vengono proiettati in un tipo anonimo perché l'elemento di origine completo non è necessario.  Si noti che le proprietà nel tipo anonimo diventano proprietà sul membro `Key` e sono accessibili tramite il nome quando la query viene eseguita.  
  
 Incollare il metodo seguente nella classe `StudentClass`.  Cambiare l'istruzione di chiamata nel metodo `Main` in `sc.GroupByBoolean()`.  
  
 [!code-cs[csProgGuideLINQ#20](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-group-query-results_6.cs)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come utilizzare un tipo anonimo per incapsulare una chiave che contiene più valori.  In questo esempio il primo valore della chiave è la prima lettera del cognome dello studente.  Il secondo valore della chiave è un valore booleano che specifica se lo studente ha ottenuto un voto superiore a 85 nel primo esame.  È possibile ordinare i gruppi in base a qualsiasi proprietà nella chiave.  
  
 Incollare il metodo seguente nella classe `StudentClass`.  Cambiare l'istruzione di chiamata nel metodo `Main` in `sc.GroupByCompositeKey()`.  
  
 [!code-cs[csProgGuideLINQ#21](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-group-query-results_7.cs)]  
  
## Compilazione del codice  
 Copiare e incollare ogni metodo che si desidera testare nella classe `StudentClass`.  Aggiungere un'istruzione di chiamata per il metodo al metodo `Main` e premere F5.  
  
 Quando si adattano questi metodi alla propria applicazione, ricordare che LINQ richiede la versione 3.5 o 4 di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] e che il progetto deve contenere un riferimento a System.Core.dll e una direttiva using per System.Linq.  I tipi LINQ to SQL, LINQ to XML e LINQ to DataSet richiedono direttive using e riferimenti aggiuntivi.  Per ulteriori informazioni, vedere [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md).  
  
## Vedere anche  
 <xref:System.Linq.Enumerable.GroupBy%2A>   
 <xref:System.Linq.IGrouping%602>   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Clausola group](../../../csharp/language-reference/keywords/group-clause.md)   
 [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [Procedura: eseguire una sottoquery su un'operazione di raggruppamento](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-a-subquery-on-a-grouping-operation.md)   
 [Procedura: creare un gruppo annidato](../../../csharp/programming-guide/linq-query-expressions/how-to-create-a-nested-group.md)   
 [Grouping Data](../../../visual-basic/programming-guide/concepts/linq/grouping-data.md)