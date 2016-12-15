---
title: "interface (Riferimenti per C#) | Microsoft Docs"
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
  - "interface_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "interface (parola chiave) [C#]"
ms.assetid: 7da38e81-4f99-4bc5-b07d-c986b687eeba
caps.latest.revision: 29
caps.handback.revision: 29
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# interface (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un'interfaccia contiene solo le firme di [metodi](../../../csharp/programming-guide/classes-and-structs/methods.md), [proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md), [eventi](../../../csharp/programming-guide/events/index.md) o [indicizzatori](../../../csharp/programming-guide/indexers/index.md).  Una classe o struttura che implementa l'interfaccia deve implementarne i membri specificati nella definizione dell'interfaccia.  Nell'esempio seguente, la classe `ImplementationClass` deve implementare un metodo denominato `SampleMethod` che non dispone di parametri e restituisce `void`.  
  
 Per ulteriori informazioni ed esempi, vedere [Interfacce](../../../csharp/programming-guide/interfaces/index.md).  
  
## Esempio  
 [!code-cs[csrefKeywordsTypes#14](../../../csharp/language-reference/keywords/codesnippet/CSharp/interface_1.cs)]  
  
 Un'interfaccia può essere membro di uno spazio dei nomi o di una classe e contenere firme dei seguenti membri:  
  
-   [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)  
  
-   [Proprietà](../../../csharp/programming-guide/classes-and-structs/using-properties.md)  
  
-   [Indicizzatori](../../../csharp/programming-guide/indexers/using-indexers.md)  
  
-   [Eventi](../../../csharp/language-reference/keywords/event.md)  
  
 Un'interfaccia può ereditare da una o più interfacce di base.  
  
 Quando un elenco di tipi di base contiene interfacce e una classe base, la classe base deve precedere le interfacce.  
  
 Una classe che implementa un'interfaccia può implementare in modo esplicito i membri di tale interfaccia.  Non è possibile accedere a un membro implementato in modo esplicito tramite un'istanza di classe, ma solo tramite un'istanza dell'interfaccia.  
  
 Per ulteriori dettagli ed esempi di codice sull'implementazione esplicita delle interfacce, vedere [Implementazione esplicita dell'interfaccia](../../../csharp/programming-guide/interfaces/explicit-interface-implementation.md).  
  
## Esempio  
 Nell'esempio seguente viene illustrata l'implementazione di un'interfaccia.  In questo esempio, l'interfaccia contiene la dichiarazione di proprietà e la classe contiene l'implementazione.  Qualsiasi istanza di una classe che implementa `IPoint` presenta proprietà `x` e `y` di tipo Integer.  
  
 [!code-cs[csrefKeywordsTypes#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/interface_2.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tipi di riferimento](../../../csharp/language-reference/keywords/reference-types.md)   
 [Interfacce](../../../csharp/programming-guide/interfaces/index.md)   
 [Utilizzo delle proprietà](../../../csharp/programming-guide/classes-and-structs/using-properties.md)   
 [Utilizzo degli indicizzatori](../../../csharp/programming-guide/indexers/using-indexers.md)   
 [classe](../../../csharp/language-reference/keywords/class.md)   
 [struct](../../../csharp/language-reference/keywords/struct.md)   
 [Interfacce](../../../csharp/programming-guide/interfaces/index.md)