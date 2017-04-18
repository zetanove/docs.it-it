---
title: L&quot;operando &quot;AddressOf&quot; deve essere il nome di un metodo (senza parentesi) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30577
- bc30577
dev_langs:
- VB
helpviewer_keywords:
- BC30577
ms.assetid: c2c55640-5c61-4e66-97a4-4322020c6001
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
ms.openlocfilehash: 04103fe23ee55bb751d9604ef74614edeead8886
ms.lasthandoff: 03/13/2017

---
# <a name="39addressof39-operand-must-be-the-name-of-a-method-without-parentheses"></a>L'operando 'AddressOf' deve essere il nome di un metodo (senza parentesi)
L'operatore `AddressOf` crea un'istanza di delegato di routine che fa riferimento a una routine specifica. La sintassi è come indicato di seguito.  
  
 `AddressOf` `procedurename`  
  
 È stato inserito tra parentesi l'argomento che segue `AddressOf`, che tuttavia non sono necessarie.  
  
 **ID errore:** BC30577  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Rimuovere le parentesi che racchiudono l'argomento che segue `AddressOf`.  
  
2.  Assicurarsi che l'argomento è un nome di metodo.  
  
## <a name="see-also"></a>Vedere anche  
 [AddressOf (operatore)](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Delegati](../../../visual-basic/programming-guide/language-features/delegates/index.md)
