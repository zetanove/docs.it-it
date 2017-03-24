---
title: "Procedura: copiare file con un criterio specifico in una directory in Visual Basic | Microsoft Docs"
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
  - "Metodo My.Computer.FileSystem.CopyFile, copia di file [Visual Basic]"
  - "file, copia"
  - "Metodo CopyFile, copia di file in Visual Basic"
  - "I/O [Visual Basic], copia di file"
ms.assetid: f205d2ad-bbe5-4d55-8a40-acda21aa82dd
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Procedura: copiare file con un criterio specifico in una directory in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il metodo <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A> restituisce una raccolta di stringhe di sola lettura che rappresentano i nomi di percorso per i file. È possibile usare il parametro `wildCards` per specificare un criterio specifico.  
  
 Se non vengono individuati file corrispondenti, viene restituita una raccolta vuota.  
  
 È possibile usare il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%2A> per copiare i file in una directory.  
  
### Per copiare file con un criterio specifico in una directory  
  
1.  Usare il metodo `GetFiles` per restituire l'elenco dei file. In questo esempio vengono restituiti tutti i file RTF nella directory specificata.  
  
     [!code-vb[VbFileIOMisc#36](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-copy-files-with-a-specific-pattern-to-a-directory_1.vb)]  
  
2.  Usare il metodo `CopyFile` per copiare i file. In questo esempio i file vengono copiati nella directory denominata `testdirectory`.  
  
     [!code-vb[VbVbcnMyFileSystem#88](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-copy-files-with-a-specific-pattern-to-a-directory_2.vb)]  
  
3.  Chiudere l'istruzione `For` con un'istruzione `Next`.  
  
     [!code-vb[VbVbcnMyFileSystem#89](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-copy-files-with-a-specific-pattern-to-a-directory_3.vb)]  
  
## Esempio  
 Nell'esempio seguente, che presenta i frammenti di codice precedenti in forma completa, tutti i file RTF nella directory specificata vengono copiati nella directory denominata `testdirectory`.  
  
 [!code-vb[VbFileIOMisc#37](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-copy-files-with-a-specific-pattern-to-a-directory_4.vb)]  
  
## Sicurezza di .NET Framework  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il percorso non è valido per uno dei seguenti motivi: è una stringa di lunghezza zero, contiene solo spazi vuoti, contiene caratteri non validi o è il percorso di un dispositivo \(inizia con \\\\.\\\) \(<xref:System.ArgumentException>\).  
  
-   Il percorso non è valido in quanto è `Nothing` \(<xref:System.ArgumentNullException>\).  
  
-   La directory non esiste \(<xref:System.IO.DirectoryNotFoundException>\).  
  
-   La directory punta a un file esistente \(<xref:System.IO.IOException>\).  
  
-   La lunghezza del percorso supera la lunghezza massima definita dal sistema \(<xref:System.IO.PathTooLongException>\).  
  
-   Il nome di un file o di una directory nel percorso contiene i due punti \(:\) o ha un formato non valido \(<xref:System.NotSupportedException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie per visualizzare il percorso \(<xref:System.Security.SecurityException>\). L'utente non dispone delle autorizzazioni necessarie \(<xref:System.UnauthorizedAccessException>\).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%2A>   
 <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A>   
 [How to: Find Subdirectories with a Specific Pattern](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-subdirectories-with-a-specific-pattern.md)   
 [Troubleshooting: Reading from and Writing to Text Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)   
 [How to: Get the Collection of Files in a Directory](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-get-the-collection-of-files-in-a-directory.md)