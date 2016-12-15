---
title: "How to: Convert an Array of Bytes into a String in Visual Basic | Microsoft Docs"
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
  - "string conversion, arrays"
  - "byte arrays, converting to strings"
  - "examples [Visual Basic], strings"
  - "arrays [Visual Basic], converting to strings"
ms.assetid: d0dc8317-9ab3-4324-99f7-3f5788c0e72a
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Convert an Array of Bytes into a String in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questo argomento viene illustrato come convertire i byte di una matrice di byte in una stringa.  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzato il metodo <xref:System.Text.Encoding.GetString%2A> della classe di codifica <xref:System.Text.Encoding.Unicode%2A?displayProperty=fullName> per convertire tutti i byte di una matrice di byte in una stringa.  
  
 [!code-vb[VbVbalrStrings#72](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-convert-an-array-of-bytes-into-a-string_1.vb)]  
  
 Per la conversione di una matrice di byte in una stringa è possibile scegliere fra diverse opzioni di codifica:  
  
-   <xref:System.Text.Encoding.ASCII%2A?displayProperty=fullName>: ottiene una codifica per il set di caratteri ASCII \(a 7 bit\).  
  
-   <xref:System.Text.Encoding.BigEndianUnicode%2A?displayProperty=fullName>: ottiene una codifica per il formato UTF\-16 mediante l'ordine di byte big\-endian.  
  
-   <xref:System.Text.Encoding.Default%2A?displayProperty=fullName>: ottiene una codifica per la tabella codici ANSI corrente del sistema.  
  
-   <xref:System.Text.Encoding.Unicode%2A?displayProperty=fullName>: ottiene una codifica per il formato UTF\-16 mediante l'ordine di byte little\-endian.  
  
-   <xref:System.Text.Encoding.UTF32%2A?displayProperty=fullName>: ottiene una codifica per il formato UTF\-32 mediante l'ordine di byte little\-endian.  
  
-   <xref:System.Text.Encoding.UTF7%2A?displayProperty=fullName>: ottiene una codifica per il formato UTF\-7.  
  
-   <xref:System.Text.Encoding.UTF8%2A?displayProperty=fullName>: ottiene una codifica per il formato UTF\-8.  
  
## Vedere anche  
 <xref:System.Text.Encoding?displayProperty=fullName>   
 <xref:System.Text.Encoding.GetString%2A>   
 [How to: Convert Strings into an Array of Bytes in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/how-to-convert-strings-into-an-array-of-bytes.md)