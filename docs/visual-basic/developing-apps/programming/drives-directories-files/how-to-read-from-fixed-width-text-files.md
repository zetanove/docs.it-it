---
title: "How to: Read From Fixed-width Text Files in Visual Basic | Microsoft Docs"
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
  - "fixed-width text file"
  - "reading text files, fixed-width"
  - "files, parsing"
  - "text files, tasks"
  - "text files, reading"
ms.assetid: 99be5692-967a-4e85-993e-cd18139a5a69
caps.latest.revision: 24
caps.handback.revision: 24
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Read From Fixed-width Text Files in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

L'oggetto `TextFieldParser` consente di analizzare in modo facile ed efficace i file di testo strutturati, ad esempio i log.  
  
 La proprietà `TextFieldType` definisce se il file analizzato è un file delimitato o un file con campi di testo a larghezza fissa.  In un file di testo a larghezza fissa, il campo alla fine può avere una larghezza variabile.  Per specificare che il campo alla fine ha una larghezza variabile, definirlo in modo che abbia una larghezza minore o uguale a zero.  
  
### Per analizzare un file di testo a larghezza fissa  
  
1.  Creare un nuovo oggetto `TextFieldParser`.  Nel codice riportato di seguito viene creato l'oggetto `TextFieldParser` denominato `Reader` e viene aperto il file `test.log`.  
  
     [!code-vb[VbFileIORead#9](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-fixed-width-text-files_1.vb)]  
  
2.  Definire la proprietà `TextFieldType` come `FixedWidth`, impostandone la larghezza e il formato.  Nel codice riportato di seguito vengono definite le colonne di testo: la prima ha una larghezza pari a 5 caratteri, la seconda a 10, la terza a 11 e la quarta ha una larghezza variabile.  
  
     [!code-vb[VbFileIORead#10](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-fixed-width-text-files_2.vb)]  
  
3.  Scorrere i campi nel file.  Se sono presenti righe danneggiate, segnalare l'errore e continuare l'analisi.  
  
     [!code-vb[VbFileIORead#11](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-fixed-width-text-files_3.vb)]  
  
4.  Chiudere i blocchi `While` e `Using` con `End While` e `End Using`.  
  
     [!code-vb[VbFileIORead#12](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-fixed-width-text-files_4.vb)]  
  
## Esempio  
 Nell'esempio riportato di seguito la lettura viene eseguita dal file `test.log`.  
  
 [!code-vb[VbFileIORead#13](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-fixed-width-text-files_5.vb)]  
  
## Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Non è possibile analizzare una riga utilizzando il formato specificato \(<xref:Microsoft.VisualBasic.FileIO.MalformedLineException>\).  Nel messaggio di eccezione viene specificata la riga che ha generato l'eccezione, mentre la proprietà <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.ErrorLine%2A> viene assegnata al testo contenuto nella riga.  
  
-   Il file specificato non esiste \(<xref:System.IO.FileNotFoundException>\).  
  
-   Un contesto di attendibilità parziale in cui gli utenti non dispongono di autorizzazioni sufficienti per accedere al file  \(<xref:System.Security.SecurityException>\).  
  
-   Il percorso è troppo lungo \(<xref:System.IO.PathTooLongException>\).  
  
-   L'utente non dispone delle autorizzazioni sufficienti per accedere al file \(<xref:System.UnauthorizedAccessException>\).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser?displayProperty=fullName>   
 [How to: Read From Comma\-Delimited Text Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-comma-delimited-text-files.md)   
 [How to: Read From Text Files with Multiple Formats](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md)   
 [Parsing Text Files with the TextFieldParser Object](../../../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)   
 [Walkthrough: Manipulating Files and Directories in Visual Basic](../../../../visual-basic/developing-apps/programming/drives-directories-files/walkthrough-manipulating-files-and-directories.md)   
 [Troubleshooting: Reading from and Writing to Text Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)   
 [Risoluzione dei problemi relativi alle eccezioni: Microsoft.VisualBasic.FileIO.TextFieldParser.MalformedLineException](../Topic/Troubleshooting%20Exceptions:%20Microsoft.VisualBasic.FileIO.TextFieldParser.MalformedLineException.md)