---
title: "Visual Basic Limitations | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "limits"
  - "limitations, Visual Basic"
  - "limitations"
  - "limits, Visual Basic code"
  - "Visual Basic code, limitations"
ms.assetid: cf1646b7-5d24-48c6-9616-bda8a4849d91
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Visual Basic Limitations
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Nelle versioni precedenti di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] venivano applicati i limiti nel codice, come la lunghezza dei nomi delle variabili, il numero di variabili consentite nei moduli e le dimensioni dei moduli.  In [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] queste limitazioni sono state ridotte, fornendo una maggiore libertà nella scrittura e nella disposizione nel codice.  
  
 I limiti fisici sono dipendenti più dalla memoria in fase di esecuzione che dalle considerazioni in fase di compilazione.  Se si utilizzano procedure di programmazione prudenti e si dividono le applicazioni di grandi dimensioni in più classi e moduli, esistono poche probabilità che si verifichi un limite interno di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
 Di seguito vengono illustrati alcuni limiti che possono verificarsi in casi estremi.  
  
-   **Lunghezza del nome.** Esiste un numero massimo di caratteri per il nome di ogni elemento di programmazione dichiarato.  Questo numero massimo si applica a un'intera stringa di qualifica se viene qualificato il nome dell'elemento.  Per informazioni, vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
-   **Lunghezza della riga.** Esiste un massimo di 65535 in una riga fisica di codice sorgente.  La riga del codice sorgente logico può essere più lunga se se utilizzano i caratteri di continuazione di riga.  Per informazioni, vedere [Procedura: Interrompere e combinare istruzioni nel codice](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md).  
  
-   **Dimensioni della matrice.** Esiste un numero massimo di dimensioni dichiarabili per una matrice.  Questo limita il numero degli indici da utilizzare per specificare un elemento della matrice.  Per informazioni, vedere [Array Dimensions in Visual Basic](../../../visual-basic/programming-guide/language-features/arrays/array-dimensions.md).  
  
-   **Lunghezza della stringa.** Esiste un numero massimo di caratteri Unicode memorizzabili in una stringa singola.  Per informazioni, vedere [String Data Type](../../../visual-basic/language-reference/data-types/string-data-type.md).  
  
-   **Lunghezza della stringa di ambiente.** Per ogni stringa di ambiente esiste un massimo di 32768 caratteri utilizzati come argomento della riga di comando.  Si tratta di una limitazione di tutte le piattaforme.  
  
## Vedere anche  
 [Struttura del programma e convenzioni di scrittura del codice](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [Visual Basic Naming Conventions](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)