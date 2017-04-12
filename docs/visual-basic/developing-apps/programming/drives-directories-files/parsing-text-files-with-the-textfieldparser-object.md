---
title: Analisi dei file di testo con l&quot;oggetto TextFieldParser (Visual Basic) | Microsoft Docs
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
- TextFieldParser object, using
- I/O [Visual Basic], parsing files
- files, parsing
ms.assetid: fc31d6e6-af0c-403f-8a00-d556b2c57567
caps.latest.revision: 20
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
ms.openlocfilehash: 570a5218ce2d750eb5f3a1a1b57e1e05f7fc0cbd
ms.lasthandoff: 03/13/2017

---
# <a name="parsing-text-files-with-the-textfieldparser-object-visual-basic"></a>Analisi dei file di testo con l'oggetto TextFieldParser (Visual Basic)
L'oggetto `TextFieldParser` consente di analizzare ed elaborare file di grandi dimensioni strutturati come colonne di testo a larghezza delimitata, ad esempio i file di log e le informazioni sul database legacy. L'analisi di un file di testo con `TextFieldParser` è simile all'esecuzione di un'iterazione di un file di testo, mentre l'uso del metodo di analisi per l'estrazione dei campi di testo è analogo ai metodi di modifica delle stringhe usati per rappresentare in formato tokene le stringhe delimitate.  
  
## <a name="parsing-different-types-of-text-files"></a>Analisi dei diversi tipi di file di testo  
 I file di testo possono contenere campi di larghezza diversa delimitati da caratteri, ad esempio da una virgola o da uno spazio di tabulazione. Definire `TextFieldType` e il delimitatore, come illustrato nell'esempio seguente, dove viene usato il metodo `SetDelimiters` per definire un file di testo delimitato da tabulazioni:  
  
 [!code-vb[VbVbalrTextFieldParser#21](../../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/parsing-text-files-with-the-textfieldparser-object_1.vb)]  
  
 Altri file di testo potrebbero contenere larghezze di campo fisse. In questi casi è necessario definire `TextFieldType` come `FixedWidth` e stabilire la larghezza di ogni campo, come nell'esempio riportato di seguito. In questo esempio viene usato il metodo `SetFieldWidths` per definire le colonne di testo: la prima colonna ha una larghezza di 5 caratteri, la seconda di 10, la terza di 11 e la quarta è di larghezza variabile.  
  
 [!code-vb[VbVbalrTextFieldParser#22](../../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/parsing-text-files-with-the-textfieldparser-object_2.vb)]  
  
 Dopo aver definito il formato, è possibile riprodurre a ciclo continuo il file usando il metodo `ReadFields` per elaborare una riga per volta.  
  
 Se un campo non corrisponde al formato specificato viene generata l'eccezione <xref:Microsoft.VisualBasic.FileIO.MalformedLineException>. Quando vengono generate eccezioni di questo genere, le proprietà `ErrorLine` e `ErrorLineNumber` contengono il testo che genera l'eccezione e il numero di riga corrispondente.  
  
## <a name="parsing-files-with-multiple-formats"></a>Analisi dei file con più formati  
 Il metodo `PeekChars` dell'oggetto `TextFieldParser` può essere usato per controllare ogni campo prima che venga letto, consentendo così di definire più formati per i campi e reagire di conseguenza. Per altre informazioni, vedere [Procedura: Leggere da file di testo con più formati](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFieldParser%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.PeekChars%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.ReadFields%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.CommentTokens%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.Delimiters%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.ErrorLine%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.ErrorLineNumber%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.FieldWidths%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.HasFieldsEnclosedInQuotes%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.LineNumber%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.TextFieldType%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.TrimWhiteSpace%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.SetDelimiters%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.SetFieldWidths%2A>
