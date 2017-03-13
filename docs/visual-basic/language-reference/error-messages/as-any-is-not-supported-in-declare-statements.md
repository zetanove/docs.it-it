---
title: "&#39;As Any&#39; is not supported in &#39;Declare&#39; statements | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30828"
  - "vbc30828"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30828"
ms.assetid: 7e5cf519-8b64-4ac5-8116-705fe26c846d
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# &#39;As Any&#39; is not supported in &#39;Declare&#39; statements
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In Visual Basic 6.0 e versioni precedenti il tipo di dati `Any` veniva utilizzato con le istruzioni `Declare` per consentire l'utilizzo di argomenti contenenti qualsiasi tipo di dati.  Poiché in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] è supportato l'overload, il tipo di dati `Any` è obsoleto.  
  
 **ID errore:** BC30828  
  
### Per correggere l'errore  
  
1.  Dichiarare parametri del tipo specifico che si desidera utilizzare, come nel seguente esempio.  
  
     [!code-vb[VbVbalrStatements#95](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/as-any-is-not-supported-in-declare-statements_1.vb)]  
  
2.  Utilizzare l'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute> per specificare `As Any` quando la routine chiamata prevede `Void*`.  
  
     [!code-vb[VbVbalrStatements#96](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/as-any-is-not-supported-in-declare-statements_2.vb)]  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Walkthrough: Calling Windows APIs](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)   
 [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Creating Prototypes in Managed Code](../Topic/Creating%20Prototypes%20in%20Managed%20Code.md)