---
title: "Nome &lt;NomeSpazioDeiNomi&gt; nello spazio dei nomi radice &lt;fullnamespacename&gt; non è conforme a CLS | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc40039
- bc40039
dev_langs:
- VB
helpviewer_keywords:
- BC40039
ms.assetid: c5bd5914-ae71-416a-8bed-f76f644f78be
caps.latest.revision: 10
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
ms.openlocfilehash: 344a0ca098160a8d9f5bc8281a941311f82000c4
ms.lasthandoff: 03/13/2017

---
# <a name="name-ltnamespacenamegt-in-the-root-namespace-ltfullnamespacenamegt-is-not-cls-compliant"></a>Nome &lt;NomeSpazioDeiNomi&gt; nello spazio dei nomi radice &lt;fullnamespacename&gt; non è conforme a CLS
Un assembly è contrassegnato come `<CLSCompliant(True)>`, ma un elemento del nome dello spazio dei nomi principale inizia con un carattere di sottolineatura (`_`).  
  
 Un elemento di programmazione può contenere uno o più caratteri di sottolineatura, ma to deve essere compatibile con il [indipendenza del linguaggio e componenti indipendenti dal linguaggio](https://msdn.microsoft.com/library/12a7a7h3) (CLS), non può iniziare con un carattere di sottolineatura. Vedere [dichiarati i nomi degli elementi](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
 Quando si applica il <xref:System.CLSCompliantAttribute>a un elemento di programmazione, impostare l'attributo `isCompliant` parametro al metodo `True` o `False` per indicare la conformità o la non conformità.</xref:System.CLSCompliantAttribute> L'impostazione predefinita per questo parametro non è disponibile, quindi è necessario specificare un valore.  
  
 Se non si applica il <xref:System.CLSCompliantAttribute>a un elemento, viene considerato come non conforme.</xref:System.CLSCompliantAttribute>  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configuring Warnings in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40039  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Se è necessaria la conformità a CLS, modificare il nome dello spazio dei nomi radice in modo che nessuno dei suoi elementi inizi con un carattere di sottolineatura.  
  
-   Se è necessario che il nome dello spazio dei nomi deve rimanere invariato, quindi rimuovere il <xref:System.CLSCompliantAttribute>dall'assembly o contrassegnarlo come `<CLSCompliant(False)>`.</xref:System.CLSCompliantAttribute>  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione Namespace](../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [/RootNamespace](../../../visual-basic/reference/command-line-compiler/rootnamespace.md)   
 [Application Page, Project Designer (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-visual-basic)  (Pagina Applicazione, Creazione progetti (Visual Basic))  
 [Nomi elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [Convenzioni di denominazione di Visual Basic](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)   
 [\<PAVE su > la scrittura di codice conforme a CLS](http://msdn.microsoft.com/en-us/4c705105-69a2-4e5e-b24e-0633bc32c7f3)
