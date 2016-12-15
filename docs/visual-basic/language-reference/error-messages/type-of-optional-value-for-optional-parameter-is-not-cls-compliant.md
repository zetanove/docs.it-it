---
title: "Il tipo di valore facoltativo per il parametro &lt;nomeparametro&gt; facoltativo non &#232; conforme a CLS | Microsoft Docs"
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
  - "BC40042"
  - "vbc40042"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40042"
ms.assetid: 1d6eae29-4ad3-4434-bde4-a53b6051adf5
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Il tipo di valore facoltativo per il parametro &lt;nomeparametro&gt; facoltativo non &#232; conforme a CLS
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Una procedura è contrassegnata come `<CLSCompliant(True)>`, ma viene dichiarato un parametro [facoltativo](../../../visual-basic/language-reference/modifiers/optional.md) con valore predefinito di un tipo non conforme.  
  
 Affinché una procedura risulti compatibile con l'[indipendenza del linguaggio e i componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) (CLS), deve usare solo tipi conformi a CLS. Questo scenario si applica ai tipi dei parametri, al tipo restituito e ai tipi di tutte le variabili locali. Si applica anche ai valori predefiniti dei parametri facoltativi.  
  
 I tipi di dati di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] seguenti non sono compatibili con CLS:  
  
-   [Tipo di dati SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
-   [Tipo di dati UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
-   [Tipo di dati ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
-   [Tipo di dati UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 Quando l'attributo <xref:System.CLSCompliantAttribute> viene applicato a un elemento di programmazione, il parametro `isCompliant` dell'attributo viene impostato su `True` o `False` per indicare la conformità o la non conformità. L'impostazione predefinita per questo parametro non è disponibile, quindi è necessario specificare un valore.  
  
 Se a un elemento non viene applicato <xref:System.CLSCompliantAttribute>, l'elemento non sarà considerato conforme.  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configuring Warnings in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40042  
  
### <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Se il parametro facoltativo deve avere un valore predefinito di questo tipo specifico, rimuovere <xref:System.CLSCompliantAttribute>. La procedura non può essere compatibile con CLS.  
  
-   Se la procedura deve essere compatibile con CLS, modificare il tipo di questo valore predefinito impostandolo sul tipo con una compatibilità con CLS più vicina. Al posto di `UInteger` ad esempio può essere possibile usare `Integer` se non è necessario l'intervallo di valore al di sopra di 2.147.483.647. Se è necessario l'intervallo esteso, è possibile sostituire `UInteger` con `Long`.  
  
-   Se si prevede l'interazione con gli oggetti COM o di automazione, tenere presente che alcuni tipi hanno un'ampiezza di dati diversa da [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]. Ad esempio, `int` è spesso a 16 bit in altri ambienti. Se si accetta un valore integer a 16 bit da tale componente, dichiararlo come `Short` anziché `Integer` nel codice [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] gestito.  
  
## <a name="see-also"></a>Vedere anche  
 [\<PAVE OVER> Scrittura di codice conforme a CLS](http://msdn.microsoft.com/it-it/4c705105-69a2-4e5e-b24e-0633bc32c7f3)