---
title: Distruttori (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- ~ [C#], in destructors
- C# language, destructors
- destructors [C#]
ms.assetid: 1ae6e46d-a4b1-4a49-abe5-b97f53d9e049
caps.latest.revision: 24
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
ms.openlocfilehash: 6940be34b6cc15f006901e6d14d2a38ebb5d012a
ms.lasthandoff: 03/13/2017

---
# <a name="destructors-c-programming-guide"></a>Distruttori (Guida per programmatori C#)
I distruttori sono utilizzati per distruggere istanze di classi.  
  
## <a name="remarks"></a>Note  
  
-   I distruttori non possono essere definiti negli struct. Vengono usati solo con le classi.  
  
-   Una classe può avere un solo distruttore.  
  
-   I distruttori non possono essere ereditati e non è possibile eseguirne l'overload.  
  
-   I distruttori non possono essere chiamati. Vengono richiamati automaticamente.  
  
-   Un distruttore non accetta modificatori né parametri.  
  
 Ad esempio, di seguito è riportata la dichiarazione di un distruttore per la classe `Car`:  
  
 [!code-cs[csProgGuideObjects#86](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/destructors_1.cs)]  
  
 Il distruttore chiama in modo implicito il metodo <xref:System.Object.Finalize%2A> nella classe base dell'oggetto. Di conseguenza, il codice del distruttore riportato sopra viene convertito implicitamente nel codice seguente:  
  
```  
protected override void Finalize()  
{  
    try  
    {  
        // Cleanup statements...  
    }  
    finally  
    {  
        base.Finalize();  
    }  
}  
```  
  
 In questo modo, il metodo `Finalize` viene chiamato in modo ricorsivo per tutte le istanze nella catena di ereditarietà, dalla più derivata alla meno derivata.  
  
> [!NOTE]
>  Non usare distruttori vuoti. Quando una classe contiene un distruttore, viene creata una voce nella coda `Finalize`. Quando si chiama il distruttore, viene richiamato Garbage Collector per elaborare la coda. Se il distruttore è vuoto, si verifica semplicemente un calo di prestazioni.  
  
 Il programmatore non ha alcun controllo sul momento in cui viene chiamato il distruttore, poiché il momento è determinato dal Garbage Collector. Il Garbage Collector controlla gli oggetti che non vengono più usati dall'applicazione e, se considera un oggetto idoneo per l'eliminazione definitiva, chiama il distruttore (se presente) e recupera la memoria usata per archiviare l'oggetto. I distruttori vengono chiamati anche quando si esce dal programma.  
  
 Sebbene sia possibile forzare l'esecuzione di Garbage Collection chiamando <xref:System.GC.Collect%2A>, nella maggior parte dei casi è preferibile non effettuare questa operazione per evitare problemi di prestazioni.  
  
## <a name="using-destructors-to-release-resources"></a>Uso di distruttori per liberare risorse  
 In generale C# non richiede una gestione della memoria come quella necessaria quando si sviluppa con un linguaggio che non ha come destinazione un runtime con Garbage Collection. Il Garbage Collector di .NET Framework, infatti, gestisce in modo implicito l'allocazione e il rilascio di memoria per gli oggetti. Tuttavia, quando l'applicazione incapsula risorse non gestite come finestre, file e connessioni di rete, è necessario usare i distruttori per rendere disponibili tali risorse. Quando l'oggetto è idoneo per l'eliminazione definitiva, il Garbage Collector esegue il metodo `Finalize` dell'oggetto.  
  
## <a name="explicit-release-of-resources"></a>Rilascio esplicito di risorse  
 Se l'applicazione usa una risorsa esterna che consuma molta memoria, è consigliabile specificare un modo per rilasciare la risorsa in modo esplicito prima che il Garbage Collector renda disponibile l'oggetto. A questo scopo, è possibile implementare un metodo `Dispose` dall'interfaccia <xref:System.IDisposable> che esegua la pulitura necessaria per l'oggetto. Questo consente di migliorare notevolmente le prestazioni dell'applicazione. Nonostante questo controllo esplicito sulle risorse, il distruttore è un metodo efficace per salvaguardare la pulitura delle risorse nei casi in cui la chiamata al metodo `Dispose` non venga eseguita correttamente.  
  
 Per informazioni dettagliate sulla pulitura delle risorse, vedere gli argomenti seguenti:  
  
-   [Pulizia delle risorse non gestite](http://msdn.microsoft.com/library/a17b0066-71c2-4ba4-9822-8e19332fc213)  
  
-   [Implementazione di un metodo Dispose](http://msdn.microsoft.com/library/eb4e1af0-3b48-4fbc-ad4e-fc2f64138bf9)  
  
-   [Istruzione using](../../../csharp/language-reference/keywords/using-statement.md)  
  
## <a name="example"></a>Esempio  
 L'esempio seguente crea tre classi che costituiscono una catena di ereditarietà. La classe `First` è la classe base, `Second` è derivata da `First` e `Third` è derivata da `Second`. Tutte e tre le classi hanno dei distruttori. In `Main()` viene creata un'istanza della classe più derivata. Durante l'esecuzione del programma, si noti che i distruttori delle tre classi vengono chiamati automaticamente e in ordine, dalla classe più derivata alla meno derivata.  
  
 [!code-cs[csProgGuideObjects#85](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/destructors_2.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.IDisposable>   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [Garbage Collection](../../../standard/garbagecollection/index.md)
