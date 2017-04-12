---
title: 'Procedura: Leggere da file di testo a larghezza fissa in Visual Basic | Microsoft Docs'
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
- fixed-width text file
- reading text files, fixed-width
- files, parsing
- text files, tasks
- text files, reading
ms.assetid: 99be5692-967a-4e85-993e-cd18139a5a69
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c1ce67620d96a35ccf1223cc4de9d34ca1aaa722
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-read-from-fixed-width-text-files-in-visual-basic"></a>Procedura: Leggere da file di testo a larghezza fissa in Visual Basic
L'oggetto `TextFieldParser` consente di analizzare in modo facile ed efficace i file di testo strutturati, ad esempio i log.  
  
 La proprietà `TextFieldType` definisce se il file analizzato è un file delimitato o un file con campi di testo a larghezza fissa. In un file di testo a larghezza fissa il campo alla fine può avere una larghezza variabile. Per specificare che il campo alla fine deve avere una larghezza variabile, definirlo in modo che abbia una larghezza minore o uguale a zero.  
  
### <a name="to-parse-a-fixed-width-text-file"></a>Per analizzare un file di testo a larghezza fissa  
  
1.  Creare un nuovo oggetto `TextFieldParser`. Il codice riportato di seguito crea l'oggetto `TextFieldParser` denominato `Reader` e apre il file `test.log`.  
  
     [!code-vb[VbFileIORead#9](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-fixed-width-text-files_1.vb)]  
  
2.  Definire la proprietà `TextFieldType` come `FixedWidth`, impostandone la larghezza e il formato. Il codice seguente definisce le colonne di testo: la prima ha una larghezza di 5 caratteri, la seconda di 10 e la terza di 11, mentre la quarta ha una larghezza variabile.  
  
     [!code-vb[VbFileIORead#10](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-fixed-width-text-files_2.vb)]  
  
3.  Eseguire il ciclo attraverso i campi nel file. Se sono presenti righe danneggiate, segnalare un errore e continuare l'analisi.  
  
     [!code-vb[VbFileIORead#11](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-fixed-width-text-files_3.vb)]  
  
4.  Chiudere i blocchi `While` e `Using` con `End While` ed `End Using`.  
  
     [!code-vb[VbFileIORead#12](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-fixed-width-text-files_4.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio riportato di seguito viene letto il file `test.log`.  
  
 [!code-vb[VbFileIORead#13](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-fixed-width-text-files_5.vb)]  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Non è possibile analizzare una riga usando il formato specificato (<xref:Microsoft.VisualBasic.FileIO.MalformedLineException>). Il messaggio di eccezione specifica la riga che ha generato l'eccezione, mentre al testo contenuto nella riga viene assegnata la proprietà <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.ErrorLine%2A>.  
  
-   Il file specificato non esiste (<xref:System.IO.FileNotFoundException>).  
  
-   Un contesto di attendibilità parziale in cui gli utenti non dispongono di autorizzazioni sufficienti per accedere al file (<xref:System.Security.SecurityException>).  
  
-   Il percorso è troppo lungo (<xref:System.IO.PathTooLongException>).  
  
-   L'utente non dispone delle autorizzazioni sufficienti per accedere al file (<xref:System.UnauthorizedAccessException>).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser?displayProperty=fullName>   
 [Procedura: Leggere da file di testo con valori delimitati da virgole](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-comma-delimited-text-files.md)   
 [Procedura: Leggere da file di testo con più formati](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md)   
 [Analisi dei file di testo con l'oggetto TextFieldParser](../../../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)   
 [Procedura dettagliata: Modifica di file e directory in Visual Basic](../../../../visual-basic/developing-apps/programming/drives-directories-files/walkthrough-manipulating-files-and-directories.md)   
 [Risoluzione dei problemi: lettura e scrittura nei file di testo](../../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)   
 
