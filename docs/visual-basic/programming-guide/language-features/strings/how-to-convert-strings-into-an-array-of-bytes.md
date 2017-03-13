---
title: "How to: Convert Strings into an Array of Bytes in Visual Basic | Microsoft Docs"
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
  - "string conversion, arrays"
  - "arrays [Visual Basic], converting strings to"
  - "byte arrays"
  - "examples [Visual Basic], string conversion"
  - "arrays [Visual Basic], byte arrays"
ms.assetid: f477d35c-a3fc-4a30-b1d4-cd0d353aae1d
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# How to: Convert Strings into an Array of Bytes in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questo argomento viene illustrato come convertire una stringa in una matrice di byte.  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzato il metodo <xref:System.Text.Encoding.GetBytes%2A> della classe di codifica <xref:System.Text.Encoding.Unicode%2A?displayProperty=fullName> per convertire una stringa in una matrice di byte.  
  
 [!code-vb[VbVbalrStrings#74](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-convert-strings-into-an-array-of-bytes_1.vb)]  
  
 Per la conversione di una stringa in una matrice di byte è possibile scegliere tra diverse opzioni di codifica:  
  
-   <xref:System.Text.Encoding.ASCII%2A?displayProperty=fullName>: ottiene una codifica per il set di caratteri ASCII \(a 7 bit\).  
  
-   <xref:System.Text.Encoding.BigEndianUnicode%2A?displayProperty=fullName>: ottiene una codifica per il formato UTF\-16 mediante l'ordine di byte big\-endian.  
  
-   <xref:System.Text.Encoding.Default%2A?displayProperty=fullName>: ottiene una codifica per la tabella codici ANSI corrente del sistema.  
  
-   <xref:System.Text.Encoding.Unicode%2A?displayProperty=fullName>: ottiene una codifica per il formato UTF\-16 mediante l'ordine di byte little\-endian.  
  
-   <xref:System.Text.Encoding.UTF32%2A?displayProperty=fullName>: ottiene una codifica per il formato UTF\-32 mediante l'ordine di byte little\-endian.  
  
-   <xref:System.Text.Encoding.UTF7%2A?displayProperty=fullName>: ottiene una codifica per il formato UTF\-7.  
  
-   <xref:System.Text.Encoding.UTF8%2A?displayProperty=fullName>: ottiene una codifica per il formato UTF\-8.  
  
## Vedere anche  
 <xref:System.Text.Encoding?displayProperty=fullName>   
 <xref:System.Text.Encoding.GetBytes%2A>   
 [How to: Convert an Array of Bytes into a String in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/how-to-convert-an-array-of-bytes-into-a-string.md)