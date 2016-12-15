---
title: "Bad record length | Microsoft Docs"
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
  - "vbrID59"
dev_langs: 
  - "VB"
ms.assetid: 0926a3a4-177b-4452-9b33-d8a01e24cc21
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Bad record length
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Di seguito sono riportate le cause possibili dell'errore.  
  
-   La lunghezza della variabile di record specificata in un'istruzione `FileGet`, `FileGetObject`, `FilePut` o `FilePutObject` è diversa da quella specificata nell'istruzione `FileOpen` corrispondente.  
  
-   La variabile in un'istruzione `FilePut` o `FilePutObject` è o include una stringa di lunghezza variabile.  
  
-   La variabile in un'istruzione `FilePut` o `FilePutObject` è o include untipo `Variant`.  
  
### Per correggere l'errore  
  
1.  Assicurarsi che la somma delle dimensioni delle variabili di lunghezza fissa nel tipo definito dall'utente che definiscono il tipo della variabile di record corrisponda al valore indicato nella clausola `Len` dell'istruzione `FileOpen`.  
  
2.  Se la variabile in un'istruzione `FilePut` o `FilePutObject` è o include una stringa di lunghezza variabile, assicurarsi che quest'ultima contenga almeno 2 caratteri in meno rispetto alla lunghezza del record specificata nella clausola `Len` dell'istruzione `FileOpen`.  
  
3.  Se la variabile in un'istruzione `FilePut` o `FilePutObject` è o include un `Variant`, assicurarsi che la stringa di lunghezza variabile contenga almeno 4 byte in meno rispetto alla lunghezza del record specificata nella clausola `Len` dell'istruzione `FileOpen`.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileSystem.FileGet%2A>   
 <xref:Microsoft.VisualBasic.FileSystem.FileGetObject%2A>   
 <xref:Microsoft.VisualBasic.FileSystem.FilePut%2A>   
 <xref:Microsoft.VisualBasic.FileSystem.FilePutObject%2A>