---
title: "base (Riferimenti per C#) | Microsoft Docs"
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
  - "base"
  - "BaseClass.BaseClass"
  - "base_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "base (parola chiave) [C#]"
ms.assetid: 8b645dbe-1a33-49b8-8716-1c401f9a5ea5
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# base (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La parola chiave `base` viene utilizzata per accedere ai membri della classe base dall'interno di una classe derivata per:  
  
-   chiamare un metodo nella classe base sottoposto a override da un altro metodo;  
  
-   specificare quale costruttore della classe base dovrà essere chiamato per creare istanze della classe derivata.  
  
 L'accesso a una classe base è consentito solo in un costruttore, in un metodo di istanza o in una funzione di accesso alle proprietà delle istanze.  
  
 È errato utilizzare la parola chiave `base` all'interno di un metodo statico.  
  
 La classe base a cui si accede è la classe base specificata nella dichiarazione della classe.  Ad esempio, se si specifica `class ClassB : ClassA`, l'accesso ai membri di ClassA viene eseguito da ClassB, indipendentemente dalla classe base di ClassA.  
  
## Esempio  
 In questo esempio sia la classe base `Person` che la classe derivata `Employee` utilizzano un metodo denominato `Getinfo`.  Mediante la parola chiave `base` è possibile chiamare il metodo `Getinfo` nella classe base dall'interno della classe derivata.  
  
 [!code-cs[csrefKeywordsAccess#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/base_1.cs)]  
  
 Per ulteriori esempi, vedere [new](../../../csharp/language-reference/keywords/new.md), [virtual](../../../csharp/language-reference/keywords/virtual.md) e [override](../../../csharp/language-reference/keywords/override.md).  
  
## Esempio  
 In questo esempio viene illustrato come specificare il costruttore della classe base che verrà chiamato durante la creazione di istanze di una classe derivata.  
  
 [!code-cs[csrefKeywordsAccess#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/base_2.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [this](../../../csharp/language-reference/keywords/this.md)