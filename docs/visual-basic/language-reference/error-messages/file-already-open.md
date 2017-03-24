---
title: "File already open | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID55"
dev_langs: 
  - "VB"
ms.assetid: d674a0fb-ef16-4cc2-9da7-709a8a07dbea
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# File already open
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

A volte, perché possa aver luogo un altro `FileOpen` o un'altra operazione, è necessario chiudere un file.  Di seguito sono riportate le cause possibili dell'errore.  
  
-   È stata eseguita un'operazione `FileOpen` in modalità output sequenziale per un file già aperto.  
  
-   Un'istruzione fa riferimento a un file aperto.  
  
### Per correggere l'errore  
  
1.  Chiudere il file prima di eseguire l'istruzione.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileSystem.FileOpen%2A>