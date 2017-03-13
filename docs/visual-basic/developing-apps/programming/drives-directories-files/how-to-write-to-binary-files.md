---
title: "How to: Write to Binary Files in Visual Basic | Microsoft Docs"
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
  - "files, binary access"
  - "WriteAllBytes method"
  - "binary files, writing in Visual Basic"
ms.assetid: 59fae125-de5b-4c96-883c-209f4a55112c
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# How to: Write to Binary Files in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllBytes%2A> scrive dati in un file binario.  Se il parametro `append` è `True`, i dati verranno aggiunti al file. In caso contrario, i dati nel file verranno sovrascritti.  
  
 Se il percorso specificato, escluso il nome del file, non è valido, verrà generata un'eccezione <xref:System.IO.DirectoryNotFoundException>.  Se il percorso è valido ma il file non esiste, il file verrà creato.  
  
### Per scrivere all'interno di un file binario  
  
-   Utilizzare il metodo `WriteAllBytes`, specificando il percorso e il nome del file e i byte da scrivere.  In questo esempio viene aggiunta la matrice di dati `CustomerData` al file denominato `CollectedData.dat`.  
  
     [!code-vb[VbVbcnMyFileSystem#27](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-to-binary-files_1.vb)]  
  
## Programmazione efficiente  
 Un'eccezione può essere generata nelle condizioni seguenti:  
  
-   Il percorso non è valido per uno dei seguenti motivi: è una stringa di lunghezza zero, contiene solo spazi vuoti o contiene caratteri non validi.  \(<xref:System.ArgumentException>\).  
  
-   Il percorso non è valido in quanto `Nothing` \(<xref:System.ArgumentNullException>\).  
  
-   `File` punta a un percorso non esistente \(<xref:System.IO.FileNotFoundException> o <xref:System.IO.DirectoryNotFoundException>\).  
  
-   Il file è utilizzato da un altro processo o si è verificato un errore di I\/O \(<xref:System.IO.IOException>\).  
  
-   La lunghezza del percorso supera la lunghezza massima definita dal sistema \(<xref:System.IO.PathTooLongException>\).  
  
-   Il nome di un file o di una directory nel percorso contiene i due punti \(:\) o ha un formato non valido \(<xref:System.NotSupportedException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie per visualizzare il percorso \(<xref:System.Security.SecurityException>\).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllBytes%2A>   
 [How to: Write Text to Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-write-text-to-files.md)