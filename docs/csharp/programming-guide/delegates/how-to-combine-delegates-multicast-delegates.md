---
title: "Procedura: combinare delegati multicast (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "delegati [C#], combinazione"
  - "delegati multicast [C#]"
ms.assetid: 4e689450-6d0c-46de-acfd-f961018ae5dd
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# Procedura: combinare delegati multicast (Guida per programmatori C#)
In questo esempio viene illustrato come creare delegati multicast.  Gli oggetti [delegati](../../../csharp/language-reference/keywords/delegate.md) risultano particolarmente utili in quanto più oggetti possono essere assegnati a un'unica istanza del delegato utilizzando l'operatore `+`.  Il delegato multicast contiene un elenco dei delegati assegnati.  Quando il delegato multicast viene chiamato, richiama i delegati nell'elenco, in ordine.  È possibile combinare solo delegati dello stesso tipo.  
  
 È possibile utilizzare l'operatore `-` per rimuovere un delegato componente da un delegato multicast.  
  
## Esempio  
 [!code-cs[csProgGuideDelegates#11](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#11)]  
  
## Vedere anche  
 <xref:System.MulticastDelegate>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)