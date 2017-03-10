---
title: "Procedura: implementare in modo esplicito i membri di due interfacce (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "ereditarietà [C#], implementazione esplicita dei membri d'interfaccia"
  - "interfacce [C#], implementazione esplicita con ereditarietà"
ms.assetid: 8b402ddc-dff9-4869-89cb-d718c764e68e
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# Procedura: implementare in modo esplicito i membri di due interfacce (Guida per programmatori C#)
L'implementazione esplicita dell'[interfaccia](../../../csharp/language-reference/keywords/interface.md) consente inoltre al programmatore di implementare due interfacce che presentano gli stessi nomi di membri e di operare un'implementazione separata per ciascun membro dell'interfaccia.  In questo sono visualizzate le dimensioni di una casella sia in unità di misura decimali che in unità di misura inglesi.  La [classe](../../../csharp/language-reference/keywords/class.md) Box implementa due interfacce, IEnglishDimensions e IMetricDimensions, che rappresentano i diversi sistemi di misura.  Entrambe le interfacce presentano gli stessi nomi di membri: Length e Width.  
  
## Esempio  
 [!code-cs[csProgGuideInheritance#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-explicitly-implem_0_1.cs)]  
  
## Programmazione efficiente  
 Se si desidera esprimere le misure predefinite in unità inglesi, implementare i metodi Length e Width normalmente e implementare in modo esplicito i metodi Length e Width dall'interfaccia IMetricDimensions:  
  
 [!code-cs[csProgGuideInheritance#10](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-explicitly-implem_0_2.cs)]  
  
 In questo caso è possibile accedere alle unità di misura inglesi dall'istanza di classe e alle unità decimali dall'istanza di interfaccia:  
  
 [!code-cs[csProgGuideInheritance#11](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-explicitly-implem_0_3.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Interfacce](../../../csharp/programming-guide/interfaces/index.md)   
 [Procedura: implementare in modo esplicito i membri di interfaccia](../../../csharp/programming-guide/interfaces/how-to-explicitly-implement-interface-members.md)