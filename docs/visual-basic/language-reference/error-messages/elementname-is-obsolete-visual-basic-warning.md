---
title: "&quot;&lt;elementname&gt;&quot; è obsoleto (avviso di Visual Basic) | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc40008
- bc40008
dev_langs:
- VB
helpviewer_keywords:
- BC40008
ms.assetid: 729e3eb5-76ac-4c55-9fdd-78350e0de55e
caps.latest.revision: 12
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
ms.openlocfilehash: ccec3b2659502c84dd4db9c9c4d796362958030b
ms.lasthandoff: 03/13/2017

---
# <a name="39ltelementnamegt39-is-obsolete-visual-basic-warning"></a>'&lt;elementname&gt;' è obsoleto (avviso di Visual Basic)
Un'istruzione tenta di accedere a un elemento di programmazione che è stato contrassegnato con il <xref:System.ObsoleteAttribute>attributo e la direttiva di considerarla come un avviso.</xref:System.ObsoleteAttribute>  
  
 È possibile contrassegnare gli elementi di programmazione come non più in uso, applicando <xref:System.ObsoleteAttribute>a tale</xref:System.ObsoleteAttribute> In questo caso, è possibile impostare l'attributo <xref:System.ObsoleteAttribute.IsError%2A>a una proprietà `True` o `False`.</xref:System.ObsoleteAttribute.IsError%2A> Se si imposta la proprietà su `True`, il compilatore considera il tentativo di usare l'elemento come un errore. Se si imposta la proprietà su `False`, o si lascia l'impostazione predefinita `False`, il compilatore genera un avviso se si prova a usare l'elemento.  
  
 Per impostazione predefinita, questo messaggio è un avviso, poiché il <xref:System.ObsoleteAttribute.IsError%2A>proprietà <xref:System.ObsoleteAttribute>è `False`.</xref:System.ObsoleteAttribute> </xref:System.ObsoleteAttribute.IsError%2A> Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [configurazione degli avvisi in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40008  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Verificare che nel riferimento del codice sorgente il nome dell'elemento sia stato digitato correttamente.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica degli attributi](../../../visual-basic/programming-guide/concepts/attributes/index.md)

