---
title: "Object variable or With block variable not set | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID91"
dev_langs: 
  - "VB"
ms.assetid: 2f03e611-f0ed-465c-99a2-a816e034faa3
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# Object variable or With block variable not set
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il riferimento interessa una variabile non valida.  Per creare una variabile oggetto, è necessario prima dichiararla e quindi assegnare ad essa un riferimento valido tramite l'istruzione `Set`.  Analogamente, un blocco `With...End With` deve essere inizializzato eseguendo il punto di ingresso dell'istruzione `With`.  
  
### Per correggere l'errore  
  
1.  Assicurarsi che la variabile oggetto faccia riferimento a un oggetto valido e specificare o rispecificare un riferimento per l'oggetto.  
  
2.  Assicurarsi di non aver utilizzato una variabile oggetto impostata su `Nothing`.  
  
3.  Assicurarsi che la libreria degli oggetti in cui è stato descritto l'oggetto sia stata selezionata nella finestra di dialogo `Add References`.  
  
4.  Assicurarsi che il blocco `With` sia inizializzato eseguendo il punto di ingresso dell'istruzione `With`.  
  
## Vedere anche  
 [Object Variable Declaration](../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [With...End With Statement](../../../visual-basic/language-reference/statements/with-end-with-statement.md)