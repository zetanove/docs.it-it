---
title: "Indicizzatori nelle interfacce (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "funzioni di accesso [C#], indicizzatori"
  - "indicizzatori [C#], in interfacce"
ms.assetid: e16b54bd-4a83-4f52-bd75-65819fca79e8
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# Indicizzatori nelle interfacce (Guida per programmatori C#)
Gli indicizzatori possono essere dichiarati su una [interfaccia](../../../csharp/language-reference/keywords/interface.md).  Le funzioni di accesso degli indicizzatori di interfaccia differiscono dalle funzioni di accesso degli indicizzatori di [classe](../../../csharp/language-reference/keywords/class.md) per i seguenti aspetti:  
  
-   Le funzioni di accesso di interfaccia non utilizzano modificatori.  
  
-   Una funzione di accesso di interfaccia non include un corpo.  
  
 Lo scopo della funzione di accesso è pertanto quello di indicare se l'indicizzatore è in lettura\/scrittura, in sola lettura o in sola scrittura.  
  
 Nell'esempio seguente viene illustrata la funzione di accesso di un indicizzatore di interfaccia:  
  
 [!code-cs[csProgGuideIndexers#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/indexers-in-interfaces_1.cs)]  
  
 È necessario che la firma di un indicizzatore sia diversa dalle firme di tutti gli altri indicizzatori dichiarati nella stessa interfaccia.  
  
## Esempio  
 Nell'esempio seguente viene illustrata la modalità di implementazione degli indicizzatori di interfaccia:  
  
 [!code-cs[csProgGuideIndexers#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/indexers-in-interfaces_2.cs)]  
  
 Nell'esempio precedente era possibile utilizzare l'implementazione esplicita del membro dell'interfaccia, utilizzando il nome completo del membro dell'interfaccia.  Di seguito è riportato un esempio:  
  
```  
public string ISomeInterface.this   
{   
}   
```  
  
 Tuttavia, il nome completo è necessario unicamente per evitare l'ambiguità quando la classe implementa più di un'interfaccia con la stessa firma di indicizzatore.  Se ad esempio la classe  `Employee` implementa due interfacce, `ICitizen` e `IEmployee`, ed entrambe le interfacce hanno la stessa firma di indicizzatore, sarà necessaria l'implementazione esplicita del membro dell'interfaccia.  In altre parole, deve essere utilizzata la seguente dichiarazione di indicizzatore:  
  
```  
public string IEmployee.this   
{   
}   
```  
  
 implementa l'indicizzatore nell'interfaccia `IEmployee`, mentre la seguente dichiarazione:  
  
```  
public string ICitizen.this   
{   
}   
```  
  
 implementa l'indicizzatore nell'interfaccia `ICitizen`.  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Indicizzatori](../../../csharp/programming-guide/indexers/index.md)   
 [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [Interfacce](../../../csharp/programming-guide/interfaces/index.md)