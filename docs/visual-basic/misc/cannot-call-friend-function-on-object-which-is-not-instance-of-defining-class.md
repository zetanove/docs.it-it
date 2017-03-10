---
title: "Non &#232; possibile chiamare la funzione Friend su un oggetto che non &#232; un&#39;istanza della classe di definizione | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID97"
ms.assetid: b9d821f0-8565-4f15-bb35-184789c69662
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Non &#232; possibile chiamare la funzione Friend su un oggetto che non &#232; un&#39;istanza della classe di definizione
Si è provato a chiamare la routine `Friend` di una classe oppure di accedere a un metodo o a una proprietà `Friend` tra più processi o cross\-thread. Una routine `Friend` può essere chiamata da un modulo all'esterno della classe, ma fa parte del progetto in cui è definita la classe.  
  
### Per correggere l'errore  
  
-   Assicurarsi di chiamare la routine o di accedervi da un modulo che fa parte del progetto in cui è definita la classe.  
  
## Vedere anche  
 [Friend](../../visual-basic/language-reference/modifiers/friend.md)