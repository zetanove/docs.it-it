---
title: "This array is fixed or temporarily locked (Visual Basic) | Microsoft Docs"
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
  - "vbrID10"
dev_langs: 
  - "VB"
ms.assetid: de6713a6-51d7-4edb-8515-d5fb544e2091
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# This array is fixed or temporarily locked (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Le cause possibili dell'errore sono le seguenti:  
  
-   Utilizzo di `ReDim` per cambiare il numero di elementi di una matrice di dimensioni fisse.  
  
-   Ridimensionamento di una matrice dinamica a livello di modulo in cui un elemento è stato passato come argomento a una routine.  Se un elemento viene passato, la matrice viene bloccata per impedire la deallocazione di memoria per il parametro di riferimento all'interno della routine.  
  
-   Tentativo di assegnazione di un valore a una variabile `Variant` contenente una matrice, ma `Variant` al momento è bloccata.  
  
### Per correggere l'errore  
  
1.  Rendere dinamica e non fissa la matrice originale dichiarandola con `ReDim`, se è dichiarata all'interno di una routine, oppure dichiarandola senza specificare il numero di elementi, se è dichiarata a livello di modulo.  
  
2.  Stabilire se è effettivamente necessario passare l'elemento, dato che è visibile all'interno di tutte le routine nel modulo.  
  
3.  Stabilire cosa blocca `Variant` e porvi rimedio.  
  
## Vedere anche  
 [Matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md)