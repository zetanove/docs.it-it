---
title: "Clausola group (Riferimento C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "group"
  - "group_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "group (clausola) [C#]"
  - "parola chiave group [C#]"
ms.assetid: c817242e-b12c-4baa-a57e-73ee138f34d1
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# Clausola group (Riferimento C#)
La clausola `group` restituisce una sequenza di oggetti <xref:System.Linq.IGrouping%602> che contengono zero o più elementi corrispondenti al valore della chiave per il gruppo.  È possibile, ad esempio, raggruppare una sequenza di stringhe in base alla prima lettera di ogni stringa.  In questo caso, la prima lettera è la chiave e dispone di un tipo [char](../../../csharp/language-reference/keywords/char.md); inoltre è memorizzata nella proprietà `Key` di ogni oggetto <xref:System.Linq.IGrouping%602>.  Il compilatore deduce il tipo della chiave.  
  
 È possibile terminare un'espressione di query con una clausola `group`, come illustrato nell'esempio seguente:  
  
 [!code-cs[cscsrefQueryKeywords#10](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Group.cs#10)]  
  
 Se si desidera eseguire operazioni di query aggiuntive in ogni gruppo, è possibile specificare un identificatore temporaneo utilizzando la parola chiave contestuale [into](../../../csharp/language-reference/keywords/into.md).  Quando si utilizza `into`, è necessario continuare con la query ed eventualmente terminarla con un'istruzione `select` o un'altra clausola `group`, come illustrato nell'estratto seguente:  
  
 [!code-cs[cscsrefQueryKeywords#11](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Group.cs#11)]  
  
 Esempi più completi relativi all'utilizzo dell'oggetto `group` con e senza l'oggetto `into` sono disponibili nella sezione relativa agli esempi di questo argomento.  
  
## Enumerazione dei risultati di una query group  
 Poiché gli oggetti <xref:System.Linq.IGrouping%602> prodotti da una query `group` sono essenzialmente un elenco di elenchi, è necessario utilizzare un ciclo [foreach](../../../csharp/language-reference/keywords/foreach-in.md) annidato per accedere agli elementi in ogni gruppo.  Il ciclo esterno scorre le chiavi di gruppo e il ciclo interno scorre ogni elemento nel gruppo stesso.  È possibile che un gruppo contenga una chiave, ma nessun elemento.  Di seguito viene riportato il ciclo `foreach` che esegue la query negli esempi di codice precedenti:  
  
 [!code-cs[cscsrefQueryKeywords#12](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Group.cs#12)]  
  
## Tipi di chiave  
 Le chiavi di gruppo possono essere qualsiasi tipo, ad esempio una stringa, un tipo numerico incorporato oppure un tipo denominato definito dall'utente o un tipo anonimo.  
  
### Raggruppamento per stringhe  
 Negli esempi di codice precedenti viene utilizzato `char`.  Sarebbe stato invece possibile specificare facilmente una chiave stringa, ad esempio il cognome completo:  
  
 [!code-cs[cscsrefQueryKeywords#13](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Group.cs#13)]  
  
### Raggruppamento per bool  
 Nell'esempio seguente viene illustrato l'utilizzo di un valore booleano per fare in modo che una chiave divida i risultati in due gruppi.  Si noti che il valore viene prodotto da una sottoespressione nella clausola `group`.  
  
 [!code-cs[cscsrefQueryKeywords#14](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Group.cs#14)]  
  
### Raggruppamento per intervallo numerico  
 Nell'esempio successivo viene utilizzata un'espressione per creare chiavi di gruppo numeriche che rappresentano un intervallo percentile.  Si noti l'utilizzo di [let](../../../csharp/language-reference/keywords/let-clause.md) come percorso appropriato per archiviare un risultato di chiamata al metodo, in modo che non sia necessario chiamare il metodo due volte nella clausola `group`.  Si noti inoltre che nella clausola `group`, per evitare un'eccezione che comporta la divisione per zero, il codice verifica che la media dello studente non sia pari a zero.  Per ulteriori informazioni sull'utilizzo sicuro dei metodi nelle espressioni di query, vedere [Procedura: gestire le eccezioni nelle espressioni di query](../../../csharp/programming-guide/linq-query-expressions/how-to-handle-exceptions-in-query-expressions.md).  
  
 [!code-cs[cscsrefQueryKeywords#15](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Group.cs#15)]  
  
### Raggruppamento per chiavi composte  
 Utilizzare una chiave composta quando si desidera raggruppare elementi in base a più di una chiave.  Si crea una chiave composta utilizzando un tipo anonimo o un tipo denominato per contenere l'elemento chiave.  Nell'esempio seguente, si supponga che una classe `Person` sia stata dichiarata con i membri denominati `surname` e `city`.  La clausola `group` fa in modo che venga creato un gruppo distinto per ogni insieme di persone con lo stesso cognome e la stessa città.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 Utilizzare un tipo denominato se è necessario passare la variabile della query a un altro metodo.  Creare una classe speciale utilizzando proprietà implementate automaticamente per le chiavi e quindi eseguire l'override dei metodi <xref:System.Object.Equals%2A> e <xref:System.Object.GetHashCode%2A>.  È anche possibile utilizzare una struttura, nel qual caso non è indispensabile eseguire l'override di tali metodi.  Per ulteriori informazioni, vedere [Procedura: implementare una classe leggera con proprietà implementate automaticamente](../../../csharp/programming-guide/classes-and-structs/how-to-implement-a-lightweight-class-with-auto-implemented-properties.md) e [How to: Query for Duplicate Files in a Directory Tree \(LINQ\)](../Topic/How%20to:%20Query%20for%20Duplicate%20Files%20in%20a%20Directory%20Tree%20\(LINQ\).md).  Nel secondo argomento è disponibile un esempio di codice che dimostra come utilizzare una chiave composta con un tipo denominato.  
  
## Esempio  
 Nell'esempio seguente viene illustrato il modello standard per l'ordinamento di dati di origine in gruppi quando non è applicata alcuna logica della query aggiuntiva ai gruppi.  Si tratta di un raggruppamento senza continuazione.  Gli elementi in una matrice di stringhe vengono raggruppati in base alla prima lettera.  Il risultato della query è un tipo <xref:System.Linq.IGrouping%602> che contiene una proprietà `Key` pubblica di tipo `char` e una raccolta <xref:System.Collections.Generic.IEnumerable%601> che contiene ogni elemento nel raggruppamento.  
  
 Il risultato di una clausola `group` è una sequenza di sequenze.  Pertanto, per accedere ai singoli elementi all'interno di ogni gruppo restituito, utilizzare un ciclo `foreach` annidato all'interno del ciclo che scorre le chiavi di gruppo, come illustrato nell'esempio seguente.  
  
 [!code-cs[cscsrefQueryKeywords#16](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Group.cs#16)]  
  
## Esempio  
 In questo esempio viene illustrato come eseguire la logica aggiuntiva nei gruppi dopo averli creati, utilizzando una *continuazione* con `into`.  Per ulteriori informazioni, vedere [into](../../../csharp/language-reference/keywords/into.md).  Nell'esempio seguente viene eseguita una query su ogni gruppo per selezionare solo quelli il cui valore della chiave è una vocale.  
  
 [!code-cs[cscsrefQueryKeywords#17](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Group.cs#17)]  
  
## Note  
 In fase di compilazione, le clausole `group` vengono convertite in chiamate al metodo <xref:System.Linq.Enumerable.GroupBy%2A>.  
  
## Vedere anche  
 <xref:System.Linq.IGrouping%602>   
 <xref:System.Linq.Enumerable.GroupBy%2A>   
 <xref:System.Linq.Enumerable.ThenBy%2A>   
 <xref:System.Linq.Enumerable.ThenByDescending%2A>   
 [Parole chiave di query \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Procedura: creare un gruppo annidato](../../../csharp/programming-guide/linq-query-expressions/how-to-create-a-nested-group.md)   
 [Procedura: raggruppare i risultati di una query](../../../csharp/programming-guide/linq-query-expressions/how-to-group-query-results.md)   
 [Procedura: eseguire una sottoquery su un'operazione di raggruppamento](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-a-subquery-on-a-grouping-operation.md)