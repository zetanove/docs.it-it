---
title: "Take Clause (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryTake"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Take statement"
  - "queries [Visual Basic], Take"
  - "Take clause"
ms.assetid: 77bf87b2-1476-4456-957f-fee922fbad8c
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Take Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Restituisce un numero specificato di elementi contigui dall'inizio di una raccolta.  
  
## Sintassi  
  
```  
Take count  
```  
  
## Parti  
 `count`  
 Obbligatorio.  Valore o espressione che restituisce il numero di elementi della sequenza da restituire.  
  
## Note  
 La clausola `Take` fa in modo che una query includa un numero specificato di elementi contigui dall'inizio di un elenco di risultati.  Il numero di elementi da includere viene specificato dal parametro `count`.  
  
 È possibile utilizzare la clausola `Take` con la clausola `Skip` per restituire un intervallo di dati da qualsiasi segmento di una query.  A tale scopo, passare l'indice del primo elemento dell'intervallo alla clausola `Skip` e la dimensione dell'intervallo alla clausola `Take`.  In questo caso, la clausola `Take` deve venire specificata dopo la clausola `Skip`.  
  
 Quando si utilizza la clausola `Take` in una query, è necessario assicurarsi che i risultati vengano restituiti in un ordine che consente alla clausola `Take` di includere i risultati desiderati.  Per ulteriori informazioni sull'ordinamento dei risultati di una query, vedere [Order By Clause](../../../visual-basic/language-reference/queries/order-by-clause.md).  
  
 È possibile utilizzare la clausola `TakeWhile` per specificare che vengano restituiti solo determinati elementi, in funzione di una condizione fornita.  
  
## Esempio  
 Nell'esempio di codice seguente viene utilizzata insieme la clausola `Take` con la clausola `Skip` per restituire dati da una query in pagine.  La funzione GetCustomers utilizza la clausola `Skip` per ignorare i clienti nell'elenco fino al valore di indice iniziale fornito e utilizza la clausola `Take` per restituire una pagina di clienti a partire da quel valore di indice.  
  
 [!code-vb[VbSimpleQuerySamples#1](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/take-clause_1.vb)]  
  
## Vedere anche  
 [Introduction to LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Queries](../../../visual-basic/language-reference/queries/queries.md)   
 [Select Clause](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From Clause](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Order By Clause](../../../visual-basic/language-reference/queries/order-by-clause.md)   
 [Take While Clause](../../../visual-basic/language-reference/queries/take-while-clause.md)   
 [Skip Clause](../../../visual-basic/language-reference/queries/skip-clause.md)