---
title: "How to: Read From Binary Files in Visual Basic | Microsoft Docs"
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
  - "binary files, reading from"
  - "I/O [Visual Basic], reading from binary files"
  - "ReadAllBytes method, reading from binary files"
  - "My.Computer.FileSystem object, reading from binary files"
ms.assetid: d2b1269e-24b6-42e0-9414-ae708db282d8
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# How to: Read From Binary Files in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

L'oggetto `My.Computer.FileSystem` fornisce il metodo `ReadAllBytes` per la lettura da file binari.  
  
### Per leggere da un file binario  
  
-   Utilizzare il metodo `ReadAllBytes`, che restituisce il contenuto di un file come una matrice di byte.  In questo esempio viene eseguita la lettura dal file `C:/Documents and Settings/selfportrait.jpg`.  
  
     [!code-vb[VbVbcnMyFileSystem#78](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-binary-files_1.vb)]  
  
-   Per file binari di grandi dimensioni, è possibile utilizzare il metodo <xref:System.IO.FileStream.Read%2A> dell'oggetto <xref:System.IO.FileStream> per leggere solo una parte specificata del file per volta.  È quindi possibile limitare la parte del file caricata nella memoria per ogni operazione di lettura.  Nell'esempio di codice seguente viene copiato un file e viene consentito al chiamante di specificare la parte di file letta nella memoria per l'operazione di lettura.  
  
     [!code-vb[VbVbcnMyFileSystem#91](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-binary-files_2.vb)]  
  
## Programmazione efficiente  
 Le seguenti condizioni possono causare la generazione di un'eccezione:  
  
-   Il percorso non è valido per uno dei seguenti motivi: è una stringa di lunghezza zero, contiene solo spazi vuoti, contiene caratteri non validi o è il percorso di un dispositivo \(<xref:System.ArgumentException>\).  
  
-   Il percorso non è valido in quanto `Nothing` \(<xref:System.ArgumentNullException>\).  
  
-   Il file non esiste \(<xref:System.IO.FileNotFoundException>\).  
  
-   Il file è utilizzato da un altro processo o si è verificato un errore di I\/O \(<xref:System.IO.IOException>\).  
  
-   La lunghezza del percorso supera la lunghezza massima definita dal sistema \(<xref:System.IO.PathTooLongException>\).  
  
-   Il nome di un file o di una directory nel percorso contiene i due punti \(:\) o ha un formato non valido \(<xref:System.NotSupportedException>\).  
  
-   La memoria disponibile non è sufficiente per la scrittura della stringa nel buffer \(<xref:System.OutOfMemoryException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie per visualizzare il percorso \(<xref:System.Security.SecurityException>\).  
  
 Non basarsi sul nome del file per prendere decisioni in merito al relativo contenuto.  Ad esempio, è possibile che il file Form1.vb non sia un file di origine Visual Basic.  
  
 Prima di usare i dati nell'applicazione verificare tutti gli input.  È possibile che il contenuto del file non corrisponda a quanto previsto e che quindi i metodi per la lettura dal file non abbiano esito positivo.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllBytes%2A>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllBytes%2A>   
 [Reading from Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)   
 [How to: Read From Text Files with Multiple Formats](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md)   
 [Storing Data to and Reading from the Clipboard](../../../../visual-basic/developing-apps/programming/computer-resources/storing-data-to-and-reading-from-the-clipboard.md)