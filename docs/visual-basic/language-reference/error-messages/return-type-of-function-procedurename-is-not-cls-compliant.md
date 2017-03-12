---
title: "Return type of function &#39;&lt;procedurename&gt;&#39; is not CLS-compliant | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc40027"
  - "vbc40027"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40027"
ms.assetid: 33c088c7-48e7-400c-920e-6d8967e1f3fc
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# Return type of function &#39;&lt;procedurename&gt;&#39; is not CLS-compliant
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una routine `Function` viene contrassegnata come `<CLSCompliant(True)>`, ma restituisce un tipo che è contrassegnato come `<CLSCompliant(False)>`, non è contrassegnato o non può essere utilizzato in quanto tipo non conforme.  
  
 Per rendere conforme una routine con [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\), è necessario utilizzare solo tipi CLS conformi.  Questa regola è valida per i tipi dei parametri, il tipo restituito e i tipi di tutte le relative variabili locali.  
  
 I seguenti tipi di dati [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] non sono conformi a CLS:  
  
-   [SByte Data Type](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
-   [UInteger Data Type](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
-   [ULong Data Type](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
-   [UShort Data Type](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 Quando si applica l'<xref:System.CLSCompliantAttribute> a un elemento di programmazione, il parametro `isCompliant` dell'attributo viene impostato su `True` o `False` per indicare la compatibilità o la non compatibilità.  L'impostazione predefinita per questo parametro non è disponibile, è necessario quindi specificare un valore.  
  
 Se <xref:System.CLSCompliantAttribute> non viene applicato a un elemento, l'elemento non sarà considerato conforme.  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40027  
  
### Per correggere l'errore  
  
-   Se è necessario che la routine `Function` restituisca questo tipo particolare, rimuovere <xref:System.CLSCompliantAttribute>.  La routine non può essere conforme a CLS.  
  
-   Per rendere la routine `Function` conforme a CLS, modificare il tipo di restituzione nel tipo conforme più vicino.  Al posto di `UInteger` ad esempio potrebbe essere possibile utilizzare `Integer` se non è necessario l'intervallo di valore al di sopra di 2.147.483.647.  Se è necessario l'intervallo esteso, è possibile sostituire `UInteger` con `Long`.  
  
-   Se si prevede l'interazione con oggetti COM o di automazione, tenere presente che altri tipi presentano un'ampiezza di dati diversi da [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)].  `int`, ad esempio, in altri ambienti è spesso rappresentato con 16 bit.  Se viene restituito un valore integer di 16 bit a un componente di questo tipo, è necessario eseguirne la dichiarazione come `Short` anziché come `Integer` nel codice gestito [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
## Vedere anche  
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/it-it/4c705105-69a2-4e5e-b24e-0633bc32c7f3)