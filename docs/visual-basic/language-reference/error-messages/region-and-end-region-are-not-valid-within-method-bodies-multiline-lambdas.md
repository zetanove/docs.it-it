---
title: "&#39;#Region&#39; and &#39;#End Region&#39; statements are not valid within method bodies/multiline lambdas | Microsoft Docs"
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
  - "bc32025"
  - "vbc32025"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32025"
ms.assetid: 43707bf1-1c6b-4d82-b081-e5a17dca51c1
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;#Region&#39; and &#39;#End Region&#39; statements are not valid within method bodies/multiline lambdas
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il blocco `#Region` deve essere dichiarato a livello di classe, modulo o spazio dei nomi.  Un'area comprimibile può includere una o più routine, ma non può iniziare o terminare all'interno di una routine.  
  
 **ID errore:** BC32025  
  
### Per correggere l'errore  
  
1.  Verificare che la routine precedente termini correttamente con un'istruzione `End Function` o `End Sub`.  
  
2.  Verificare che le direttive `#Region` e `#End Region` si trovino nello stesso blocco di codice.  
  
## Vedere anche  
 [\#Region Directive](../../../visual-basic/language-reference/directives/region-directive.md)