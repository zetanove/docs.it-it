---
title: "Type of parameter &#39;&lt;parametername&gt;&#39; is not CLS-compliant | Microsoft Docs"
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
  - "vbc40028"
  - "bc40028"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40028"
ms.assetid: dfa1f6f9-bb88-44ad-b85f-149144363d41
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Type of parameter &#39;&lt;parametername&gt;&#39; is not CLS-compliant
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Una routine è contrassegnata come `<CLSCompliant(True)>` ma dichiara una parametro con un tipo contrassegnato come `<CLSCompliant(False)>` o non contrassegnato, oppure non qualifica perché si tratta di un tipo non conforme.  
  
 Per rendere conforme una routine con [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\), è necessario utilizzare solo tipi CLS conformi.  Questa regola è valida per i tipi dei parametri, il tipo restituito e i tipi di tutte le relative variabili locali.  
  
 I seguenti tipi di dati [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non sono conformi a CLS:  
  
-   [SByte Data Type](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
-   [UInteger Data Type](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
-   [ULong Data Type](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
-   [UShort Data Type](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 Quando si applica l'<xref:System.CLSCompliantAttribute> a un elemento di programmazione, il parametro `isCompliant` dell'attributo viene impostato su `True` o `False` per indicare la compatibilità o la non compatibilità.  L'impostazione predefinita per questo parametro non è disponibile, è necessario quindi specificare un valore.  
  
 Se <xref:System.CLSCompliantAttribute> non viene applicato a un elemento, l'elemento non sarà considerato conforme.  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40028  
  
### Per correggere l'errore  
  
-   Se la routine deve accettare un parametro di questo particolare tipo, rimuovere <xref:System.CLSCompliantAttribute>.  La routine non può essere conforme a CLS.  
  
-   Se la routine deve essere conforme a CLS, sostituire il tipo di questo parametro con il tipo CLS conforme più simile.  Al posto di `UInteger` ad esempio potrebbe essere possibile utilizzare `Integer` se non è necessario l'intervallo di valore al di sopra di 2.147.483.647.  Se è necessario l'intervallo esteso, è possibile sostituire `UInteger` con `Long`.  
  
-   Se si prevede l'interazione con oggetti COM o di automazione, tenere presente che altri tipi presentano un'ampiezza di dati diversi da [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)].  `int`, ad esempio, in altri ambienti è spesso rappresentato con 16 bit.  Se si accetta un valore integer a 16 bit da un componente di questo tipo, è necessario eseguirne la dichiarazione come `Short` anziché come `Integer` nel codice [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] gestito.  
  
## Vedere anche  
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/it-it/4c705105-69a2-4e5e-b24e-0633bc32c7f3)