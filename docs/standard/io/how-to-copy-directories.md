---
title: "Procedura: copiare le directory | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "copia di directory"
  - "directory [.NET Framework], copia"
  - "directory (copia)"
  - "I/O [.NET Framework], copia di directory"
  - "sottodirectory (copia)"
ms.assetid: 5a969765-e5f8-4b4e-977e-90e2b0a1fe3c
caps.latest.revision: 11
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: copiare le directory
Questo esempio mostra come usare classi di I\/O per copiare in modo sincronizzato il contenuto di una directory in un altro percorso. In questo esempio l'utente può specificare se copiare anche le sottodirectory. In caso affermativo, le sottodirectory vengono copiate in modo ricorsivo dal metodo di esempio, che chiama se stesso su ogni successiva sottodirectory finché non ci sono più sottodirectory da copiare.  
  
 Per un esempio di copia di file in modo asincrono, vedere [I\/O di file asincrono](../../../docs/standard/io/i-o-di-file-asincrono.md).  
  
## Esempio  
 [!code-csharp[System.IO.Directory_Copy#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Directory_Copy/cs/program.cs#1)]
 [!code-vb[System.IO.Directory_Copy#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Directory_Copy/vb/Program.vb#1)]  
  
## Vedere anche  
 <xref:System.IO.FileInfo>   
 <xref:System.IO.DirectoryInfo>   
 <xref:System.IO.FileStream>   
 [I\/O di file e di flussi](../../../docs/standard/io/index.md)   
 [Attività di I\/O comuni](../../../docs/standard/io/commons-tasks.md)   
 [I\/O di file asincrono](../../../docs/standard/io/i-o-di-file-asincrono.md)