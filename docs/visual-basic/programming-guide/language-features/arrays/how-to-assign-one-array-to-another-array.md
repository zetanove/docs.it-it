---
title: "How to: Assign One Array to Another Array (Visual Basic) | Microsoft Docs"
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
  - "covariance, arrays"
  - "arrays [Visual Basic], assigning"
  - "arrays [Visual Basic], covariance"
ms.assetid: 1ae89ea5-f292-4282-bcfc-e9b06b37fbd5
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# How to: Assign One Array to Another Array (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Poiché le matrici sono oggetti, è possibile utilizzarle in istruzioni di assegnazione in modo del tutto analogo agli altri tipi di oggetti.  Una variabile di matrice contiene un puntatore ai dati che costituiscono gli elementi della matrice e le informazioni su numero di dimensioni e lunghezza. Un'assegnazione prevede solo la copia di tale puntatore.  
  
### Per assegnare una matrice a un'altra matrice  
  
1.  Assicurarsi che le due matrici abbiano lo stesso numero di dimensioni e tipi di dati degli elementi compatibili.  
  
2.  Assegnare la matrice di origine a quella di destinazione utilizzando un'istruzione di assegnazione standard.  Non far seguire da parentesi i nomi delle matrici.  
  
    ```  
    Dim formArray() As System.Windows.Forms.Form  
    Dim controlArray() As System.Windows.Forms.Control  
    controlArray = formArray  
    ```  
  
 Quando si assegna una matrice a un'altra, vengono adottati i seguenti criteri:  
  
-   **Numeri di dimensioni uguali.** Il numero di dimensioni della matrice di destinazione deve corrispondere a quello della matrice di origine.  
  
     A differenza del numero di dimensioni, non è necessario che le dimensioni delle due matrici corrispondano.  Il numero di elementi di una data dimensione può essere modificato durante l'assegnazione.  
  
-   **Tipi degli elementi.** È necessario che entrambe le matrici contengano elementi *tipo di riferimento* o *tipo di valore*.  Per ulteriori informazioni, vedere [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md).  
  
    -   Se entrambe le matrici contengono elementi di tipo valore, è necessario che i tipi di dati degli elementi siano identici.  L'unica eccezione è che è possibile assegnare una matrice di elementi `Enum` a una matrice del tipo base dell'elemento `Enum`.  
  
    -   Se entrambe le matrici contengono elementi tipo di riferimento, è necessario che il tipo di elemento di origine derivi dal tipo di elemento di destinazione.  In tal caso, le due matrici presentano la stessa relazione di ereditarietà dei rispettivi elementi.  Questa condizione è denominata *covariante di matrici*.  
  
 Se i criteri sopra esposti non vengono rispettati, ad esempio se i tipi di dati non sono compatibili o se i numeri di dimensioni non corrispondono, verrà generato un errore di compilazione.  È possibile aggiungere al codice istruzioni per la gestione degli errori per garantire, prima di tentare un'assegnazione, che le matrici siano compatibili.  Per evitare di generare un'eccezione, è anche possibile utilizzare la parola chiave [TryCast Operator](../../../../visual-basic/language-reference/operators/trycast-operator.md).  
  
## Vedere anche  
 [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [Troubleshooting Arrays](../../../../visual-basic/programming-guide/language-features/arrays/troubleshooting-arrays.md)   
 [Enum Statement](../../../../visual-basic/language-reference/statements/enum-statement.md)   
 [Array Conversions](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)