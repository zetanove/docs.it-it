---
title: "How to: Read Text from Files with a StreamReader (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "reading files, text"
  - "text, reading from files"
  - "reading text from files"
  - "files, reading"
ms.assetid: 384033c6-18f9-4d59-9610-36371226558f
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Read Text from Files with a StreamReader (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

L'oggetto `My.Computer.FileSystem` fornisce i metodi per aprire <xref:System.IO.TextReader> e <xref:System.IO.TextWriter>.  `OpenTextFileWriter` e `OpenTextFileReader` sono metodi avanzati che non vengono visualizzati in IntelliSense, a meno che non venga selezionata la scheda **Tutti**.  
  
### Per leggere una riga da un file con il lettore di testo  
  
-   Utilizzare il metodo `OpenTextFileReader` per aprire <xref:System.IO.TextReader>, specificando il file.  In questo esempio viene aperto il file `testfile.txt`, da cui una riga viene letta e visualizzata in una casella di messaggio.  
  
     [!code-vb[VbFileIORead#1](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-text-from-files-with-a-streamreader_1.vb)]  
  
## Programmazione efficiente  
 Il file letto deve essere un file di testo.  
  
 Non basarsi sul nome del file per prendere decisioni in merito al relativo contenuto.  Ad esempio, è possibile che il file Form1.vb non sia un file di origine Visual Basic.  
  
 Prima di usare i dati nell'applicazione verificare tutti gli input.  È possibile che il contenuto del file non corrisponda a quanto previsto e che quindi i metodi per la lettura dal file non abbiano esito positivo.  
  
## Sicurezza di .NET Framework  
 Per leggere da un file, l'assembly richiede un livello di privilegio garantito dalla classe <xref:System.Security.Permissions.FileIOPermission>.  Se eseguito in un contesto ad attendibilità parziale, il codice potrebbe generare un'eccezione a causa dell'insufficienza di privilegi.  Per ulteriori informazioni, vedere [Code Access Security Basics](../Topic/Code%20Access%20Security%20Basics.md).  Inoltre, per l'utente è necessario anche l'accesso al file.  Per ulteriori informazioni, vedere [ACL Technology Overview](http://msdn.microsoft.com/it-it/06fbf66d-6f02-4378-b863-b2f12e349045).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:System.Windows.Forms.OpenFileDialog>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileWriter%2A>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileReader%2A>   
 [Componente SaveFileDialog](../Topic/SaveFileDialog%20Component%20\(Windows%20Forms\).md)   
 [Reading from Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)