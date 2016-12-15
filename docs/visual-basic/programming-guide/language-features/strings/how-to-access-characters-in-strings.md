---
title: "How to: Access Characters in Strings in Visual Basic | Microsoft Docs"
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
  - "strings [Visual Basic], accessing characters"
  - "characters [Visual Basic], accessing in strings"
ms.assetid: 02c5206c-ffab-494d-b648-3b2ea358dc34
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Access Characters in Strings in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Nell'esempio viene utilizzata la proprietà <xref:System.String.Chars%2A> per accedere al carattere nella posizione specificata all'interno di una stringa.  
  
## Esempio  
 In alcuni casi è utile disporre dei dati relativi ai caratteri di una stringa e alle posizioni di tali caratteri all'interno della stringa.  Una stringa può essere considerata una matrice di caratteri \(istanze `Char`\). È possibile recuperare un particolare carattere facendo riferimento all'indice di tale carattere mediante la proprietà <xref:System.String.Chars%2A>.  
  
 [!code-vb[VbVbalrStrings#49](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-access-characters-in-strings_1.vb)]  
  
 Il parametro `index` della proprietà <xref:System.String.Chars%2A> è a base zero.  
  
## Programmazione efficiente  
 La proprietà <xref:System.String.Chars%2A> restituisce il carattere in corrispondenza della posizione specificata.  Tuttavia, alcuni caratteri Unicode possono essere rappresentati da più di un carattere.  Per ulteriori informazioni su come utilizzare i caratteri Unicode, vedere [How to: Convert a String to an Array of Characters](../../../../visual-basic/programming-guide/language-features/strings/how-to-convert-a-string-to-an-array-of-characters.md).  
  
 La proprietà <xref:System.String.Chars%2A> genera un'eccezione <xref:System.IndexOutOfRangeException> se la lunghezza del parametro `index` è maggiore o uguale a quella della stringa oppure è minore di zero.  
  
## Vedere anche  
 <xref:System.String.Chars%2A>   
 [How to: Convert a String to an Array of Characters](../../../../visual-basic/programming-guide/language-features/strings/how-to-convert-a-string-to-an-array-of-characters.md)   
 [Converting Between Strings and Other Data Types in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/converting-between-strings-and-other-data-types.md)   
 [Strings](../../../../visual-basic/programming-guide/language-features/strings/index.md)