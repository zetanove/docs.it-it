---
title: Altre strutture di controllo (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- statements [Visual Basic], control flow
- control structures
ms.assetid: 24b811f7-98ba-40ec-8dd3-4d528cfa4574
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
ms.openlocfilehash: 639571b493037f26951bd8fbf140d7bce3244889
ms.lasthandoff: 03/13/2017

---
# <a name="other-control-structures-visual-basic"></a>Altre strutture di controllo (Visual Basic)
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce le strutture di controllo che consentono di eliminare una risorsa o ridurre il numero di volte in cui che è necessario ripetere un riferimento all'oggetto.  
  
## <a name="usingend-using-construction"></a>Utilizzo... Usando la costruzione di fine  
 Il `Using...End Using` costruzione definisce un blocco di istruzioni all'interno del quale utilizza una risorsa, ad esempio una connessione SQL. Facoltativamente è possibile acquisire la risorsa con il `Using` istruzione. Quando si esce dal `Using` blocco [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] Elimina automaticamente la risorsa in modo che sia disponibile per altro codice. La risorsa deve essere locale ed eliminabile. Per ulteriori informazioni, vedere [istruzione Using](../../../../visual-basic/language-reference/statements/using-statement.md).  
  
## <a name="withend-with-construction"></a>Con... Termina con la costruzione  
 Il `With...End With` costruzione consente di specificare un riferimento all'oggetto una sola volta e quindi eseguire una serie di istruzioni che accedono ai membri. Ciò consente di semplificare il codice e migliorare le prestazioni perché [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non è necessario ristabilire il riferimento per ogni istruzione che vi accede. Per ulteriori informazioni, vedere [con... Terminare con l'istruzione](../../../../visual-basic/language-reference/statements/with-end-with-statement.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di controllo](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [Strutture decisionali](../../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)   
 [Cicli (strutture)](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [Strutture di controllo annidate](../../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Istruzione using](../../../../visual-basic/language-reference/statements/using-statement.md)   
 [Istruzione With...End With](../../../../visual-basic/language-reference/statements/with-end-with-statement.md)
