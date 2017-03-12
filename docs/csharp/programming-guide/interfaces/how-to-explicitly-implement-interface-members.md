---
title: "Procedura: implementare in modo esplicito i membri di interfaccia (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "interfacce [C#], implementazione esplicita"
ms.assetid: 514cde76-f981-474e-8b40-9493619f899c
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# Procedura: implementare in modo esplicito i membri di interfaccia (Guida per programmatori C#)
In questo esempio vengono dichiarate un'[interfaccia](../../../csharp/language-reference/keywords/interface.md) `IDimensions` e una classe `Box`, che implementa in modo esplicito i membri di interfaccia `getLength` e `getWidth`.  L'accesso ai membri avviene tramite l'istanza di interfaccia `dimensions`.  
  
## Esempio  
 [!code-cs[csProgGuideInheritance#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-explicitly-implem_1_1.cs)]  
  
## Programmazione efficiente  
  
-   Le righe che seguono, nel metodo `Main`, sono impostate come commento perché, in caso contrario, genererebbero errori di compilazione.  Non è possibile accedere da un'istanza di [classe](../../../csharp/language-reference/keywords/class.md) a un membro di interfaccia implementato in modo esplicito:  
  
     [!code-cs[csProgGuideInheritance#45](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-explicitly-implem_1_2.cs)]  
  
-   Inoltre, le righe che seguono, nel metodo `Main`, stampano le dimensioni della casella, in quanto i metodi vengono richiamati da un'istanza dell'interfaccia:  
  
     [!code-cs[csProgGuideInheritance#46](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-explicitly-implem_1_3.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Interfacce](../../../csharp/programming-guide/interfaces/index.md)   
 [Procedura: implementare in modo esplicito i membri di due interfacce](../../../csharp/programming-guide/interfaces/how-to-explicitly-implement-members-of-two-interfaces.md)