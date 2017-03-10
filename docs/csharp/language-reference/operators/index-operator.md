---
title: "Operatore (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "[]_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "operatore di indice [C#]"
  - "parentesi quadre [ ] (operatore) [C#]"
  - "[] (operatore) [C#]"
  - "operatore di indicizzazione [C#]"
ms.assetid: 5c16bb45-88f7-45ff-b42c-1af1972b042c
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# Operatore (Riferimenti per C#)
Le parentesi quadre \(`[]`\) vengono utilizzate per le matrici, gli indicizzatori e gli attributi,  ma possono essere utilizzate anche per i puntatori.  
  
## Note  
 Un tipo matrice è un tipo seguito da `[]`:  
  
 [!code-cs[csRefOperators#43](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#43)]  
  
 Per consentire l'accesso a un elemento di una matrice, l'indice dell'elemento desiderato viene racchiuso tra parentesi:  
  
 [!code-cs[csRefOperators#44](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#44)]  
  
 Se l'indice di una matrice non è incluso nell'intervallo, viene generata un'eccezione.  
  
 L'operatore di indicizzazione della matrice non può essere sottoposto a overload; tuttavia, i tipi possono definire gli indicizzatori nonché le proprietà che accettano uno o più parametri.  I parametri dell'indicizzatore sono racchiusi tra parentesi quadre, come qualsiasi indice di matrice, ma, differentemente da questi ultimi che devono essere integrali, possono essere dichiarati come appartenenti a un tipo qualsiasi.  
  
 In .NET Framework, ad esempio, viene definito un tipo `Hashtable` che associa chiavi e valori di tipo arbitrario:  
  
 [!code-cs[csRefOperators#45](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#45)]  
  
 Le parentesi quadre vengono inoltre utilizzate per specificare [Attributi](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md):  
  
 [!code-cs[csRefOperators#46](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#46)]  
  
 È possibile utilizzare le parentesi quadre per effettuare l'indicizzazione a partire da un puntatore:  
  
 [!code-cs[csRefOperators#47](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#47)]  
  
 Non viene effettuata alcuna verifica dei limiti.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)   
 [Matrici](../../../csharp/programming-guide/arrays/index.md)   
 [Indicizzatori](../../../csharp/programming-guide/indexers/index.md)   
 [non protette](../../../csharp/language-reference/keywords/unsafe.md)   
 [Istruzione fixed](../../../csharp/language-reference/keywords/fixed-statement.md)