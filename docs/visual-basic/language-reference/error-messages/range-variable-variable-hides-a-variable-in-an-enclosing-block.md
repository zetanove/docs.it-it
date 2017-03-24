---
title: "Range variable &lt;variable&gt; hides a variable in an enclosing block, a previously defined range variable, or an implicitly declared variable in a query expression | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc36633"
  - "vbc36633"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36633"
ms.assetid: 5d5470e4-3de5-49c2-8831-1087625f4a77
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# Range variable &lt;variable&gt; hides a variable in an enclosing block, a previously defined range variable, or an implicitly declared variable in a query expression
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un nome di variabile di intervallo specificato in una clausola `Select`, `From`, `Aggregate` o `Let` duplica il nome di una variabile di intervallo già specificato nella query o il nome di una variabile dichiarata implicitamente dalla query, ad esempio un nome di campo o il nome di una funzione di aggregazione.  
  
 **ID errore:** BC36633  
  
### Per correggere l'errore  
  
-   Assicurarsi che tutte le variabili di intervallo in un particolare ambito di query abbiano nomi univoci.  È possibile includere una query tra parentesi per assicurare che le query annidate abbiano un ambito univoco.  
  
## Vedere anche  
 [Introduction to LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [From Clause](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Let Clause](../../../visual-basic/language-reference/queries/let-clause.md)   
 [Aggregate Clause](../../../visual-basic/language-reference/queries/aggregate-clause.md)   
 [Select Clause](../../../visual-basic/language-reference/queries/select-clause.md)