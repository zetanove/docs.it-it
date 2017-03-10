---
title: "Una chiamata a una propriet&#224; o a un metodo non pu&#242; includere un riferimento a un oggetto privato, n&#233; come argomento n&#233; come valore restituito | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID98"
dev_langs: 
  - "VB"
ms.assetid: 059b43e1-202d-4fa2-806b-7bad63c1e7ca
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Una chiamata a una propriet&#224; o a un metodo non pu&#242; includere un riferimento a un oggetto privato, n&#233; come argomento n&#233; come valore restituito
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Di seguito sono riportate le cause possibili dell'errore:  
  
-   Un client ha richiamato una proprietà o un metodo di un componente out\-of\-process e ha tentato di passare un riferimento a un oggetto privato come uno degli argomenti.  
  
-   Un componente out\-of\-process ha richiamato un metodo di richiamata sul relativo client e ha tentato di passare un riferimento a un oggetto privato.  
  
-   Un componente out\-of\-process ha tentato di passare un riferimento a un oggetto privato come argomento dell'evento che stava generando.  
  
-   Un client ha tentato di assegnare un riferimento a un oggetto privato a un argomento `ByRef` dell'evento che stava gestendo.  
  
### Per correggere l'errore  
  
1.  Rimuovere il riferimento.  
  
## Vedere anche  
 [Private](../../../visual-basic/language-reference/modifiers/private.md)