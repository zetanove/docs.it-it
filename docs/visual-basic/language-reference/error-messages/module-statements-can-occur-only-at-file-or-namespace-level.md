---
title: "&#39;Module&#39; statements can occur only at file or namespace level | Microsoft Docs"
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
  - "bc30617"
  - "vbc30617"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30617"
ms.assetid: 5e9de8e5-d26b-4fb2-9e28-814413fe9cef
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;Module&#39; statements can occur only at file or namespace level
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Le istruzioni `Module` devono essere visualizzate all'inizio del file di origine, subito dopo le istruzioni `Option` e `Imports`, gli attributi globali e le dichiarazioni dello spazio dei nomi, ma prima di tutte le altre dichiarazioni.  
  
 **ID errore:** BC30617  
  
### Per correggere l'errore  
  
-   Spostare l'istruzione `Module` all'inizio della dichiarazione dello spazio dei nomi o del file di origine.  
  
## Vedere anche  
 [Module Statement](../../../visual-basic/language-reference/statements/module-statement.md)