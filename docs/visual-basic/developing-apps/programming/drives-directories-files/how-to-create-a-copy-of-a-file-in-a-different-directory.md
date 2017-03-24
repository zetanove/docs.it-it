---
title: "How to: Create a Copy of a File in a Different Directory in Visual Basic | Microsoft Docs"
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
  - "My.Computer.FileSystem.CopyFile method, copying files [Visual Basic]"
  - "files, copying"
  - "CopyFile method, copying files in Visual Basic"
  - "I/O [Visual Basic], copying files"
ms.assetid: 88e2145c-d414-45a5-ad03-6f5d58ecca26
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# How to: Create a Copy of a File in a Different Directory in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il metodo `My.Computer.FileSystem.CopyFile` consente di copiare i file.  I parametri consentono di sovrascrivere i file esistenti, rinominare il file, mostrare l'avanzamento dell'operazione e consentire all'utente di annullare l'operazione.  
  
### Per copiare un file di testo in un'altra cartella  
  
-   Utilizzare il metodo `CopyFile` per copiare un file, specificando il file di origine e la directory di destinazione.  Il parametro `overwrite` consente di specificare se sovrascrivere o meno i file esistenti.  Nell'esempio di codice riportato di seguito viene illustrato l'utilizzo di `CopyFile`.  
  
     [!code-vb[VbFileIOMisc#24](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-create-a-copy-of-a-file-in-a-different-directory_1.vb)]  
  
## Programmazione efficiente  
 Le seguenti condizioni possono causare la generazione di un'eccezione:  
  
-   Il percorso non è valido per uno dei seguenti motivi: è una stringa di lunghezza zero, contiene solo spazi vuoti, contiene caratteri non validi o è il percorso di un dispositivo, ovvero inizia con \\\\  \\\) \(<xref:System.ArgumentException>\).  
  
-   Il sistema potrebbe non recuperare il percorso assoluto \(<xref:System.ArgumentException>\).  
  
-   Il percorso non è valido in quanto `Nothing` \(<xref:System.ArgumentNullException>\).  
  
-   Il file di origine non è valido o non esiste \(<xref:System.IO.FileNotFoundException>\).  
  
-   Il percorso combinato fa riferimento a una directory esistente \(<xref:System.IO.IOException>\).  
  
-   Il file di destinazione esiste già e `overwrite` è impostato su `False` \(<xref:System.IO.IOException>\).  
  
-   L'utente non dispone delle autorizzazioni sufficienti per accedere al file \(<xref:System.IO.IOException>\).  
  
-   Un file nella cartella di destinazione con lo stesso nome è già in uso \(<xref:System.IO.IOException>\).  
  
-   Il nome di un file o di una cartella nel percorso contiene i due punti \(:\) o ha un formato non valido \(<xref:System.NotSupportedException>\).  
  
-   `ShowUI` è impostato su `True`, `onUserCancel` è impostato su `ThrowException` e l'utente ha annullato l'operazione \(<xref:System.OperationCanceledException>\).  
  
-   `ShowUI` è impostato su `True`, `onUserCancel` è impostato su `ThrowException` e si è verificato un errore di I\/O non specificato \(<xref:System.OperationCanceledException>\).  
  
-   La lunghezza del percorso supera la lunghezza massima definita dal sistema \(<xref:System.IO.PathTooLongException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie \(<xref:System.UnauthorizedAccessException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie per visualizzare il percorso \(<xref:System.Security.SecurityException>\).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%2A>   
 <xref:Microsoft.VisualBasic.FileIO.UICancelOption>   
 [Procedura: copiare file con un criterio specifico in una directory](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-copy-files-with-a-specific-pattern-to-a-directory.md)   
 [How to: Create a Copy of a File in the Same Directory](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-create-a-copy-of-a-file-in-the-same-directory.md)   
 [How to: Copy a Directory to Another Directory](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-copy-a-directory-to-another-directory.md)   
 [How to: Rename a File](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-rename-a-file.md)