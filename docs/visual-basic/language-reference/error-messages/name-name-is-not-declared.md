---
title: "Nome &quot;&lt;nome&gt;&quot; non è dichiarato | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30451
- vbc30451
dev_langs:
- VB
helpviewer_keywords:
- BC30451
ms.assetid: 765f099b-e21e-47c6-a906-a065444e56b3
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
ms.openlocfilehash: 81b6862a7f8ceb7998b2ea53336ed3af46b1db5f
ms.lasthandoff: 03/13/2017

---
# <a name="name-39ltnamegt39-is-not-declared"></a>Nome '&lt;nome&gt;' non è dichiarato
Un'istruzione fa riferimento a un elemento di programmazione, ma il compilatore non trova un elemento con il nome esatto.  
  
 **ID errore:** BC30451  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Controllare l'ortografia del nome nell'istruzione di riferimento. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]tra maiuscole e minuscole, ma qualsiasi altra variazione nell'ortografia verrà considerata come un nome completamente diverso. Si noti che il carattere di sottolineatura (`_`) fa parte del nome e quindi dell'ortografia.  
  
2.  Verificare di disporre l'operatore di accesso ai membri (`.`) tra un oggetto e il relativo membro. Ad esempio, se si dispone di un <xref:System.Windows.Forms.TextBox>controllo denominato `TextBox1`, per accedere ai relativi <xref:System.Windows.Forms.TextBoxBase.Text%2A>proprietà è necessario digitare `TextBox1.Text`.</xref:System.Windows.Forms.TextBoxBase.Text%2A> </xref:System.Windows.Forms.TextBox> Se invece si digita `TextBox1Text`, viene creato un nome diverso.  
  
3.  Se l'ortografia e la sintassi di accesso ai membri qualsiasi oggetto sia corretta, verificare che l'elemento è stato dichiarato. Per ulteriori informazioni, vedere [gli elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/index.md).  
  
4.  Se l'elemento di programmazione è stata dichiarata, controllare che si trova nell'ambito. Se l'istruzione di riferimento è all'esterno dell'area di dichiarazione di elemento di programmazione, potrebbe essere necessario qualificare il nome dell'elemento. Per ulteriori informazioni, vedere [ambito in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/scope.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Riepilogo delle dichiarazioni e costanti](../../../visual-basic/language-reference/keywords/declarations-and-constants-summary.md)   
 [Convenzioni di denominazione di Visual Basic](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)   
 [Nomi elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [Riferimenti a elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
