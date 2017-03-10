---
title: "&#39;&lt;typename&gt;&#39; is a delegate type | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc32008"
  - "vbc32008"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32008"
ms.assetid: dc6abba0-a9ad-450f-8899-87265bc84abc
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# &#39;&lt;typename&gt;&#39; is a delegate type
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

'\<nometipo\>' è un tipo delegato.La costruzione di delegati consente solo una singola espressione AddressOf come elenco di argomenti.È spesso possibile utilizzare l'espressione AddressOf anziché una costruzione di delegati.  
  
 Una clausola `New` che crea un'istanza di una classe delegata fornisce un elenco di argomenti non valido al costruttore di delegato.  
  
 Durante la creazione di una nuova istanza delegata è possibile fornire una sola espressione `AddressOf`.  
  
 Questo errore può verificarsi se non si passano argomenti al costruttore di delegato oppure se si passano più argomenti o un argomento che non corrisponde a un'espressione `AddressOf` valida.  
  
 **ID errore:** BC32008  
  
### Per correggere l'errore  
  
-   Utilizzare una sola espressione `AddressOf` nell'elenco di argomenti per la classe delegata nella clausola `New`.  
  
## Vedere anche  
 [New Operator](../../../visual-basic/language-reference/operators/new-operator.md)   
 [AddressOf Operator](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Delegates](../../../visual-basic/programming-guide/language-features/delegates/delegates.md)   
 [How to: Invoke a Delegate Method](../../../visual-basic/programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)