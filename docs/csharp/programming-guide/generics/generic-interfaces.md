---
title: "Interfacce generiche (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, interfacce generiche"
  - "generics [C#], interfacce"
ms.assetid: a8fa49a1-6e78-4a09-87e5-84a0b9f5ffbe
caps.latest.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 28
---
# Interfacce generiche (Guida per programmatori C#)
Risulta spesso utile definire interfacce per classi di raccolte generiche o per le classi generiche che rappresentano gli elementi della raccolta.  Con le classi generiche è preferibile utilizzare interfacce generiche, ad esempio <xref:System.IComparable%601>, anziché <xref:System.IComparable>, per evitare operazioni di boxing e unboxing sui tipi valore.  Nella libreria di classi .NET Framework vengono definite numerose interfacce generiche da utilizzare con le classi di raccolte nello spazio dei nomi <xref:System.Collections.Generic>.  
  
 Quando un'interfaccia viene specificata come vincolo su un parametro di tipo, è possibile utilizzare esclusivamente tipi che implementano l'interfaccia.  Nell'esempio di codice riportato di seguito viene illustrata una classe `SortedList<T>` che deriva dalla classe `GenericList<T>`.  Per ulteriori informazioni, vedere [Introduzione ai generics](../../../csharp/programming-guide/generics/introduction-to-generics.md).  `SortedList<T>` aggiunge il vincolo `where T : IComparable<T>`.  In questo modo, il metodo `BubbleSort` in `SortedList<T>` utilizzerà il metodo <xref:System.IComparable%601.CompareTo%2A> generico su elementi dell'elenco.  Nell'esempio riportato di seguito, gli elementi dell'elenco sono una classe semplice, `Person`, che implementa `IComparable<Person>`.  
  
 [!code-cs[csProgGuideGenerics#29](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-interfaces_1.cs)]  
  
 È possibile specificare più interfacce come vincoli su un solo tipo, come riportato di seguito:  
  
 [!code-cs[csProgGuideGenerics#30](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-interfaces_2.cs)]  
  
 Un'interfaccia può definire più parametri di tipo, come riportato di seguito:  
  
 [!code-cs[csProgGuideGenerics#31](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-interfaces_3.cs)]  
  
 Le regole di ereditarietà valgono sia per le interfacce che per le classi:  
  
 [!code-cs[csProgGuideGenerics#32](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-interfaces_4.cs)]  
  
 Le interfacce generiche possono ereditare da interfacce non generiche se l'interfaccia generica è controvariante, ovvero se utilizza esclusivamente il relativo parametro di tipo come valore restituito.  Nella libreria di classi .NET Framework <xref:System.Collections.Generic.IEnumerable%601> eredita da <xref:System.Collections.IEnumerable> poiché <xref:System.Collections.Generic.IEnumerable%601> utilizza esclusivamente `T` nel valore restituito di <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> e nella proprietà Get <xref:System.Collections.Generic.IEnumerator%601.Current%2A>.  
  
 Le classi concrete possono implementare interfacce costruite chiuse, come riportato di seguito:  
  
 [!code-cs[csProgGuideGenerics#33](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-interfaces_5.cs)]  
  
 Le classi generiche possono implementare interfacce generiche oppure interfacce costruite chiuse purché l'elenco di parametri di classi fornisca tutti gli argomenti necessari all'interfaccia, come riportato di seguito:  
  
 [!code-cs[csProgGuideGenerics#34](../../../csharp/programming-guide/generics/codesnippet/csharp/generic-interfaces_6.cs)]  
  
 Le regole che controllano l'overload dei metodi sono identiche per i metodi all'interno di classi generiche, strutture generiche o interfacce generiche.  Per ulteriori informazioni, vedere [Metodi generici](../../../csharp/programming-guide/generics/generic-methods.md).  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Introduzione ai generics](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [interfaccia](../../../csharp/language-reference/keywords/interface.md)   
 [Generics](../Topic/Generics%20in%20the%20.NET%20Framework.md)