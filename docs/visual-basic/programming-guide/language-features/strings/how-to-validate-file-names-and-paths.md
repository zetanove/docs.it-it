---
title: "How to: Validate File Names and Paths in Visual Basic | Microsoft Docs"
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
  - "file names, validating"
  - "strings [Visual Basic], validating"
  - "Boolean values"
  - "paths, validating"
ms.assetid: f673462d-57b7-4120-b13a-6a7592f7ab2c
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# How to: Validate File Names and Paths in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Nell'esempio viene restituito un valore `Boolean` che indica se la stringa rappresenta un nome o un percorso di file.  Viene eseguito il controllo di convalida alla ricerca di caratteri nel nome non supportati dal the file system.  
  
## Esempio  
 [!code-vb[VbVbcnRegEx#4](../../../../visual-basic/programming-guide/language-features/strings/codesnippet/VisualBasic/how-to-validate-file-names-and-paths_1.vb)]  
  
 Nell'esempio non viene controllato se nel nome i due punti sono stati inseriti nella posizione errata, se le directory sono senza nome oppure se la lunghezza del nome supera la lunghezza massima definita dall'utente.  Inoltre, non viene verificato se l'applicazione dispone dell'autorizzazione di accesso alle risorse del file system con il nome specificato.  
  
## Vedere anche  
 <xref:System.IO.Path.GetInvalidPathChars%2A>   
 [Validating Strings in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/validating-strings.md)