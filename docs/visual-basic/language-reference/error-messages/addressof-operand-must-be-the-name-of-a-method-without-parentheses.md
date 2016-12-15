---
title: "&#39;AddressOf&#39; operand must be the name of a method (without parentheses) | Microsoft Docs"
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
  - "vbc30577"
  - "bc30577"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30577"
ms.assetid: c2c55640-5c61-4e66-97a4-4322020c6001
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;AddressOf&#39; operand must be the name of a method (without parentheses)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'operatore `AddressOf` consente di creare un'istanza delegata della routine che fa riferimento a una routine specifica.  La sintassi è la seguente:  
  
 `AddressOf` `procedurename`  
  
 L'argomento che segue `AddressOf` è stato racchiuso tra parentesi, che tuttavia non sono necessarie.  
  
 **ID errore:** BC30577  
  
### Per correggere l'errore  
  
1.  Rimuovere le parentesi dell'argomento che segue `AddressOf`.  
  
2.  Controllare che l'argomento sia un nome di metodo.  
  
## Vedere anche  
 [AddressOf Operator](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Delegates](../../../visual-basic/programming-guide/language-features/delegates/delegates.md)