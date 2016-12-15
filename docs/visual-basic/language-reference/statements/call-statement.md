---
title: "Call Statement (Visual Basic) | Microsoft Docs"
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
  - "vb.Call"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "procedures, Call statement"
  - "Call statement"
  - "procedures, calling"
ms.assetid: e5b31571-6867-406f-b8e7-a3f9aae4723a
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Call Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di trasferire un controllo a una routine `Function`, `Sub` oppure a una routine della libreria a collegamento dinamico \(DLL\).  
  
## Sintassi  
  
```  
[ Call ] procedureName [ (argumentList) ]  
```  
  
## Parti  
 `procedureName`  
 Obbligatorio.  Nome della routine da chiamare.  
  
 `argumentList`  
 Parametro facoltativo.  Elenco di variabili o espressioni che costituiscono gli argomenti passati alla routine quando viene chiamata.  Gli argomenti sono separati da una virgola.  Se specificato, è necessario che la parte `argumentList` sia racchiusa tra parentesi.  
  
## Note  
 È possibile utilizzare la parola chiave di `Call` quando si chiama una routine.  Per la maggior parte delle chiamate di routine, non è necessario utilizzare la parola chiave.  
  
 In genere si utilizza la parola chiave di `Call` quando l'espressione chiamata non inizia con un identificatore.  L'utilizzo della parola chiave di `Call` per altri utilizzi non è consigliato.  
  
 Se la routine restituisce un valore, l'istruzione `Call` lo ignora.  
  
## Esempio  
 Nel codice seguente a due esempi in cui la parola chiave di `Call` è necessaria per chiamare una routine.  In entrambi gli esempi, l'espressione chiamata non inizia con un identificatore.  
  
 [!code-vb[VbVbalrStatements#97](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/call-statement_1.vb)]  
  
## Vedere anche  
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Lambda Expressions](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)