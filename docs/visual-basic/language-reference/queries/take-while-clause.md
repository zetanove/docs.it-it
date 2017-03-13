---
title: "Take While Clause (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryTakeWhile"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "queries [Visual Basic], Take While"
  - "Take While clause"
  - "Take While statement"
ms.assetid: db8f9f2f-fc9f-4a6c-b0b8-1bf048147e11
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# Take While Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Include gli elementi in una raccolta finché la condizione specificata è `true` e quindi ignora gli elementi rimanenti.  
  
## Sintassi  
  
```  
Take While expression  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`expression`|Obbligatorio.  Espressione che rappresenta una condizione di test per gli elementi.  L'espressione deve restituire un valore `Boolean` o un equivalente funzionale, ad esempio un `Integer` da valutare come un `Boolean`.|  
  
## Note  
 La clausola `Take While` include elementi dall'inizio di un risultato della query finché l'oggetto `expression` fornito restituisce `false`.  Quando `expression` restituisce `false`, la query ignora tutti gli elementi rimanenti.  Per i restanti risultati `expression` viene ignorata.  
  
 La clausola `Take While` differisce dalla clausola `Where` per il fatto che la clausola `Where` può essere utilizzata per includere da una query tutti gli elementi che soddisfano una particolare condizione.  La clausola `Take While` include gli elementi solo fino alla prima occasione in cui la condizione non è soddisfatta.  La clausola `Take While` è molto utile quando si sta lavorando con un risultato della query ordinato.  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrato come utilizzare la clausola `Take While` per recuperare i risultati finché non viene trovato il primo dei clienti senza ordini.  
  
 [!code-vb[VbSimpleQuerySamples#2](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/take-while-clause_1.vb)]  
  
## Vedere anche  
 [Introduction to LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Queries](../../../visual-basic/language-reference/queries/queries.md)   
 [Select Clause](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From Clause](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Take Clause](../../../visual-basic/language-reference/queries/take-clause.md)   
 [Skip While Clause](../../../visual-basic/language-reference/queries/skip-while-clause.md)   
 [Where Clause](../../../visual-basic/language-reference/queries/where-clause.md)