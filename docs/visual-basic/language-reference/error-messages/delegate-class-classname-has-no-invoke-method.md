---
title: "Classe delegata&lt;classname&gt;&quot; dispone di alcun metodo Invoke, in modo da un&quot;espressione di questo tipo non può essere la destinazione di una chiamata al metodo | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30220
- bc30220
dev_langs:
- VB
helpviewer_keywords:
- BC30220
ms.assetid: 6be0d61c-f2f9-4f9b-ab90-8871a0d7206d
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
ms.openlocfilehash: ddc5ef0f0b3e9baa58f17dafb727e250c0fba9fd
ms.lasthandoff: 03/13/2017

---
# <a name="delegate-class-39ltclassnamegt39-has-no-invoke-method-so-an-expression-of-this-type-cannot-be-the-target-of-a-method-call"></a>Classe delegata&lt;classname&gt;' dispone di alcun metodo Invoke, in modo da un'espressione di questo tipo non può essere la destinazione di una chiamata al metodo
Una chiamata a `Invoke` tramite un delegato non è riuscito perché `Invoke` non è implementata nella classe delegata.  
  
 **ID errore:** BC30220  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Assicurarsi che sia stata creata un'istanza della classe delegato con un `Dim` istruzione e che sia stata assegnata una routine per l'istanza del delegato con il `AddressOf` operatore.  
  
2.  Individuare il codice che implementa la classe delegata e controllare che implementi la `Invoke` procedura.  
  
## <a name="see-also"></a>Vedere anche  
 [Delegati](../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [Delegate (istruzione)](../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [AddressOf (operatore)](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Istruzione Dim](../../../visual-basic/language-reference/statements/dim-statement.md)
