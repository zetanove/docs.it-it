---
title: "How to: Initialize an Array Variable in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "variables [Visual Basic], initializing"
  - "arrays [Visual Basic], variables"
  - "arrays [Visual Basic], initializing"
  - "arrays [Visual Basic], declaring"
ms.assetid: aadd7a60-7ca4-4608-b986-091f19e7fc10
caps.latest.revision: 42
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 42
---
# How to: Initialize an Array Variable in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Inizializzare una variabile di matrice includendo un valore letterale di matrice in una clausola `New` e specificando i valori iniziali della matrice.  È possibile specificare il tipo o consentire che sia dedotto dai valori nel valore letterale di matrice.  Per ulteriori informazioni su come viene dedotto il tipo, vedere l'argomento relativo al popolamento di una matrice con i valori iniziali in [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
### Per inizializzare una variabile di matrice tramite un valore letterale di matrice  
  
-   Nella clausola `New` o quando si assegna il valore della matrice, fornire i valori degli elementi tra parentesi graffe \(`{}`\).  Nell'esempio seguente vengono illustrati diversi modi per dichiarare, creare e inizializzare una variabile in modo che contenga una matrice con elementi di tipo `Char`.  
  
     [!code-vb[VbVbalrArrays#16](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/how-to-initialize-an-array-variable_1.vb)]  
  
     Dopo l'esecuzione di ciascuna istruzione, la matrice creata ha una lunghezza di 3, con elementi tra l'indice 0 e l'indice 2 contenenti i valori iniziali.  Se si specificano sia il limite superiore che i valori, è necessario includere un valore per ogni elemento dall'indice 0 al limite superiore.  
  
     Si noti che non è necessario specificare il limite superiore dell'indice se si forniscono i valori degli elementi in un valore letterale di matrice.  Se non viene specificato alcun limite superiore, la dimensione della matrice viene dedotta in base al numero di valori nel valore letterale di matrice.  
  
### Per inizializzare una variabile di matrice multidimensionale tramite valori letterali della matrice  
  
-   Annidare i valori tra parentesi graffe \(`{}`\).  Assicurarsi che i valori letterali della matrice annidati vengano tutti dedotti come matrici dello stesso tipo e con la stessa lunghezza.  Nell'esempio di codice seguente vengono illustrati diversi esempi di inizializzazione di matrici multidimensionali.  
  
     [!code-vb[VbVbalrArrays#17](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/how-to-initialize-an-array-variable_2.vb)]  
  
-   È possibile specificare in modo esplicito i limiti della matrice o tralasciarli e fare in modo che il compilatore li deduca in base ai valori nel valore letterale di matrice.  Se si specificano sia i limiti superiori che i valori, è necessario includere un valore per ogni elemento dall'indice 0 al limite superiore in ciascuna dimensione.  Nell'esempio seguente vengono illustrati diversi modi per dichiarare, creare e inizializzare una variabile in modo che contenga una matrice bidimensionale con elementi di tipo `Short`.  
  
     [!code-vb[VbVbalrArrays#18](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/how-to-initialize-an-array-variable_3.vb)]  
  
     Dopo l'esecuzione di ciascuna istruzione, la matrice creata contiene sei elementi inizializzati che includono gli indici `(0,0)`, `(0,1)`, `(0,2)`, `(1,0)`, `(1,1)` e `(1,2)`.  Ogni posizione della matrice contiene il valore `10`.  
  
-   L'esempio seguente scorrere una matrice multidimensionale.  In un'applicazione della console Windows scritta in Visual Basic, incollare il codice nel metodo `Sub Main()`.  Gli ultimi commenti illustrano l'output.  
  
     [!code-vb[VbVbalrArrays#31](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/how-to-initialize-an-array-variable_4.vb)]  
  
### Per inizializzare una variabile di matrice di matrici tramite valori letterali della matrice  
  
-   Annidare i valori degli oggetti tra parentesi graffe \(`{}`\).  Sebbene sia possibile annidare anche valori letterali della matrice che specificano matrici di lunghezze diverse, nel caso di una matrice di matrici assicurarsi che i valori letterali della matrice annidati siano racchiusi tra parentesi \(`()`\).  Le parentesi forzano la valutazione dei valori letterali della matrice annidati e le matrici risultanti vengono utilizzate come valori iniziali della matrice di matrici.  Nell'esempio di codice seguente vengono illustrati diversi esempi di inizializzazione di matrici di matrici.  
  
     [!code-vb[VbVbalrArrays#19](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/how-to-initialize-an-array-variable_5.vb)]  
  
-   L'esempio seguente scorrere una matrice di matrici.  In un'applicazione della console Windows scritta in Visual Basic, incollare il codice nel metodo `Sub Main()`.  Gli ultimi commenti nel codice illustrano l'output.  
  
     [!code-vb[VbVbalrArrays#32](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/how-to-initialize-an-array-variable_6.vb)]  
  
## Vedere anche  
 [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [Troubleshooting Arrays](../../../../visual-basic/programming-guide/language-features/arrays/troubleshooting-arrays.md)