---
title: "Type of member &#39;&lt;membername&gt;&#39; is not CLS-compliant | Microsoft Docs"
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
  - "bc40025"
  - "vbc40025"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40025"
ms.assetid: adbd34bb-43d2-4266-90e7-cd1afaf49b4e
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Type of member &#39;&lt;membername&gt;&#39; is not CLS-compliant
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il tipo di dati specificati per questo membro non fa parte di [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\).  Non si tratta di un errore all'interno del componente, in quanto [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] e [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] supportano questo tipo di dati.  Tuttavia è probabile che un altro componente scritto in codice strettamente conforme a CLS non supporti questo tipo di dati.  È probabile che tale componente non sia in grado di interagire correttamente con il componente.  
  
 I seguenti tipi di dati [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non sono conformi a CLS:  
  
-   [SByte Data Type](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
-   [UInteger Data Type](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
-   [ULong Data Type](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
-   [UShort Data Type](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40025  
  
### Per correggere l'errore  
  
-   Se per il componente si prevede l'interazione solo con altri componenti [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] o non si interfaccia con nessun altro componente, non è necessario modificare nulla.  
  
-   Se si prevede l'interazione con un componente non scritto per [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)], è probabile che sia possibile determinare, tramite reflection o dalla documentazione, se supporta questo tipo di dati.  In tal caso non è necessario modificare nulla.  
  
-   Se si prevede l'interazione con un componente che non supporta questo tipo di dati, è necessario sostituirlo con il tipo più conforme a CLS.  Al posto di `UInteger` ad esempio potrebbe essere possibile utilizzare `Integer` se non è necessario l'intervallo di valore al di sopra di 2.147.483.647.  Se è necessario l'intervallo esteso, è possibile sostituire `UInteger` con `Long`.  
  
-   Se si prevede l'interazione con oggetti COM o di automazione, tenere presente che altri tipi presentano un'ampiezza di dati diversi da [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)].  `uint` , ad esempio, è spesso a 16 bit.  Se si stanno passando argomenti a 16 bit a tale componente, dichiararlo come `UShort` invece di `UInteger` nel codice [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] gestito.  
  
## Vedere anche  
 [Reflection](../Topic/Reflection%20in%20the%20.NET%20Framework.md)   
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/it-it/4c705105-69a2-4e5e-b24e-0633bc32c7f3)