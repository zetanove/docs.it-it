---
title: "Bad file name or number | Microsoft Docs"
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
  - "vbrID52"
dev_langs: 
  - "VB"
ms.assetid: d0e96aea-7621-48f6-a78b-5d37d18aaa4e
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Bad file name or number
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Si è verificato un errore durante il tentativo di accedere al file specificato.  Di seguito sono riportate le cause possibili dell'errore.  
  
-   Un'istruzione fa riferimento a un file con un nome o un numero che non è stato specificato nell'istruzione `FileOpen` o che è stato specificato in un'istruzione `FileOpen` ma è stato successivamente chiuso.  
  
-   Un'istruzione fa riferimento a un file con un numero che non rientra nell'intervallo dei numeri di file.  
  
-   Un'istruzione fa riferimento a un nome o a un numero di file non valido.  
  
### Per correggere l'errore  
  
1.  Controllare che il nome del file sia specificato in un'istruzione `FileOpen`.  Se l'istruzione `FileClose` è stata richiamata senza argomenti, tutti i file aperti potrebbero essere stati inavvertitamente chiusi.  
  
2.  Se il codice sta generando numeri di file in modo algoritmico, accertarsi che i numeri siano validi.  
  
3.  Assicurarsi che i nomi dei file siano conformi alle convenzioni del sistema operativo.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileSystem.FileOpen%2A>   
 [Visual Basic Naming Conventions](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)