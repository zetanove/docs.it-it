---
title: Risoluzione dei problemi di gestori eventi ereditati in Visual Basic | Documenti di Microsoft
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
- troubleshooting events
- inherited events
- troubleshooting Visual Basic, event handlers
- event handling, troubleshooting
- event handlers, troubleshooting
ms.assetid: e1c8759f-5370-4308-8476-8c48b73509bf
caps.latest.revision: 11
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
ms.openlocfilehash: 0dae6b48b1885a52b99ae3e7328340cac7b2d7d4
ms.lasthandoff: 03/13/2017

---
# <a name="troubleshooting-inherited-event-handlers-in-visual-basic"></a>Risoluzione dei problemi relativi ai gestori eventi ereditati in Visual Basic
In questo argomento vengono elencati i problemi che si verificano con i gestori eventi nei componenti ereditati.  
  
## <a name="procedures"></a>Procedure  
  
#### <a name="code-in-event-handler-executes-twice-for-every-call"></a>Codice nel gestore eventi viene eseguita due volte per ogni chiamata  
  
-   Un gestore eventi ereditato non deve includere un [gestisce](../../../../visual-basic/language-reference/statements/handles-clause.md) clausola. Il metodo nella classe di base è già associato all'evento e verrà generato di conseguenza. Rimuovere il `Handles` clausola dal metodo ereditato.  
  
     [!code-vb[VbVbalrEvents n.&32;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/troubleshooting-inherited-event-handlers_1.vb)]  
  
-   Se il metodo ereditato non ha un `Handles` (parola chiave), verificare che il codice non è presente un ulteriore [AddHandler (istruzione)](../../../../visual-basic/language-reference/statements/addhandler-statement.md) o qualsiasi altro metodo che gestisce l'evento stesso.  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi](../../../../visual-basic/programming-guide/language-features/events/index.md)
