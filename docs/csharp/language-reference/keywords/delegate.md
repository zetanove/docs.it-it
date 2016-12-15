---
title: "delegate (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "delegate_CSharpKeyword"
  - "delegate"
  - "CS0123"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "delegate (parola chiave) [C#]"
  - "puntatori a funzione [C#]"
ms.assetid: 0bb8cb6d-2f87-47c7-9d1f-d65c1cd01e9f
caps.latest.revision: 24
caps.handback.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# delegate (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La dichiarazione di un tipo delegato è simile alla firma di un metodo.  Dispone di un valore restituito e di una serie di parametri di qualsiasi tipo:  
  
```  
public delegate void TestDelegate(string message);  
public delegate int TestDelegate(MyType m, long num);  
```  
  
 `delegate` è un tipo riferimento che può essere utilizzato per incapsulare un metodo denominato o anonimo.  I delegati sono simili ai puntatori a funzioni di C\+\+, sono tuttavia indipendenti dai tipi e protetti.  Per le applicazioni dei delegati, vedere [Delegati](../../../csharp/programming-guide/delegates/index.md) e [Delegati generici](../../../csharp/programming-guide/generics/generic-delegates.md).  
  
## Note  
 I delegati rappresentano la base degli [eventi](../../../csharp/programming-guide/events/index.md).  
  
 È possibile creare un'istanza di un delegato associandolo a un metodo denominato o anonimo.  Per ulteriori informazioni, vedere [Metodi denominati](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md) e [Metodi anonimi](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md).  
  
 È necessario creare un'istanza del delegato con un metodo o un'espressione lambda che dispone di un tipo restituito compatibile e di parametri di input.  Per ulteriori informazioni sul grado di varianza consentito nella firma del metodo, vedere [Varianza nei delegati](../Topic/Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md).  Per l'utilizzo con i metodi anonimi, è necessario dichiarare insieme il delegato e il codice da associare ad esso.  In questa sezione vengono trattati entrambi i metodi per creare istanze dei delegati.  
  
## Esempio  
 [!code-cs[csrefKeywordsTypes#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/delegate_1.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tipi di riferimento](../../../csharp/language-reference/keywords/reference-types.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)   
 [Delegati con metodi denominati e anonimi](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)   
 [Metodi anonimi](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)