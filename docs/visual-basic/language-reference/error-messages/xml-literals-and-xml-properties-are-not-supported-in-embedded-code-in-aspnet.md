---
title: "XML literals and XML properties are not supported in embedded code within ASP.NET | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc31200"
  - "bc31200"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31200"
ms.assetid: 053e8cba-8584-45cc-9fa0-43d122779772
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# XML literals and XML properties are not supported in embedded code within ASP.NET
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

I valori letterali XML e le proprietà XML non sono supportati nel codice incorporato all'interno di ASP.NET.Per utilizzare funzionalità XML, spostare il codice nel codice associato.  
  
 Un valore letterale XML o una proprietà axis XML viene definita all'interno del codice incorporato \(`<%= =>`\) in un file ASP.NET.  
  
 **ID errore:** BC31200  
  
### Per correggere l'errore  
  
-   Spostare il codice che include il valore letterale XML o la proprietà axis XML in un file code\-behind ASP.NET.  
  
## Vedere anche  
 [XML Literals](../../../visual-basic/language-reference/xml-literals/index.md)   
 [XML Axis Properties](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)