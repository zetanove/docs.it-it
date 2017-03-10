---
title: "Limitazione dell&#39;accessibilit&#224; delle funzioni di accesso (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "funzioni di accesso [C#]"
  - "accessibilità asimmetrica delle funzioni di accesso [C#]"
  - "indicizzatori [C#], sola lettura"
  - "proprietà [C#], sola lettura"
  - "indicizzatori di sola lettura [C#]"
  - "proprietà di sola lettura [C#]"
ms.assetid: 6e655798-e112-4301-a680-6310a6e012e1
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# Limitazione dell&#39;accessibilit&#224; delle funzioni di accesso (Guida per programmatori C#)
Le parti [get](../../../csharp/language-reference/keywords/get.md) e [set](../../../csharp/language-reference/keywords/set.md) di una proprietà o di un indicizzatore sono denominate *funzioni di accesso*.  Per impostazione predefinita, queste funzioni di accesso hanno la stessa visibilità, ovvero livello di accesso, della proprietà o dell'indicizzatore cui appartengono.  Per ulteriori informazioni, vedere [Livelli di accessibilità](../../../csharp/language-reference/keywords/accessibility-levels.md).  Risulta tuttavia utile a volte limitare l'accesso a una di queste funzioni di accesso.  In genere, ciò implica la restrizione dell'accessibilità della funzione di accesso `set`, mantenendo pubblicamente accessibile la funzione di accesso `get`.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideIndexers#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/restricting-accessor-acc_1.cs)]  
  
 In questo esempio una proprietà denominata `Name` definisce le funzioni di accesso `get` e `set`.  La funzione di accesso `get` riceve il livello di accessibilità della proprietà stessa, in questo caso `public`, mentre la funzione di accesso `set` viene limitata in modo esplicito applicando il modificatore di accesso [protected](../../../csharp/language-reference/keywords/protected.md).  
  
## Restrizioni dei modificatori di accesso sulle funzioni di accesso  
 L'utilizzo dei modificatori delle funzioni di accesso per le proprietà o gli indicizzatori è soggetto alle seguenti condizioni:  
  
-   Non è possibile utilizzare i modificatori delle funzioni di accesso su un'interfaccia o su un'implementazione esplicita di un membro di [interfaccia](../../../csharp/language-reference/keywords/interface.md).  
  
-   È possibile utilizzare i modificatori delle funzioni di accesso solo se la proprietà o l'indicizzatore contiene entrambe le funzioni di accesso `set` e `get`.  In questo caso, il modificatore è consentito solo per una delle due funzioni di accesso.  
  
-   Se la proprietà o l'indicizzatore contiene un modificatore [override](../../../csharp/language-reference/keywords/override.md), il modificatore della funzione di accesso deve corrispondere alla funzione di accesso dell'eventuale funzione di accesso di cui è stato eseguito l'override.  
  
-   Il livello di accessibilità per la funzione di accesso deve essere più restrittivo di quello per la proprietà o per l'indicizzatore.  
  
## Modificatori di accesso per le funzioni di accesso di override  
 Quando si esegue l'override di una proprietà o di un indicizzatore, le funzioni di accesso sottoposte a override devono essere accessibili per il codice di override.  Il livello di accessibilità della proprietà\/indicizzatore e delle funzioni di accesso deve essere uguale a quello delle corrispondenti proprietà\/indicizzatore e funzioni di accesso sottoposte a override.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideIndexers#7](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/restricting-accessor-acc_2.cs)]  
  
## Implementazione di interfacce  
 Se utilizzata per implementare un'interfaccia, una funzione di accesso non può contenere un modificatore di accesso.  Se tuttavia l'interfaccia viene implementata utilizzando un'unica funzione di accesso, ad esempio `get`, l'altra funzione di accesso può contenere un modificatore, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideIndexers#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/restricting-accessor-acc_3.cs)]  
  
## Dominio di accessibilità delle funzioni di accesso  
 Se per la funzione di accesso si utilizza un modificatore di accesso, il [dominio di accessibilità](../../../csharp/language-reference/keywords/accessibility-domain.md) di tale funzione è determinato da questo modificatore.  
  
 Se per la funzione di accesso non si utilizza alcun modificatore di accesso, il dominio di accessibilità della funzione è determinato dal livello di accessibilità della proprietà o dell'indicizzatore.  
  
## Esempio  
 Nell'esempio seguente sono riportate tre classi, ovvero `BaseClass`, `DerivedClass` e `MainClass`.  La classe `BaseClass` contiene due proprietà, `Name` e `Id` in entrambe le classi.  Nell'esempio viene dimostrato che la proprietà `Id` della classe `DerivedClass` può essere nascosta dalla proprietà `Id` della classe `BaseClass` quando si utilizza un modificatore di accesso restrittivo come [protected](../../../csharp/language-reference/keywords/protected.md) o [private](../../../csharp/language-reference/keywords/private.md).  Di conseguenza, quando si assegnano valori a questa proprietà, viene invece chiamata la proprietà della classe `BaseClass`.  Se il modificatore di accesso viene sostituito con [public](../../../csharp/language-reference/keywords/public.md), la proprietà diventerà accessibile.  
  
 Nell'esempio viene inoltre dimostrato che un modificatore di accesso restrittivo, ad esempio `private` o `protected`, per la funzione di accesso `set` della proprietà `Name` nella classe `DerivedClass` impedisce l'accesso alla funzione di accesso e genera un errore quando vengono assegnati i valori.  
  
 [!code-cs[csProgGuideIndexers#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/restricting-accessor-acc_4.cs)]  
  
## Commenti  
 Se la dichiarazione `new private string Id` viene sostituita con `new public string Id`, si otterrà l'output:  
  
 `Name and ID in the base class: Name-BaseClass, ID-BaseClass`  
  
 `Name and ID in the derived class: John, John123`  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [Indicizzatori](../../../csharp/programming-guide/indexers/index.md)   
 [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)