---
title: "Eccezioni generate dal compilatore (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "eccezioni [C#], generate dal compilatore"
ms.assetid: 53b52f97-b366-4ed7-b05b-9eb78096b7f9
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# Eccezioni generate dal compilatore (Guida per programmatori C#)
Alcune eccezioni vengono generate automaticamente da Common Language Runtime di .NET Framework quando si verificano errori durante l'esecuzione di operazioni di base.  Nella tabella riportata di seguito sono elencate queste eccezioni e le relative condizioni di errore.  
  
|Eccezione|Descrizione|  
|---------------|-----------------|  
|<xref:System.ArithmeticException>|Classe base per eccezioni che si verificano durante operazioni aritmetiche, quali <xref:System.DivideByZeroException> e <xref:System.OverflowException>.|  
|<xref:System.ArrayTypeMismatchException>|Generata quando una matrice non è in grado di archiviare un dato elemento perché il tipo effettivo dell'elemento è incompatibile con il tipo effettivo della matrice.|  
|<xref:System.DivideByZeroException>|Generata quando si tenta di dividere un valore integer per zero.|  
|<xref:System.IndexOutOfRangeException>|Generata quando si tenta di indicizzare una matrice e l'indice è inferiore a zero o esterno ai limiti della matrice.|  
|<xref:System.InvalidCastException>|Generata in caso di errore di una conversione esplicita di un tipo di base in un'interfaccia o in un tipo derivato in fase di esecuzione.|  
|<xref:System.NullReferenceException>|Generata quando si tenta di fare riferimento a un oggetto il cui valore è [null](../../../csharp/language-reference/keywords/null.md).|  
|<xref:System.OutOfMemoryException>|Generata quando il tentativo di allocare memoria utilizzando l'operatore [new](../../../csharp/language-reference/keywords/new-operator.md) ha esito negativo.  Indica che la memoria disponibile per Common Language Runtime è esaurita.|  
|<xref:System.OverflowException>|Generata in caso di overflow di un'operazione aritmetica in un contesto `checked`.|  
|<xref:System.StackOverflowException>|Generata quando lo stack di esecuzione si è esaurito in seguito a un numero eccessivo di chiamate a metodi in sospeso. È in genere indicativo di ricorsione molto profonda o infinita.|  
|<xref:System.TypeInitializationException>|Generata quando un costruttore statico genera un'eccezione e non esiste alcuna clausola `catch` compatibile per intercettarla.|  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Eccezioni e gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exceptions-and-exception-handling.md)   
 [Gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exception-handling.md)   
 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [try...finally](../../../csharp/language-reference/keywords/try-finally.md)   
 [try...catch...finally](../../../csharp/language-reference/keywords/try-catch-finally.md)