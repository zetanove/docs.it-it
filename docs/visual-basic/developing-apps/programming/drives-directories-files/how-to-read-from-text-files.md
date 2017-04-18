---
title: 'Procedura: leggere da file di testo in Visual Basic | Documentazione Microsoft'
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
- extended characters, reading
- reading text files
- reading data, text files
- examples [Visual Basic], reading text files
- text files, reading
ms.assetid: 735fe9d7-0f7a-4185-ba02-f35e580ec4b8
caps.latest.revision: 27
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
ms.openlocfilehash: 362745101d1a8f7dd61b5e3aabe1c27190c46c07
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-read-from-text-files-in-visual-basic"></a>Procedura: leggere da file di testo in Visual Basic
Il metodo <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.ReadAllText%2A> dell'oggetto `My.Computer.FileSystem` consente di leggere da un file di testo. È possibile specificare la codifica file se il contenuto del file utilizza, ad esempio, la codifica ASCII o UTF-8.  
  
 Se la lettura è eseguita da un file contenente caratteri estesi, è necessario specificare la codifica del file.  
  
> [!NOTE]
>  Per leggere un file una riga di testo alla volta, usare il metodo <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.OpenTextFileReader%2A> dell'oggetto `My.Computer.FileSystem`. Il metodo `OpenTextFileReader` restituisce un oggetto <xref:System.IO.StreamReader>. È possibile usare il metodo <xref:System.IO.StreamReader.ReadLine%2A> dell'oggetto `StreamReader` per leggere un file una riga alla volta. È possibile eseguire un test per individuare la fine del file usando il metodo <xref:System.IO.StreamReader.EndOfStream%2A> dell'oggetto `StreamReader`.  
  
### <a name="to-read-from-a-text-file"></a>Per leggere da un file di testo  
  
-   Utilizzare il metodo `ReadAllText` dell'oggetto `My.Computer.FileSystem` per leggere il contenuto di un file di testo in una stringa, specificando il percorso. Nell'esempio seguente viene letto il contenuto del file test.txt in una stringa e quindi tale contenuto viene visualizzato in una finestra di messaggio.  
  
     [!code-vb[VbFileIORead#2](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-text-files_1.vb)]  
  
### <a name="to-read-from-a-text-file-that-is-encoded"></a>Per leggere da un file di testo codificato  
  
-   Utilizzare il metodo `ReadAllText` dell'oggetto `My.Computer.FileSystem` per leggere il contenuto di un file di testo in una stringa, specificando il percorso e il tipo di codifica file. Nell'esempio seguente viene letto il contenuto del file test.txt UTF32 in una stringa e quindi tale contenuto viene visualizzato in una finestra di messaggio.  
  
     [!code-vb[VbFileIORead#3](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-text-files_2.vb)]  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il percorso non è valido per uno dei motivi seguenti: è una stringa di lunghezza zero, contiene solo spazi vuoti, contiene caratteri non validi o è il percorso di un dispositivo (<xref:System.ArgumentException>).  
  
-   Il percorso non è valido perché è `Nothing` (<xref:System.ArgumentNullException>).  
  
-   Il file non esiste (<xref:System.IO.FileNotFoundException>).  
  
-   Il file è in uso in un altro processo oppure si verifica un errore di I/O (<xref:System.IO.IOException>).  
  
-   Il percorso supera la lunghezza massima definita dal sistema (<xref:System.IO.PathTooLongException>).  
  
-   Il nome di un file o di una directory nel percorso contiene i due punti (:) o ha un formato non valido (<xref:System.NotSupportedException>).  
  
-   La memoria disponibile non è sufficiente per la scrittura della stringa nel buffer (<xref:System.OutOfMemoryException>).  
  
-   L'utente non dispone delle autorizzazioni necessarie per visualizzare il percorso (<xref:System.Security.SecurityException>).  
  
 Non basarsi sul nome del file per prendere decisioni in merito al relativo contenuto. È possibile ad esempio che il file Form1.vb non sia un file di origine di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
 Prima di usare i dati nell'applicazione verificare tutti gli input. È possibile che il contenuto del file non corrisponda a quanto previsto e che quindi i metodi per la lettura dal file non abbiano esito positivo.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllText%2A>   
 [Lettura da file](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)   
 [Procedura: leggere da file di testo delimitati da virgola](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-comma-delimited-text-files.md)   
 [Procedura: leggere da file di testo a larghezza fissa](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-fixed-width-text-files.md)   
 [Procedura: leggere da file di testo con più formati](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md)   
 [Risoluzione dei problemi: lettura e scrittura nei file di testo](../../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)   
 [Procedura dettagliata: modifica di file e directory in Visual Basic](../../../../visual-basic/developing-apps/programming/drives-directories-files/walkthrough-manipulating-files-and-directories.md)   
 [Codifiche dei file](../../../../visual-basic/developing-apps/programming/drives-directories-files/file-encodings.md)
