---
title: "Return Statement (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Return"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Return statement, syntax"
  - "control flow, returning control to expressions"
  - "Return statement"
  - "expressions [Visual Basic], returning control to"
ms.assetid: ac86e7f0-5a67-42c3-9834-0e0381efa3ec
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Return Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Restituisce il controllo al codice che ha chiamato una routine `Function`, `Sub`, `Get`, `Set` o `Operator`.  
  
## Sintassi  
  
```  
Return  
-or-  
Return expression  
```  
  
## Parte  
 `expression`  
 Richiesta in una routine `Function`, `Get` o `Operator`.  Espressione che rappresenta il valore da restituire al codice che effettua la chiamata.  
  
## Note  
 In una procedura `Sub` o `Set`, l'istruzione `Return` equivale a un'istruzione `Exit Sub` o `Exit Property` e non è necessario fornire `expression`.  
  
 In una routine `Function`, `Get` o `Operator`, la routine `Return` deve includere `expression` ed`expression` deve restituire un tipo di dati convertibile nel tipo restituito della routine.  In una routine `Function` or `Get` è anche possibile assegnare un'espressione al nome della routine come valore restituito e di eseguire quindi una routine `Exit Function` o `Exit Property`.  In una routine `Operator` è necessario utilizzare `Return` `expression`.  
  
 È possibile includere un numero di istruzioni `Return` appropriate nella stessa procedura.  
  
> [!NOTE]
>  Il codice incluso in un blocco `Finally` viene eseguito dopo che un'istruzione `Return` viene rilevata in un blocco `Try` o `Catch` ma prima dell'esecuzione dell'istruzione `Return`.  In `Return` l'istruzione non può essere incluso in un oggetto  `Finally` blocco.  
  
## Esempio  
 Nell'esempio seguente viene utilizzata l'istruzione `Return` diverse volte per tornare al codice che effettua la chiamata quando non è necessario che la procedura faccia altro.  
  
 [!code-vb[VbVbalrStatements#53](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/return-statement_1.vb)]  
  
## Vedere anche  
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Get Statement](../../../visual-basic/language-reference/statements/get-statement.md)   
 [Set Statement](../../../visual-basic/language-reference/statements/set-statement.md)   
 [Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Exit Statement](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)