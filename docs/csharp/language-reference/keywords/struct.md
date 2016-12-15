---
title: "struct (Riferimenti per C#) | Microsoft Docs"
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
  - "struct_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "struct (parola chiave) [C#]"
  - "struct [C#], parola chiave struct"
ms.assetid: ff3dd9b7-dc93-4720-8855-ef5558f65c7c
caps.latest.revision: 23
caps.handback.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# struct (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un `struct` è un tipo di valore generalmente usato per incapsulare piccoli gruppi di variabili correlate, ad esempio le coordinate di un rettangolo o le caratteristiche di un articolo in un inventario.  Nell'esempio che segue è illustrata una semplice dichiarazione struct:  
  
```  
public struct Book  
{  
    public decimal price;  
    public string title;  
    public string author;  
}  
```  
  
## Note  
 Gli struct possono contenere anche [costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md), [costanti](../../../csharp/programming-guide/classes-and-structs/constants.md), [campi](../../../csharp/programming-guide/classes-and-structs/fields.md), [metodi](../../../csharp/programming-guide/classes-and-structs/methods.md), [proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md), [indicizzatori](../../../csharp/programming-guide/indexers/index.md), [operatori](../../../csharp/programming-guide/statements-expressions-operators/operators.md), [eventi](../../../csharp/programming-guide/events/index.md) and [tipi nidificati](../../../csharp/programming-guide/classes-and-structs/nested-types.md), anche se è consigliabile trasformare il tipo in classe se sono necessari molti di questi membri.  
  
 Per i relativi esempi, vedere [Utilizzo di struct](../../../csharp/programming-guide/classes-and-structs/using-structs.md).  
  
 Gli struct possono implementare un'interfaccia, ma non possono ereditare da altri struct.  Per questo motivo i membri di struct non possono essere dichiarati come `protected`.  
  
 Per altre informazioni, vedere [Struct](../../../csharp/programming-guide/classes-and-structs/structs.md).  
  
## Esempi  
 Per ulteriori esempi e informazioni, vedere [Utilizzo di struct](../../../csharp/programming-guide/classes-and-structs/using-structs.md).  
  
## Specifiche del linguaggio C\#  
 Per i relativi esempi, vedere [Utilizzo di struct](../../../csharp/programming-guide/classes-and-structs/using-structs.md).  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei valori predefiniti](../../../csharp/language-reference/keywords/default-values-table.md)   
 [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tipi](../../../csharp/language-reference/keywords/types.md)   
 [Tipi valore](../../../csharp/language-reference/keywords/value-types.md)   
 [classe](../../../csharp/language-reference/keywords/class.md)   
 [interfaccia](../../../csharp/language-reference/keywords/interface.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)