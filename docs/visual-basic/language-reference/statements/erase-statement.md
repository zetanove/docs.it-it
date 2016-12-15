---
title: "Erase Statement (Visual Basic) | Microsoft Docs"
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
  - "vb.Erase"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Erase keyword"
  - "Erase statement"
ms.assetid: 7a8133d7-b750-4d74-8b66-ba1dd9778d4b
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Erase Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Viene utilizzata per rilasciare variabili di matrice e rendere nuovamente disponibile la memoria utilizzata per i relativi elementi.  
  
## Sintassi  
  
```  
Erase arraylist  
```  
  
## Parti  
 `arraylist`  
 Obbligatorio.  Elenco delle variabili di matrice da cancellare.  Le variabili sono separate da una virgola.  
  
## Note  
 L'istruzione `Erase` può essere utilizzata solo a livello di routine.  e non consente quindi di rilasciare matrici a livello di modulo o classe ma solo in una routine.  
  
 L'istruzione `Erase` equivale ad assegnare `Nothing` a ogni variabile di matrice.  
  
## Esempio  
 Nell'esempio seguente l'istruzione `Erase` viene utilizzata per cancellare due matrici e liberare la relativa memoria \(rispettivamente 1000 e 100 elementi memorizzati\).  L'istruzione `ReDim` consente quindi di assegnare una nuova istanza di matrice alla matrice tridimensionale.  
  
 [!code-vb[VbVbalrStatements#19](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/erase-statement_1.vb)]  
  
## Vedere anche  
 [Nothing](../../../visual-basic/language-reference/nothing.md)   
 [ReDim Statement](../../../visual-basic/language-reference/statements/redim-statement.md)