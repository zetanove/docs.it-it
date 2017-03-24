---
title: "sealed (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "sealed"
  - "sealed_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "sealed (parola chiave) [C#]"
ms.assetid: 8e4ed5d3-10be-47db-9488-0da2008e6f3f
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# sealed (Riferimenti per C#)
Quando viene applicato a una classe, il modificatore `sealed` impedisce ad altre classi di ereditare da tale classe.  Nell'esempio riportato di seguito, la classe `B` eredita dalla classe `A`, ma nessuna classe può ereditare dalla classe `B`.  
  
```  
class A {}      
sealed class B : A {}  
```  
  
 È anche possibile utilizzare il modificatore `sealed` su un metodo o una proprietà che esegue l'override di un metodo o una proprietà virtuale in una classe di base.  In questo modo è possibile consentire alle classi di derivare dalla classe in questione pur impedendone l'override di metodi o proprietà virtuali.  
  
## Esempio  
 Nell'esempio riportato di seguito, `Z` eredita da `Y` ma `Z` non può eseguire l'override della funzione virtuale `F` dichiarata in `X` e contrassegnata come sealed in `Y`.  
  
 [!code-cs[csrefKeywordsModifiers#16](../../../csharp/language-reference/keywords/codesnippet/CSharp/sealed_1.cs)]  
  
 Quando si definiscono metodi o proprietà nuove in una classe, è possibile impedire alle classi derivate di eseguire l'override non dichiarandole [virtual](../../../csharp/language-reference/keywords/virtual.md).  
  
 L'utilizzo del modificatore [abstract](../../../csharp/language-reference/keywords/abstract.md) con una classe sealed è un errore, in quanto una classe abstract deve essere ereditata da una classe che fornisce un'implementazione di metodi o proprietà abstract.  
  
 Se applicato a un metodo o a una proprietà, il modificatore `sealed` deve essere sempre utilizzato con [override](../../../csharp/language-reference/keywords/override.md).  
  
 Poiché le strutture sono implicitamente sealed, non possono essere ereditate.  
  
 Per ulteriori informazioni, vedere [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md).  
  
 Per ulteriori esempi, vedere [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md).  
  
## Esempio  
 [!code-cs[csrefKeywordsModifiers#17](../../../csharp/language-reference/keywords/codesnippet/CSharp/sealed_2.cs)]  
  
 Nell'esempio riportato in precedenza, se si tentasse di ereditare dalla classe sealed utilizzando l'istruzione seguente:  
  
 `class MyDerivedC: SealedClass {}   // Error`  
  
 verrebbe restituito un messaggio di errore:  
  
 `'MyDerivedC' cannot inherit from sealed class 'SealedClass'.`  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Note  
 Per determinare se contrassegnare come sealed una classe, un metodo o una proprietà, è in genere opportuno considerare i due punti seguenti:  
  
-   I vantaggi potenziali dati dalla possibilità di personalizzare la classe grazie alla derivazione di classi.  
  
-   La possibilità che la derivazione di classi modifichi le classi in modo da impedirne il funzionamento corretto o previsto.  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)   
 [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)   
 [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)   
 [override](../../../csharp/language-reference/keywords/override.md)   
 [virtuale](../../../csharp/language-reference/keywords/virtual.md)