---
title: "Procedura: utilizzare l&#39;overload degli operatori per creare una classe di numeri complessi (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "classi [C#], overload di operatori"
  - "numeri complessi [C#]"
  - "overload degli operatori [C#], numeri complessi"
  - "overload degli operatori [C#], utilizzo per creare classi"
  - "operatori [C#], overload per creare una classe di numeri complessi"
ms.assetid: c9b8d982-5112-413f-bae3-b42ae3248ddf
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# Procedura: utilizzare l&#39;overload degli operatori per creare una classe di numeri complessi (Guida per programmatori C#)
Questo esempio illustra come è possibile utilizzare l'overload dell'operatore per creare una classe di numeri complessi `Complex` che definisce l'operazione di addizione tra numeri complessi.  Il programma visualizza le parti immaginaria e reale dei numeri nonché il risultato dell'addizione mediante un override del metodo `ToString`.  
  
## Esempio  
 [!code-cs[csProgGuideStatements#16](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-operator-overloading-to-create-a-complex-number-class_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)   
 [operatore](../../../csharp/language-reference/keywords/operator.md)   
 [Perché gli operatori di overload sono sempre statici in C\#?](http://go.microsoft.com/fwlink/?LinkId=112383)