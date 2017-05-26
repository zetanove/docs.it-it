---
title: 'Procedura: dichiarare un delegato, crearne un&quot;istanza e usarlo (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- delegates [C#], declaring and instantiating
ms.assetid: 61c4895f-f785-48f8-8bfe-db73b411c4ae
caps.latest.revision: 21
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
ms.sourcegitcommit: a780a11d8dd238187eb82933359bbb151bb3c333
ms.openlocfilehash: f80f50d7d6630aa5738c077cc2f278993e792eb8
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-declare-instantiate-and-use-a-delegate-c-programming-guide"></a>Procedura: dichiarare un delegato, crearne un'istanza e utilizzarlo (Guida per programmatori C#)
In C# 1.0 e versioni successive i delegati possono essere dichiarati come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideDelegates#13](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_1.cs)]  
  
 [!code-cs[csProgGuideDelegates#14](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_2.cs)]  
  
 In C# 2.0 è disponibile un metodo più semplice per scrivere la dichiarazione precedente, come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideDelegates#32](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_3.cs)]  
  
 In C# 2.0 e versioni successive, è anche possibile usare un metodo anonimo per dichiarare e inizializzare un [delegato](../../../csharp/language-reference/keywords/delegate.md), come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideDelegates#15](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_4.cs)]  
  
 In C# 3.0 e versioni successive, è inoltre possibile dichiarare i delegati e crearne un'istanza usando un'espressione lambda, come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideDelegates#31](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_5.cs)]  
  
 Per altre informazioni, vedere [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
 Nell'esempio che segue viene illustrato come dichiarare un delegato, crearne un'istanza e usarlo. La classe `BookDB` incapsula il database di una libreria che gestisce un database di volumi. Espone un metodo, `ProcessPaperbackBooks`, che ricerca tutti i tascabili all'interno del database e chiama un delegato per ciascuno di essi. Il tipo `delegate` usato viene denominato `ProcessBookDelegate`. La classe `Test` usa questa classe per stampare i titoli e il prezzo medio dei tascabili.  
  
 L'uso dei delegati consente la separazione ottimale delle funzionalità tra il database della libreria e il codice client. Il codice client non contiene alcuna informazione sulle modalità di archiviazione dei libri o sul meccanismo che consente al codice di individuare i tascabili. Il codice della libreria non contiene alcuna informazione sull'elaborazione effettuata sui tascabili individuati.  
  
## <a name="example"></a>Esempio  
 [!code-cs[csProgGuideDelegates#12](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_6.cs)]  
  
## <a name="robust-programming"></a>Programmazione efficiente  
  
-   Dichiarazione di un delegato.  
  
     L'istruzione seguente dichiara un nuovo tipo di delegato.  
  
     [!code-cs[csProgGuideDelegates#16](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_7.cs)]  
  
     Ogni tipo di delegato descrive il numero e il tipo degli argomenti e il tipo di valore restituito dai metodi in esso incapsulati. Ogni volta che è necessario un nuovo set di tipi di argomento o un nuovo tipo di valore restituito, è necessario dichiarare un nuovo tipo di delegato.  
  
-   Creazione di un'istanza di un delegato.  
  
     Dopo aver dichiarato un tipo delegato, è necessario creare un oggetto delegato e associarlo a un determinato metodo. Nell'esempio precedente questa operazione viene eseguita passando il metodo `PrintTitle` al metodo `ProcessPaperbackBooks`, come illustrato nell'esempio seguente:  
  
     [!code-cs[csProgGuideDelegates#17](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_8.cs)]  
  
     In questo modo viene creato un nuovo oggetto delegato associato al metodo [statico](../../../csharp/language-reference/keywords/static.md) `Test.PrintTitle`. Analogamente, il metodo non statico `AddBookToTotal` dell'oggetto `totaller` viene passato come illustrato nell'esempio seguente:  
  
     [!code-cs[csProgGuideDelegates#18](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_9.cs)]  
  
     In entrambi i casi, al metodo `ProcessPaperbackBooks` viene passato un nuovo oggetto delegato.  
  
     Dopo la creazione di un delegato, il metodo ad esso associato non viene mai modificato, poiché gli oggetti delegati non sono modificabili.  
  
-   Chiamata a un delegato.  
  
     Una volta creato, un oggetto delegato viene in genere passato a un altro codice che chiamerà il delegato. Per la chiamata di un oggetto delegato viene usato il nome dell'oggetto stesso, seguito dagli argomenti, racchiusi tra parentesi, che devono essere passati al delegato. Di seguito viene riportato un esempio di chiamata a un delegato:  
  
     [!code-cs[csProgGuideDelegates#19](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_10.cs)]  
  
     Un delegato può essere chiamato in modo sincrono, come in questo esempio, oppure in modo asincrono usando i metodi `BeginInvoke` e `EndInvoke`.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)
