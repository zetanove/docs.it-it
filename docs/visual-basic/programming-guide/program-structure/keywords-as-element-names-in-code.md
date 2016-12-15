---
title: "Keywords as Element Names in Code (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Visual Basic code, naming conventions"
  - "keywords [Visual Basic], in code"
  - "name conflicts"
  - "element names, in code"
ms.assetid: 2e4e8e02-23f7-49b9-a1c8-2b0402b6b525
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Keywords as Element Names in Code (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Qualsiasi elemento del programma \(variabile, classe o membro\) può avere lo stesso nome di una parola chiave riservata.  È ad esempio possibile creare una variabile denominata `Loop`.  Tuttavia, per fare riferimento alla propria versione della variabile \(che ha lo stesso nome della parola chiave riservata `Loop`\), è necessario qualificarla anteponendo la corrispondente stringa completa o racchiuderla tra parentesi quadre \(`[ ]`\), come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbcnConventions#8](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/keywords-as-element-names-in-code_1.vb)]  
  
 In caso contrario, Visual Basic presupporrà l'utilizzo della parola chiave intrinseca `Loop` e genererà un errore, come nell'esempio seguente:  
  
 `' The following statement causes a compiler error.`  
  
 `Loop.Visible = True`  
  
 Le parentesi quadre possono essere utilizzate per fare riferimento a form e controlli e per la dichiarazione di una variabile o la definizione di una routine con lo stesso nome di una parola chiave riservata.  Spesso può accadere che si dimentichi di qualificare i nomi o di racchiuderli tra parentesi quadre, introducendo così errori nel codice oltre a renderne più difficile la lettura.  Si consiglia pertanto di non utilizzare le parole chiave riservate come nome di elementi del programma.  Tuttavia, se in una versione futura di Visual Basic verrà definita una nuova parola chiave in conflitto con un nome di form o di controllo esistente, si potrà adottare questa tecnica durante l'aggiornamento del codice per renderlo compatibile con la nuova versione.  
  
> [!NOTE]
>  Nel programma è possibile includere anche nomi di elementi forniti da altri assembly a cui si fa riferimento.  Se tali nomi sono in conflitto con parole chiave riservate, racchiudendoli tra parentesi quadre si costringerà Visual Basic a interpretarli come elementi definiti.  
  
## Vedere anche  
 [Visual Basic Naming Conventions](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)   
 [Struttura del programma e convenzioni di scrittura del codice](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)