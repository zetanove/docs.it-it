---
title: Eccezioni generate dal compilatore (Guida per programmatori C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- exceptions [C#], compiler-generated
ms.assetid: 53b52f97-b366-4ed7-b05b-9eb78096b7f9
caps.latest.revision: 13
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 4015551ac983610afc8bf1f08e73a33c1ac338ff
ms.lasthandoff: 03/13/2017

---
# <a name="compiler-generated-exceptions-c-programming-guide"></a>Eccezioni generate dal compilatore (Guida per programmatori C#)
Alcune eccezioni vengono generate automaticamente da Common Language Runtime (CLR) di .NET Framework quando le operazioni di base hanno esito negativo. Nella tabella seguente sono elencate queste eccezioni e le relative condizioni di errore.  
  
|Eccezione|Descrizione|  
|---------------|-----------------|  
|<xref:System.ArithmeticException>|Una classe di base per le eccezioni che si verificano durante operazioni aritmetiche, quali <xref:System.DivideByZeroException> e <xref:System.OverflowException>.|  
|<xref:System.ArrayTypeMismatchException>|Generata quando una matrice non può archiviare un determinato elemento perché il tipo effettivo dell'elemento non è compatibile con il tipo effettivo della matrice.|  
|<xref:System.DivideByZeroException>|Generata quando viene eseguito un tentativo di dividere un valore integrale per zero.|  
|<xref:System.IndexOutOfRangeException>|Generata quando viene eseguito un tentativo di indicizzare una matrice, quando l'indice è minore di zero o supera i limiti della matrice.|  
|<xref:System.InvalidCastException>|Generata quando una conversione esplicita dal tipo di base a un'interfaccia o a un tipo derivato ha esito negativo in fase di runtime.|  
|<xref:System.NullReferenceException>|Generata quando si tenta di fare riferimento a un oggetto il cui valore è [null](../../../csharp/language-reference/keywords/null.md).|  
|<xref:System.OutOfMemoryException>|Generata quando un tentativo di allocazione della memoria tramite l'operatore [new](../../../csharp/language-reference/keywords/new-operator.md) ha esito negativo. Ciò indica che è stata esaurita la memoria disponibile per Common Language Runtime.|  
|<xref:System.OverflowException>|Generata quando si verifica un overflow di un'operazione aritmetica in un contesto `checked`.|  
|<xref:System.StackOverflowException>|Generata quando viene esaurito lo stack di esecuzione da un numero eccessivo di chiamate in sospeso verso il metodo; in genere indica un problema di ricorsione molto profondo o infinito.|  
|<xref:System.TypeInitializationException>|Generata quando un costruttore statico genera un'eccezione e non è presente una clausola `catch` compatibile per intercettarla.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Eccezioni e gestione delle eccezioni](../../../csharp/programming-guide/exceptions/index.md)   
 [Gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exception-handling.md)   
 [try-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [try-finally](../../../csharp/language-reference/keywords/try-finally.md)   
 [try-catch-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)
