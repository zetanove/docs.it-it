---
title: "Procedura: spostare un file in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
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
  - "file, spostamento"
ms.assetid: 53a7457b-5815-41ad-b37d-28537c1fb77a
caps.latest.revision: 20
caps.handback.revision: 20
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Procedura: spostare un file in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Il metodo `My.Computer.FileSystem.MoveFile` consente di spostare un file in una cartella diversa. Se la struttura di destinazione non esiste, verrà creata.  
  
### Per spostare un file  
  
-   Per spostare il file, usare il metodo `MoveFile`, specificando il nome e il percorso del file di origine e del file di destinazione. In questo esempio il file `test.txt` viene spostato da `TestDir1` a `TestDir2`. Si noti che il nome del file di destinazione viene specificato anche se corrisponde al nome del file di origine.  
  
     [!code-vb[VbVbcnMyFileSystem#24](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-move-a-file_1.vb)]  
  
### Per spostare un file e rinominarlo  
  
-   Per spostare il file, usare il metodo `MoveFile`, specificando il nome e il percorso del file di origine, il percorso di destinazione e il nome che si desidera assegnare al file di destinazione. In questo esempio il file `test.txt` viene spostato da `TestDir1` a `TestDir2` e viene rinominato `nexttest.txt`.  
  
     [!code-vb[VbVbcnMyFileSystem#25](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-move-a-file_2.vb)]  
  
## Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il percorso non è valido per uno dei seguenti motivi: è una stringa di lunghezza zero, contiene solo spazi vuoti, contiene caratteri non validi o è il percorso di un dispositivo \(inizia con \\\\.\\\) \(<xref:System.ArgumentException>\).  
  
-   Il percorso non è valido in quanto è `Nothing` \(<xref:System.ArgumentNullException>\).  
  
-   `destinationFileName` è `Nothing` o una stringa vuota \(<xref:System.ArgumentNullException>\).  
  
-   Il file di origine non è valido o non esiste \(<xref:System.IO.FileNotFoundException>\).  
  
-   Il percorso complessivo corrisponde a una directory esistente, il file di destinazione esiste e `overwrite` è impostato su `False`, un file con lo stesso nome è già in uso nella directory di destinazione oppure l'utente non dispone di autorizzazioni sufficienti per accedere al file \(<xref:System.IO.IOException>\).  
  
-   Il nome di un file o di una directory nel percorso contiene i due punti \(:\) o ha un formato non valido \(<xref:System.NotSupportedException>\).  
  
-   `showUI` è impostato su `True`, `onUserCancel` è impostato su `ThrowException` e l'utente ha annullato l'operazione oppure si è verificato un errore di I\/O non specificato \(<xref:System.OperationCanceledException>\).  
  
-   La lunghezza del percorso supera la lunghezza massima definita dal sistema \(<xref:System.IO.PathTooLongException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie per visualizzare il percorso \(<xref:System.Security.SecurityException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie \(<xref:System.UnauthorizedAccessException>\).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.MoveFile%2A>   
 [How to: Rename a File](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-rename-a-file.md)   
 [How to: Create a Copy of a File in a Different Directory](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-create-a-copy-of-a-file-in-a-different-directory.md)   
 [Procedura: analizzare percorsi di file](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)