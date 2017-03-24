---
title: "&quot;&lt;classname&gt;&quot; non è conforme a CLS perché l&quot;interfaccia &quot;&lt;interfacename&gt;&quot; viene implementata non è conforme a CLS | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc40029
- vbc40029
dev_langs:
- VB
helpviewer_keywords:
- BC40029
ms.assetid: 178452f3-5575-4da0-9d6c-53bcddb6a338
caps.latest.revision: 13
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
ms.openlocfilehash: 1e5c948ed5ddeaa2f8a8efd4aa83a2539cc862f3
ms.lasthandoff: 03/13/2017

---
# <a name="39ltclassnamegt39-is-not-cls-compliant-because-the-interface-39ltinterfacenamegt39-it-implements-is-not-cls-compliant"></a>'&lt;classname&gt;' non è conforme a CLS perché l'interfaccia '&lt;interfacename&gt;' viene implementata non è conforme a CLS
Una classe o interfaccia è contrassegnata come `<CLSCompliant(True)>` quando deriva da o implementa un tipo contrassegnato come `<CLSCompliant(False)>` o non è contrassegnata.  
  
 Per una classe o un'interfaccia è compatibile con il [indipendenza del linguaggio e componenti indipendenti dal linguaggio](https://msdn.microsoft.com/library/12a7a7h3) (CLS), la gerarchia di ereditarietà deve essere conforme. Ciò significa che ogni tipo da cui eredita, direttamente o indirettamente, deve essere conforme. Analogamente, se una classe implementa una o più interfacce, esse devono essere tutte conformi nelle relative gerarchie di ereditarietà.  
  
 Quando si applica il <xref:System.CLSCompliantAttribute>a un elemento di programmazione, impostare l'attributo `isCompliant` parametro al metodo `True` o `False` per indicare la conformità o la non conformità.</xref:System.CLSCompliantAttribute> L'impostazione predefinita per questo parametro non è disponibile, quindi è necessario specificare un valore.  
  
 Se non si applica il <xref:System.CLSCompliantAttribute>a un elemento, viene considerato come non conforme.</xref:System.CLSCompliantAttribute>  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configuring Warnings in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40029  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Se è necessaria la conformità a CLS, definire il tipo all'interno di uno schema di implementazione o una gerarchia di ereditarietà diversi.  
  
-   Se è necessario che questo tipo deve rimanere all'interno di schema di implementazione o gerarchia di ereditarietà corrente, rimuovere il <xref:System.CLSCompliantAttribute>dalla relativa definizione o contrassegnarlo come `<CLSCompliant(False)>`.</xref:System.CLSCompliantAttribute>  
  
## <a name="see-also"></a>Vedere anche  
 [\<PAVE su > la scrittura di codice conforme a CLS](http://msdn.microsoft.com/en-us/4c705105-69a2-4e5e-b24e-0633bc32c7f3)
