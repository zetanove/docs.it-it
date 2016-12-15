---
title: "Clausola join (Riferimento C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "join"
  - "join_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "join (clausola) [C#]"
  - "parola chiave join [C#]"
ms.assetid: 76e9df84-092c-41a6-9537-c3f1cbd7f0fb
caps.latest.revision: 29
caps.handback.revision: 29
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Clausola join (Riferimento C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La clausola `join` è utile per l'associazione di elementi da sequenze di origine diverse senza relazione diretta nel modello a oggetti.  Il requisito solo è che gli elementi in ogni origine condividano alcuni valori di cui può essere verificata l'uguaglianza.  Un distributore di prodotti alimentari, ad esempio, potrebbe disporre di un elenco di fornitori di un determinato prodotto e di un elenco di acquirenti.  Una clausola `join` consente, ad esempio, di creare un elenco dei fornitori e degli acquirenti di tale prodotto che si trovano tutti nell'area specificata.  
  
 La clausola `join` accetta due sequenze di origine come input.  Gli elementi in ogni sequenza devono essere o contenere una proprietà che può essere confrontata con una proprietà corrispondente nell'altra sequenza.  La clausola `join` verifica l'uguaglianza delle chiavi specificate utilizzando la speciale parola chiave `equals`.  Tutti i join eseguiti dalla clausola `join` sono equijoin.  La forma dell'output di una clausola `join` dipende dal tipo specifico di join che si sta eseguendo.  Di seguito vengono riportati i tre tipi di join più comuni:  
  
-   Inner join  
  
-   Group join  
  
-   Left outer join  
  
## Inner join  
 Nell'esempio che segue viene fornito un inner equijoin.  Questa query produce una semplice sequenza di coppie "nome prodotto \/ categoria".  La stessa stringa della categoria verrà visualizzata in più elementi.  Se per un elemento di `categories` non esistono `products` corrispondenti, tale categoria non verrà visualizzata nei risultati.  
  
 [!code-cs[cscsrefQueryKeywords#24](../../../csharp/language-reference/keywords/codesnippet/CSharp/join-clause_1.cs)]  
  
 Per ulteriori informazioni, vedere [Procedura: eseguire degli inner join](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md).  
  
## Group Join  
 Una clausola `join` con un'espressione `into` viene detta group join.  
  
 [!code-cs[cscsrefQueryKeywords#25](../../../csharp/language-reference/keywords/codesnippet/CSharp/join-clause_2.cs)]  
  
 Un group join produce una sequenza di risultati gerarchica, che associa gli elementi nella sequenza di origine a sinistra con uno o più elementi corrispondenti nella sequenza di origine sul lato destro.  Un group join non ha equivalente in termini relazionali. Si tratta essenzialmente di una sequenza di matrici di oggetti.  
  
 Se nessun elemento della sequenza di origine a destra corrisponde a un elemento nell'origine a sinistra, la clausola `join` produrrà una matrice vuota per tale elemento.  Pertanto, il group join è ancora fondamentalmente un inner equijoin tranne per il fatto che la sequenza di risultati è organizzata in gruppi.  
  
 Se si selezionano i risultati di un group join, è possibile accedere agli elementi, ma non è possibile identificare la chiave alla quale corrispondono.  È, pertanto, generalmente più utile selezionare i risultati del group join in un tipo nuovo che dispone anche del nome della chiave, come illustrato nell'esempio precedente.  
  
 È inoltre ovviamente possibile utilizzare il risultato di un group join come generatore di un'altra sottoquery:  
  
 [!code-cs[cscsrefQueryKeywords#26](../../../csharp/language-reference/keywords/codesnippet/CSharp/join-clause_3.cs)]  
  
 Per ulteriori informazioni, vedere [Procedura: eseguire dei join raggruppati](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-grouped-joins.md).  
  
## Left outer join  
 In un left outer join, vengono restituiti tutti gli elementi nella sequenza di origine di sinistra, anche se non sono disponibili elementi corrispondenti nella sequenza di destra.  Per eseguire un left outer join in [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)], utilizzare il metodo `DefaultIfEmpty` in combinazione con un group join per specificare di produrre un elemento del lato destro predefinito se un elemento del lato sinistro non ha corrispondenze.  È possibile utilizzare `null` come valore predefinito per qualsiasi tipo di riferimento o specificare un tipo predefinito definito dall'utente.  Nell'esempio seguente, viene illustrato un tipo predefinito definito dall'utente:  
  
 [!code-cs[cscsrefQueryKeywords#27](../../../csharp/language-reference/keywords/codesnippet/CSharp/join-clause_4.cs)]  
  
 Per ulteriori informazioni, vedere [Procedura: Eseguire i left outer join](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-left-outer-joins.md).  
  
## Operatore equals  
 Una clausola `join` esegue un equijoin.  In altre parole, è possibile basare le corrispondenze solo sull'uguaglianza di due chiavi.  Altri tipi di confronti, quale "greater than" o "not equals", non sono supportati.  Per specificare chiaramente che tutti i join sono equijoin, la clausola `join` utilizza la parola chiave `equals` anziché l'operatore `==`.  La parola chiave `equals` può essere utilizzata solo in una clausola `join` e differisce dall'operatore `==` per un aspetto importante.  Con `equals` la chiave sinistra utilizza la sequenza di origine esterna e la chiave destra utilizza l'origine interna.  L'origine esterna si trova solo nell'ambito sul lato sinistro di `equals` e la sequenza di origine interna si trova solo nell'ambito sul lato destro.  
  
## Non equijoin  
 È possibile eseguire non equijoin, cross join e altre operazioni di join personalizzate utilizzando più clausole `from` per introdurre indipendentemente nuove sequenze in una query.  Per ulteriori informazioni, vedere [Procedura: eseguire operazioni di join personalizzate](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-custom-join-operations.md).  
  
## Join su raccolte di oggetti etabelle relazionali  
 In un'espressione di query [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)], le operazioni di join vengono eseguite su raccolte di oggetti.  Le raccolte di oggetti non possono essere "associate in join" con la stessa identica procedura utilizzata per due tabelle relazionali.  In [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)], le clausole `join` esplicite sono necessarie solo quando due sequenze di origine non sono associate da una relazione.  Quando si utilizza [!INCLUDE[vbtecdlinq](../../../csharp/includes/vbtecdlinq_md.md)], le tabelle di chiave esterna vengono rappresentate nel modello a oggetti come proprietà della tabella primaria.  Nel database Northwind, ad esempio, la tabella Customer ha una relazione di chiave esterna con la tabella Orders.  Quando si esegue il mapping delle tabelle al modello a oggetti, la classe Customer dispone di una proprietà Orders che contiene la raccolta di ordini associati a tale cliente.  In effetti, il join è già stato eseguito automaticamente.  
  
 Per ulteriori informazioni sull'esecuzione di una query in tabelle correlate nel contesto di [!INCLUDE[vbtecdlinq](../../../csharp/includes/vbtecdlinq_md.md)], vedere [Procedura: eseguire il mapping delle relazioni di database](../Topic/How%20to:%20Map%20Database%20Relationships.md).  
  
## Chiavi composte  
 È possibile verificare l'uguaglianza di più valori utilizzando una chiave composta.  Per ulteriori informazioni, vedere [Procedura: eseguire un join utilizzando una chiave composta](../../../csharp/programming-guide/linq-query-expressions/how-to-join-by-using-composite-keys.md).  Le chiavi composte possono essere utilizzate anche nella clausola `group`.  
  
## Esempio  
 Nell'esempio seguente vengono confrontati i risultati di un inner join, di un group join e di un left outer join nelle stesse origini dati utilizzando le stesse chiavi corrispondenti.  A questi esempi viene aggiunto altro codice per chiarire i risultati nella visualizzazione della console.  
  
 [!code-cs[cscsrefQueryKeywords#23](../../../csharp/language-reference/keywords/codesnippet/CSharp/join-clause_5.cs)]  
  
## Note  
 Una clausola `join` non seguita da `into` viene convertita in una chiamata al metodo <xref:System.Linq.Enumerable.Join%2A>.  Una clausola `join` seguita da `into` viene convertita in una chiamata al metodo <xref:System.Linq.Enumerable.GroupJoin%2A>.  
  
## Vedere anche  
 [Parole chiave di query \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Join Operations](../../../visual-basic/programming-guide/concepts/linq/join-operations.md)   
 [Clausola group](../../../csharp/language-reference/keywords/group-clause.md)   
 [Procedura: Eseguire i left outer join](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-left-outer-joins.md)   
 [Procedura: eseguire degli inner join](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md)   
 [Procedura: eseguire dei join raggruppati](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-grouped-joins.md)   
 [Procedura: ordinare i risultati di una clausola join](../../../csharp/programming-guide/linq-query-expressions/how-to-order-the-results-of-a-join-clause.md)   
 [Procedura: eseguire un join utilizzando una chiave composta](../../../csharp/programming-guide/linq-query-expressions/how-to-join-by-using-composite-keys.md)   
 [Procedura: installare database di esempio](../Topic/How%20to:%20Install%20Sample%20Databases.md)