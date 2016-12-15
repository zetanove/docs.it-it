---
title: "abstract (Riferimenti per C#) | Microsoft Docs"
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
  - "abstract"
  - "abstract_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "abstract (parola chiave) [C#]"
ms.assetid: b0797770-c1f3-4b4d-9441-b9122602a6bb
caps.latest.revision: 24
caps.handback.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# abstract (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il modificatore `abstract` indica che l'implementazione dell'oggetto modificato è mancante o incompleta.  Il modificatore abstract può essere utilizzato con classi, metodi, proprietà, indicizzatori ed eventi.  Utilizzare il modificatore `abstract` in una dichiarazione di classe per indicare che una classe può essere utilizzata soltanto come classe base di altre classi.  I membri contrassegnati come astratti o inclusi in una classe astratta devono essere implementati da classi che derivano dalla classe astratta.  
  
## Esempio  
 Nell'esempio riportato di seguito, la classe `Square` deve fornire un'implementazione di `Area` poiché deriva da `ShapesClass`:  
  
 [!code-cs[csrefKeywordsModifiers#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/abstract_1.cs)]  
  
 Le classi astratte presentano le caratteristiche descritte di seguito.  
  
-   Non è possibile creare un'istanza di una classe astratta.  
  
-   Una classe astratta può contenere metodi e funzioni di accesso astratti.  
  
-   Non è possibile modificare una classe astratta con il modificatore [sealed](../../../csharp/language-reference/keywords/sealed.md) in quanto i due modificatori hanno significati opposti.  Il modificatore `sealed` impedisce a una classe di essere ereditata e il modificatore `abstract` richiede che una classe venga ereditata.  
  
-   Una classe non astratta derivata da una classe astratta deve includere le implementazioni effettive di tutti i metodi e le funzioni di accesso astratti ereditati.  
  
 Utilizzare il modificatore `abstract` nella dichiarazione di un metodo o di una proprietà per indicare che il metodo o la proprietà non contengono implementazioni.  
  
 I metodi astratti presentano le caratteristiche descritte di seguito.  
  
-   Un metodo astratto è in modo implicito un metodo virtuale.  
  
-   Le dichiarazioni dei metodi astratti possono essere utilizzate solo per le classi astratte.  
  
-   Poiché la dichiarazione di un metodo astratto non fornisce alcuna implementazione effettiva, non esiste un corpo del metodo. La dichiarazione del metodo termina semplicemente con un punto e virgola e dopo la firma non sono presenti parentesi graffe \({ }\).  Di seguito è riportato un esempio:  
  
    ```  
    public abstract void MyMethod();  
    ```  
  
     L'implementazione viene fornita da un metodo di overriding[override](../../../csharp/language-reference/keywords/override.md), che è membro di una classe non astratta.  
  
-   È errato utilizzare il modificatore [static](../../../csharp/language-reference/keywords/static.md) o [virtual](../../../csharp/language-reference/keywords/virtual.md) per la dichiarazione di un metodo astratto.  
  
 Le proprietà astratte hanno un comportamento analogo a quello dei metodi astratti, ma presentano delle differenze nella sintassi della dichiarazione e delle chiamate.  
  
-   È errato utilizzare il modificatore `abstract` per una proprietà statica.  
  
-   È possibile sottoporre a override una proprietà astratta ereditata in una classe derivata includendo una dichiarazione di proprietà che utilizza il modificatore [override](../../../csharp/language-reference/keywords/override.md).  
  
 Per ulteriori informazioni sulle classi astratte, vedere [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md).  
  
 Una classe astratta deve fornire l'implementazione per tutti i membri di interfaccia.  
  
 La classe astratta che implementa un'interfaccia può associare i metodi di interfaccia a metodi astratti.  Di seguito è riportato un esempio:  
  
 [!code-cs[csrefKeywordsModifiers#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/abstract_2.cs)]  
  
## Esempio  
 In questo esempio la classe `DerivedClass` deriva da una classe astratta `BaseClass`.  La classe astratta contiene il metodo astratto `AbstractMethod` e le due proprietà astratte `X` e `Y`.  
  
 [!code-cs[csrefKeywordsModifiers#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/abstract_3.cs)]  
  
 Nell'esempio precedente, se si tenta di creare un'istanza per la classe astratta tramite una dichiarazione di questo tipo:  
  
```  
BaseClass bc = new BaseClass();   // Error  
```  
  
 si otterrà un errore che indica che il compilatore non può creare un'istanza della classe astratta 'BaseClass'.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)   
 [virtuale](../../../csharp/language-reference/keywords/virtual.md)   
 [override](../../../csharp/language-reference/keywords/override.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)