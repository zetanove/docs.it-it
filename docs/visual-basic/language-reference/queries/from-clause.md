---
title: "From Clause (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryFrom"
  - "vb.QueryFromIn"
  - "vb.QueryFromLet"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "queries [Visual Basic], From"
  - "From clause"
  - "From statement"
ms.assetid: 83e3665e-68a0-4540-a3a3-3d777a0f95d5
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# From Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica uno o più variabili di intervallo e una raccolta su cui eseguire una query.  
  
## Sintassi  
  
```  
From element [ As type ] In collection [ _ ]  
  [, element2 [ As type2 ] In collection2 [, ... ] ]  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`element`|Obbligatorio.  Una *variabile di intervallo* utilizzata per scorrere gli elementi della raccolta.  Una variabile di intervallo viene utilizzata per fare riferimento a ogni membro di `collection` quando la query scorre `collection`.  Deve essere un tipo enumerabile.|  
|`type`|Parametro facoltativo.  Tipo di `element`.  Se non è specificato alcun `type`, il tipo di `element` viene dedotto da `collection`.|  
|`collection`|Obbligatorio.  Fa riferimento alla raccolta su cui deve essere eseguita la query.  Deve essere un tipo enumerabile.|  
  
## Note  
 La clausola `From` viene utilizzata per identificare i dati di origine per una query e le variabili utilizzate per fare riferimento a un elemento dalla raccolta di origine.  Queste variabili sono chiamate *variabili di intervallo*.  La clausola `From` è obbligatoria per una query, salvo quando viene utilizzata la clausola `Aggregate` per identificare una query che restituisce solo risultati aggregati.  Per ulteriori informazioni, vedere [Aggregate Clause](../../../visual-basic/language-reference/queries/aggregate-clause.md).  
  
 È possibile specificare più clausole `From` in una query per identificare più raccolte da unire.  Quando sono specificati più raccolte, l'iterazione viene eseguita su ognuna in modo indipendente, oppure è possibile unirle se sono correlate.  È possibile unire le raccolte implicitamente utilizzando la clausola `Select` o in modo esplicito utilizzando le clausole `Join` o `Group Join` In alternativa, è possibile specificare più variabili di intervallo e raccolte in una sola clausola `From`, con ogni variabile di intervallo correlata e ogni raccolta separate dalle altre da una virgola.  Nell'esempio di codice seguente vengono illustrate entrambe le opzioni di sintassi per la clausola `From`.  
  
 [!code-vb[VbSimpleQuerySamples#21](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/from-clause_1.vb)]  
  
 La clausola `From` definisce l'ambito di una query, che è simile all'ambito di un ciclo `For`.  Pertanto, la variabile di intervallo di ogni `element` nell'ambito di una query deve avere un nome univoco.  Poiché è possibile specificare più clausole `From` per una query, le clausole `From` successive possono fare riferimento alle variabili di intervallo nella clausola `From` oppure possono fare riferimento alle variabili di intervallo in una clausola `From` precedente.  Nell'esempio seguente viene illustrata una clausola `From` annidata in cui la raccolta nella seconda clausola è basata su una proprietà della variabile di intervallo della prima clausola.  
  
 [!code-vb[VbSimpleQuerySamples#22](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/from-clause_2.vb)]  
  
 Ogni clausola `From` può essere seguita da una qualsiasi combinazione di clausole query aggiuntive per perfezionare la query.  A tale proposito, è possibile procedere come indicato di seguito:  
  
-   Unire le raccolte implicitamente utilizzando le clausole `From` e `Select`, oppure in modo esplicito utilizzando le clausole `Join` o `Group Join`  
  
-   Utilizzare la clausola `Where` per filtrare il risultato della query.  
  
-   Ordinare il risultato utilizzando la clausola `Order By`.  
  
-   Raggruppare risultati simili utilizzando la clausola `Group By`.  
  
-   Utilizzare la clausola `Aggregate` per identificare funzioni di aggregazione per valutare l'intero risultato della query.  
  
-   Utilizzare la clausola `Let` per introdurre una variabile di iterazione il cui valore viene determinato da un'espressione anziché da una raccolta.  
  
-   Utilizzare la clausola `Distinct` per ignorare i risultati duplicati della query.  
  
-   Identificare parti del risultato da restituire utilizzando le clausole `Skip`, `Take`, `Skip While`e `Take While`  
  
## Esempio  
 Nell'espressione di query seguente viene utilizzata una clausola `From` per dichiarare una variabile di intervallo `cust` per ogni oggetto `Customer` nella raccolta `customers`.  La clausola `Where` utilizza la variabile di intervallo per restringere l'output ai clienti dalla regione specificata.  Il ciclo `For Each` visualizza il nome di azienda per ogni cliente nel risultato della query.  
  
 [!code-vb[VbSimpleQuerySamples#23](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/from-clause_3.vb)]  
  
## Vedere anche  
 [Queries](../../../visual-basic/language-reference/queries/queries.md)   
 [Introduction to LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Istruzione For Each...Next](../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [Istruzione For...Next](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Select Clause](../../../visual-basic/language-reference/queries/select-clause.md)   
 [Where Clause](../../../visual-basic/language-reference/queries/where-clause.md)   
 [Aggregate Clause](../../../visual-basic/language-reference/queries/aggregate-clause.md)   
 [Distinct Clause](../../../visual-basic/language-reference/queries/distinct-clause.md)   
 [Join Clause](../../../visual-basic/language-reference/queries/join-clause.md)   
 [Group Join Clause](../../../visual-basic/language-reference/queries/group-join-clause.md)   
 [Order By Clause](../../../visual-basic/language-reference/queries/order-by-clause.md)   
 [Let Clause](../../../visual-basic/language-reference/queries/let-clause.md)   
 [Skip Clause](../../../visual-basic/language-reference/queries/skip-clause.md)   
 [Take Clause](../../../visual-basic/language-reference/queries/take-clause.md)   
 [Skip While Clause](../../../visual-basic/language-reference/queries/skip-while-clause.md)   
 [Take While Clause](../../../visual-basic/language-reference/queries/take-while-clause.md)