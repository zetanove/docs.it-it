---
title: "How to: Convert a String to an Array of Characters in Visual Basic | Microsoft Docs"
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
  - "character arrays, converting strings"
  - "arrays [Visual Basic], converting strings to"
  - "examples [Visual Basic], string conversion"
  - "strings [Visual Basic], converting to arrays"
  - "string conversion [Visual Basic], arrays"
ms.assetid: 1b54b686-ab29-413b-adce-6bd5422376eb
caps.latest.revision: 7
caps.handback.revision: 7
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Convert a String to an Array of Characters in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In alcuni casi, è utile disporre dei dati relativi ai caratteri e alle relative posizioni all'interno della stringa, ad esempio quando si analizza la stringa.  Nell'esempio, viene illustrato in che modo ottenere una matrice dei caratteri di una stringa chiamando il metodo <xref:System.String.ToCharArray%2A> della stringa.  
  
## Esempio  
 Nell'esempio, viene descritto come suddividere una stringa in una matrice `Char` e come suddividere una stringa in una matrice `String` dei relativi caratteri di testo Unicode.  Il motivo di questa distinzione risiede nel fatto che i caratteri di testo Unicode possono essere costituiti da due o più caratteri `Char`, quali una coppia di surrogati o una sequenza di caratteri in combinazione.  Per ulteriori informazioni, vedere <xref:System.Globalization.TextElementEnumerator> e lo standard Unicode all'indirizzo http:\/\/www.unicode.org.  
  
 [!code-vb[VbVbalrStrings#75](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-convert-a-string-to-an-array-of-characters_1.vb)]  
  
## Esempio  
 Suddividere una stringa nei relativi caratteri di testo Unicode è un'operazione più complessa, ma è necessaria per ottenere informazioni sulla rappresentazione visiva della stringa.  In questo esempio, il metodo <xref:System.Globalization.StringInfo.SubstringByTextElements%2A> viene utilizzato per ottenere informazioni sui caratteri di testo Unicode che costituiscono una stringa.  
  
 [!code-vb[VbVbalrStrings#76](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-convert-a-string-to-an-array-of-characters_2.vb)]  
  
## Vedere anche  
 <xref:System.String.Chars%2A>   
 <xref:System.Globalization.StringInfo?displayProperty=fullName>   
 [How to: Access Characters in Strings](../../../../visual-basic/programming-guide/language-features/strings/how-to-access-characters-in-strings.md)   
 [Converting Between Strings and Other Data Types in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/converting-between-strings-and-other-data-types.md)   
 [Strings](../../../../visual-basic/programming-guide/language-features/strings/index.md)