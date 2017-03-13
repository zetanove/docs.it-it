---
title: "Implementazione esplicita dell&#39;interfaccia (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "interfacce esplicite [C#]"
  - "interfacce [C#], esplicite"
ms.assetid: 181c901f-0d4c-4f29-97fc-895079617bf2
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# Implementazione esplicita dell&#39;interfaccia (Guida per programmatori C#)
Se una [classe](../../../csharp/language-reference/keywords/class.md) implementa due interfacce che contengono un membro con la stessa firma e quest'ultimo viene implementato sulla classe, entrambe le interfacce utilizzeranno il membro come propria implementazione.  Nell'esempio seguente, tutte le chiamate a `Paint` richiamare lo stesso metodo.  
  
 [!code-cs[csProgGuideInheritance#39](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/explicit-interface-implementation_1.cs)]  
  
 Se tuttavia due membri di [interfaccia](../../../csharp/language-reference/keywords/interface.md) non eseguono la stessa funzione, l'implementazione di una o di entrambe le interfacce potrebbe non risultare corretta.  È possibile implementare un membro di interfaccia in modo esplicito, ossia creando un membro di classe che viene chiamato solo tramite l'interfaccia e che è specifico di tale interfaccia.  Per questa operazione è necessario assegnare al membro di classe il nome dell'interfaccia seguito da un punto.  Ad esempio:  
  
 [!code-cs[csProgGuideInheritance#40](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/explicit-interface-implementation_2.cs)]  
  
 Il membro di classe `IControl.Paint` è disponibile solo tramite l'interfaccia `IControl`, mentre `ISurface.Paint` è disponibile solo tramite `ISurface`.  Entrambe le implementazioni del metodo sono distinte e nessuna è direttamente disponibile sulla classe.  Ad esempio:  
  
 [!code-cs[csProgGuideInheritance#41](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/explicit-interface-implementation_3.cs)]  
  
 L'implementazione esplicita consente inoltre di risolvere i casi in cui due interfacce dichiarano membri diversi con lo stesso nome, ad esempio una proprietà e un metodo:  
  
 [!code-cs[csProgGuideInheritance#42](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/explicit-interface-implementation_4.cs)]  
  
 Per implementare entrambe le interfacce, una classe deve utilizzare l'implementazione esplicita per la proprietà P o il metodo P oppure per entrambi, in modo da evitare che venga generato un errore del compilatore.  Ad esempio:  
  
 [!code-cs[csProgGuideInheritance#43](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/explicit-interface-implementation_5.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Interfacce](../../../csharp/programming-guide/interfaces/index.md)   
 [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md)