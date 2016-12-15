---
title: "How to: Write Text to Files in Visual Basic | Microsoft Docs"
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
  - "files, writing to"
  - "text, writing to files"
  - "writing to files"
  - "examples [Visual Basic], text files"
ms.assetid: 304956eb-530d-4df7-b48f-9b4d1f2581a0
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Write Text to Files in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

È possibile utilizzare il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A> per scrivere testo in file.  Se il file specificato non esiste, viene creato automaticamente.  
  
## Procedura  
  
#### Per scrivere testo all'interno di un file  
  
-   Utilizzare il metodo `WriteAllText` per scrivere testo all'interno di un file, specificando il file e il testo da scrivere.  In questo esempio viene scritta la riga `"This is new text."` nel file `test.txt`, aggiungendo il nuovo testo al testo eventualmente già esistente nel file.  
  
     [!code-vb[VbFileIOWrite#3](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-text-to-files_1.vb)]  
  
#### Per scrivere una serie di stringhe in un file  
  
-   Scorrere la raccolta di stringhe.  Utilizzare il metodo `WriteAllText` per scrivere del testo in un file, specificando il file di destinazione e la stringa da aggiungere e impostando `append` su `True`.  
  
     In questo esempio vengono scritti i nomi dei file nella directory `Documents and Settings` in `FileList.txt`, inserendo un ritorno a capo tra ciascuno di essi per una migliore leggibilità.  
  
     [!code-vb[VbFileIOWrite#4](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-text-to-files_2.vb)]  
  
## Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il percorso non è valido per uno dei seguenti motivi: è una stringa di lunghezza zero, contiene solo spazi vuoti, contiene caratteri non validi o è il percorso di un dispositivo, ovvero inizia con \\\\  \\\) \(<xref:System.ArgumentException>\).  
  
-   Il percorso non è valido in quanto `Nothing` \(<xref:System.ArgumentNullException>\).  
  
-   `File` punta a un percorso non esistente \(<xref:System.IO.FileNotFoundException> o <xref:System.IO.DirectoryNotFoundException>\).  
  
-   Il file è utilizzato da un altro processo o si è verificato un errore di I\/O \(<xref:System.IO.IOException>\).  
  
-   La lunghezza del percorso supera la lunghezza massima definita dal sistema \(<xref:System.IO.PathTooLongException>\).  
  
-   Il nome di un file o di una directory nel percorso contiene i due punti \(:\) o ha un formato non valido \(<xref:System.NotSupportedException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie per visualizzare il percorso \(<xref:System.Security.SecurityException>\).  
  
-   Il disco è pieno e la chiamata a `WriteAllText` non ha avuto esito positivo \(<xref:System.IO.IOException>\).  
  
 Se eseguito in un contesto ad attendibilità parziale, il codice potrebbe generare un'eccezione a causa dell'insufficienza di privilegi.  Per ulteriori informazioni, vedere [Code Access Security Basics](../Topic/Code%20Access%20Security%20Basics.md).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>   
 [How to: Read from Text Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files.md)