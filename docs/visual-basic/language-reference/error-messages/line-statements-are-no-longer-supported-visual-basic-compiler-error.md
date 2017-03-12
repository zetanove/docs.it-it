---
title: "&#39;Line&#39; statements are no longer supported (Visual Basic Compiler Error) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30830"
  - "vbc30830"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30830"
ms.assetid: 4734bc1d-882e-4555-b498-1f1ec0399d16
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# &#39;Line&#39; statements are no longer supported (Visual Basic Compiler Error)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Le istruzioni Line non sono più supportate.  La funzionalità di I\/O dei file è disponibile come `Microsoft.VisualBasic.FileSystem.LineInput` e la funzionalità grafica è disponibile come `System.Drawing.Graphics.DrawLine`.  
  
 **ID errore:** BC30830  
  
### Per correggere l'errore  
  
1.  Se si eseguono operazioni di accesso ai file, utilizzare `Microsoft.VisualBasic.FileSystem.LineInput`.  
  
2.  Se si eseguono operazioni di grafica, utilizzare `System.Drawing.Graphics.Drawline`.  
  
## Vedere anche  
 <xref:System.IO>   
 <xref:System.Drawing>   
 [File Access with Visual Basic](../../../visual-basic/developing-apps/programming/drives-directories-files/file-access.md)