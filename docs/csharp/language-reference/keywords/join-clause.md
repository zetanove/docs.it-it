---
title: Clausola join (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- join
- join_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- join clause [C#]
- join keyword [C#]
ms.assetid: 76e9df84-092c-41a6-9537-c3f1cbd7f0fb
caps.latest.revision: 29
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 26027418b70d211dcadf6ace58b24927d94e427a
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="join-clause-c-reference"></a>Clausola join (Riferimento C#)
Il clausola `join` è utile per l'associazione di elementi di sequenze di origine diverse che non hanno una relazione diretta nel modello a oggetti. L'unico requisito è che gli elementi in ogni origine condividano alcuni valori di cui può essere verificata l'uguaglianza. Un distributore di prodotti alimentari, ad esempio, potrebbe avere un elenco di fornitori di un determinato prodotto e un elenco di acquirenti. Con una clausola `join` è ad esempio possibile creare un elenco dei fornitori e degli acquirenti di tale prodotto che si trovano tutti nella stessa area specificata.  
  
 Una clausola `join` accetta due sequenze di origine come input. Gli elementi in ogni sequenza devono essere o devono contenere una proprietà che può essere confrontata con una proprietà corrispondente nell'altra sequenza. La clausola `join` verifica l'uguaglianza delle chiavi specificate usando la speciale parola chiave `equals`. Tutti i join eseguiti dalla clausola `join` sono equijoin. La forma dell'output di una clausola `join` dipende dal tipo specifico di join che si sta eseguendo. Di seguito vengono riportati i tre tipi di join più comuni:  
  
-   Inner join  
  
-   Group join  
  
-   Left outer join  
  
## <a name="inner-join"></a>Inner Join  
 In questo esempio viene illustrato un semplice inner equijoin. Questa query genera una sequenza semplice di coppie "nome prodotto / categoria". La stessa stringa della categoria verrà visualizzata in più elementi. Se per un elemento di `categories` non esistono `products` corrispondenti, tale categoria non verrà visualizzata nei risultati.  
  
 [!code-cs[cscsrefQueryKeywords#24](../../../csharp/language-reference/keywords/codesnippet/CSharp/join-clause_1.cs)]  
  
 Per altre informazioni, vedere [Procedura: Eseguire inner join](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md).  
  
## <a name="group-join"></a>Group Join  
 Una clausola `join` con un'espressione `into` viene detta group join.  
  
 [!code-cs[cscsrefQueryKeywords#25](../../../csharp/language-reference/keywords/codesnippet/CSharp/join-clause_2.cs)]  
  
 Un group join genera una sequenza di risultati gerarchici, che associa gli elementi nella sequenza di origine a sinistra con uno o più elementi corrispondenti nella sequenza di origine a destra. Un group join non ha equivalente in termini relazionali. Si tratta essenzialmente di una sequenza di matrici di oggetti.  
  
 Se nessun elemento della sequenza di origine a destra corrisponde a un elemento nell'origine a sinistra, la clausola `join` genererà una matrice vuota per tale elemento. Il group join rimane fondamentalmente un inner equijoin tranne per il fatto che la sequenza di risultati è organizzata in gruppi.  
  
 Se si selezionano i risultati di un group join, è possibile accedere agli elementi, ma non è possibile identificare la chiave alla quale corrispondono. È quindi generalmente più utile selezionare i risultati del group join in un tipo nuovo che ha anche il nome della chiave, come illustrato nell'esempio precedente.  
  
 È ovviamente anche possibile usare il risultato di un group join come generatore di un'altra sottoquery:  
  
 [!code-cs[cscsrefQueryKeywords#26](../../../csharp/language-reference/keywords/codesnippet/CSharp/join-clause_3.cs)]  
  
 Per altre informazioni, vedere [Procedura: Eseguire join raggrupati](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-grouped-joins.md).  
  
## <a name="left-outer-join"></a>Left Outer Join  
 In un left outer join vengono restituiti tutti gli elementi nella sequenza di origine a sinistra, anche se non sono disponibili elementi corrispondenti nella sequenza a destra. Per eseguire un left outer join in [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)], usare il metodo `DefaultIfEmpty` insieme a un group join per specificare di generare un elemento di destra predefinito se un elemento di sinistra non ha corrispondenze. È possibile usare `null` come valore predefinito per qualsiasi tipo di riferimento oppure specificare un tipo predefinito definito dall'utente. Nell'esempio seguente viene illustrato un tipo predefinito definito dall'utente:  
  
 [!code-cs[cscsrefQueryKeywords#27](../../../csharp/language-reference/keywords/codesnippet/CSharp/join-clause_4.cs)]  
  
 Per altre informazioni, vedere [Procedura: Eseguire left outer join](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-left-outer-joins.md).  
  
## <a name="the-equals-operator"></a>Operatore di uguaglianza  
 Una clausola `join` esegue un equijoin. In altre parole, è possibile basare le corrispondenze solo sull'uguaglianza di due chiavi. Altri tipi di confronti, quale "maggiore di" o "diverso da", non sono supportati. Per specificare chiaramente che tutti i join sono equijoin, la clausola `join` usa la parola chiave `equals` anziché l'operatore `==`. La parola chiave `equals` può essere usata solo in una clausola `join` e differisce dall'operatore `==` per un aspetto importante. Con `equals` la chiave a sinistra usa la sequenza di origine esterna, mentre la chiave a destra usa l'origine interna. L'origine esterna si trova solo nell'ambito sul lato sinistro di `equals` e la sequenza di origine interna si trova solo nell'ambito sul lato destro.  
  
## <a name="non-equijoins"></a>Non equijoin  
 È possibile eseguire non equijoin, cross join e altre operazioni di join personalizzate usando più clausole `from` per introdurre indipendentemente nuove sequenze in una query. Per altre informazioni, vedere [Procedura: Eseguire operazioni di join personalizzate](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-custom-join-operations.md).  
  
## <a name="joins-on-object-collections-vs-relational-tables"></a>Join su raccolte di oggetti e tabelle relazionali  
 In un'espressione di query [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] le operazioni di join vengono eseguite su raccolte di oggetti. Le raccolte di oggetti non possono essere "aggiunte" nello stesso modo in cui si aggiungono due tabelle relazionali. In [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] le clausole `join` esplicite sono necessarie solo quando due sequenze di origine non sono legate da una relazione. Quando si usa [!INCLUDE[vbtecdlinq](../../../csharp/includes/vbtecdlinq_md.md)], le tabelle di chiavi esterne vengono rappresentate nel modello a oggetti come proprietà della tabella primaria. Nel database Northwind, ad esempio, la tabella Customer ha una relazione di chiavi esterne con la tabella Orders. Quando si esegue il mapping delle tabelle al modello a oggetti, la classe Customer presenta una proprietà Orders che contiene la raccolta degli ordini associati a tale cliente. In effetti, il join è già stato automaticamente eseguito.  
  
 Per altre informazioni sull'esecuzione di una query in tabelle correlate nel contesto di [!INCLUDE[vbtecdlinq](../../../csharp/includes/vbtecdlinq_md.md)], vedere [Procedura: Eseguire il mapping delle relazioni di database](../../../framework/data/adonet/sql/linq/how-to-map-database-relationships.md).  
  
## <a name="composite-keys"></a>Chiavi composte  
 È possibile verificare l'uguaglianza di più valori usando una chiave composta. Per altre informazioni, vedere [Procedura: Eseguire un join usando chiavi composte](../../../csharp/programming-guide/linq-query-expressions/how-to-join-by-using-composite-keys.md). Le chiavi composte possono essere usate anche nella clausola `group`.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono confrontati i risultati di un inner join, di un group join e di un left outer join nelle stesse origini dati usando le medesime chiavi corrispondenti. A questi esempi viene aggiunto altro codice per chiarire i risultati nella visualizzazione della console.  
  
 [!code-cs[cscsrefQueryKeywords#23](../../../csharp/language-reference/keywords/codesnippet/CSharp/join-clause_5.cs)]  
  
## <a name="remarks"></a>Note  
 Una clausola `join` non seguita da `into` viene traslata in una chiamata al metodo <xref:System.Linq.Enumerable.Join%2A>. Una clausola `join` seguita da `into` viene traslata in una chiamata al metodo <xref:System.Linq.Enumerable.GroupJoin%2A>.  
  
## <a name="see-also"></a>Vedere anche  
 [Parole chiave di query (LINQ)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Operazioni di join](http://msdn.microsoft.com/library/442d176d-028c-4beb-8d22-407d4ef89107)   
 [Clausola group](../../../csharp/language-reference/keywords/group-clause.md)   
 [Procedura: Eseguire left outer join](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-left-outer-joins.md)   
 [Procedura: Eseguire inner join](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md)   
 [Procedura: Eseguire join raggruppati](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-grouped-joins.md)   
 [Procedura: Ordinare i risultati di una clausola join](../../../csharp/programming-guide/linq-query-expressions/how-to-order-the-results-of-a-join-clause.md)   
 [Procedura: Eseguire un join usando chiavi composte](../../../csharp/programming-guide/linq-query-expressions/how-to-join-by-using-composite-keys.md)   
 [Procedura: Installare database di esempio](http://msdn.microsoft.com/library/ed1291f6-604c-4972-ae22-0345c6dea12e)
