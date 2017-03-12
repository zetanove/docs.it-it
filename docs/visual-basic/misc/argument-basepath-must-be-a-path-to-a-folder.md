---
title: "L&#39;argomento BasePath deve essere un percorso a una cartella | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
ms.assetid: b180ce60-ad57-41a6-a313-491d86d84cc7
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# L&#39;argomento BasePath deve essere un percorso a una cartella
L'argomento `BasePath` deve essere costituito da un percorso a una cartella. È possibile che si stia analizzando la stringa in modo errato e che sia stato specificato un valore che non è riconosciuto come un percorso valido.  
  
### Per correggere l'errore  
  
-   Controllare il valore specificato per `BasePath` per assicurarsi che sia un percorso valido a una cartella.  
  
## Vedere anche  
 <xref:System.CodeDom.Compiler.TempFileCollection.BasePath%2A>   
 <xref:System.Resources.ResXResourceWriter.BasePath%2A>   
 <xref:System.Resources.ResXResourceReader.BasePath%2A>   
 [Procedura: analizzare percorsi di file](../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)