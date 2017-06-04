---
title: "How to: Iterate File Directories with PLINQ | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "PLINQ queries, how to iterate directories"
ms.assetid: 354e8ce3-35c4-431c-99ca-7661d1f3901b
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Iterate File Directories with PLINQ
In questo esempio vengono illustrati due semplici modi di parallelizzare le operazioni nelle directory di file.  La prima query utilizza il metodo <xref:System.IO.Directory.GetFiles%2A> per popolare una matrice di nomi file in una directory e in tutte le sottodirectory.  Questo metodo non restituisce alcun risultato finché l'intera matrice non è popolata, quindi è possibile che venga introdotta una certa latenza all'inizio dell'operazione.  Tuttavia, dopo il popolamento della matrice, PLINQ è in grado di elaborarla in parallelo molto rapidamente.  
  
 La seconda query utilizza i metodi statici <xref:System.IO.Directory.EnumerateDirectories%2A> e <xref:System.IO.DirectoryInfo.EnumerateFiles%2A> che iniziano a restituire i risultati immediatamente.  Questo approccio può essere più rapido quando si esegue l'iterazione in strutture ad albero di directory di grandi dimensioni, anche se il tempo di elaborazione rispetto al primo esempio può dipendere da molti fattori.  
  
> [!WARNING]
>  Lo scopo di questi esempi è dimostrare l'utilizzo e potrebbero non essere eseguiti più velocemente dell'equivalente query LINQ to Objects sequenziale.  Per ulteriori informazioni sull'aumento di velocità, vedere [Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md).  
  
## Esempio  
 Il seguente esempio mostra come eseguire l'iterazione in directory di file in semplici scenari quando si dispone dell'accesso a tutte le directory della struttura ad albero, le dimensioni dei file non sono molto elevate e i tempi di accesso non sono significativi.  Questo approccio prevede un periodo di latenza iniziale durante la costruzione della matrice dei nomi file.  
  
 [!code-csharp[PLINQ#33](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqfileiteration.cs#33)]  
  
## Esempio  
 Il seguente esempio mostra come eseguire l'iterazione in directory di file in semplici scenari quando si dispone dell'accesso a tutte le directory della struttura ad albero, le dimensioni dei file non sono molto elevate e i tempi di accesso non sono significativi.  Questo approccio inizia a fornire i risultati più velocemente dell'esempio precedente.  
  
 [!code-csharp[PLINQ#34](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqfileiteration.cs#34)]  
  
 Quando si utilizza <xref:System.IO.Directory.GetFiles%2A>, accertarsi di disporre di autorizzazioni sufficienti per tutte le directory della struttura ad albero.  In caso contrario verrà generata un'eccezione e non verrà restituito alcun risultato.  Quando si utilizza <xref:System.IO.Directory.EnumerateDirectories%2A> in una query PLINQ, è problematico gestire le eccezioni I\/O in un modo che consenta di continuare l'iterazione.  Se tramite il codice è necessario gestire eccezioni di I\/O o di accesso non autorizzato, considerare l'approccio descritto in [Procedura: scorrere le directory dei file con la classe Parallel](../../../docs/standard/parallel-programming/how-to-iterate-file-directories-with-the-parallel-class.md).  
  
 Se la latenza di I\/O costituisce un problema, ad esempio con l'I\/O dei file su una rete, considerare la possibilità di utilizzare una delle tecniche di I\/O asincrono descritte in [TPL and Traditional .NET Framework Asynchronous Programming](../../../docs/standard/parallel-programming/tpl-and-traditional-async-programming.md) e in questo [post di blog](http://go.microsoft.com/fwlink/?LinkID=186458).  
  
## Vedere anche  
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)