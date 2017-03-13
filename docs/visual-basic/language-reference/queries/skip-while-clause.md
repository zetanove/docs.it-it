---
title: "Skip While Clause (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QuerySkipWhile"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Skip While statement"
  - "Skip While clause"
  - "queries [Visual Basic], Skip While"
ms.assetid: 5dee8350-7520-4f1a-b00d-590cacd572d6
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Skip While Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Ignora gli elementi in una raccolta finché la condizione specificata è `true` e quindi restituisce gli elementi rimanenti.  
  
## Sintassi  
  
```  
Skip While expression  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`expression`|Obbligatorio.  Espressione che rappresenta una condizione di test per gli elementi.  L'espressione deve restituire un valore `Boolean` o un equivalente funzionale, ad esempio un `Integer` da valutare come un `Boolean`.|  
  
## Note  
 La clausola `Skip While` ignora elementi dall'inizio di un risultato della query finché l'oggetto `expression` fornito non restituisce `false`.  Quando `expression` restituisce `false`, la query restituisce tutti gli elementi rimanenti.  Per i restanti risultati `expression` viene ignorata.  
  
 La clausola `Skip While` differisce dalla clausola `Where` per il fatto che la clausola `Where` può essere utilizzata per escludere da una query tutti gli elementi che non soddisfano una particolare condizione.  La clausola `Skip While` esclude gli elementi solo fino alla prima volta che la condizione non è soddisfatta.  La clausola `Skip While` è molto utile quando si sta lavorando con un risultato della query ordinato.  
  
 È possibile ignorare un numero specificato di risultati dall'inizio di un risultato della query utilizzando la clausola `Skip`.  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrato come utilizzare la clausola `Skip While` per ignorare i risultati finché non viene trovato il primo cliente dagli Stati Uniti.  
  
 [!code-vb[VbSimpleQuerySamples#3](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/skip-while-clause_1.vb)]  
  
## Vedere anche  
 [Introduction to LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Queries](../../../visual-basic/language-reference/queries/queries.md)   
 [Select Clause](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From Clause](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Skip Clause](../../../visual-basic/language-reference/queries/skip-clause.md)   
 [Take While Clause](../../../visual-basic/language-reference/queries/take-while-clause.md)   
 [Where Clause](../../../visual-basic/language-reference/queries/where-clause.md)