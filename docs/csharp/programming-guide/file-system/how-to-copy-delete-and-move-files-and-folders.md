---
title: "Procedura: copiare, eliminare e spostare file e cartelle (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "I/O [C#]"
ms.assetid: 62e52cd7-9597-4e4a-acf9-1315f5cdbf05
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# Procedura: copiare, eliminare e spostare file e cartelle (Guida per programmatori C#)
Negli esempi seguenti viene mostrato come copiare, spostare ed eliminare file e cartelle in modo sincrono tramite le classi <xref:System.IO.File?displayProperty=fullName>, <xref:System.IO.Directory?displayProperty=fullName>, <xref:System.IO.FileInfo?displayProperty=fullName> e <xref:System.IO.DirectoryInfo?displayProperty=fullName> dello spazio dei nomi <xref:System.IO?displayProperty=fullName>.  In questi esempi non viene fornito un indicatore di stato o altri elementi di interfaccia utente.  Se si desidera fornire una finestra di dialogo di stato standard, vedere [Procedura: fornire una finestra di dialogo dello stato di avanzamento per operazioni su file](../../../csharp/programming-guide/file-system/how-to-provide-a-progress-dialog-box-for-file-operations.md).  
  
 Utilizzare <xref:System.IO.FileSystemWatcher?displayProperty=fullName> per fornire eventi che consentiranno di calcolare lo stato di avanzamento quando si opera su più file.  Un altro approccio consiste nell'utilizzare pInvoke per chiamare i metodi correlati ai file rilevanti nella shell di Windows.  Per informazioni su come eseguire queste operazioni sui file in modo asincrono, vedere [I\/O di file asincrono](../Topic/Asynchronous%20File%20I-O.md).  
  
## Esempio  
 Nell'esempio seguente viene mostrato come copiare file e directory.  
  
 [!code-cs[csFilesandFolders#7](../../../csharp/programming-guide/file-system/codesnippet/csharp/csFilesFolders/FileIteration.cs#7)]  
  
## Esempio  
 Nell'esempio seguente viene mostrato come spostare file e directory.  
  
 [!code-cs[csFilesandFolders#8](../../../csharp/programming-guide/file-system/codesnippet/csharp/csFilesFolders/FileIteration.cs#8)]  
  
## Esempio  
 Nell'esempio seguente viene mostrato come eliminare file e directory.  
  
 [!code-cs[csFilesandFolders#9](../../../csharp/programming-guide/file-system/codesnippet/csharp/csFilesFolders/FileIteration.cs#9)]  
  
## Vedere anche  
 <xref:System.IO?displayProperty=fullName>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [File system e Registro di sistema](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)   
 [Procedura: fornire una finestra di dialogo dello stato di avanzamento per operazioni su file](../../../csharp/programming-guide/file-system/how-to-provide-a-progress-dialog-box-for-file-operations.md)   
 [I\/O di file e di flussi](../Topic/File%20and%20Stream%20I-O.md)   
 [Attività di I\/O comuni](../Topic/Common%20I-O%20Tasks.md)