---
title: "Operatore * (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "*_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "* (operatore) [C#]"
  - "moltiplicazione (operatore) (*) [C#]"
ms.assetid: abd9a5f0-9b24-431e-971a-09ee1c45c50e
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# Operatore * (Riferimenti per C#)
L'operatore di moltiplicazione \(`*`\) calcola il prodotto degli operandi.  Inoltre, l'operatore di dereferenziazione, che consente la lettura e la scrittura in un puntatore.  
  
## Note  
 Tutti i tipi numerici hanno operatori di moltiplicazione già definiti.  
  
 L'operatore `*` viene inoltre utilizzato per dichiarare tipi puntatore e dereferenziare i puntatori.  Questo operatore può essere utilizzato soltanto in contesti unsafe, identificati dall'utilizzo della parola chiave [unsafe](../../../csharp/language-reference/keywords/unsafe.md), e che richiedono l'opzione del compilatore [\/unsafe](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md).  L'operatore di dereferenziazione è noto anche come operatore di riferimento indiretto.  
  
 I tipi definiti dall'utente possono eseguire l'overload dell'operatore `*` binario. Vedere [operator](../../../csharp/language-reference/keywords/operator.md).  Quando si esegue l'overload di un operatore binario, viene eseguito in modo implicito anche l'overload dell'eventuale operatore di assegnazione corrispondente.  
  
## Esempio  
 [!code-cs[csRefOperators#50](../../../csharp/language-reference/operators/codesnippet/CSharp/multiplication-operator_1.cs)]  
  
## Esempio  
 [!code-cs[csRefOperators#51](../../../csharp/language-reference/operators/codesnippet/CSharp/multiplication-operator_2.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)