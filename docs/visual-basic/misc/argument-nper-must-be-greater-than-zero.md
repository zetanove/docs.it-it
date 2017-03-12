---
title: "L&#39;argomento &#39;NPer&#39; deve essere maggiore di zero | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrRate_NPerMustBeGTZero"
ms.assetid: d49242df-dbd1-4b26-bd8c-ed56d24fdfcd
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# L&#39;argomento &#39;NPer&#39; deve essere maggiore di zero
La funzione `NPer`, che restituisce un valore `Double` che specifica il numero di periodi per un'annualità in base a pagamenti periodici fissi e a un tasso di interesse fisso, richiede un argomento maggiore di zero.  
  
### Per correggere l'errore  
  
-   Controllare l'ortografia degli argomenti nell'espressione. Un nome di variabile scritto in modo non corretto può creare implicitamente una variabile numerica inizializzata su zero.  
  
-   Controllare le operazioni precedenti nelle variabili dell'espressione, specialmente quelle passate alla routine come argomenti da altre routine.  
  
## Vedere anche  
 [NOT IN BUILD: Funzione NPer](http://msdn.microsoft.com/it-it/56567d16-29f7-4928-b05f-b4cd56d4fd42)   
 [Passing Arguments by Value and by Reference](../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)