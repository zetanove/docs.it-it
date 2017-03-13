---
title: "Group Join Clause (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryGroupJoinIn"
  - "vb.QueryGroupJoinOn"
  - "vb.QueryGroupJoin"
  - "vb.QueryGroupJoinInto"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Group Join clause"
  - "Group Join statement"
  - "queries [Visual Basic], Group Join"
ms.assetid: 37dbf79c-7b5c-421b-bbb7-dadfd2b92a1c
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# Group Join Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Combina due raccolte in un'unica raccolta gerarchica.  L'operazione di join è basata sulla corrispondenza di chiavi.  
  
## Sintassi  
  
```  
Group Join element [As type] In collection _  
  On key1 Equals key2 [ And key3 Equals key4 [... ] ] _  
  Into expressionList  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`element`|Obbligatorio.  La variabile di controllo per la raccolta da unire.|  
|`type`|Parametro facoltativo.  Tipo di `element`.  Se non è specificato alcun `type`, il tipo di `element` viene dedotto da `collection`.|  
|`collection`|Obbligatorio.  La raccolta da combinare con la raccolta sul lato sinistro dell'operatore `Group Join`.  Una clausola `Group Join` può essere annidata in una clausola `Join` o in un'altra clausola `Group Join`.|  
|`key1` `Equals` `key2`|Obbligatorio.  Identifica le chiavi per le raccolte da unire.  È necessario utilizzare l'operatore `Equals` per confrontare le chiavi dalle raccolte da unire.  È possibile combinare condizioni di join utilizzando l'operatore `And` per identificare più chiavi.  Il parametro `key1` deve provenire dalla raccolta sul lato sinistro dell'operatore `Join`.  Il parametro `key2` deve provenire dalla raccolta sul lato destro dell'operatore `Join`.<br /><br /> Le chiavi utilizzate nella condizione di join possono essere espressioni che includono più di un elemento della raccolta.  Tuttavia ogni espressione di chiave può contenere solo elementi della rispettiva raccolta.|  
|`expressionList`|Obbligatorio.  Una o più espressioni che identificano come vengono aggregati i gruppi di elementi della raccolta.  Per identificare un nome di membro per i risultati raggruppati, utilizzare la parola chiave `Group` \(`<alias> = Group`\).  È anche possibile includere funzioni di aggregazione da applicare al gruppo.|  
  
## Note  
 La clausola `Group Join` combina due raccolte in base ai valori chiave corrispondenti delle raccolte da unire.  La raccolta risultante può contenere un membro che fa riferimento a una raccolta di elementi dalla seconda raccolta che corrispondono al valore della chiave della prima raccolta.  È anche possibile specificare funzioni di aggregazione da applicare agli elementi raggruppati della seconda raccolta.  Per ulteriori informazioni sulle funzioni di aggregazione, vedere [Aggregate Clause](../../../visual-basic/language-reference/queries/aggregate-clause.md).  
  
 Si consideri, ad esempio, una raccolta di amministratori e una raccolta di dipendenti.  Gli elementi di entrambe le raccolte hanno una proprietà ManagerID che identifica i dipendenti che riportano a un particolare amministratore.  I risultati di un'operazione di join conterrebbero un risultato per ogni amministratore e ogni dipendente con valore corrispondente di ManagerID.  I risultati di un'operazione `Group Join` conterrebbero l'elenco completo degli amministratori.  Ogni amministratore nel risultato avrebbe un membro che fa riferimento all'elenco dei dipendenti che hanno una corrispondenza con lo specifico amministratore.  
  
 La raccolta risultante per un'operazione `Group Join` può contenere qualsiasi combinazione dei valori della raccolta identificata nella clausola `From` e delle espressioni identificate nella clausola `Into` della clausola `Group Join`.  Per ulteriori informazioni sulle espressioni valide per la clausola `Into`, vedere [Aggregate Clause](../../../visual-basic/language-reference/queries/aggregate-clause.md).  
  
 Un'operazione `Group Join` restituirà tutti i risultati della raccolta identificata sul lato sinistro dell'operatore `Group Join` Questo si verifica anche se non esistono corrispondenze tra le raccolte da unire.  Equivale a `LEFT OUTER JOIN` in SQL.  
  
 È possibile utilizzare la clausola `Join` per combinare più raccolte in un'unica raccolta.  Equivale ad un `INNER JOIN` in SQL.  
  
## Esempio  
 Nell'esempio di codice seguente vengono unite due raccolte utilizzando la clausola `Group Join`.  
  
 [!code-vb[VbSimpleQuerySamples#14](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/group-join-clause_1.vb)]  
  
## Vedere anche  
 [Introduction to LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Queries](../../../visual-basic/language-reference/queries/queries.md)   
 [Select Clause](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From Clause](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Join Clause](../../../visual-basic/language-reference/queries/join-clause.md)   
 [Where Clause](../../../visual-basic/language-reference/queries/where-clause.md)   
 [Clausola Group By](../../../visual-basic/language-reference/queries/group-by-clause.md)