---
title: "Delegati con metodi denominati e anonimi (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "delegati [C#], con metodi denominati e anonimi"
  - "metodi [C#], in delegati"
ms.assetid: 98fa8c61-66b6-4146-986c-3236c4045733
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# Delegati con metodi denominati e anonimi (Guida per programmatori C#)
È possibile associare un [delegato](../../../csharp/language-reference/keywords/delegate.md) a un metodo denominato.  Quando si crea un'istanza di un delegato utilizzando un metodo denominato, il metodo viene passato come parametro, come nell'esempio seguente:  
  
 [!code-cs[csProgGuideDelegates#1](../../../csharp/programming-guide/delegates/codesnippet/CSharp/delegates-with-named-vs-anonymous-methods_1.cs)]  
  
 Questa operazione corrisponde a utilizzare un metodo denominato.  I delegati costruiti con un metodo denominato possono incapsulare un metodo [statico](../../../csharp/language-reference/keywords/static.md) o un metodo di istanza.  I metodi denominati rappresentano l'unico modo per creare un'istanza di un delegato nelle versioni precedenti di C\#.  In una situazione in cui la creazione di un nuovo metodo rappresenta un sovraccarico inutile, C\# consente di creare un'istanza di un delegato e di specificare immediatamente un blocco di codice che verrà elaborato dal delegato al momento della chiamata.  Il blocco può contenere un'espressione lambda oppure un metodo anonimo.  Per ulteriori informazioni, vedere [Funzioni anonime](../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md).  
  
## Note  
 La firma del metodo che viene passato come parametro di delegato deve essere identica a quella della dichiarazione del delegato.  
  
 Un'istanza di delegato può incapsulare un metodo statico o un metodo di istanza.  
  
 Sebbene il delegato possa utilizzare un parametro [out](../../../csharp/language-reference/keywords/out.md), è consigliabile non utilizzarlo con delegati di eventi multicast perché non è possibile sapere quale delegato verrà chiamato.  
  
## Esempio 1  
 Di seguito è illustrato un semplice esempio di dichiarazione e utilizzo di un delegato.  Si noti che sia il delegato `Del` che il metodo associato `MultiplyNumbers` presentano la stessa firma.  
  
 [!code-cs[csProgGuideDelegates#2](../../../csharp/programming-guide/delegates/codesnippet/CSharp/delegates-with-named-vs-anonymous-methods_2.cs)]  
  
## Esempio 2  
 Nell'esempio che segue un delegato viene associato a metodi static e di istanza e restituisce informazioni specifiche da ciascuno di essi.  
  
 [!code-cs[csProgGuideDelegates#3](../../../csharp/programming-guide/delegates/codesnippet/CSharp/delegates-with-named-vs-anonymous-methods_3.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)   
 [Metodi anonimi](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)   
 [Procedura: combinare delegati multicast](../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)