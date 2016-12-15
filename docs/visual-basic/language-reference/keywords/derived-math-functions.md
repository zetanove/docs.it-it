---
title: "Derived Math Functions (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "arithmetic operations, derived math functions"
  - "cosecant function"
  - "arcsecant function"
  - "arccotangent function"
  - "functions [Visual Basic], derived math functions"
  - "inverse functions"
  - "math functions, derived"
  - "derived math functions"
  - "cotangent function"
  - "angles"
  - "secant function"
  - "trigonometric functions"
  - "logarithms"
  - "arccosecant function"
  - "hyperbolic functions"
  - "arcsine function"
  - "degrees"
  - "arccosine function"
ms.assetid: 63e449d8-9444-44fb-8db1-6d9cf346e2aa
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Derived Math Functions (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Nella tabella seguente sono contenute funzioni matematiche non intrinseche che possono essere derivate da funzioni matematiche intrinseche dell'oggetto <xref:System.Math?displayProperty=fullName>.  È possibile accedere alle funzioni matematiche intrinseche aggiungendo `Imports System.Math` al file o progetto.  
  
|Funzione|Funzione equivalente derivata|  
|--------------|-----------------------------------|  
|Secante \(Sec\(x\)\)|1 \/ Cos\(x\)|  
|Cosecante \(Csc\(x\)\)|1 \/ Sin\(x\)|  
|Cotangente \(Ctan\(x\)\)|1 \/ Tan\(x\)|  
|Seno inverso \(Asin\(x\)\)|Atan\(x \/ Sqrt\(\-x \* x \+ 1\)\)|  
|Coseno inverso \(Acos\(x\)\)|Atan\(\-x \/ Sqrt\(\-x \* x \+ 1\)\) \+ 2 \* Atan\(1\)|  
|Secante inversa \(Asec\(x\)\)|2 \* Atan\(1\) – Atan\(Sign\(x\) \/ Sqrt\(x \* x – 1\)\)|  
|Cosecante inversa \(Acsc\(x\)\)|Atan\(Sign\(x\) \/ Sqrt\(x \* x – 1\)\)|  
|Cotangente inversa \(Acot\(x\)\)|2 \* Atan\(1\) \- Atan\(x\)|  
|Seno iperbolico \(Sinh\(x\)\)|\(Exp\(x\) – Exp\(\-x\)\) \/ 2|  
|Coseno iperbolico \(Cosh\(x\)\)|\(Exp\(x\) \+ Exp\(\-x\)\) \/ 2|  
|Tangente iperbolica \(Tanh\(x\)\)|\(Exp\(x\) – Exp\(\-x\)\) \/ \(Exp\(x\) \+ Exp\(\-x\)\)|  
|Secante iperbolica \(Sech\(x\)\)|2 \/ \(Exp\(x\) \+ Exp\(\-x\)\)|  
|Cosecante iperbolica \(Csch\(x\)\)|2 \/ \(Exp\(x\) – Exp\(\-x\)\)|  
|Cotangente iperbolica \(Coth\(x\)\)|\(Exp\(x\) \+ Exp\(\-x\)\) \/ \(Exp\(x\) – Exp\(\-x\)\)|  
|Seno iperbolico inverso \(Asinh\(x\)\)|Log\(x \+ Sqrt\(x \* x \+ 1\)\)|  
|Coseno iperbolico inverso \(Acosh\(x\)\)|Log\(x \+ Sqrt\(x \* x – 1\)\)|  
|Tangente iperbolica inversa \(Atanh\(x\)\)|Log\(\(1 \+ x\) \/ \(1 – x\)\) \/ 2|  
|Secante iperbolica inversa \(AsecH\(x\)\)|Log\(\(Sqrt\(\-x \* x \+ 1\) \+ 1\) \/ x\)|  
|Cosecante iperbolica inversa \(Acsch\(x\)\)|Log\(\(Sign\(x\) \* Sqrt\(x \* x \+ 1\) \+ 1\) \/ x\)|  
|Cotangente iperbolica inversa \(Acoth\(x\)\)|Log\(\(x \+ 1\) \/ \(x – 1\)\) \/ 2|  
  
## Vedere anche  
 [Funzioni matematiche](../../../visual-basic/language-reference/functions/math-functions.md)