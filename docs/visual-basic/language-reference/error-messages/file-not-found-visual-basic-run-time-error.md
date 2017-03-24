---
title: "File not found (Visual Basic Run-Time Error) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID53"
dev_langs: 
  - "VB"
ms.assetid: 57addb16-6f9a-444d-8af8-dda52431daca
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# File not found (Visual Basic Run-Time Error)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il file non è stato trovato dove specificato.  Le cause possibili dell'errore sono le seguenti:  
  
-   Un'istruzione fa riferimento a un file che non esiste.  
  
-   Si è tentato di chiamare una routine in una libreria a collegamento dinamico \(DLL\), ma è impossibile trovare la libreria specificata nella clausola `Lib` dell'istruzione `Declare`.  
  
-   Si è tentato di aprire un progetto o di caricare un file di testo che non esiste.  
  
### Per correggere l'errore  
  
1.  Controllare che il nome del file e la specifica del percorso siano stati digitati correttamente.  
  
## Vedere anche  
 [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)