---
title: "Troubleshooting: Reading from and Writing to Text Files (Visual Basic) | Microsoft Docs"
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
  - "troubleshooting file I/O"
  - "writing text to files, troubleshooting"
  - "troubleshooting Visual Basic, text files"
  - "I/O [Visual Basic], troubleshooting text files"
  - "writing to files, troubleshooting"
  - "reading text files, troubleshooting"
ms.assetid: a8e9b44d-facb-4718-8c0f-466537171182
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Troubleshooting: Reading from and Writing to Text Files (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questo argomento vengono descritti i problemi comuni riscontranti quando si utilizzano file di testo e viene suggerita una soluzione a ogni problema.  
  
## Problemi comuni  
 I problemi comuni riscontrati quando si utilizzano file di testo comprendono eccezioni di sicurezza, codifiche dei file o percorsi non validi.  
  
### Eccezioni di sicurezza  
 Una <xref:System.Security.SecurityException> viene generata quando viene rilevato un errore di sicurezza.  Spesso tale situazione dipende dal fatto che l'utente non dispone delle autorizzazioni necessarie e può essere risolta aggiungendo le autorizzazioni o utilizzando i file nell'archiviazione isolata.   Per ulteriori informazioni, vedere [Risoluzione dei problemi relativi alle eccezioni: System.Security.SecurityException](../Topic/Troubleshooting%20Exceptions:%20System.Security.SecurityException.md).  
  
### Codifiche dei file  
 Le codifiche dei file, note anche come codifiche del carattere, specificano come rappresentare i caratteri durante l'elaborazione del testo.  I caratteri imprevisti in un file di testo possono creare una codifica errata.  Per la maggior parte dei file, una codifica è preferibile a un'altra in termini di quali caratteri del linguaggio gestire. Tuttavia, in genere, si preferisce l'utilizzo di Unicode.  Per ulteriori informazioni, vedere [File Encodings](../../../../visual-basic/developing-apps/programming/drives-directories-files/file-encodings.md) e <xref:System.Text.Encoding>.  
  
### Percorsi non validi  
 Quando si analizzano i percorsi dei file, in specifico i percorsi relativi, è facile fornire i dati errati.  Molti problemi possono essere corretti verificando la correttezza del percorso fornito.  Per ulteriori informazioni, vedere [Procedura: analizzare percorsi di file](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 [Reading from Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)   
 [Writing to Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/writing-to-files.md)   
 [Parsing Text Files with the TextFieldParser Object](../../../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)