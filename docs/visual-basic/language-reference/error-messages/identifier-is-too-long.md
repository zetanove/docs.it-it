---
title: "Identifier is too long | Microsoft Docs"
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
  - "bc30033"
  - "vbc30033"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30033"
ms.assetid: 3d07f6d0-9a2f-49ca-94e8-1e354932e855
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Identifier is too long
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il nome, o identificatore, di ogni elemento di programmazione non può superare i 1023 caratteri.  Anche un nome completo non può superare i 1023 caratteri.  Questo significa che l'intera stringa dell'identificatore \(`<namespace>.<...>.<namespace>.<class>.<element>`\) non può superare i 1023 caratteri, inclusi i caratteri dell'operatore di accesso ai membri \(`.`\).  
  
 **ID errore:** BC30033  
  
### Per correggere l'errore  
  
-   Ridurre la lunghezza dell'identificatore.  
  
## Vedere anche  
 [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)