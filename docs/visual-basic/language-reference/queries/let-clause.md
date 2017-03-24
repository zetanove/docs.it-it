---
title: "Let Clause (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryLet"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "queries [Visual Basic], Let"
  - "Let clause"
  - "Let statement"
ms.assetid: 981aa516-16eb-4c53-b1f1-5aa3e82f316e
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Let Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Calcola un valore e lo assegna a una nuova variabile nella query.  
  
## Sintassi  
  
```  
Let variable = expression [, ...]  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`variable`|Obbligatorio.  Alias che può essere utilizzato per fare riferimento ai risultati dell'espressione fornita.|  
|`expression`|Obbligatorio.  Espressione che verrà valutata e assegnata alla variabile specificata.|  
  
## Note  
 La clausola `Let` consente di calcolare valori per ogni risultato della query e fare riferimento a essi utilizzando un alias.  L'alias può essere utilizzato in altre clausole, ad esempio nella clausola `Where`.  La clausola `Let` consente di creare un'istruzione di query che è più facile leggere perché è possibile specificare un alias per una clausola dell'espressione inclusa nella query e sostituire l'alias ogni volta che la clausola dell'espressione viene utilizzata.  
  
 È possibile includere un numero qualsiasi di assegnazioni `variable` e `expression` nella clausola `Let`.  Separare ogni assegnazione con una virgola \(,\).  
  
## Esempio  
 Nell'esempio di codice seguente viene utilizzata la clausola `Let` per calcolare un 10 percento di sconto sui prodotti.  
  
 [!code-vb[VbSimpleQuerySamples#16](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/let-clause_1.vb)]  
  
## Vedere anche  
 [Introduction to LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Queries](../../../visual-basic/language-reference/queries/queries.md)   
 [Select Clause](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From Clause](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Where Clause](../../../visual-basic/language-reference/queries/where-clause.md)