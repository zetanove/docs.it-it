---
title: "How to: Read From Text Files with Multiple Formats in Visual Basic | Microsoft Docs"
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
  - "TextFieldParser object, reading from a file"
  - "TextFieldType enumeration"
  - "My.Computer.FileSystem.WriteAllText method, parsing structured text files"
  - "WriteAllText method, parsing structured text files"
  - "PeekChars method, determining format of text"
  - "reading text files, multiple formats"
  - "I/O [Visual Basic], reading text files"
  - "text files, reading"
ms.assetid: 8d185eb2-79ca-42cd-95a7-d3ff44a5a0f8
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# How to: Read From Text Files with Multiple Formats in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

L'oggetto <xref:Microsoft.VisualBasic.FileIO.TextFieldParser> consente di analizzare in modo facile ed efficace i file di testo strutturati, ad esempio i log.  È possibile elaborare un file con più formati utilizzando il metodo `PeekChars` per determinare il formato di ciascuna riga mentre si analizza il file.  
  
### Per analizzare un file di testo con più formati  
  
1.  Aggiungere un file di testo denominato testfile.txt al progetto.  Aggiungere al file di testo quanto segue:  
  
    ```  
    Err  1001 Cannot access resource.  
    Err  2014 Resource not found.  
    Acc  10/03/2009User1      Administrator.  
    Err  0323 Warning: Invalid access attempt.  
    Acc  10/03/2009User2      Standard user.  
    Acc  10/04/2009User2      Standard user.  
    ```  
  
2.  Definire il formato previsto e il formato utilizzato quando viene restituito un errore.  Dato che l'ultima voce di ogni matrice è \- 1, si presuppone quindi che il campo sia di larghezza variabile.  Questo si verifica quando l'ultima voce della matrice è minore o uguale a 0.  
  
     [!code-vb[VbFileIORead#4](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-text-files-with-multiple-formats_1.vb)]  
  
3.  Creare un nuovo oggetto <xref:Microsoft.VisualBasic.FileIO.TextFieldParser>, definendone l'ampiezza e il formato.  
  
     [!code-vb[VbFileIORead#5](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-text-files-with-multiple-formats_2.vb)]  
  
4.  Far scorrere le righe, verificando il formato prima di eseguire la lettura.  
  
     [!code-vb[VbFileIORead#6](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-text-files-with-multiple-formats_3.vb)]  
  
5.  Scrivere gli errori nella console.  
  
     [!code-vb[VbFileIORead#7](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-text-files-with-multiple-formats_4.vb)]  
  
## Esempio  
 Di seguito è riportato un esempio completo che legge dal file `testfile.txt`.  
  
 [!code-vb[VbFileIORead#8](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-text-files-with-multiple-formats_5.vb)]  
  
## Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Non è possibile analizzare una riga utilizzando il formato specificato \(<xref:Microsoft.VisualBasic.FileIO.MalformedLineException>\).  Nel messaggio di eccezione viene specificata la riga che ha generato l'eccezione, mentre la proprietà <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.ErrorLine%2A> viene assegnata al testo contenuto nella riga.  
  
-   Il file specificato non esiste \(<xref:System.IO.FileNotFoundException>\).  
  
-   Un contesto di attendibilità parziale in cui gli utenti non dispongono di autorizzazioni sufficienti per accedere al file  \(<xref:System.Security.SecurityException>\).  
  
-   Il percorso è troppo lungo \(<xref:System.IO.PathTooLongException>\).  
  
-   L'utente non dispone delle autorizzazioni sufficienti per accedere al file \(<xref:System.UnauthorizedAccessException>\).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser?displayProperty=fullName>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.PeekChars%2A>   
 <xref:Microsoft.VisualBasic.FileIO.MalformedLineException>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.EndOfData%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.TextFieldType%2A>   
 [How to: Read From Comma\-Delimited Text Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-comma-delimited-text-files.md)   
 [How to: Read From Fixed\-width Text Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-fixed-width-text-files.md)   
 [Parsing Text Files with the TextFieldParser Object](../../../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)