---
title: "Distinct Clause (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryDistinct"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Distinct clause"
  - "Distinct statement"
  - "queries [Visual Basic], Distinct"
ms.assetid: 86f42614-0d8f-4ffc-b888-ce8a37a8d36a
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Distinct Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Limita i valori della variabile di intervallo corrente per eliminare i valori duplicati nelle successive clausole di query.  
  
## Sintassi  
  
```  
Distinct  
```  
  
## Note  
 È possibile utilizzare la clausola `Distinct` per restituire un elenco di elementi univoci.  La clausola `Distinct` consente alla query di ignorare i risultati duplicati.  La clausola `Distinct` si applica ai valori duplicati per tutti i campi restituiti specificati dalla clausola `Select`.  Se non viene specificata alcuna clausola `Select`, la clausola `Distinct` viene applicata alla variabile di intervallo per la query identificata nella clausola `From`.  Se la variabile di intervallo non è un tipo non modificabile, la query ignorerà un risultato solo se tutti i membri del tipo corrispondono a un risultato della query esistente.  
  
## Esempio  
 Nell'espressione di query seguente vengono uniti un elenco di clienti e un elenco di ordini del cliente.  La clausola `Distinct` viene inclusa per restituire un elenco di nomi cliente e data ordine univoci.  
  
 [!code-vb[VbSimpleQuerySamples#20](../../../visual-basic/language-reference/queries/codesnippet/VisualBasic/distinct-clause_1.vb)]  
  
## Vedere anche  
 [Introduction to LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Queries](../../../visual-basic/language-reference/queries/queries.md)   
 [From Clause](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Select Clause](../../../visual-basic/language-reference/queries/select-clause.md)   
 [Where Clause](../../../visual-basic/language-reference/queries/where-clause.md)