---
title: "Error in loading DLL (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID48"
dev_langs: 
  - "VB"
ms.assetid: 4226cd1f-028c-477d-88a5-cb57f7e0cdc8
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Error in loading DLL (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una libreria a collegamento dinamico \(DLL\) è una libreria specificata nella clausola `Lib` di un'istruzione `Declare`.  Alcune cause possibili di questo errore sono:  
  
-   Il file non è un eseguibile DLL.  
  
-   Il file non è una DLL di Microsoft Windows.  
  
-   La DLL fa riferimento a un'altra DLL che non esiste.  
  
-   La DLL o la DLL a cui si fa riferimento non si trova nella directory specificata nel percorso.  
  
### Per correggere l'errore  
  
-   Se il file è un file di testo di origine e non un eseguibile DLL, deve essere compilato e collegato a un form eseguibile DLL.  
  
-   Se il file non è una DLL di Microsoft Windows, procurarsi l'equivalente di Microsoft Windows.  
  
-   Se la DLL fa riferimento a un'altra DLL che non è presente, procurarsela e renderla disponibile.  
  
-   Se la DLL o la DLL a cui si fa riferimento non si trova nella directory specificata dal percorso, spostarla in una directory con riferimento.  
  
## Vedere anche  
 [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)