---
title: Clausola Handles (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- Handles
- vb.Handles
dev_langs:
- VB
helpviewer_keywords:
- Handles keyword
ms.assetid: 1b051c0e-f499-42f6-acb5-6f4f27824b40
caps.latest.revision: 19
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
ms.openlocfilehash: 7c79935e7f15f31abca7efddbc443239d5db2f58
ms.lasthandoff: 03/13/2017

---
# <a name="handles-clause-visual-basic"></a>Clausola Handles (Visual Basic)
Dichiara che una routine gestisce un evento specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
proceduredeclaration Handles eventlist  
```  
  
## <a name="parts"></a>Parti  
 `proceduredeclaration`  
 Dichiarazione `Sub` per la routine che gestirà l'evento.  
  
 `eventlist`  
 Elenco degli eventi che devono essere gestiti da `proceduredeclaration`. Gli eventi devono essere generati dalla classe base per la classe corrente o da un oggetto dichiarato usando la parola chiave `WithEvents`.  
  
## <a name="remarks"></a>Note  
 Usare la parola chiave `Handles` alla fine di una dichiarazione di routine per fare in modo che la routine gestisca eventi generati da una variabile oggetto dichiarata con la parola chiave `WithEvents` . La parola chiave `Handles` può anche essere usata in una classe derivata per gestire eventi da una classe base.  
  
 La parola chiave `Handles` e l'istruzione `AddHandler` consentono entrambe di specificare che quelle particolari routine gestiscono particolari eventi, ma esistono alcune differenze. Usare la parola chiave `Handles` quando si definisce una routine, per specificare che questa gestisce un particolare evento. L'istruzione `AddHandler` connette le routine agli eventi in fase di esecuzione. Per ulteriori informazioni, vedere [AddHandler (istruzione)](../../../visual-basic/language-reference/statements/addhandler-statement.md).  
  
 Per gli eventi personalizzati, l'applicazione richiama la funzione di accesso `AddHandler` dell'evento quando aggiunge la routine come gestore eventi. Per ulteriori informazioni sugli eventi personalizzati, vedere [istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md).  
  
## <a name="example"></a>Esempio  
 [!code-vb[VbVbalrEvents n.&2;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/handles-clause_1.vb)]  
  
 L'esempio seguente illustra come una classe derivata può usare l'istruzione `Handles` per gestire un evento da una classe base.  
  
 [!code-vb[VbVbalrEvents n.&3;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/handles-clause_2.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente contiene due gestori eventi del pulsante per un **applicazione WPF** project.  
  
 [!code-vb[VbVbalrEvents n.&41;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/handles-clause_3.vb)]  
  
## <a name="example"></a>Esempio  
 L'esempio che segue equivale a quello precedente. L'oggetto `eventlist` nella clausola `Handles` contiene gli eventi per entrambi i pulsanti.  
  
 [!code-vb[VbVbalrEvents&#42;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/handles-clause_4.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [WithEvents](../../../visual-basic/language-reference/modifiers/withevents.md)   
 [AddHandler (istruzione)](../../../visual-basic/language-reference/statements/addhandler-statement.md)   
 [RemoveHandler (istruzione)](../../../visual-basic/language-reference/statements/removehandler-statement.md)   
 [Istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md)   
 [RaiseEvent (istruzione)](../../../visual-basic/language-reference/statements/raiseevent-statement.md)   
 [Eventi](../../../visual-basic/programming-guide/language-features/events/index.md)
