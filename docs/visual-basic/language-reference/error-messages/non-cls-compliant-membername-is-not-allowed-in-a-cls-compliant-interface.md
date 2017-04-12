---
title: "Non conforme a CLS &lt;membername&gt; non è consentita in un&quot;interfaccia conforme a CLS | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc40033
- vbc40033
dev_langs:
- VB
helpviewer_keywords:
- BC40033
ms.assetid: 060c4b08-798e-40f1-94cf-c05c524f1b8a
caps.latest.revision: 9
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 2861ef22c9307e5bd7d2eabf4f6e37bbd9086345
ms.lasthandoff: 03/13/2017

---
# <a name="non-cls-compliant-ltmembernamegt-is-not-allowed-in-a-cls-compliant-interface"></a>Non conforme a CLS &lt;membername&gt; non è consentita in un'interfaccia conforme a CLS
Una proprietà, una routine o un evento in un'interfaccia è contrassegnata come `<CLSCompliant(True)>` quando l'interfaccia stessa è contrassegnato come `<CLSCompliant(False)>` o non è contrassegnata.  
  
 Per un'interfaccia deve essere compatibile con il [indipendenza del linguaggio e componenti indipendenti dal linguaggio](https://msdn.microsoft.com/library/12a7a7h3) (CLS), tutti i relativi membri devono essere conformi.  
  
 Quando si applica il <xref:System.CLSCompliantAttribute>a un elemento di programmazione, impostare l'attributo `isCompliant` parametro al metodo `True` o `False` per indicare la conformità o la non conformità.</xref:System.CLSCompliantAttribute> L'impostazione predefinita per questo parametro non è disponibile, quindi è necessario specificare un valore.  
  
 Se non si applica il <xref:System.CLSCompliantAttribute>a un elemento, viene considerato come non conforme.</xref:System.CLSCompliantAttribute>  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configuring Warnings in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40033  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Se è necessaria la conformità a CLS ed è possibile il codice sorgente dell'interfaccia, contrassegnare l'interfaccia come `<CLSCompliant(True)>` se tutti i relativi membri sono conformi.  
  
-   Se si richiedono la conformità a CLS e non è possibile controllare il codice sorgente dell'interfaccia oppure non qualifica essere conforme, definire il membro all'interno di un'interfaccia diversa.  
  
-   Se è necessario mantenere il membro nell'interfaccia corrente, rimuovere il <xref:System.CLSCompliantAttribute>dalla relativa definizione o contrassegnarlo come `<CLSCompliant(False)>`.</xref:System.CLSCompliantAttribute>  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione Interface](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [\<PAVE su > la scrittura di codice conforme a CLS](http://msdn.microsoft.com/en-us/4c705105-69a2-4e5e-b24e-0633bc32c7f3)
