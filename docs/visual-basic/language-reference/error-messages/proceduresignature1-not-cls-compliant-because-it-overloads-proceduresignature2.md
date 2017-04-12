---
title: "&lt;proceduresignature1&gt; non è conforme a CLS perché esegue l&quot;overload &lt;proceduresignature2&gt; che differisce da esso solo per matrice di tipi di parametro matrice o per la classificazione dei tipi di parametro matrice | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc40035
- bc40035
dev_langs:
- VB
helpviewer_keywords:
- BC40035
ms.assetid: 50a66dbe-2c1e-41bf-96bc-369301c891ac
caps.latest.revision: 11
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
ms.openlocfilehash: 984c04a107444036b980439b231d27a8a81656c1
ms.lasthandoff: 03/13/2017

---
# <a name="ltproceduresignature1gt-is-not-cls-compliant-because-it-overloads-ltproceduresignature2gt-which-differs-from-it-only-by-array-of-array-parameter-types-or-by-the-rank-of-the-array-parameter-types"></a>&lt;proceduresignature1&gt; non è conforme a CLS perché esegue l'overload &lt;proceduresignature2&gt; che differisce da esso solo per matrice di tipi di parametro matrice o per la classificazione dei tipi di parametro matrice
Una routine o proprietà è contrassegnata come `<CLSCompliant(True)>` quando esegue l'override di un'altra routine o una proprietà e l'unica differenza tra gli elenchi dei parametri è il livello di nidificazione di una matrice di matrici o il rango di una matrice.  
  
 Nel seguente elenco, le dichiarazioni di seconda e terza generano questo errore.  
  
 `Overloads Sub processArray(ByVal arrayParam() As Integer)`  
  
 `Overloads Sub processArray(ByVal arrayParam()() As Integer)`  
  
 `Overloads Sub processArray(ByVal arrayParam(,) As Integer)`  
  
 La seconda dichiarazione modifica il parametro unidimensionale originario `arrayParam` a una matrice di matrici. La terza dichiarazione modifica `arrayParam` a una matrice bidimensionale (2 dimensioni). Visual Basic consente di overload per differiscano solo una di queste modifiche, questo tipo di overload non è conforme con la [indipendenza del linguaggio e componenti indipendenti dal linguaggio](https://msdn.microsoft.com/library/12a7a7h3) (CLS).  
  
 Quando si applica il <xref:System.CLSCompliantAttribute>a un elemento di programmazione, impostare l'attributo `isCompliant` parametro al metodo `True` o `False` per indicare la conformità o la non conformità.</xref:System.CLSCompliantAttribute> L'impostazione predefinita per questo parametro non è disponibile, quindi è necessario specificare un valore.  
  
 Se non si applica il <xref:System.CLSCompliantAttribute>a un elemento, viene considerato come non conforme.</xref:System.CLSCompliantAttribute>  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configuring Warnings in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40035  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Se è necessaria la conformità a CLS, definire overload per differenziarsi in più modi rispetto a quelle elencate in questa pagina della Guida in linea.  
  
-   Se è necessario che gli overload differiscono solo per le modifiche citate in questa Guida di pagina, rimuovere il <xref:System.CLSCompliantAttribute>dalle definizioni o contrassegnarli come `<CLSCompliant(False)>`.</xref:System.CLSCompliantAttribute>  
  
## <a name="see-also"></a>Vedere anche  
 [\<PAVE su > la scrittura di codice conforme a CLS](http://msdn.microsoft.com/en-us/4c705105-69a2-4e5e-b24e-0633bc32c7f3)   
 [Overload di routine](../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Overload](../../../visual-basic/language-reference/modifiers/overloads.md)
