---
title: "Impossibile completare l&#39;operazione. La directory di destinazione &#232; una sottodirectory della directory di origine | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrIO_CyclicOperation"
ms.assetid: 850d3a24-5d51-4ac8-a912-630efcd75278
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Impossibile completare l&#39;operazione. La directory di destinazione &#232; una sottodirectory della directory di origine
Un'operazione ciclica non è riuscita. Queste operazioni sono cicliche e quindi non possono essere completate. Ad esempio, un oggetto A potrebbe provare a ereditare dall'oggetto B, che a sua volta eredita dall'oggetto A.  
  
### Per correggere l'errore  
  
-   Quando si eredita, assicurarsi che non siano presenti riferimenti ciclici.  
  
## Vedere anche  
 [Error Types](../../visual-basic/programming-guide/language-features/error-types.md)   
 [Debugging Basics: Breakpoints](http://msdn.microsoft.com/it-it/752a02c2-0ac7-4c8b-aa1b-4b2b3b21152e)