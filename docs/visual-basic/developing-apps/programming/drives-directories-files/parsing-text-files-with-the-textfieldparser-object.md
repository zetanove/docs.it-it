---
title: "Parsing Text Files with the TextFieldParser Object (Visual Basic) | Microsoft Docs"
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
  - "TextFieldParser object, using"
  - "I/O [Visual Basic], parsing files"
  - "files, parsing"
ms.assetid: fc31d6e6-af0c-403f-8a00-d556b2c57567
caps.latest.revision: 20
caps.handback.revision: 20
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Parsing Text Files with the TextFieldParser Object (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

L'oggetto `TextFieldParser` consente di analizzare ed elaborare file di grandi dimensioni strutturati come colonne di testo a larghezza delimitata, ad esempio i file di log e le informazioni di database legacy.  L'analisi di un file di testo con `TextFieldParser` è simile all'esecuzione di un'operazione di scorrimento in un file di testo, mentre l'uso del metodo di analisi per l'estrazione dei campi di testo è analogo ai metodi di manipolazione delle stringhe utilizzati per rappresentare le stringhe delimitate in token di dati.  
  
## Analisi dei diversi tipi di file di testo  
 I file di testo possono contenere campi di larghezza diversa delimitati da caratteri, ad esempio da una virgola o da uno spazio di tabulazione.   Definire `TextFieldType` e il delimitatore, come mostrato nell'esempio seguente, dove viene utilizzato il metodo `SetDelimiters` per definire un file di testo delimitato da tabulazione.  
  
 [!code-vb[VbVbalrTextFieldParser#21](../../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/parsing-text-files-with-the-textfieldparser-object_1.vb)]  
  
 Altri file di testo potrebbero contenere larghezze di campo fisse.  In questi casi è necessario definire il `TextFieldType` come `FixedWidth` e definire la larghezza di ogni campo, come nell'esempio riportato di seguito.  In questo esempio viene utilizzato il metodo `SetFieldWidths` per definire le colonne di testo: la prima colonna ha una larghezza di 5 caratteri, la seconda di 10, la terza di 11 e la quarta è di larghezza variabile.  
  
 [!code-vb[VbVbalrTextFieldParser#22](../../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/parsing-text-files-with-the-textfieldparser-object_2.vb)]  
  
 Una volta definito il formato, è possibile scorrere in ciclo il file utilizzando il metodo `ReadFields` per elaborare una riga per volta.  
  
 Se un campo non corrisponde al formato specificato viene generata l'eccezione <xref:Microsoft.VisualBasic.FileIO.MalformedLineException>.  Quando vengono generate tali eccezioni, le proprietà `ErrorLine` e `ErrorLineNumber` contengono il testo che causa l'eccezione nonché il numero di riga corrispondente.  
  
## Analisi dei file con più formati  
 Il metodo `PeekChars` dell'oggetto `TextFieldParser` può essere utilizzato per controllare ogni campo prima che venga letto, consentendo così di definire più formati per i campi e reagire di conseguenza.   Per ulteriori informazioni, vedere [How to: Read From Text Files with Multiple Formats](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md).  
  
## Vedere anche  
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
 [Risoluzione dei problemi relativi alle eccezioni: Microsoft.VisualBasic.FileIO.TextFieldParser.MalformedLineException](../Topic/Troubleshooting%20Exceptions:%20Microsoft.VisualBasic.FileIO.TextFieldParser.MalformedLineException.md)