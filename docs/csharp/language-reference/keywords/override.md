---
title: "override (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "override"
  - "override_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "override (parola chiave) [F#]"
ms.assetid: dd1907a8-acf8-46d3-80b9-c2ca4febada8
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# override (Riferimenti per C#)
Il modificatore `override` è necessario per estendere o modificare l'implementazione astratta o virtuale di un metodo, una proprietà, un indicizzatore o un evento ereditato.  
  
## Esempio  
 In questo esempio, la classe `Square` deve fornire un'implementazione sottoposta a override dell'oggetto `Area` poiché quest'ultimo viene ereditato dall'oggetto `ShapesClass` astratto.  
  
 [!code-cs[csrefKeywordsModifiers#1](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#1)]  
  
 Un metodo `override` fornisce una nuova implementazione di un membro ereditato da una classe base.  Il metodo che viene sottoposto a override mediante una dichiarazione `override` viene definito metodo di base sottoposto a override.  Il metodo di base sottoposto a override deve avere la stessa firma del metodo di `override`.  Per informazioni sull'eredità, vedere [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md).  
  
 Non è possibile eseguire l'override di un metodo non virtuale o static.  Il metodo di base sottoposto a override deve essere `virtual`, `abstract` o `override`.  
  
 Le dichiarazioni `override` non possono modificare l'accessibilità del metodo `virtual`.  Il metodo di `override` e il metodo `virtual` devono avere lo stesso [modificatore del livello di accesso](../../../csharp/language-reference/keywords/access-modifiers.md).  
  
 Non è possibile utilizzare i modificatori `new`, `static`, o `virtual` per modificare un metodo `override`.  
  
 Una dichiarazione di proprietà di override deve indicare esattamente lo stesso modificatore di accesso, lo stesso tipo e lo stesso nome della proprietà ereditata. Inoltre, la proprietà sottoposta a override deve essere `virtual`, `abstract` o `override`.  
  
 Per ulteriori informazioni su come utilizzare la parola chiave `override`, vedere [Controllo delle versioni con le parole chiave Override e New](../../../csharp/programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md) e [Sapere quando utilizzare le parole chiave Override e New](../../../csharp/programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md).  
  
## Esempio  
 Nell'esempio seguente vengono definite una classe base denominata `Employee` e una classe derivata denominata `SalesEmployee`.  La classe `SalesEmployee` comprende una proprietà aggiuntiva, `salesbonus`, ed esegue l'override del metodo `CalculatePay` per prenderla in considerazione.  
  
 [!code-cs[csrefKeywordsModifiers#9](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#9)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)   
 [abstract](../../../csharp/language-reference/keywords/abstract.md)   
 [virtuale](../../../csharp/language-reference/keywords/virtual.md)   
 [new](../../../csharp/language-reference/keywords/new.md)   
 [Polimorfismo](../../../csharp/programming-guide/classes-and-structs/polymorphism.md)