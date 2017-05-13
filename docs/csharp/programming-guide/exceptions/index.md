---
title: Eccezioni e gestione delle eccezioni (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- exception handling [C#]
- exceptions [C#]
- C# language, exceptions
ms.assetid: 0001887f-4fa2-47e2-8034-2819477e2344
caps.latest.revision: 33
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
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 561113241f7433d8e0f7f1f1f96f0338ebe81ae3
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="exceptions-and-exception-handling-c-programming-guide"></a>Eccezioni e gestione delle eccezioni (Guida per programmatori C#)
Le funzionalità di gestione delle eccezioni del linguaggio C# sono utili per gestire qualsiasi situazione imprevista o eccezionale che può verificarsi durante l'esecuzione di un programma. Per la gestione delle eccezioni vengono usate le parole chiave `try`, `catch` e `finally` per provare a eseguire azioni che potrebbero non riuscire, per gestire gli errori quando si decide che è ragionevole farlo e per pulire le risorse in un secondo momento. Le eccezioni possono essere generate da CLR (Common Language Runtime), da .NET Framework o qualsiasi libreria di terze parti o dal codice dell'applicazione. Per creare le eccezioni viene usata la parola chiave `throw`.  
  
 In molti casi, un'eccezione può essere generata non da un metodo che chiamato direttamente dal codice, ma da qualsiasi metodo più in basso nello stack di chiamate. In questo caso, CLR ripercorrerà lo stack alla ricerca di un metodo con un blocco `catch` per il tipo di eccezione specifico ed eseguirà il primo blocco `catch` trovato. Se non trova un blocco `catch` appropriato nello stack di chiamate, terminerà il processo e visualizzerà un messaggio all'utente.  
  
 In questo esempio, un metodo verifica la presenza di divisioni per zero e intercetta l'errore. Senza la gestione delle eccezioni, il programma verrebbe chiuso con un errore **DivideByZeroException non è stata gestita**.  
  
 [!code-cs[csProgGuideExceptions#18](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/exceptions-and-exception-handling_1.cs)]  
  
## <a name="exceptions-overview"></a>Panoramica delle eccezioni  
 Le eccezioni hanno le proprietà seguenti:  
  
-   Le eccezioni sono tipi che derivano fondamentalmente tutti da `System.Exception`.  
  
-   Racchiudere all'interno di un blocco `try` le istruzioni che potrebbero generare un'eccezione.  
  
-   Quando si verifica un'eccezione nel blocco `try`, il flusso di controllo passa al primo gestore delle eccezioni associato presente in qualsiasi punto nello stack di chiamate. In C#, per definire un gestore di eccezioni viene usata la parola chiave `catch`.  
  
-   Se non è presente alcun gestore di eccezioni per una determinata eccezione, il programma interrompe l'esecuzione con un messaggio di errore.  
  
-   Non intercettare un'eccezione a meno che non sia possibile gestirla e lasciare l'applicazione in uno stato noto. Se si intercetta `System.Exception`, generare di nuovo l'eccezione tramite la parola chiave `throw` alla fine del blocco `catch`.  
  
-   Se un blocco `catch` definisce una variabile di eccezione, è possibile usarla per ottenere altre informazioni sul tipo di eccezione che si è verificato.  
  
-   Le eccezioni possono essere generate in modo esplicito da un programma usando la parola chiave `throw`.  
  
-   Gli oggetti eccezione contengono informazioni dettagliate sull'errore, ad esempio lo stato dello stack di chiamate e una descrizione testuale dell'errore.  
  
-   Il codice in un blocco `finally` viene eseguito anche se viene generata un'eccezione. Usare un blocco `finally` per rilasciare le risorse, ad esempio per chiudere eventuali flussi o file aperti nel blocco `try`.  
  
-   Le eccezioni gestite in .NET Framework vengono implementate sulla base del meccanismo di gestione strutturata delle eccezioni in Win32. Per altre informazioni, vedere [Gestione strutturata delle eccezioni (C/C++)](https://docs.microsoft.com/cpp/cpp/structured-exception-handling-c-cpp) e [A Crash Course on the Depths of Win32 Structured Exception Handling](http://go.microsoft.com/fwlink/?LinkId=119654) (Corso intensivo su tutti i concetti fondamentali della gestione delle eccezioni strutturata in Win32).  
  
## <a name="related-sections"></a>Sezioni correlate  
 Per altre informazioni sulle eccezioni e la gestione delle eccezioni, vedere gli argomenti seguenti:  
  
-   [Uso delle eccezioni](../../../csharp/programming-guide/exceptions/using-exceptions.md)  
  
-   [Gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exception-handling.md)  
  
-   [Creazione e generazione di eccezioni](../../../csharp/programming-guide/exceptions/creating-and-throwing-exceptions.md)  
  
-   [Eccezioni generate dal compilatore](../../../csharp/programming-guide/exceptions/compiler-generated-exceptions.md)  
  
-   [Procedura: Gestire un'eccezione usando try-catch (Guida per programmatori C#)](../../../csharp/programming-guide/exceptions/how-to-handle-an-exception-using-try-catch.md)  
  
-   [Procedura: Eseguire codice di pulitura con finally](../../../csharp/programming-guide/exceptions/how-to-execute-cleanup-code-using-finally.md)  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.SystemException>   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [throw](../../../csharp/language-reference/keywords/throw.md)   
 [try-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [try-finally](../../../csharp/language-reference/keywords/try-finally.md)   
 [try-catch-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)   
 [Eccezioni](../../../standard/exceptions/index.md)   
 [Gerarchia delle eccezioni](http://msdn.microsoft.com/library/f7d68675-be06-40fb-a555-05f0c5a6f66b)   
 [Scrittura di codice .NET affidabile](http://go.microsoft.com/fwlink/?LinkId=112400)   
 [Minidump per eccezioni specifiche](http://go.microsoft.com/fwlink/?LinkId=112408)
