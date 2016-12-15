---
title: "Aggregate Clause (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.QueryAggregateIn"
  - "vb.QueryAggregate"
  - "vb.QueryAggregateInto"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Aggregate clause"
  - "Aggregate statement"
  - "queries [Visual Basic], Aggregate"
ms.assetid: 1315a814-5db6-4077-b34b-b141e11cc0eb
caps.latest.revision: 25
caps.handback.revision: 25
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Aggregate Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Applica uno o più funzioni di aggregazione a una raccolta di elementi.  
  
## Sintassi  
  
```  
Aggregate element [As type] In collection _  
  [, element2 [As type2] In collection2, [...]]  
  [ clause ]  
  Into expressionList  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`element`|Obbligatorio.  Variabile utilizzata per scorrere gli elementi della raccolta.|  
|`type`|Parametro facoltativo.  Tipo di `element`.  Se non è specificato, il tipo di `element` viene dedotto da `collection`.|  
|`collection`|Obbligatorio.  Fa riferimento alla raccolta su cui eseguire l'operazione.|  
|`clause`|Parametro facoltativo.  Uno o più clausole query, ad esempio una clausola `Where`, per perfezionare il risultato della query a cui applicare la clausola o le clausole di aggregazione.|  
|`expressionList`|Obbligatorio.  Uno o espressioni più delimitate da virgole che identificano una funzione di aggregazione da applicare alla raccolta.  È possibile applicare un alias a una funzione di aggregazione per specificare un nome di membro per il risultato della query.  Se non viene fornito alcun alias, viene utilizzato il nome della funzione di aggregazione.  Per i relativi esempi, vedere la sezione dedicata alle funzioni di aggregazione più avanti in questo argomento.|  
  
## Note  
 La clausola `Aggregate` può essere utilizzata per includere nelle query funzioni di aggregazione.  Le funzioni di aggregazione eseguono controlli e calcoli su un insieme di valori e restituiscono un solo valore.  È possibile accedere al valore calcolato utilizzando un membro del tipo di risultato della query.  Le funzioni di aggregazione standard che possono venire utilizzate sono le funzioni `All`, `Any`, `Average`, `Count`, `LongCount`, `Max`, `Min` e `Sum`.  Queste funzioni sono note agli sviluppatori che utilizzano comunemente le aggregazioni in SQL.  Vengono descritte nelle sezioni seguenti di questo argomento.  
  
 Il risultato di una funzione di aggregazione viene incluso nel risultato della query come un campo del tipo di risultato della query.  È possibile fornire un alias affinché il risultato della funzione di aggregazione specifichi il nome di membro del tipo di risultato della query che conterrà il valore di aggregazione.  Se non viene fornito alcun alias, viene utilizzato il nome della funzione di aggregazione.  
  
 La clausola `Aggregate` può iniziare una query, o può essere inclusa come una clausola aggiuntiva in una query.  Se la clausola `Aggregate` inizia una query, il risultato è un solo valore che è il risultato della funzione di aggregazione specificato nella clausola `Into`.  Se viene specificata più di una funzione di aggregazione nella clausola `Into`, la query restituisce un solo tipo con una proprietà separata per fare riferimento al risultato di ogni funzione di aggregazione nella clausola `Into`.  Se la clausola `Aggregate` viene inclusa come clausola aggiuntiva in una query, il tipo restituito nella raccolta della query avrà una proprietà separata per fare riferimento al risultato di ogni funzione di aggregazione nella clausola `Into`.  
  
## Funzioni di aggregazione  
 Nell'elenco seguente vengono descritte le funzioni di aggregazione standard che possono essere utilizzate con la clausola `Aggregate`.  
  
|||  
|-|-|  
|Funzione|Descrizione|  
|`All`|Restituisce `true` se tutti gli elementi nella raccolta soddisfano una condizione specificata; in caso contrario restituisce`false`.  Di seguito è riportato un esempio:<br /><br /> [!code-vb[VbSimpleQuerySamples#5](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_1.vb)]|  
|`Any`|Restituisce `true` se ogni elemento nella raccolta soddisfa una condizione specificata; in caso contrario restituisce`false`.  Di seguito è riportato un esempio:<br /><br /> [!code-vb[VbSimpleQuerySamples#6](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_2.vb)]|  
|`Average`|Calcola la media di tutti gli elementi nella raccolta oppure calcola l'espressione fornita per tutti gli elementi nella raccolta.  Di seguito è riportato un esempio:<br /><br /> [!code-vb[VbSimpleQuerySamples#7](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_3.vb)]|  
|`Count`|Conta il numero di elementi nella raccolta.  È possibile fornire un'espressione `Boolean` facoltativa per contare solo il numero di elementi nella raccolta che soddisfano una condizione.  Di seguito è riportato un esempio:<br /><br /> [!code-vb[VbSimpleQuerySamples#8](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_4.vb)]|  
|`Group`|Fa riferimento ai risultati della query raggruppati come risultato di una clausola `Group By` o `Group Join` La funzione `Group` è valida solo nella clausola `Into` di una clausola `Group By``Group Join` Per ulteriori informazioni ed esempi, vedere [Clausola Group By](../../../visual-basic/language-reference/queries/group-by-clause.md) e [Group Join Clause](../../../visual-basic/language-reference/queries/group-join-clause.md).|  
|`LongCount`|Conta il numero di elementi nella raccolta.  È possibile fornire un'espressione `Boolean` facoltativa per contare solo il numero di elementi nella raccolta che soddisfano una condizione.  Restituisce il risultato sotto forma di `Long`.  Per un esempio, vedere la funzione di aggregazione `Count`.|  
|`Max`|Calcola il valore massimo della raccolta oppure calcola un'espressione fornita per tutti gli elementi della raccolta.  Di seguito è riportato un esempio:<br /><br /> [!code-vb[VbSimpleQuerySamples#9](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_5.vb)]|  
|`Min`|Calcola il valore minimo della raccolta oppure calcola un'espressione fornita per tutti gli elementi della raccolta.  Di seguito è riportato un esempio:<br /><br /> [!code-vb[VbSimpleQuerySamples#10](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_6.vb)]|  
|`Sum`|Calcola la somma di tutti gli elementi nella raccolta oppure calcola un'espressione fornita per tutti gli elementi della raccolta.  Di seguito è riportato un esempio:<br /><br /> [!code-vb[VbSimpleQuerySamples#15](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_7.vb)]|  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrato come utilizzare la clausola `Aggregate` per applicare funzioni di aggregazione a un risultato della query.  
  
 [!code-vb[VbSimpleQuerySamples#4](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_8.vb)]  
  
## Creazione di funzioni di aggregazione definite dall'utente  
 È possibile includere funzioni di aggregazione personalizzate in un'espressione di query aggiungendo metodi di estensione al tipo <xref:System.Collections.Generic.IEnumerable%601>.  Il metodo personalizzato può quindi eseguire un calcolo o un'operazione sulla raccolta enumerabile che ha fatto riferimento alla funzione di aggregazione.  Per ulteriori informazioni sui metodi di estensione, vedere [Metodi di estensione](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md).  
  
 Nell'esempio di codice riportato di seguito viene illustrata una funzione di aggregazione personalizzata che calcola il valore mediano di una raccolta di numeri.  Esistono due overload del metodo di estensione `Median`:  Il primo overload accetta come input una raccolta di tipo `IEnumerable(Of Double)`.  Se la funzione di aggregazione `Median` viene chiamata un campo della query di tipo `Double`, verrà chiamato questo metodo.  Il secondo overload del metodo `Median` può passare qualsiasi tipo generico.  L'overload generico del metodo `Median` prende un secondo parametro che fa riferimento all'espressione lambda `Func(Of T, Double)` per proiettare un valore per un tipo \(da una raccolta\) come valore corrispondente di tipo `Double`.  Delega quindi il calcolo del valore mediano all'altro overload del metodo `Median`.  Per ulteriori informazioni sulle espressioni lambda, vedere [Lambda Expressions](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
 [!code-vb[VbSimpleQuerySamples#18](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_9.vb)]  
  
 Nell'esempio di codice seguente vengono illustrate query che chiamano la funzione di aggregazione `Median` su una raccolta di tipo `Integer` e una raccolta di tipo `Double`.  La query che chiama la funzione di aggregazione `Median` sulla raccolta di tipo `Double` chiama l'overload del metodo `Median` che accetta come input una raccolta di tipo `Double`.  La query che chiama la funzione di aggregazione `Median` sulla raccolta di tipo `Integer` chiama l'overload generico del metodo `Median`.  
  
 [!code-vb[VbSimpleQuerySamples#19](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/aggregate-clause_10.vb)]  
  
## Vedere anche  
 [Introduction to LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Queries](../../../visual-basic/language-reference/queries/queries.md)   
 [Select Clause](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From Clause](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Where Clause](../../../visual-basic/language-reference/queries/where-clause.md)   
 [Clausola Group By](../../../visual-basic/language-reference/queries/group-by-clause.md)