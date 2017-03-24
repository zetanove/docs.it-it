---
title: "var (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "var"
  - "var_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "var (parola chiave) [C#]"
ms.assetid: 0777850a-2691-4e3e-927f-0c850f5efe15
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# var (Riferimenti per C#)
A partire da Visual C\# 3.0, le variabili dichiarate in corrispondenza dell'ambito del metodo possono contenere un oggetto `var` di tipo implicito.  Una variabile locale implicitamente tipizzata è fortemente tipizzata come se si fosse dichiarato il tipo stesso, ma il compilatore determina il tipo.  Le due dichiarazioni seguenti di `i` sono funzionalmente equivalenti:  
  
```  
var i = 10; // implicitly typed  
int i = 10; //explicitly typed  
```  
  
 Per ulteriori informazioni, vedere [Variabili locali tipizzate in modo implicito](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md) e [Type Relationships in LINQ Query Operations](../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md).  
  
## Esempio  
 Nell'esempio seguente vengono illustrate due espressioni di query.  Nella prima espressione, l'utilizzo di `var` è consentito, ma non necessario, perché il tipo del risultato della query può essere dichiarato in modo esplicito come `IEnumerable<string>`.  Tuttavia, nella seconda espressione, `var` deve essere utilizzato, perché il risultato è una raccolta di tipi anonimi e il nome di tale tipo non è accessibile tranne che al compilatore stesso.  Si noti che nell'esempio n. 2, anche la variabile di iterazione `foreach``item` deve essere implicitamente tipizzata.  
  
 [!code-cs[csrefKeywordsTypes#18](../../../csharp/language-reference/keywords/codesnippet/CSharp/var_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Variabili locali tipizzate in modo implicito](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)