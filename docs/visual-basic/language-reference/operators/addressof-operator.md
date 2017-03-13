---
title: "AddressOf Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "AddressOf"
  - "vb.AddressOf"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "AddressOf operator"
  - "addresses, passing to API procedures"
ms.assetid: 8105a59d-60d8-4ab5-b221-5899cdfacbf4
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# AddressOf Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Crea un'istanza delegata della routine che fa riferimento alla routine specifica.  
  
## Sintassi  
  
```  
  
AddressOf procedurename  
```  
  
## Parti  
 `procedurename`  
 Obbligatorio.  Specifica la routine a cui deve fare riferimento il delegato appena creato.  
  
## Note  
 L'operatore `AddressOf` crea un delegato di funzione che fa riferimento alla funzione specificata da `procedurename`.  Quando la routine specificata è un metodo di istanza, il delegato di funzione fa riferimento sia all'istanza che al metodo.  Quando successivamente viene richiamato il delegato di funzione, viene effettuata la chiamata al metodo specificato dell'istanza indicata.  
  
 È possibile utilizzare l'operatore `AddressOf` come operando di un costruttore delegato oppure in un contesto nel quale il tipo del delegato può essere determinato dal compilatore.  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `AddressOf` viene utilizzato per specificare un delegato per la gestione dell'evento `Click` di un pulsante.  
  
 [!code-vb[VbVbalrDelegates#8](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addressof-operator_1.vb)]  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `AddressOf` viene utilizzato per specificare la funzione di avvio per un thread.  
  
 [!code-vb[VbVbalrDelegates#9](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addressof-operator_2.vb)]  
  
## Vedere anche  
 [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Delegates](../../../visual-basic/programming-guide/language-features/delegates/delegates.md)