---
title: "&#39;ReDim&#39; pu&#242; modificare solo la prima dimensione a destra | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrArray_TypeMismatch"
ms.assetid: d53cf41b-7a7a-466c-a29a-920d99698fa9
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# &#39;ReDim&#39; pu&#242; modificare solo la prima dimensione a destra
Un'istruzione `ReDim` ha tentato di usare la parola chiave `Preserve` per modificare una dimensione di una matrice che non è l'ultima dimensione. Quando si usa `Preserve`, si può ridimensionare solo l'ultima dimensione di una matrice. Per tutte le altre, è necessario specificare le stesse dimensioni di una matrice esistente.  
  
### Per correggere l'errore  
  
-   Rimuovere la parola chiave `Preserve`.  
  
## Vedere anche  
 [NOTINBUILD Cenni preliminari sulle matrici in Visual Basic](http://msdn.microsoft.com/it-it/ca50e2f2-b4d2-4c57-9169-9abbcc3392d8)   
 [NOTINBUILD Matrici multidimensionali in Visual Basic](http://msdn.microsoft.com/it-it/d92cad25-07e2-4d79-8ea4-ab269700f5de)   
 [ReDim Statement](../../visual-basic/language-reference/statements/redim-statement.md)   
 [Dim Statement](../../visual-basic/language-reference/statements/dim-statement.md)   
 [Preserve \- eliminazione](http://msdn.microsoft.com/it-it/91badeab-b4e0-48b6-92c9-9f0c8f995d81)