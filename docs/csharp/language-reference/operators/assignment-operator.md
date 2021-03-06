---
title: "Operatore = (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "= (operatore) [C#]"
ms.assetid: d802a6d5-32f0-42b8-b180-12f5a081bfc1
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# Operatore = (Riferimenti per C#)
L'operatore di assegnazione \(`=`\) archivia il valore dell'operando a destra nella posizione di archiviazione, nella proprietà o nell'indicizzatore indicati dall'operando a sinistra e restituisce il valore come risultato.  Gli operandi devono essere dello stesso tipo oppure l'operando a destra deve essere implicitamente convertibile nel tipo dell'operando a sinistra.  
  
## Note  
 L'operatore di assegnazione non può essere sottoposto a overload.  È tuttavia possibile definire operatori di conversione impliciti per un tipo, che consentono di utilizzare l'operatore di assegnazione con tali tipi.  Per ulteriori informazioni, vedere [Utilizzo degli operatori di conversione](../../../csharp/programming-guide/statements-expressions-operators/using-conversion-operators.md).  
  
## Esempio  
 [!code-cs[csRefOperators#49](../../../csharp/language-reference/operators/codesnippet/CSharp/assignment-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)