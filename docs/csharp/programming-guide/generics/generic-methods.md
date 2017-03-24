---
title: "Metodi generici (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "generics [C#], metodi"
ms.assetid: 673eeea2-4b48-4faa-9c4e-2e89449221b9
caps.latest.revision: 27
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 27
---
# Metodi generici (Guida per programmatori C#)
I metodi generici sono metodi dichiarati con parametri di tipo, come illustrato di seguito:  
  
 [!code-cs[csProgGuideGenerics#22](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_1.cs)]  
  
 Nell'esempio di codice seguente viene illustrato un modo per chiamare il metodo utilizzando `int` come argomento di tipo:  
  
 [!code-cs[csProgGuideGenerics#23](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_2.cs)]  
  
 È anche possibile omettere l'argomento di tipo, che verrà dedotto dal compilatore.  La seguente chiamata a `Swap` è equivalente alla precedente:  
  
 [!code-cs[csProgGuideGenerics#24](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_3.cs)]  
  
 Le regole per l'inferenza dei tipi sono valide anche per i metodi statici e i metodi di istanza.  Il compilatore è in grado di dedurre i parametri di tipo in base agli argomenti del metodo passati, ma non unicamente da un vincolo o da un valore restituito,  pertanto l'inferenza dei tipi non funziona con metodi privi di parametri.  L'inferenza dei tipi si verifica in fase di compilazione, prima che il compilatore tenti di risolvere le firme del metodo di overload.  Il compilatore applica la logica dell'inferenza dei tipi a tutti i metodi generici che condividono lo stesso nome.  Nel passaggio di risoluzione dell'overload il compilatore include solo metodi generici per i quali l'inferenza dei tipi ha avuto esito positivo.  
  
 All'interno di una classe generica i metodi non generici possono accedere ai parametri di tipo a livello di classe, come illustrato di seguito:  
  
 [!code-cs[csProgGuideGenerics#25](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_4.cs)]  
  
 Se si definisce un metodo generico che accetta gli stessi parametri di tipo della classe che lo contiene, il compilatore genererà il messaggio di avviso CS0693 perché nell'ambito del metodo l'argomento fornito per il parametro `T` interno nasconderà quello specificato per il parametro `T` esterno.  Se è necessario disporre di maggiore flessibilità durante la chiamata a un metodo di classe generico con argomenti di tipo diversi da quelli forniti al momento della creazione di un'istanza della classe, è consigliabile specificare un altro identificatore per il parametro di tipo del metodo, come illustrato in `GenericList2<T>` nell'esempio seguente.  
  
 [!code-cs[csProgGuideGenerics#26](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_5.cs)]  
  
 Utilizzare i vincoli per consentire operazioni più specifiche sui parametri di tipo nei metodi.  Questa versione di `Swap<T>`, ora denominata `SwapIfGreater<T>`, può essere utilizzata solo con argomenti di tipo che implementino <xref:System.IComparable%601>.  
  
 [!code-cs[csProgGuideGenerics#27](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_6.cs)]  
  
 Per l'overload di metodi generici è possibile utilizzare diversi parametri di tipo.  Tutti i metodi riportati di seguito possono, ad esempio, risiedere nella stessa classe:  
  
 [!code-cs[csProgGuideGenerics#28](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-methods_7.cs)]  
  
## Specifiche del linguaggio C\#  
 Per ulteriori informazioni, vedere [Specifiche del linguaggio C\#](../../../csharp/language-reference/language-specification.md).  
  
## Vedere anche  
 <xref:System.Collections.Generic>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Introduzione ai generics](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)