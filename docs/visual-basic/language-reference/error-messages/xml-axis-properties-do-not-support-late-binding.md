---
title: "XML axis properties do not support late binding | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc31168"
  - "vbc31168"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31168"
ms.assetid: 45707363-55e4-4151-892d-d8729106355b
caps.latest.revision: 6
caps.handback.revision: 6
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# XML axis properties do not support late binding
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È stato fatto riferimento a una proprietà axis XML per un oggetto non tipizzato.  
  
 **ID errore:** BC31168  
  
### Per correggere l'errore  
  
-   Assicurarsi che l'oggetto sia un oggetto <xref:System.Xml.Linq.XElement> fortemente tipizzato prima di fare riferimento alla proprietà axis XML.  
  
## Vedere anche  
 [XML Axis Properties](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)