---
title: "Constructor &#39;&lt;name&gt;&#39; cannot call itself | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30298"
  - "vbc30298"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30298"
ms.assetid: 2d77b7f4-0640-4f89-9c65-f101fd2847c0
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Constructor &#39;&lt;name&gt;&#39; cannot call itself
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una routine `Sub New` di una classe o di una struttura chiama se stessa.  
  
 Lo scopo di un costruttore consiste nell'inizializzare un'istanza di una classe o di una struttura quando viene creata per la prima volta.  Per una classe o una struttura possono esistere numerosi costruttori, ammesso che dispongano di elenchi di parametri diversi.  Un costruttore può chiamarne un altro per eseguirne la funzionalità oltre alla propria.  Tuttavia, non è significativo che un costruttore chiami se stesso poiché, se tale operazione fosse consentita, determinerebbe una ricorsione infinita.  
  
 **ID errore:** BC30298  
  
### Per correggere l'errore  
  
1.  Controllare l'elenco dei parametri del costruttore da chiamare.  Tale elenco dovrebbe differire da quello del costruttore che effettua la chiamata.  
  
2.  Se non si desidera chiamare un altro costruttore, rimuovere completamente la chiamata `Sub New`.  
  
## Vedere anche  
 [Object Lifetime: How Objects Are Created and Destroyed](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)