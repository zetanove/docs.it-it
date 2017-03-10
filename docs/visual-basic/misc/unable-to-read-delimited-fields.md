---
title: "Impossibile leggere i campi delimitati. Le virgolette non sono un delimitatore consentito se EscapeQuotes &#232; impostato su True | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrTextFieldParser_IllegalDelimiter"
ms.assetid: ab8a0c3a-b89c-4617-9e31-7e81f5dca433
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Impossibile leggere i campi delimitati. Le virgolette non sono un delimitatore consentito se EscapeQuotes &#232; impostato su True
`TextFieldParser` non può leggere dal file perché sono state fornite le virgolette \("\) come delimitatore e `EscapeQuotes` è impostato su `True`.  
  
### Per correggere l'errore  
  
-   Impostare `EscapeQuotes` su `False`.  
  
## Vedere anche  
 [Metodo TextFieldParser.SetDelimiters](http://msdn.microsoft.com/it-it/21fa40ec-5866-4d0e-9fd9-c708a190dcc9)   
 [Proprietà TextFieldParser.Delimiters](http://msdn.microsoft.com/it-it/4eb18f4d-3011-40a9-b668-be93eed0444f)   
 [How to: Read From Comma\-Delimited Text Files](../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-comma-delimited-text-files.md)   
 [TextFieldParser Object](../../visual-basic/language-reference/objects/textfieldparser-object.md)