---
title: "File already open | Microsoft Docs"
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
  - "vbrID55"
dev_langs: 
  - "VB"
ms.assetid: d674a0fb-ef16-4cc2-9da7-709a8a07dbea
caps.latest.revision: 7
caps.handback.revision: 7
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# File already open
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

A volte, perché possa aver luogo un altro `FileOpen` o un'altra operazione, è necessario chiudere un file.  Di seguito sono riportate le cause possibili dell'errore.  
  
-   È stata eseguita un'operazione `FileOpen` in modalità output sequenziale per un file già aperto.  
  
-   Un'istruzione fa riferimento a un file aperto.  
  
### Per correggere l'errore  
  
1.  Chiudere il file prima di eseguire l'istruzione.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileSystem.FileOpen%2A>