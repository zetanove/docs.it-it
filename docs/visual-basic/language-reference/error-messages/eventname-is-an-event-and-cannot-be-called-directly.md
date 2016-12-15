---
title: "&#39;&lt;eventname&gt;&#39; is an event, and cannot be called directly | Microsoft Docs"
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
  - "bc32022"
  - "vbc32022"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32022"
ms.assetid: 4dcfcb8d-a9fa-46a7-a034-29d9ff3a59b3
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;&lt;eventname&gt;&#39; is an event, and cannot be called directly
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

'`eventname`\>' è un evento e non può essere chiamato direttamente.  Utilizzare un'istruzione `RaiseEvent` per generare un evento.  
  
 Una routine di chiamata specifica un evento per il nome della routine.  Un gestore eventi è una routine, ma l'evento stesso è una periferica di segnalazione, che deve essere generata e gestita.  
  
 **ID errore:** BC32022  
  
### Per correggere l'errore  
  
1.  Utilizzare un'istruzione `RaiseEvent` per segnalare un evento e richiamare la routine o le routine che lo gestiscono.  
  
## Vedere anche  
 [RaiseEvent Statement](../../../visual-basic/language-reference/statements/raiseevent-statement.md)