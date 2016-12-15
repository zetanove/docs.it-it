---
title: "How to: Convert Hexadecimal Strings to Numbers (Visual Basic) | Microsoft Docs"
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
  - "numbers, hexadecimals"
  - "hexadecimals, decimals"
  - "examples [Visual Basic], string conversion"
  - "decimals, hexadecimals"
  - "string conversion, hexadecimal to numbers"
ms.assetid: 76675807-eadb-4c08-bd50-e6c6ff4b8ced
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Convert Hexadecimal Strings to Numbers (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questo esempio una stringa esadecimale viene convertita in un Integer mediante il metodo <xref:System.Convert.ToInt32%2A>.  
  
### Per convertire una stringa esadecimale in un numero  
  
-   Utilizzare il metodo <xref:System.Convert.ToInt32%2A> per convertire il numero espresso in base 16 in un Integer.  
  
     Il primo argomento del metodo <xref:System.Convert.ToInt32%2A> è la stringa da convertire.  Il secondo argomento descrive la base in cui è espresso il numero. I valori esadecimali sono espressi in base 16.  
  
     [!code-vb[VbVbalrStrings#62](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-convert-hexadecimal-strings-to-numbers_1.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Conversion.Hex%2A>   
 <xref:System.Convert.ToInt32%2A>