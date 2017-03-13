---
title: "How to: Copy a Directory to Another Directory in Visual Basic | Microsoft Docs"
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
  - "I/O [Visual Basic], copying directories"
  - "I/O [Visual Basic], copying folders"
  - "folders [Visual Basic], copying"
  - "directories [Visual Basic], copying"
ms.assetid: 2a370bd7-10ba-4219-afc4-4519d031eb6c
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# How to: Copy a Directory to Another Directory in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Utilizzare il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyDirectory%2A> per copiare una directory in un'altra directory.  Questo metodo consente di copiare il contenuto della directory nonché la directory stessa.  Se la directory di destinazione non esiste, viene creata.  Se è presente una directory con lo stesso nome nel percorso di destinazione e `overwrite` è impostato su `False`, il contenuto delle due directory viene unito.  È possibile specificare un nuovo nome per la directory durante l'operazione.  
  
 Quando si copiano file in una directory, è possibile che vengano generate eccezioni causate da un file specifico, ad esempio un file presente durante un'unione con `overwrite` impostato su `False`.  Quando vengono generate, queste eccezioni vengono consolidate in un'unica eccezione, la cui proprietà `Data` contiene le voci in cui il percorso del file o della directory è la chiave e il messaggio di eccezione specifico è contenuto nel valore corrispondente.  
  
### Per copiare una directory in un'altra directory  
  
-   Utilizzare il metodo `CopyDirectory`, specificando i nomi della directory di origine e di destinazione.  Nell'esempio di codice riportato di seguito, la directory denominata `TestDirectory1` viene copiata in `TestDirectory2`, sovrascrivendo i file esistenti.  
  
     [!code-vb[VbVbcnMyFileSystem#16](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-copy-a-directory-to-another-directory_1.vb)]  
  
     Questo esempio di codice è anche disponibile come frammento di codice IntelliSense.  Nella casella di selezione dei frammenti di codice si trova in **File system \- Elaborazione di unità, cartelle e file**.  Per ulteriori informazioni, vedere [Frammenti di codice](/visual-studio/ide/code-snippets).  
  
## Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nuovo nome specificato per la directory contiene il segno dei due punti \(:\) o una barra \(\\ o \/\) \(<xref:System.ArgumentException>\).  
  
-   Il percorso non è valido per uno dei seguenti motivi: è una stringa di lunghezza zero, contiene solo spazi vuoti, contiene caratteri non validi o è il percorso di un dispositivo, ovvero inizia con \\\\  \\\) \(<xref:System.ArgumentException>\).  
  
-   Il percorso non è valido in quanto `Nothing` \(<xref:System.ArgumentNullException>\).  
  
-   `destinationDirectoryName` è `Nothing` o una stringa vuota \(<xref:System.ArgumentNullException>\)  
  
-   La directory di origine non esiste \(<xref:System.IO.DirectoryNotFoundException>\).  
  
-   La directory di origine è una directory radice \(<xref:System.IO.IOException>\).  
  
-   Il percorso combinato punta a un file esistente \(<xref:System.IO.IOException>\).  
  
-   Il percorso di origine e il percorso di destinazione coincidono \(<xref:System.IO.IOException>\).  
  
-   `ShowUI` è impostato su `UIOption.AllDialogs` e l'utente annulla l'operazione oppure uno o più file nella directory non possono essere copiati \(<xref:System.OperationCanceledException>\).  
  
-   Questa operazione è ciclica \(<xref:System.InvalidOperationException>\).  
  
-   Il percorso contiene il segno dei due punti \(:\) \(<xref:System.NotSupportedException>\).  
  
-   La lunghezza del percorso supera la lunghezza massima definita dal sistema \(<xref:System.IO.PathTooLongException>\).  
  
-   Il nome di un file o di una cartella nel percorso contiene i due punti \(:\) o ha un formato non valido \(<xref:System.NotSupportedException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie per visualizzare il percorso \(<xref:System.Security.SecurityException>\).  
  
-   Esiste un file di destinazione ma non è possibile aprirlo \(<xref:System.UnauthorizedAccessException>\).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyDirectory%2A>   
 [How to: Find Subdirectories with a Specific Pattern](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-subdirectories-with-a-specific-pattern.md)   
 [How to: Get the Collection of Files in a Directory](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-get-the-collection-of-files-in-a-directory.md)