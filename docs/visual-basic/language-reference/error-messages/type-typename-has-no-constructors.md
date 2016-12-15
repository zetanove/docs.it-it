---
title: "Type &#39;&lt;typename&gt;&#39; has no constructors | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc30251"
  - "vbc30251"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30251"
ms.assetid: aff3e1df-abe6-4bc0-9abc-a1e70514c561
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Type &#39;&lt;typename&gt;&#39; has no constructors
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un tipo non supporta una chiamata a `Sub New()`.  Causa possibile: compilatore o un file binario danneggiato.  
  
 **Error ID:** BC30251  
  
### Per correggere l'errore  
  
1.  Se il tipo si trova in un progetto diverso o in un file di riferimento, reinstallare il progetto o il file.  
  
2.  Se il tipo si trova nello stesso progetto, ricompilare l'assembly in cui è contenuto.  
  
3.  Se l'errore si ripresenta, reinstallare il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
4.  Se l'errore persiste, raccogliere informazioni sulla situazione contingente e informare il Servizio Supporto Tecnico Clienti Microsoft.  
  
## Vedere anche  
 [Objects and Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Comunicazioni con Microsoft](/visual-studio/ide/talk-to-us)