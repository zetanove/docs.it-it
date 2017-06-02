---
title: abstract (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- abstract
- abstract_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- abstract keyword [C#]
ms.assetid: b0797770-c1f3-4b4d-9441-b9122602a6bb
caps.latest.revision: 24
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: acb9c5748addd75f741e97688fca707910b042a0
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="abstract-c-reference"></a>abstract (Riferimenti per C#)
Il modificatore `abstract` indica che l'oggetto in fase di modifica ha un'implementazione mancante o incompleta. Il modificatore abstract può essere usato con classi, metodi, proprietà, indicizzatori ed eventi. Usare il modificatore `abstract` in una dichiarazione di classe per indicare che una classe verrà usata solo come classe di base per altre classi. I membri contrassegnati come astratti o inclusi in una classe astratta devono essere implementati dalle classi che derivano dalla classe astratta.  
  
## <a name="example"></a>Esempio  
 In questo esempio, la classe `Square` deve eseguire un'implementazione di `Area` poiché deriva da `ShapesClass`:  
  
 [!code-cs[csrefKeywordsModifiers#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/abstract_1.cs)]  
  
 Le classi astratte hanno le caratteristiche seguenti:  
  
-   Non è possibile creare un'istanza di una classe astratta.  
  
-   Una classe astratta può contenere funzioni di accesso e metodi astratti.  
  
-   Non è possibile modificare una classe astratta con il modificatore [sealed](../../../csharp/language-reference/keywords/sealed.md) perché i due modificatori hanno significati opposti. Il modificatore `sealed` impedisce a una classe che venga ereditata e il modificatore `abstract` richiede una classe da ereditare.  
  
-   Una classe non astratta derivata da una classe astratta deve includere implementazioni effettive di tutte le funzioni di accesso e di tutti i metodi astratti ereditati.  
  
 Usare il modificatore `abstract` in una dichiarazione di metodo o proprietà per indicare che il metodo o proprietà non contiene implementazioni.  
  
 I metodi astratti hanno le caratteristiche seguenti:  
  
-   Un metodo astratto è implicitamente un metodo virtuale.  
  
-   Le dichiarazioni di metodi astratti sono consentite solo in classi astratte.  
  
-   Poiché una dichiarazione di un metodo astratto non offre alcuna implementazione effettiva, non c'è nessun corpo del metodo. La dichiarazione del metodo termina semplicemente con un punto e virgola e non ci sono parentesi graffe ({ }) dopo la firma. Ad esempio:  
  
    ```  
    public abstract void MyMethod();  
    ```  
  
     L'implementazione viene specificata da un metodo di [override](../../../csharp/language-reference/keywords/override.md), che è un membro di una classe non astratta.  
  
-   Non è possibile usare il modificatore [static](../../../csharp/language-reference/keywords/static.md) o [virtual](../../../csharp/language-reference/keywords/virtual.md) in una dichiarazione di un metodo astratto.  
  
 Le proprietà astratte si comportano come i metodi astratti, ad eccezione delle differenze nella sintassi di dichiarazione e di chiamata.  
  
-   Non è possibile usare il modificatore `abstract` su una proprietà static.  
  
-   Una proprietà astratta ereditata può essere sottoposta a override in una classe derivata includendo una dichiarazione di proprietà che usa il modificatore di [override](../../../csharp/language-reference/keywords/override.md).  
  
 Per altre informazioni sulle classi astratte, vedere [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md).  
  
 Una classe astratta deve specificare l'implementazione per tutti i membri di interfaccia.  
  
 Una classe astratta che implementa un'interfaccia può eseguire il mapping dei metodi di interfaccia su metodi astratti. Ad esempio:  
  
 [!code-cs[csrefKeywordsModifiers#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/abstract_2.cs)]  
  
## <a name="example"></a>Esempio  
 In questo esempio, la classe `DerivedClass` è derivata da una classe di base astratta `BaseClass`. La classe astratta contiene un metodo astratto, `AbstractMethod`, e due proprietà astratte, `X` e `Y`.  
  
 [!code-cs[csrefKeywordsModifiers#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/abstract_3.cs)]  
  
 Nell'esempio precedente, se si prova a creare un'istanza della classe astratta tramite un'istruzione simile alla seguente:  
  
```  
BaseClass bc = new BaseClass();   // Error  
```  
  
 si otterrà un errore che informa che il compilatore non può creare un'istanza della classe astratta "BaseClass".  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)   
 [virtual](../../../csharp/language-reference/keywords/virtual.md)   
 [override](../../../csharp/language-reference/keywords/override.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)
