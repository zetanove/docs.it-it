---
title: "La prima istruzione di questo &quot;Sub New&quot; deve essere una chiamata esplicita a &quot;MyClass. New&quot; o &quot;MyBase. New&quot; perché il &quot;&lt;constructorname&gt;&quot;nella classe di base&quot;&lt;baseclassname&gt;&quot;di&quot;&lt;derivedclassname&gt;&quot; è contrassegnato come obsoleto: &quot;&lt;errormessage&gt;&quot; | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30920
- bc30920
dev_langs:
- VB
helpviewer_keywords:
- BC30920
ms.assetid: e47dc755-4294-4368-b813-2177b7677957
caps.latest.revision: 10
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
ms.openlocfilehash: feb04d426b7e050b7ad05cdfd4d481172dda3a49
ms.lasthandoff: 03/13/2017

---
# <a name="first-statement-of-this-39sub-new39-must-be-an-explicit-call-to-39mybasenew39-or-39myclassnew39-because-the-39ltconstructornamegt39-in-the-base-class-39ltbaseclassnamegt39-of-39ltderivedclassnamegt39-is-marked-obsolete-39lterrormessagegt39"></a>La prima istruzione di questo 'Sub New' deve essere una chiamata esplicita a 'MyClass. New' o 'MyBase. New' perché il '&lt;constructorname&gt;'nella classe di base'&lt;baseclassname&gt;'di'&lt;derivedclassname&gt;' è contrassegnato come obsoleto: '&lt;errormessage&gt;'
Un costruttore di classe non chiama in modo esplicito un costruttore di classe di base e il costruttore della classe base implicito è contrassegnato con il <xref:System.ObsoleteAttribute>attributo e la direttiva di considerarla come un errore.</xref:System.ObsoleteAttribute>  
  
 Quando un costruttore di classe derivata non chiama un costruttore di classe base, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tenta di generare una chiamata implicita a un costruttore senza parametri della classe base. Se non vi è alcun costruttore accessibile nella classe di base che può essere chiamata senza argomenti, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non può generare una chiamata implicita. In questo caso, il costruttore richiesto è contrassegnato con il <xref:System.ObsoleteAttribute>attributo, operazione [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non può chiamare tale</xref:System.ObsoleteAttribute>  
  
 È possibile contrassegnare gli elementi di programmazione come non più in uso, applicando <xref:System.ObsoleteAttribute>a tale</xref:System.ObsoleteAttribute> In questo caso, è possibile impostare l'attributo <xref:System.ObsoleteAttribute.IsError%2A>a una proprietà `True` o `False`.</xref:System.ObsoleteAttribute.IsError%2A> Se si imposta la proprietà su `True`, il compilatore considera il tentativo di usare l'elemento come un errore. Se si imposta la proprietà su `False`, o si lascia l'impostazione predefinita `False`, il compilatore genera un avviso se si prova a usare l'elemento.  
  
 **ID errore:** BC30920  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Esaminare il messaggio di errore tra virgolette e intraprendere l'azione appropriata.  
  
2.  Includere una chiamata a `MyBase.New()` o `MyClass.New()` come prima istruzione di `Sub New` nella classe derivata.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica degli attributi](../../../visual-basic/programming-guide/concepts/attributes/index.md)
 
