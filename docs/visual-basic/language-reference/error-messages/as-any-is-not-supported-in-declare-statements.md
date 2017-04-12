---
title: '&quot;As Any&quot; non supportato nelle istruzioni &quot;Declare&quot; | Documenti di Microsoft'
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30828
- vbc30828
dev_langs:
- VB
helpviewer_keywords:
- BC30828
ms.assetid: 7e5cf519-8b64-4ac5-8116-705fe26c846d
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
ms.openlocfilehash: fb179ae938d4c132f61e2076248729f7ea15a13f
ms.lasthandoff: 03/13/2017

---
# <a name="39as-any39-is-not-supported-in-39declare39-statements"></a>'As Any' non supportato nelle istruzioni 'Declare'
Il `Any` tipo di dati è stato utilizzato con `Declare` istruzioni in Visual Basic 6.0 e versioni precedenti per consentire l'utilizzo di argomenti che può contenere qualsiasi tipo di dati. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]supporta l'overload, tuttavia e consente pertanto di `Any` obsoleto del tipo di dati.  
  
 **ID errore:** BC30828  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Dichiarare i parametri del tipo specifico di cui che si desidera utilizzare. Per esempio.  
  
     [!code-vb[&#95; VbVbalrStatements](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/as-any-is-not-supported-in-declare-statements_1.vb)]  
  
2.  Utilizzare il <xref:System.Runtime.InteropServices.MarshalAsAttribute>attributo per specificare `As Any` quando `Void*` prevede la routine chiamata.</xref:System.Runtime.InteropServices.MarshalAsAttribute>  
  
     [!code-vb[&#96; VbVbalrStatements](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/as-any-is-not-supported-in-declare-statements_2.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute></xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Procedura dettagliata: Chiamata delle API di Windows](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)   
 [Declare (istruzione)](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Creazione di prototipi nel codice gestito](http://msdn.microsoft.com/library/ecdcf25d-cae3-4f07-a2b6-8397ac6dc42d)
