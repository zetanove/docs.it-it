---
title: "Skip Clause (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QuerySkip"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "queries [Visual Basic], Skip"
  - "Skip statement"
  - "Skip clause"
ms.assetid: f00eb172-3907-4c43-9745-d8546ab86234
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Skip Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Ignora un numero specificato di elementi in una raccolta e quindi restituisce gli elementi rimanenti.  
  
## Sintassi  
  
```  
Skip count  
```  
  
## Parti  
 `count`  
 Obbligatorio.  Valore o espressione che restituisce il numero di elementi della sequenza da ignorare.  
  
## Note  
 La clausola `Skip` fa in modo che una query ignori gli elementi all'inizio di un elenco di risultati e restituisca gli elementi rimanenti.  Il numero di elementi da ignorare viene specificato dal parametro `count`.  
  
 È possibile utilizzare la clausola `Skip` con la clausola `Take` per restituire un intervallo di dati da qualsiasi segmento di una query.  A tale scopo, passare l'indice del primo elemento dell'intervallo alla clausola `Skip` e la dimensione dell'intervallo alla clausola `Take`.  
  
 Quando si utilizza la clausola `Skip` in una query, è necessario assicurarsi che i risultati vengano restituiti in un ordine che consente alla clausola `Skip` di ignorare i risultati desiderati.  Per ulteriori informazioni sull'ordinamento dei risultati di una query, vedere [Order By Clause](../../../visual-basic/language-reference/queries/order-by-clause.md).  
  
 È possibile utilizzare la clausola `SkipWhile` per specificare che vengano ignorati solo determinati elementi, in funzione di una condizione fornita.  
  
## Esempio  
 Nell'esempio di codice seguente viene utilizzata insieme la clausola `Skip` con la clausola `Take` per restituire dati da una query in pagine.  La funzione `GetCustomers` utilizza la clausola `Skip` per ignorare i clienti nell'elenco fino al valore di indice iniziale fornito e utilizza la clausola `Take` per restituire una pagina di clienti a partire da quel valore di indice.  
  
 [!code-vb[VbSimpleQuerySamples#1](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/skip-clause_1.vb)]  
  
## Vedere anche  
 [Introduction to LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Queries](../../../visual-basic/language-reference/queries/queries.md)   
 [Select Clause](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From Clause](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Order By Clause](../../../visual-basic/language-reference/queries/order-by-clause.md)   
 [Skip While Clause](../../../visual-basic/language-reference/queries/skip-while-clause.md)   
 [Take Clause](../../../visual-basic/language-reference/queries/take-clause.md)