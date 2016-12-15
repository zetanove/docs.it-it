---
title: "Type &lt;typename&gt; is not CLS-compliant | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc40041"
  - "vbc40041"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40041"
ms.assetid: 634132c2-5646-44aa-98c6-f773e2e63882
caps.latest.revision: 7
caps.handback.revision: 7
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Type &lt;typename&gt; is not CLS-compliant
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Una variabile, una proprietà o il valore restituito di una funzione è dichiarato con un tipo di dati che non è conforme con CLS.  
  
 Un'applicazione può essere conforme con [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\), soltanto se utilizza esclusivamente tipi conformi con CLS.  
  
 I seguenti tipi di dati [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non sono conformi a CLS:  
  
-   [SByte Data Type](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
-   [UInteger Data Type](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
-   [ULong Data Type](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
-   [UShort Data Type](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 **ID errore:** BC40041  
  
### Per correggere l'errore  
  
-   Se si desidera che l'applicazione sia conforme con CLS, sostituire il tipo di dati di questo elemento con il tipo di dati conforme con CLS più simile.  Al posto di `UInteger` ad esempio potrebbe essere possibile utilizzare `Integer` se non è necessario l'intervallo di valore al di sopra di 2.147.483.647.  Se è necessario l'intervallo esteso, è possibile sostituire `UInteger` con `Long`.  
  
-   Se non è necessario che l'applicazione sia conforme con CLS, non occorre apportare alcuna modifica.  Tenere tuttavia presente che esiste questa non conformità.  
  
## Vedere anche  
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/it-it/4c705105-69a2-4e5e-b24e-0633bc32c7f3)