---
title: "How to: Delete a File in Visual Basic | Microsoft Docs"
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
  - "Delete method"
  - "files, deleting"
  - "files, manipulating"
  - "File object"
ms.assetid: 4b721769-3e45-4be7-b7fe-b08dc4141b44
caps.latest.revision: 24
caps.handback.revision: 24
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Delete a File in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Il metodo `DeleteFile` dell'oggetto `My.Computer.FileSystem` consente di eliminare un file.  Le opzioni disponibili consentono, ad esempio, di inviare il file eliminato al **Cestino**, chiedere all'utente di confermare l'eliminazione del file e stabilire l'azione da intraprendere quando l'utente annulla l'operazione.  
  
### Per eliminare un file di testo  
  
-   Utilizzare il metodo `DeleteFile` per eliminare un file.  Nel seguente codice viene mostrato come eliminare il file `test.txt`.  
  
     [!code-vb[VbVbcnMyFileSystem#22](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-delete-a-file_1.vb)]  
  
### Per eliminare un file di testo e chiedere all'utente di confermare l'eliminazione del file  
  
-   Utilizzare il metodo `DeleteFile` per eliminare il file, impostando `showUI` su `AllDialogs`.  Nel seguente codice viene dimostrato come eliminare il file `test.txt` e consentire all'utente di confermare l'eliminazione del file.  
  
     [!code-vb[VbFileIOMisc#9](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-delete-a-file_2.vb)]  
  
### Per eliminare un file di testo e inviarlo al Cestino  
  
-   Utilizzare il metodo `DeleteFile` per eliminare il file, specificando `SendToRecycleBin` per il parametro `recycle`.  Nel seguente codice viene mostrato come eliminare il file `test.txt` e inviarlo al **Cestino**.  
  
     [!code-vb[VbFileIOMisc#10](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-delete-a-file_3.vb)]  
  
## Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il percorso non è valido per uno dei seguenti motivi: è una stringa di lunghezza zero, contiene solo spazi vuoti, contiene caratteri non validi o è il percorso di un dispositivo, ovvero inizia con \\\\  \\\) \(<xref:System.ArgumentException>\).  
  
-   Il percorso non è valido in quanto `Nothing` \(<xref:System.ArgumentNullException>\).  
  
-   La lunghezza del percorso supera la lunghezza massima definita dal sistema \(<xref:System.IO.PathTooLongException>\).  
  
-   Il nome di un file o di una cartella nel percorso contiene i due punti \(:\) o ha un formato non valido \(<xref:System.NotSupportedException>\).  
  
-   Il file è in uso \(<xref:System.IO.IOException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie per visualizzare il percorso \(<xref:System.Security.SecurityException>\).  
  
-   Il file non esiste \(<xref:System.IO.FileNotFoundException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie per cancellare il file oppure il file è in sola lettura \(<xref:System.UnauthorizedAccessException>\).  
  
-   Esiste una situazione con attendibilità parziale nella quale l'utente non dispone delle autorizzazioni necessarie \(<xref:System.Security.SecurityException>\).  
  
-   L'utente ha annullato l'operazione e `onUserCancel` è impostato su `ThrowException` \(<xref:System.OperationCanceledException>\).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.UICancelOption>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.UIOption>   
 <xref:Microsoft.VisualBasic.FileIO.RecycleOption>   
 [How to: Get the Collection of Files in a Directory](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-get-the-collection-of-files-in-a-directory.md)