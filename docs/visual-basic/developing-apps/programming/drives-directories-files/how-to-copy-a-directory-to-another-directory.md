---
title: 'Procedura: Copiare una directory in un&quot;altra directory di Visual Basic | Microsoft Docs'
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
- I/O [Visual Basic], copying directories
- I/O [Visual Basic], copying folders
- folders [Visual Basic], copying
- directories [Visual Basic], copying
ms.assetid: 2a370bd7-10ba-4219-afc4-4519d031eb6c
caps.latest.revision: 19
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0b2d59f347df075e3f8c4f952b62e8ad7fa1643f
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-copy-a-directory-to-another-directory-in-visual-basic"></a>Procedura: copiare una directory in un'altra directory di Visual Basic
Usare il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyDirectory%2A> per copiare una directory in un'altra directory. Questo metodo consente di copiare il contenuto della directory nonché la directory stessa. Se la directory di destinazione non esiste, viene creata. Se è presente una directory con lo stesso nome nel percorso di destinazione e `overwrite` è impostato su `False`, il contenuto delle due directory viene unito. È possibile specificare un nuovo nome per la directory durante l'operazione.  
  
 Quando si copiano file in una directory, è possibile che vengano generate eccezioni causate da un file specifico, ad esempio un file presente durante un'unione con `overwrite` impostato su `False`. Quando vengono generate, queste eccezioni vengono consolidate in un'unica eccezione, la cui proprietà `Data` contiene le voci in cui il percorso del file o della directory è la chiave e il messaggio di eccezione specifico è contenuto nel valore corrispondente.  
  
### <a name="to-copy-a-directory-to-another-directory"></a>Per copiare una directory in un'altra directory  
  
-   Usare il metodo `CopyDirectory` specificando i nomi della directory di origine e di destinazione. Nell'esempio di codice riportato di seguito la directory denominata `TestDirectory1` viene copiata in `TestDirectory2`, sovrascrivendo i file esistenti.  
  
     [!code-vb[VbVbcnMyFileSystem#16](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-copy-a-directory-to-another-directory_1.vb)]  
  
     Questo esempio di codice è disponibile anche come frammento di codice IntelliSense. Nella casella di selezione dei frammenti di codice si trova in **File system - Elaborazione di unità, cartelle e file**. Per altre informazioni, vedere [Code Snippets](https://docs.microsoft.com/visualstudio/ide/code-snippets) (Frammenti di codice).  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nuovo nome specificato per la directory contiene il segno dei due punti (:) o una barra (\ o /) (<xref:System.ArgumentException>).  
  
-   Il percorso non è valido per uno dei motivi seguenti: è una stringa di lunghezza zero, contiene solo spazi vuoti, contiene caratteri non validi o è il percorso di un dispositivo, ovvero inizia con \\\\.\\ (<xref:System.ArgumentException>).  
  
-   Il percorso non è valido in quanto `Nothing` (<xref:System.ArgumentNullException>).  
  
-   `destinationDirectoryName` è `Nothing` o una stringa vuota (<xref:System.ArgumentNullException>)  
  
-   La directory di origine non esiste (<xref:System.IO.DirectoryNotFoundException>).  
  
-   La directory di origine è una directory radice (<xref:System.IO.IOException>).  
  
-   Il percorso combinato punta a un file esistente (<xref:System.IO.IOException>).  
  
-   Il percorso di origine e il percorso di destinazione coincidono (<xref:System.IO.IOException>).  
  
-   `ShowUI` è impostato su `UIOption.AllDialogs` e l'utente annulla l'operazione oppure non è possibile copiare uno o più file nella directory (<xref:System.OperationCanceledException>).  
  
-   L'operazione è ciclica (<xref:System.InvalidOperationException>).  
  
-   Il percorso contiene il segno dei due punti (:) (<xref:System.NotSupportedException>).  
  
-   La lunghezza del percorso supera la lunghezza massima definita dal sistema (<xref:System.IO.PathTooLongException>).  
  
-   Il nome di un file o di una cartella nel percorso contiene i due punti (:) o ha un formato non valido (<xref:System.NotSupportedException>).  
  
-   L'utente non ha le autorizzazioni necessarie per visualizzare il percorso (<xref:System.Security.SecurityException>).  
  
-   Esiste un file di destinazione ma non è possibile accedervi (<xref:System.UnauthorizedAccessException>).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyDirectory%2A>   
 [Procedura: Cercare sottodirectory con un modello specifico](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-subdirectories-with-a-specific-pattern.md)   
 [Procedura: ottenere la raccolta di file di una directory](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-get-the-collection-of-files-in-a-directory.md)
