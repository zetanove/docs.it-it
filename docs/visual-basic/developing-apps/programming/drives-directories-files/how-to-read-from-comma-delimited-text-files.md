---
title: 'Procedura: Leggere da file di testo con valori delimitati da virgole in Visual Basic | Microsoft Docs'
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
- files, parsing
- text files, tasks
- reading text files, comma-delimited
- text files, reading
ms.assetid: a8413fe4-0dba-49c8-8692-44fb67a9ec4f
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 011e92f1d3c4aa7fae5a1022815dfe83b313685f
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-read-from-comma-delimited-text-files-in-visual-basic"></a>Procedura: Leggere da file di testo con valori delimitati da virgole in Visual Basic
L'oggetto `TextFieldParser` consente di analizzare in modo facile ed efficace i file di testo strutturati, ad esempio i log. La proprietà `TextFieldType` definisce se si tratta di un file delimitato o di un file con campi di testo a larghezza fissa.  
  
### <a name="to-parse-a-comma-delimited-text-file"></a>Per analizzare un file di testo con valori delimitati da virgole  
  
1.  Creare un nuovo oggetto `TextFieldParser`. Il codice riportato di seguito crea l'oggetto `TextFieldParser` denominato `MyReader` e apre il file `test.txt`.  
  
     [!code-vb[VbFileIORead#15](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-comma-delimited-text-files_1.vb)]  
  
2.  Definire il tipo `TextField` e il delimitatore. Nel codice riportato di seguito viene definita la proprietà `TextFieldType` come `Delimited` e il delimitatore come ",".  
  
     [!code-vb[VbFileIORead#16](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-comma-delimited-text-files_2.vb)]  
  
3.  Eseguire il ciclo attraverso i campi nel file. Se sono presenti righe danneggiate, segnalare un errore e continuare l'analisi. Nel codice riportato di seguito viene eseguito un ciclo attraverso il file, visualizzando ogni campo e segnalando eventuali campi formattati in modo errato.  
  
     [!code-vb[VbFileIORead#17](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-comma-delimited-text-files_3.vb)]  
  
4.  Chiudere i blocchi `While` e `Using` con `End While` ed `End Using`.  
  
     [!code-vb[VbFileIORead#18](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-comma-delimited-text-files_4.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio riportato di seguito viene letto il file `test.txt`.  
  
 [!code-vb[VbFileIORead#19](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-comma-delimited-text-files_5.vb)]  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Impossibile analizzare la riga usando il formato specificato (<xref:Microsoft.VisualBasic.FileIO.MalformedLineException>). Il messaggio di eccezione specifica la riga che ha generato l'eccezione, mentre alla proprietà <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.ErrorLine%2A> viene assegnato il testo contenuto nella riga.  
  
-   File specificato inesistente (<xref:System.IO.FileNotFoundException>).  
  
-   Un contesto di attendibilità parziale in cui gli utenti non dispongono di autorizzazioni sufficienti per accedere al file (<xref:System.Security.SecurityException>).  
  
-   Percorso del file troppo lungo (<xref:System.IO.PathTooLongException>).  
  
-   L'utente non dispone di autorizzazioni sufficienti per accedere al file (<xref:System.UnauthorizedAccessException>).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser?displayProperty=fullName>   
 [Procedura: Leggere da file di testo a larghezza fissa](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-fixed-width-text-files.md)   
 [Procedura: Leggere da file di testo con più formati](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md)   
 [Analisi dei file di testo con l'oggetto TextFieldParser](../../../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)   
 [Procedura dettagliata: Modifica di file e directory in Visual Basic](../../../../visual-basic/developing-apps/programming/drives-directories-files/walkthrough-manipulating-files-and-directories.md)   
 [Risoluzione dei problemi: lettura e scrittura nei file di testo](../../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)
