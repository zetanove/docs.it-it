---
title: Operatore AddressOf (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- AddressOf
- vb.AddressOf
dev_langs:
- VB
helpviewer_keywords:
- AddressOf operator
- addresses, passing to API procedures
ms.assetid: 8105a59d-60d8-4ab5-b221-5899cdfacbf4
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
ms.openlocfilehash: 04a7c5be9b890faea561c28715093a271cf9eaa8
ms.lasthandoff: 03/13/2017

---
# <a name="addressof-operator-visual-basic"></a>Operatore AddressOf (Visual Basic)
Crea un'istanza del delegato procedure che fa riferimento la procedura specifica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
AddressOf procedurename  
```  
  
## <a name="parts"></a>Parti  
 `procedurename`  
 Obbligatorio. Specifica la procedura per fare riferimento il delegato appena creato.  
  
## <a name="remarks"></a>Note  
 Il `AddressOf` operatore crea un delegato della funzione che fa riferimento alla funzione specificata da `procedurename`. Quando la procedura specificata è che un metodo di istanza quindi delegato della funzione fa riferimento l'istanza sia il metodo. Quindi, quando viene richiamato il delegato della funzione viene chiamato il metodo specificato dell'istanza specificata.  
  
 Il `AddressOf` operatore può essere utilizzato come operando di un costruttore di delegato o può essere utilizzato in un contesto in cui il tipo del delegato può essere determinato dal compilatore.  
  
## <a name="example"></a>Esempio  
 Questo esempio viene utilizzato il `AddressOf` operatore per designare un delegato per gestire il `Click` evento di un pulsante.  
  
 [!code-vb[VbVbalrDelegates n.&8;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addressof-operator_1.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la `AddressOf` operatore per specificare la funzione di avvio per un thread.  
  
 [!code-vb[9 VbVbalrDelegates](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addressof-operator_2.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Declare (istruzione)](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub (istruzione)](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Delegati](../../../visual-basic/programming-guide/language-features/delegates/index.md)
