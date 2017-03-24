---
title: "Tipo di membro &quot;&lt;membername&gt;&quot; non è conforme a CLS | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc40025
- vbc40025
dev_langs:
- VB
helpviewer_keywords:
- BC40025
ms.assetid: adbd34bb-43d2-4266-90e7-cd1afaf49b4e
caps.latest.revision: 14
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
ms.openlocfilehash: 3ea35f54cf8f0fb5a11148b8017456feb8d3524a
ms.lasthandoff: 03/13/2017

---
# <a name="type-of-member-39ltmembernamegt39-is-not-cls-compliant"></a>Tipo di membro '&lt;membername&gt;' non è conforme a CLS
Il tipo di dati specificato per questo membro non è in parte il [indipendenza del linguaggio e componenti indipendenti dal linguaggio](https://msdn.microsoft.com/library/12a7a7h3) (CLS). Non si tratta di un errore all'interno del componente, poiché il [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] e [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] supporta questo tipo di dati. Tuttavia, un altro componente scritto in codice strettamente conforme a CLS potrebbe non supportare questo tipo di dati. Tale componente potrebbe non essere in grado di interagire correttamente con il componente.  
  
 I tipi di dati di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] seguenti non sono compatibili con CLS:  
  
-   [Tipo di dati SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
-   [Tipo di dati UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
-   [Tipo di dati ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
-   [Tipo di dati UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [configurazione degli avvisi in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40025  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Se il componente interagisce solo con altri [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] componenti o non si interfaccia con altri componenti, non occorre apportare alcuna modifica.  
  
-   Se si prevede l'interazione con un componente non scritto per il [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)], potrebbe essere in grado di determinare, tramite reflection o dalla documentazione, se supporta questo tipo di dati. In questo caso, non occorre apportare alcuna modifica.  
  
-   Se si prevede l'interazione con un componente che non supporta questo tipo di dati, è necessario sostituirlo con il tipo più conforme a CLS. Al posto di `UInteger` ad esempio può essere possibile usare `Integer` se non è necessario l'intervallo di valore al di sopra di 2.147.483.647. Se è necessario l'intervallo esteso, è possibile sostituire `UInteger` con `Long`.  
  
-   Se si prevede l'interazione con gli oggetti COM o di automazione, tenere presente che alcuni tipi hanno un'ampiezza di dati diversa da [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]. Ad esempio, `uint` è spesso a 16 bit in altri ambienti. Se si passa un argomento a 16 bit a tale componente, dichiararla come `UShort` invece di `UInteger` in gestito [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] codice.  
  
## <a name="see-also"></a>Vedere anche  
 [Reflection](http://msdn.microsoft.com/library/d1a58e7f-fb39-4d50-bf84-e3b8f9bf9775)   
 [\<PAVE su > la scrittura di codice conforme a CLS](http://msdn.microsoft.com/en-us/4c705105-69a2-4e5e-b24e-0633bc32c7f3)
