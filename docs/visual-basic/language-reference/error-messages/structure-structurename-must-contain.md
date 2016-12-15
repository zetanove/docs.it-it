---
title: "Structure &#39;&lt;structurename&gt;&#39; must contain at least one instance member variable or at least one instance event declaration not marked &#39;Custom&#39; | Microsoft Docs"
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
  - "bc30941"
  - "vbc30941"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30941"
ms.assetid: 7054cc1e-bac3-4c3d-82f3-35772bd8dd3b
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Structure &#39;&lt;structurename&gt;&#39; must contain at least one instance member variable or at least one instance event declaration not marked &#39;Custom&#39;
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In una definizione di struttura non sono incluse variabili non condivise o eventi non personalizzati e non condivisi.  
  
 A ogni struttura deve essere associato un evento o una variabile applicabile a ciascuna istanza specifica \(non condivisa\) anziché a tutte le istanze collettivamente \([Shared](../../../visual-basic/language-reference/modifiers/shared.md)\).  Costanti, proprietà e routine non soddisfano questo requisito.  Inoltre, se è presente un solo evento non condiviso e nessuna variabile non condivisa, tale evento non può essere di tipo `Custom`.  
  
 **ID errore:** BC30941  
  
### Per correggere l'errore  
  
-   Definire almeno una variabile o un evento che non sia `Shared`.  Se si definisce un solo evento, questo deve essere non personalizzato e non condiviso.  
  
## Vedere anche  
 [Structures](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [How to: Declare a Structure](../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md)