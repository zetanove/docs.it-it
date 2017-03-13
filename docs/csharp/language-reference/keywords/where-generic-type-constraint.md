---
title: "where (vincolo di tipo generico) (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "whereconstraint"
  - "whereconstraint_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "where (vincolo di tipo generico) [C#]"
ms.assetid: d7aa871b-0714-416a-bab2-96f87ada4310
caps.latest.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 10
---
# where (vincolo di tipo generico) (Riferimenti per C#)
In una definizione di tipo generico, la clausola `where` viene utilizzata per specificare i vincoli sui tipi che possono essere utilizzati come argomenti per un parametro di tipo definito in una dichiarazione generica.  È possibile ad esempio dichiarare una classe generica, `MyGenericClass`, in modo tale che il parametro di tipo `T` implementi l'interfaccia <xref:System.IComparable%601>:  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
> [!NOTE]
>  Per ulteriori informazioni sulla clausola where in un'espressione di query, vedere [Clausola where](../../../csharp/language-reference/keywords/where-clause.md).  
  
 Oltre ai vincoli di interfaccia, una clausola `where` può comprendere un vincolo di classe base, mediante cui si stabilisce che un tipo deve disporre della classe specificata come classe base o essere esso stesso tale classe, per essere utilizzato come argomento di tipo per tale tipo generico.  Se si utilizza un vincolo di questo tipo, è necessario inserirlo prima di qualsiasi altro vincolo su tale parametro di tipo.  
  
 [!code-cs[csrefKeywordsContextual#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/where-generic-type-constraint_1.cs)]  
  
 La clausola `where` può anche includere un vincolo di costruttore.  È possibile creare un'istanza di un parametro di tipo utilizzando il nuovo operatore; tuttavia, per eseguire questa operazione è necessario impostare sul parametro di tipo il vincolo di costruttore, `new()`.  Il [vincolo new\(\)](../../../csharp/language-reference/keywords/new-constraint.md) comunica al compilatore che ogni argomento di tipo fornito deve disporre di un costruttore senza parametri, o predefinito, accessibile.  Di seguito è riportato un esempio:  
  
 [!code-cs[csrefKeywordsContextual#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/where-generic-type-constraint_2.cs)]  
  
 Il vincolo `new()` viene visualizzato per ultimo nella clausola `where`.  
  
 Con i parametri a più tipi, utilizzare una clausola `where` per ogni parametro di tipo, ad esempio:  
  
 [!code-cs[csrefKeywordsContextual#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/where-generic-type-constraint_3.cs)]  
  
 È inoltre possibile associare vincoli a parametri di tipo di metodi generici, nel modo seguente:  
  
```  
public bool MyMethod<T>(T t) where T : IMyInterface { }  
```  
  
 Si noti che la sintassi per descrivere i vincoli di parametri di tipo sui delegati è uguale a quella dei metodi:  
  
```  
delegate T MyDelegate<T>() where T : new()  
```  
  
 Per informazioni sui delegati generici, vedere [Delegati generici](../../../csharp/programming-guide/generics/generic-delegates.md).  
  
 Per informazioni dettagliate sulla sintassi e l'utilizzo di vincoli, vedere [Vincoli sui parametri di tipo](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Introduzione ai generics](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [Vincolo new](../../../csharp/language-reference/keywords/new-constraint.md)   
 [Vincoli sui parametri di tipo](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md)