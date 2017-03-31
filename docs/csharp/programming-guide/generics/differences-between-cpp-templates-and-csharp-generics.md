---
title: Differenze tra modelli C++ e generics C# (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- generics [C#], vs. C++ templates
ms.assetid: 1da6beeb-d4a4-4da0-87b7-0cfbe04920b7
caps.latest.revision: 14
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
ms.openlocfilehash: d3171b1e3f48907778be6e256780e06bad36481f
ms.lasthandoff: 03/13/2017

---
# <a name="differences-between-c-templates-and-c-generics-c-programming-guide"></a>Differenze tra modelli C++ e generics C# (Guida per programmatori C#)
I generics C# e i modelli C++ sono entrambi funzionalità del linguaggio che offrono il supporto per i tipi con parametri. Esistono tuttavia numerose differenze tra queste due funzionalità. A livello di sintassi, i generics C# rappresentano un approccio più semplice ai tipi con parametri, senza la complessità dei modelli C++. Inoltre, il linguaggio C# non è stato concepito per offrire tutte le funzionalità dei modelli C++. A livello di implementazione, la differenza principale consiste nel fatto che le sostituzioni di tipi generici C# vengono eseguite durante il runtime e, di conseguenza, le informazioni sui tipi generici vengono mantenute per gli oggetti di cui viene creata un'istanza. Per altre informazioni, vedere [Generics nel runtime](../../../csharp/programming-guide/generics/generics-in-the-run-time.md).  
  
 Di seguito sono riportate le differenze principali tra generics C# e modelli C++:  
  
-   I generics C# non offrono lo stesso livello di flessibilità dei modelli C++. Ad esempio non è possibile chiamare operatori aritmetici in una classe generica C#, anche se è possibile chiamare operatori definiti dall'utente.  
  
-   C# non consente di usare parametri di modello non di tipo, ad esempio `template C<int i> {}`.  
  
-   C# non supporta la specializzazione esplicita, ovvero un'implementazione personalizzata di un modello per un tipo specifico.  
  
-   C# non supporta la specializzazione parziale, ovvero un'implementazione personalizzata per un subset degli argomenti del tipo.  
  
-   C# non consente l'uso del parametro di tipo come classe base per il tipo generico.  
  
-   C# non consente l'uso di tipi predefiniti per i parametri di tipo.  
  
-   In C# un parametro di tipo generico non può essere di per sé un elemento generico, anche se i tipi costruiti possono essere usati come generics. C++ non consente l'uso di parametri di modello.  
  
-   C++ consente di usare codice che potrebbe non essere valido per tutti i parametri di tipo nel modello, che viene quindi controllato per verificare la disponibilità del tipo specifico usato come parametro di tipo. In C# il codice di una classe deve essere scritto in modo da funzionare con qualsiasi tipo in grado di soddisfare i vincoli. Ad esempio, in C++ è possibile scrivere una funzione che usa gli operatori aritmetici `+` e `-` sugli oggetti del parametro di tipo, generando un errore al momento della creazione di un'istanza del modello con un tipo che non supporta gli operatori. In C# questo non è possibile. Gli unici costrutti di linguaggio ammessi sono quelli deducibili dai vincoli.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Introduzione ai generics](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [Modelli](https://docs.microsoft.com/cpp/cpp/templates-cpp)
