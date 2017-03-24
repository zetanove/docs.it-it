---
title: "Tipo di parametro &quot;&lt;parametername&gt;&quot; non è conforme a CLS | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc40028
- bc40028
dev_langs:
- VB
helpviewer_keywords:
- BC40028
ms.assetid: dfa1f6f9-bb88-44ad-b85f-149144363d41
caps.latest.revision: 11
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 75891a7268489b69e8d0c1bf91570a67fc004c6b
ms.lasthandoff: 03/13/2017

---
# <a name="type-of-parameter-39ltparameternamegt39-is-not-cls-compliant"></a>Tipo di parametro '&lt;parametername&gt;' non è conforme a CLS
Una routine è contrassegnata come `<CLSCompliant(True)>` ma dichiara un parametro con un tipo che è contrassegnato come `<CLSCompliant(False)>`, non è contrassegnato come oppure non qualifica perché si tratta di un tipo non conforme.  
  
 Affinché una procedura risulti compatibile con l'[indipendenza del linguaggio e i componenti indipendenti dal linguaggio](https://msdn.microsoft.com/library/12a7a7h3) (CLS), deve usare solo tipi conformi a CLS. Questo scenario si applica ai tipi dei parametri, al tipo restituito e ai tipi di tutte le variabili locali.  
  
 I tipi di dati di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] seguenti non sono compatibili con CLS:  
  
-   [Tipo di dati SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
-   [Tipo di dati UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
-   [Tipo di dati ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
-   [Tipo di dati UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 Quando si applica il <xref:System.CLSCompliantAttribute>a un elemento di programmazione, impostare l'attributo `isCompliant` parametro al metodo `True` o `False` per indicare la conformità o la non conformità.</xref:System.CLSCompliantAttribute> L'impostazione predefinita per questo parametro non è disponibile, quindi è necessario specificare un valore.  
  
 Se non si applica il <xref:System.CLSCompliantAttribute>a un elemento, viene considerato come non conforme.</xref:System.CLSCompliantAttribute>  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configuring Warnings in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40028  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Se la routine deve accettare un parametro di tipo particolare, rimuovere il <xref:System.CLSCompliantAttribute>.</xref:System.CLSCompliantAttribute> La procedura non può essere compatibile con CLS.  
  
-   Se la procedura deve essere conforme a CLS, modificare il tipo di questo parametro per il tipo conforme a CLS più vicino. Al posto di `UInteger` ad esempio può essere possibile usare `Integer` se non è necessario l'intervallo di valore al di sopra di 2.147.483.647. Se è necessario l'intervallo esteso, è possibile sostituire `UInteger` con `Long`.  
  
-   Se si prevede l'interazione con gli oggetti COM o di automazione, tenere presente che alcuni tipi hanno un'ampiezza di dati diversa da [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]. Ad esempio, `int` è spesso a 16 bit in altri ambienti. Se si accetta un valore integer a 16 bit da tale componente, dichiararlo come `Short` anziché `Integer` nel codice [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] gestito.  
  
## <a name="see-also"></a>Vedere anche  
 [\<PAVE su > la scrittura di codice conforme a CLS](http://msdn.microsoft.com/en-us/4c705105-69a2-4e5e-b24e-0633bc32c7f3)
