---
title: "How to: Move Data Into and Out of a Variable (Visual Basic) | Microsoft Docs"
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
  - "variables [Visual Basic], retrieving values"
  - "variables [Visual Basic], storing data"
ms.assetid: 93744f46-bf78-4fa0-9640-1de01bc38d9a
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Move Data Into and Out of a Variable (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Per memorizzare un valore in una variabile, è necessario inserirne il nome a sinistra di un'istruzione di assegnazione.  
  
## Inserimento di dati in una variabile  
  
#### Per memorizzare un valore in una variabile  
  
-   Utilizzare il nome della variabile a sinistra di un'istruzione di assegnazione.  
  
     Nell'esempio riportato di seguito viene impostato il valore della variabile `alpha`.  
  
    ```  
    alpha = (beta * 6.27) / (gamma + 2.1)  
    ```  
  
     Il valore generato a destra dell'istruzione di assegnazione viene memorizzato nella variabile.  
  
## Recupero di dati da una variabile  
 Per recuperare il valore di una variabile, includerne il nome in un'espressione.  
  
#### Per recuperare un valore da una variabile  
  
-   Utilizzare il nome della variabile in un'espressione.  Le variabili possono essere utilizzate in tutte le occasioni in cui è consentito l'utilizzo di una costante o di un valore letterale, con l'unica eccezione delle espressioni in cui viene definito il valore di una costante.  
  
     In alternativa  
  
-   Utilizzare il nome della variabile che segue il segno di uguale \(`=`\) in un'istruzione di assegnazione.  
  
     Nell'esempio riportato di seguito il valore della variabile `startValue` viene letto, dopodiché il valore della variabile `counter` viene utilizzato in un'espressione.  
  
    ```  
    counter = startValue  
    cellValue = (counter + 5) ^ 2  
    ```  
  
     Il valore della variabile partecipa nell'espressione con le stesse modalità di una costante e viene quindi memorizzato nella variabile o proprietà a sinistra dell'istruzione di assegnazione.  
  
## Vedere anche  
 [Variables](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [Dichiarazione di variabili](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Object Variables](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)