---
title: 'Procedura: Eliminare un file in Visual Basic | Microsoft Docs'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Delete method
- files, deleting
- files, manipulating
- File object
ms.assetid: 4b721769-3e45-4be7-b7fe-b08dc4141b44
caps.latest.revision: 24
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: f6cf3192d6983b6222815c5c77a3dfd0b3845650
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-delete-a-file-in-visual-basic"></a>Procedura: eliminare un file in Visual Basic
Il metodo `DeleteFile` dell'oggetto `My.Computer.FileSystem` consente l'eliminazione di un file. È possibile scegliere di inviare il file eliminato al **Cestino**, chiedere all'utente di confermare l'eliminazione del file e decidere cosa fare quando l'utente annulla l'operazione.  
  
### <a name="to-delete-a-text-file"></a>Per eliminare un file di testo  
  
-   Usare il metodo `DeleteFile` per eliminare il file. Il codice seguente illustra come eliminare il file denominato `test.txt`.  
  
     [!code-vb[VbVbcnMyFileSystem#22](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-delete-a-file_1.vb)]  
  
### <a name="to-delete-a-text-file-and-ask-the-user-to-confirm-that-the-file-should-be-deleted"></a>Per eliminare un file di testo e chiedere all'utente di confermare l'eliminazione del file  
  
-   Usare il metodo `DeleteFile` per eliminare il file, impostando `showUI` su `AllDialogs`. Il codice seguente illustra come eliminare il file denominato `test.txt` e consentire all'utente di confermare l'eliminazione del file.  
  
     [!code-vb[VbFileIOMisc#9](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-delete-a-file_2.vb)]  
  
### <a name="to-delete-a-text-file-and-send-it-to-the-recycle-bin"></a>Per eliminare un file di testo e inviarlo al Cestino  
  
-   Usare il metodo `DeleteFile` per eliminare il file, specificando `SendToRecycleBin` per il parametro `recycle`. Il codice seguente illustra come eliminare il file denominato `test.txt` e inviarlo al **Cestino**.  
  
     [!code-vb[VbFileIOMisc#10](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-delete-a-file_3.vb)]  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il percorso non è valido per uno dei motivi seguenti: è una stringa di lunghezza zero, contiene solo spazi vuoti, contiene caratteri non validi o è il percorso di un dispositivo (inizia con \\\\.\\) (<xref:System.ArgumentException>).  
  
-   Il percorso non è valido in quanto è `Nothing` (<xref:System.ArgumentNullException>).  
  
-   La lunghezza del percorso supera la lunghezza massima definita dal sistema (<xref:System.IO.PathTooLongException>).  
  
-   Il nome di un file o di una cartella nel percorso contiene i due punti (:) o ha un formato non valido (<xref:System.NotSupportedException>).  
  
-   Il file è in uso (<xref:System.IO.IOException>).  
  
-   L'utente non dispone delle autorizzazioni necessarie per visualizzare il percorso (<xref:System.Security.SecurityException>).  
  
-   Il file non esiste (<xref:System.IO.FileNotFoundException>).  
  
-   L'utente non è autorizzato a eliminare il file oppure il file è di sola lettura (<xref:System.UnauthorizedAccessException>).  
  
-   Esiste un contesto di attendibilità parziale in cui l'utente non ha autorizzazioni sufficienti (<xref:System.Security.SecurityException>).  
  
-   L'utente ha annullato l'operazione e `onUserCancel` è impostato su `ThrowException` (<xref:System.OperationCanceledException>).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.UICancelOption>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.UIOption>   
 <xref:Microsoft.VisualBasic.FileIO.RecycleOption>   
 [Procedura: ottenere la raccolta di file di una directory](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-get-the-collection-of-files-in-a-directory.md)
