---
title: "Procedura: scrivere un costruttore di copia (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "Linguaggio C#, costruttore di copia"
  - "costruttore di copia [C#]"
ms.assetid: fba899b5-fc41-428e-a745-3ebdbf37990a
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# Procedura: scrivere un costruttore di copia (Guida per programmatori C#)
C\# non fornisce un costruttore di copia per gli oggetti, tuttavia è possibile scriverne uno manualmente.  
  
## Esempio  
 Nell'esempio seguente, nella [classe](../../../csharp/language-reference/keywords/class.md) `Person` viene definito un costruttore di copia che accetta come argomento un'istanza di `Person`.  I valori delle proprietà dell'argomento vengono assegnati alle proprietà della nuova istanza di `Person`.  Il codice contiene un costruttore di copia alternativo che invia le proprietà `Name` e `Age` dell'istanza che si desidera copiare al costruttore di istanza della classe.  
  
 [!code-cs[csProgGuideObjects#16](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-write-a-copy-cons_1.cs)]  
  
## Vedere anche  
 <xref:System.ICloneable>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [Distruttori](../../../csharp/programming-guide/classes-and-structs/destructors.md)