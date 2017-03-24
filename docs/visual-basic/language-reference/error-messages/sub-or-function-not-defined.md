---
title: Sub o Function non definita (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrID35
dev_langs:
- VB
ms.assetid: 661fdb90-ee7d-40ce-b30b-5e7267bd957a
caps.latest.revision: 12
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
ms.openlocfilehash: 7d32bc9c8f13b245e6333c4460cab541f6e9409e
ms.lasthandoff: 03/13/2017

---
# <a name="sub-or-function-not-defined-visual-basic"></a>Sub o Function non definita (Visual Basic)
Oggetto `Sub` o `Function` deve essere definito per essere chiamati. Alcune cause possibili di questo errore sono:  
  
-   Errore di ortografia il nome della routine.  
  
-   Tentativo di chiamare una routine da un altro progetto senza aggiungere in modo esplicito un riferimento a tale progetto nel **riferimenti** la finestra di dialogo.  
  
-   Specifica una routine che non è visibile alla routine chiamante.  
  
-   Dichiarazione di una routine di libreria a collegamento dinamico (DLL) di Windows o di una routine di risorsa di codice Macintosh che non si trova la risorsa di libreria o di codice specificata.  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Assicurarsi che il nome della routine sia digitato correttamente.  
  
2.  Individuare il nome del progetto contenente la routine da chiamare **riferimenti** la finestra di dialogo. Se non viene visualizzato, fare clic su di **Sfoglia** pulsante per eseguire la ricerca. Selezionare la casella di controllo a sinistra del nome del progetto e quindi fare clic su **OK**.  
  
3.  Controllare il nome della routine.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di errore](../../../visual-basic/programming-guide/language-features/error-types.md)   
 [Gestione dei riferimenti in un progetto](https://docs.microsoft.com/visualstudio/ide/managing-references-in-a-project)   
 [Sub (istruzione)](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)
