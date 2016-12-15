---
title: "Join Clause (Visual Basic) | Microsoft Docs"
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
  - "vb.QueryJoinIn"
  - "vb.QueryJoin"
  - "vb.QueryJoinOn"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "queries [Visual Basic], Join"
  - "Join statement"
  - "Join clause"
ms.assetid: 6dd37936-b27c-4e00-98ad-154b23f4de64
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Join Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Combina due raccolte in un'unica raccolta.  L'operazione di join è basata sulla corrispondenza di chiavi e utilizza l'operatore `Equals`.  
  
## Sintassi  
  
```  
Join element In collection _  
  [ joinClause _ ]   
  [ groupJoinClause ... _ ]   
On key1 Equals key2 [ And key3 Equals key4 [... ]  
```  
  
## Parti  
 `element`  
 Necessario.  La variabile di controllo per la raccolta da unire.  
  
 `collection`  
 Necessario.  La raccolta da combinare con la raccolta identificata sul lato sinistro dell'operatore `Join`.  Una clausola `Join` può essere annidata in un'altra clausola `Join` o in una clausola `Group Join`.  
  
 `joinClause`  
 Opzionale.  Uno o più clausole `Join` aggiuntive per perfezionare la query.  
  
 `groupJoinClause`  
 Opzionale.  Uno o più clausole `Group Join` aggiuntive per perfezionare la query.  
  
 `key1` `Equals` `key2`  
 Necessario.  Identifica le chiavi per le raccolte da unire.  È necessario utilizzare l'operatore `Equals` per confrontare le chiavi dalle raccolte da unire.  È possibile combinare condizioni di join utilizzando l'operatore `And` per identificare più chiavi.  Il parametro `key1` deve provenire dalla raccolta sul lato sinistro dell'operatore `Join`.  Il parametro `key2` deve provenire dalla raccolta sul lato destro dell'operatore `Join`.  
  
 Le chiavi utilizzate nella condizione di join possono essere espressioni che includono più di un elemento della raccolta.  Tuttavia ogni espressione di chiave può contenere solo elementi della rispettiva raccolta.  
  
## Note  
 La clausola `Join` combina due raccolte in base ai valori chiave corrispondenti delle raccolte da unire.  La raccolta risultante può contenere qualsiasi combinazione di valori dalla raccolta identificata sul lato sinistro dell'operatore `Join` e dalla raccolta identificata nella clausola `Join`.  La query restituirà solo risultati per cui la condizione specificata dall'operatore `Equals` è soddisfatta.  Equivale ad un `INNER JOIN` in SQL.  
  
 È possibile utilizzare più clausole `Join` in una query per unire due o più raccolte in un'unica raccolta.  
  
 È possibile eseguire un join implicito per unire raccolte senza la clausola `Join`.  Per eseguire questa operazione, includere più clausole `In` nella clausola `From` e specificare una clausola `Where` che identifica le chiavi da utilizzare per il join.  
  
 È possibile utilizzare la clausola `Group Join` per combinare più raccolte in un' unica raccolta gerarchica.  Equivale a `LEFT OUTER JOIN` in SQL.  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrato come eseguire un join implicito per combinare un elenco di clienti con i rispettivi ordini.  
  
 [!code-vb[VbSimpleQuerySamples#13](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/join-clause_1.vb)]  
  
## Esempio  
 Nell'esempio di codice seguente vengono unite due raccolte utilizzando la clausola `Join`.  
  
 [!code-vb[VbSimpleQuerySamples#12](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/join-clause_2.vb)]  
  
 In questo esempio viene prodotto un output simile al seguente:  
  
 `winlogon (968), Windows Logon`  
  
 `explorer (2424), File Explorer`  
  
 `cmd (5136), Command Window`  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrato come unire due raccolte utilizzando la clausola `Join`con due colonne di chiavi.  
  
 [!code-vb[VbSimpleQuerySamples#17](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/join-clause_3.vb)]  
  
 In questo esempio viene prodotto un output simile al seguente:  
  
 `winlogon (968), Windows Logon, Priority = 13`  
  
 `cmd (700), Command Window, Priority = 8`  
  
 `explorer (2424), File Explorer, Priority = 8`  
  
## Vedere anche  
 [Introduction to LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Queries](../../../visual-basic/language-reference/queries/queries.md)   
 [Select Clause](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From Clause](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Group Join Clause](../../../visual-basic/language-reference/queries/group-join-clause.md)   
 [Where Clause](../../../visual-basic/language-reference/queries/where-clause.md)