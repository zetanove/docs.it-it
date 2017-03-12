---
title: "How to: Write Text to Files with a StreamWriter in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "files, writing to"
  - "text, writing to files"
  - "writing to files, StreamWriter"
ms.assetid: 99762e57-ef46-4dcc-8959-a8f79c22f067
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# How to: Write Text to Files with a StreamWriter in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Nell'esempio riportato di seguito viene aperto un oggetto <xref:System.IO.StreamWriter> con il metodo `My.Computer.FileSystem.OpenTextFileWriter` e quindi viene utilizzato per scrivere una stringa in un file di testo con il metodo <xref:System.IO.TextWriter.WriteLine%2A> della classe <xref:System.IO.StreamWriter>.  
  
## Esempio  
 [!code-vb[VbFileIOWrite#5](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-write-text-to-fil_0_1.vb)]  
  
## Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il file esiste ed è di sola lettura \(<xref:System.IO.IOException>\).  
  
-   Il disco è pieno \(<xref:System.IO.IOException>\).  
  
-   Il nome del percorso è troppo lungo \(<xref:System.IO.PathTooLongException>\).  
  
## Sicurezza di .NET Framework  
 Se il file non esiste, ne viene creato uno nuovo nell'esempio.  Per poter creare un file in un'applicazione, è necessario che l'applicazione disponga dell'accesso `Create` alla cartella.  Se il file esiste già, sarà necessario solo l'accesso `Write`, ossia un privilegio minore.  Laddove possibile, è più sicuro creare il file durante la fase di distribuzione e concedere solo l'accesso `Read` a un unico file, anziché l'accesso `Create` a una cartella.  
  
## Vedere anche  
 <xref:System.IO.StreamWriter>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileWriter%2A>   
 [How to: Read from Text Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files.md)   
 [Writing to Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/writing-to-files.md)