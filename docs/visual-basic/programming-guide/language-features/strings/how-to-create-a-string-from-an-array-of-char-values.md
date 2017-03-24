---
title: "How to: Create a String from An Array of Char Values (Visual Basic) | Microsoft Docs"
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
  - "examples [Visual Basic], arrays"
  - "examples [Visual Basic], Char data type"
ms.assetid: 69f94e85-d57c-4ccc-a62a-426e829f5c5e
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# How to: Create a String from An Array of Char Values (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Nell'esempio riportato di seguito viene creata la stringa "abcd" da singoli caratteri.  
  
## Esempio  
 [!code-vb[VbVbalrStrings#61](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-create-a-string-from-an-array-of-char-values_1.vb)]  
  
## Compilazione del codice  
 Per questo metodo non vi sono requisiti particolari.  
  
 La sintassi `"a"c`, in cui un singolo carattere `c` segue un singolo carattere tra virgolette, viene utilizzata per creare un carattere letterale.  
  
## Programmazione efficiente  
 I caratteri null, ovvero equivalenti a `Chr(0)`, nella stringa generano risultati imprevisti quando si utilizza la stringa.  Il carattere null viene incluso nella stringa, ma i caratteri seguenti non vengono visualizzati in alcune situazioni.  
  
## Vedere anche  
 <xref:System.String>   
 [Char Data Type](../../../../visual-basic/language-reference/data-types/char-data-type.md)   
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)