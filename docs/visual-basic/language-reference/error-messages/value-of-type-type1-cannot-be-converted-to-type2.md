---
title: "Value of type &#39;type1&#39; cannot be converted to &#39;type2&#39; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc31194"
  - "bc31194"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31194"
ms.assetid: 03d50c31-addd-4c90-9c53-725b84f9782e
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# Value of type &#39;type1&#39; cannot be converted to &#39;type2&#39;
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Impossibile convertire il valore di tipo 'type1' in 'type2'.È possibile utilizzare la proprietà 'Value' per ottenere il valore di stringa del primo elemento di '\<parentElement\>'.  
  
 Si è tentato di eseguire implicitamente il cast di un valore letterale XML a un tipo specifico.  Non è possibile eseguire implicitamente il cast del valore letterale XML al tipo specificato.  
  
 **ID errore:** BC31194  
  
### Per correggere l'errore  
  
-   Utilizzare la proprietà `Value` del valore letterale XML per fare riferimento al rispettivo valore come `String`.  Utilizzare la funzione `CType`, un'altra funzione di conversione del tipo o la classe <xref:System.Convert> per eseguire il cast del valore come tipo specificato.  
  
## Vedere anche  
 <xref:System.Convert>   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [XML Literals](../../../visual-basic/language-reference/xml-literals/index.md)   
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)