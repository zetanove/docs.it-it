---
title: WithEvents (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.WithEvents
- WithEvents
dev_langs:
- VB
helpviewer_keywords:
- WithEvents keyword
ms.assetid: 19d461f5-d72f-4de9-8c1d-0a6650316990
caps.latest.revision: 17
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
ms.openlocfilehash: 708cf6fec78faf2c7a5959a3a2694d237d728882
ms.lasthandoff: 03/13/2017

---
# <a name="withevents-visual-basic"></a>WithEvents (Visual Basic)
Specifica che una o più variabili membro dichiarato fare riferimento a un'istanza di una classe che può generare eventi.  
  
## <a name="remarks"></a>Note  
 Quando una variabile viene definita mediante `WithEvents`, è possibile specificare in modo dichiarativo che un metodo gestisce gli eventi della variabile usando il `Handles` (parola chiave).  
  
 È possibile utilizzare `WithEvents` solo a livello di classe o modulo. Ciò significa che il contesto della dichiarazione per un `WithEvents` variabile deve essere una classe o modulo e non può essere un file di origine, lo spazio dei nomi, struttura o routine.  
  
 Non è possibile utilizzare `WithEvents` su un membro della struttura.  
  
 È possibile dichiarare solo variabili singole, ovvero non matrici, con `WithEvents`.  
  
## <a name="rules"></a>Regole  
  
-   **Tipi di elemento.** È necessario dichiarare `WithEvents` le variabili come variabili oggetto in modo che accettino le istanze di classe. Tuttavia, è possibile dichiarare le variabili come `Object`. È necessario dichiararle come la classe specifica in grado di generare eventi.  
  
 Il `WithEvents` modificatore può essere utilizzato in questo contesto: [Dim (istruzione)](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Handle](../../../visual-basic/language-reference/statements/handles-clause.md)   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)   
 [Eventi](../../../visual-basic/programming-guide/language-features/events/index.md)
