---
title: "Alias Clause (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Alias"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Alias keyword"
ms.assetid: 58c06b11-465d-4d87-906a-73200a3d7f19
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# Alias Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Indica che il nome della routine esterna è diverso nella rispettiva DLL.  
  
## Note  
 È possibile utilizzare la parola chiave `Alias` nel seguente contesto:  
  
 [Istruzione Declare](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 Nell'esempio seguente la parola chiave `Alias` viene utilizzata per fornire il nome della funzione in advapi32.dll, `GetUserNameA`, al posto della quale in questo esempio viene utilizzata `getUserName`.  La funzione `getUserName` viene chiamata nella routine `getUser`, che consente di visualizzare il nome dell'utente corrente.  
  
 [!code-vb[VbVbalrStatements#15](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/alias-clause_1.vb)]  
  
## Vedere anche  
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)