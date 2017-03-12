---
title: "How to: Find Subdirectories with a Specific Pattern in Visual Basic | Microsoft Docs"
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
  - "pattern matching"
  - "folders, finding"
ms.assetid: c9265fd1-7483-4150-8b7f-ff642caa939d
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# How to: Find Subdirectories with a Specific Pattern in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetDirectories%2A> restituisce una raccolta di stringhe di sola lettura che rappresentano i nomi di percorso delle sottodirectory di una directory.  Per specificare un modello specifico, utilizzare il parametro `wildCards`.  Se nella ricerca si desiderano includere i contenuti delle sottodirectory, impostare il parametro `searchType` su `SearchOption.SearchAllSubDirectories`.  
  
 Se non vengono trovate directory corrispondenti al criterio di ricerca specificato verrà restituita una raccolta vuota.  
  
### Per cercare sottodirectory con un criterio specifico  
  
-   Utilizzare il metodo `GetDirectories`, specificando il nome e il percorso della directory che si desidera cercare.  Nell'esempio riportato di seguito sono restituite tutte le directory nella struttura della directory nel cui nome è contenuta la parola "Logs" e vengono aggiunte a `ListBox1`.  
  
     [!code-vb[VbVbcnFileAccess#1](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-find-subdirectori_1.vb)]  
  
## Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il percorso non è valido per uno dei seguenti motivi: è una stringa di lunghezza zero, contiene solo spazi vuoti, contiene caratteri non validi o è il percorso di un dispositivo, ovvero inizia con \\\\  \\\) \(<xref:System.ArgumentException>\).  
  
-   Il percorso non è valido in quanto `Nothing` \(<xref:System.ArgumentNullException>\).  
  
-   Uno o più dei caratteri jolly specificati è `Nothing`, una stringa vuota o contiene solo spazi \(<xref:System.ArgumentNullException>\).  
  
-   `directory` non esiste \(<xref:System.IO.DirectoryNotFoundException>\).  
  
-   `directory` fa riferimento a un file esistente \(<xref:System.IO.IOException>\).  
  
-   La lunghezza del percorso supera la lunghezza massima definita dal sistema \(<xref:System.IO.PathTooLongException>\).  
  
-   Il nome di un file o di una cartella nel percorso contiene i due punti \(:\) o ha un formato non valido \(<xref:System.NotSupportedException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie per visualizzare il percorso \(<xref:System.Security.SecurityException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie \(<xref:System.UnauthorizedAccessException>\).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetDirectories%2A>   
 [How to: Find Files with a Specific Pattern](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-files-with-a-specific-pattern.md)