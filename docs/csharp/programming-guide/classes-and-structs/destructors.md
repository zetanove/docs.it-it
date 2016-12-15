---
title: "Distruttori (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "~ [C#], nei distruttori"
  - "linguaggio C#, distruttori"
  - "distruttori [C#]"
ms.assetid: 1ae6e46d-a4b1-4a49-abe5-b97f53d9e049
caps.latest.revision: 24
caps.handback.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Distruttori (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

I distruttori sono utilizzati per distruggere istanze di classi.  
  
## Note  
  
-   I distruttori non possono essere definiti nelle strutture,  ma solamente nelle classi.  
  
-   Per una classe è possibile utilizzare un solo distruttore.  
  
-   I distruttori non possono essere ereditati e non è possibile eseguirne l'overload.  
  
-   I distruttori non possono essere chiamati.  Vengono richiamati automaticamente.  
  
-   Un distruttore non accetta modificatori né parametri.  
  
 Di seguito è riportato un esempio di dichiarazione di un distruttore per la classe `Car`:  
  
 [!code-cs[csProgGuideObjects#86](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/destructors_1.cs)]  
  
 Il distruttore chiama in modo implicito il metodo <xref:System.Object.Finalize%2A> sulla classe di base dell'oggetto.  Il codice del distruttore riportato sopra viene quindi convertito implicitamente nel codice seguente:  
  
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
>  Non utilizzare distruttori vuoti.  Quando una classe contiene un distruttore, viene creata una voce nella coda `Finalize`.  Quando si chiama il distruttore, viene richiamato Garbage Collector per elaborare la coda.  Se il distruttore è vuoto, si verifica semplicemente un calo di prestazioni.  
  
 Il programmatore non ha alcun controllo sul momento in cui il distruttore viene chiamato, poiché questa decisione dipende dal Garbage Collector.  Il Garbage Collector controlla gli oggetti che non vengono più utilizzati dall'applicazione e,  se considera un oggetto idoneo per la distruzione, chiama il distruttore \(se presente\) e recupera la memoria utilizzata per archiviare l'oggetto in questione.  I distruttori vengono chiamati anche quando si esce dal programma.  
  
 È possibile imporre l'esecuzione della Garbage Collection chiamando <xref:System.GC.Collect%2A>. Nella maggior parte dei casi, tuttavia, è preferibile non effettuare questa operazione per evitare potenziali problemi di prestazioni.  
  
## Utilizzo dei distruttori per liberare risorse  
 In generale in C\#  non sono necessarie le numerose attività di gestione della memoria richieste quando si sviluppa con un linguaggio che non ha come destinazione un runtime con Garbage Collection.  Il Garbage Collector di .NET Framework, infatti, gestisce in modo implicito l'allocazione e il rilascio di memoria per gli oggetti.  Tuttavia, quando l'applicazione incapsula risorse non gestite come finestre, file e connessioni di rete, è necessario utilizzare i distruttori per rendere disponibili tali risorse.  Quando l'oggetto può essere distrutto, il Garbage Collector esegue il metodo `Finalize` dell'oggetto.  
  
## Rilascio esplicito di risorse  
 Se l'applicazione utilizza una risorsa esterna che consuma molta memoria, si consiglia di fornire un modo per rilasciare la risorsa in modo esplicito prima che il Garbage Collector renda disponibile l'oggetto.  A questo scopo, è possibile implementare un metodo `Dispose` dall'interfaccia <xref:System.IDisposable> che esegua la pulitura necessaria per l'oggetto.  Questo consente di migliorare notevolmente le prestazioni dell'applicazione.  Nonostante questa possibilità di controllo esplicito sulle risorse, il distruttore è un metodo efficace per salvaguardare la pulitura delle risorse nei casi in cui la chiamata al metodo `Dispose` non venga eseguita correttamente.  
  
 Per ulteriori informazioni sulla pulitura delle risorse, vedere i seguenti argomenti:  
  
-   [Cleaning Up Unmanaged Resources](../Topic/Cleaning%20Up%20Unmanaged%20Resources.md)  
  
-   [Implementing a Dispose Method](../Topic/Implementing%20a%20Dispose%20Method.md)  
  
-   [Istruzione using](../../../csharp/language-reference/keywords/using-statement.md)  
  
## Esempio  
 Nell'esempio riportato di seguito vengono create tre classi che costituiscono una catena di ereditarietà.  La classe `First` è la classe base, `Second` è derivata da `First` e `Third` è derivata da `Second`.  Per tutte e tre le classi sono definiti dei distruttori.  In `Main()` viene creata un'istanza della classe più derivata.  Quando il programma viene eseguito, i distruttori delle tre classi vengono chiamati automaticamente e in ordine, dalla classe più derivata alla meno derivata.  
  
 [!code-cs[csProgGuideObjects#85](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/destructors_2.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 <xref:System.IDisposable>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [Garbage Collection](../Topic/Garbage%20Collection.md)