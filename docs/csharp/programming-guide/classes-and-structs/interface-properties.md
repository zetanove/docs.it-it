---
title: "Propriet&#224; dell&#39;interfaccia (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "interfacce [C#], proprietà"
  - "proprietà [C#], nelle interfacce"
ms.assetid: 6503e9ed-33d7-44ec-b4c1-cc16c084b795
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# Propriet&#224; dell&#39;interfaccia (Guida per programmatori C#)
Le proprietà possono essere dichiarate su una [interfaccia](../../../csharp/language-reference/keywords/interface.md).  Nell'esempio seguente viene illustrata la funzione di accesso di un indicizzatore di interfaccia:  
  
 [!code-cs[csProgGuideProperties#14](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/interface-properties_1.cs)]  
  
 La funzione di accesso di una proprietà di interfaccia non include un corpo.  Lo scopo delle funzioni di accesso è quindi di indicare se la proprietà è in lettura\/scrittura, in sola scrittura o in sola lettura.  
  
## Esempio  
 Nell'esempio che segue l'interfaccia `IEmployee` è associata a una proprietà di lettura\/scrittura, `Name`, e a una proprietà in sola lettura, `Counter`.  La classe `Employee` implementa l'interfaccia `IEmployee` e utilizza le due proprietà.  Il programma legge il nome di un nuovo dipendente e il numero corrente di dipendenti, quindi visualizza il nome del dipendente e il relativo numero calcolato.  
  
 È possibile utilizzare il nome completo della proprietà, che fa riferimento all'interfaccia in cui il membro è dichiarato.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideProperties#16](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/interface-properties_2.cs)]  
  
 Questo meccanismo è denominato [Implementazione esplicita dell'interfaccia](../../../csharp/programming-guide/interfaces/explicit-interface-implementation.md).  Se la classe `Employee`, ad esempio, implementa due interfacce, `ICitizen` e `IEmployee`, ed entrambe le interfacce sono associate alla proprietà `Name`, sarà necessaria l'implementazione esplicita del membro di interfaccia.  Pertanto, la dichiarazione di proprietà  
  
 [!code-cs[csProgGuideProperties#16](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/interface-properties_2.cs)]  
  
 implementa la proprietà `Name` nell'interfaccia `IEmployee`, mentre la dichiarazione  
  
 [!code-cs[csProgGuideProperties#17](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/interface-properties_3.cs)]  
  
 implementa la proprietà `Name` nell'interfaccia `ICitizen`.  
  
 [!code-cs[csProgGuideProperties#15](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/interface-properties_4.cs)]  
  
  **`210 Hazem Abolrous`**    
## Esempio di output  
 `Enter number of employees: 210`  
  
 `Enter the name of the new employee: Hazem Abolrous`  
  
 `The employee information:`  
  
 `Employee number: 211`  
  
 `Employee name: Hazem Abolrous`  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [Utilizzo delle proprietà](../../../csharp/programming-guide/classes-and-structs/using-properties.md)   
 [Confronto tra proprietà e indicizzatori](../../../csharp/programming-guide/indexers/comparison-between-properties-and-indexers.md)   
 [Indicizzatori](../../../csharp/programming-guide/indexers/index.md)   
 [Interfacce](../../../csharp/programming-guide/interfaces/index.md)