---
title: "&#39;&lt;functionname&gt;&#39; is not declared (Smart Device/Visual Basic Compiler Error) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30766"
  - "vbc30766"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30766"
ms.assetid: 13918600-6087-40d7-8134-32aa9d3bfda4
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# &#39;&lt;functionname&gt;&#39; is not declared (Smart Device/Visual Basic Compiler Error)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il parametro \<`functionname`\> non è dichiarato.  La funzionalità di I\/O dei file è normalmente disponibile nello spazio dei nomi `Microsoft.VisualBasic`, ma la versione di destinazione di .NET Compact Framework non la supporta.  
  
 **ID errore:** BC30760  
  
### Per correggere l'errore  
  
-   Eseguire operazioni sui file con funzioni definite nello spazio dei nomi `System.IO`.  
  
## Vedere anche  
 <xref:System.IO>   
 [File Access with Visual Basic](../../../visual-basic/developing-apps/programming/drives-directories-files/file-access.md)