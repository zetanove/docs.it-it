---
redirect_url: /dotnet/articles/csharp/linq/perform-custom-join-operations
caps.handback.revision: 13
---
# Procedura: eseguire operazioni di join personalizzate (Guida per programmatori C#)
In questo esempio viene illustrato come eseguire operazioni di join che non sono possibili con la clausola `join`.  In un'espressione di query, la clausola `join` è limitata e ottimizzata per gli equijoin, che sono in assoluto il tipo più comune di operazione di join.  Quando si esegue un equijoin, è probabile che le prestazioni raggiungano sempre il livello ottimale utilizzando la clausola `join`.  
  
 Non è tuttavia possibile utilizzare la clausola `join` nei casi seguenti:  
  
-   Quando il join viene affermato su un'espressione di ineguaglianza \(un non equijoin\).  
  
-   Quando il join viene affermato su più di un'espressione di eguaglianza o di ineguaglianza.  
  
-   Quando è necessario introdurre una variabile di intervallo temporanea per la sequenza del lato destro \(interno\) prima dell'operazione di join.  
  
 Per eseguire join che non sono equijoin, è possibile utilizzare più clausole `from` per introdurre ogni origine dati in modo indipendente.  Si applica quindi un'espressione di predicato in una clausola `where` alla variabile di intervallo per ogni origine.  L'espressione può inoltre avere il formato di una chiamata al metodo.  
  
> [!NOTE]
>  Non confondere questo tipo di operazione di join personalizzata con l'utilizzo di più clausole `from` per accedere a raccolte interne.  Per ulteriori informazioni, vedere [Clausola join](../../../csharp/language-reference/keywords/join-clause.md).  
  
## Esempio  
 Nel primo metodo dell'esempio seguente viene illustrato un cross join semplice.  I cross join devono essere utilizzati con attenzione perché possono produrre set di risultati molto grandi.  Tuttavia, possono essere utili in alcuni scenari per la creazione di sequenze di origine a fronte delle quali vengono eseguite query aggiuntive.  
  
 Il secondo metodo produce una sequenza di tutti i prodotti il cui ID di categoria è presente nell'elenco di categorie sul lato sinistro.  Si noti l'utilizzo della clausola `let` e del metodo `Contains` per creare una matrice temporanea.  È inoltre possibile creare la matrice prima della query ed eliminare la prima clausola `from`.  
  
 [!code-cs[csProgGuideLINQ#64](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-perform-custom-join-operations_1.cs)]  
  
## Esempio  
 Nell'esempio seguente la query deve creare un join di due sequenze basate su chiavi corrispondenti che, nel caso della sequenza interna \(lato destro\), non possono essere ottenute prima della clausola join stessa.  Qualora questo join venga eseguito con una clausola `join`, il metodo `Split` dovrà essere chiamato per ogni elemento.  L'utilizzo di più clausole `from` consente alla query di evitare l'overhead della chiamata al metodo ripetuta.  Tuttavia, poiché il `join` è ottimizzato, in questo caso particolare potrebbe risultare ancora più veloce rispetto all'utilizzo di più clausole `from`.  I risultati varieranno principalmente in base al costo in termini di utilizzo della chiamata al metodo.  
  
 [!code-cs[csProgGuideLINQ#13](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-perform-custom-join-operations_2.cs)]  
  
## Compilazione del codice  
  
-   Creare un progetto di applicazione console di [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)] destinato a [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] versione 3.5 o successiva.  Per impostazione predefinita, il progetto include un riferimento a System.Core.dll e una direttiva `using` per lo spazio dei nomi System.Linq.  
  
-   Sostituire la classe `Program` con il codice dell'esempio precedente.  
  
-   Seguire le istruzioni riportate in [How to: Join Content from Dissimilar Files \(LINQ\)](../Topic/How%20to:%20Join%20Content%20from%20Dissimilar%20Files%20\(LINQ\).md) per impostare i file di dati, scores.csv e names.csv.  
  
-   Premere F5 per compilare ed eseguire il programma.  
  
-   Premere un tasto per chiudere la finestra della console.  
  
## Vedere anche  
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Clausola join](../../../csharp/language-reference/keywords/join-clause.md)   
 [Join Operations](../../../visual-basic/programming-guide/concepts/linq/join-operations.md)   
 [Procedura: ordinare i risultati di una clausola join](../../../csharp/programming-guide/linq-query-expressions/how-to-order-the-results-of-a-join-clause.md)