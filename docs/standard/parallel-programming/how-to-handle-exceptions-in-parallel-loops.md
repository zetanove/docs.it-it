---
title: "How to: Handle Exceptions in Parallel Loops | Microsoft Docs"
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
  - "parallel loops, how to handle exceptions"
ms.assetid: 512f0d5a-4636-4875-b766-88f20044f143
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# How to: Handle Exceptions in Parallel Loops
Gli overload dei metodi <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> e <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> non presentano alcun meccanismo speciale per gestire le eccezioni eventualmente generate.  Sotto questo aspetto assomigliano ai cicli `for` e `foreach` \(`For` e `For Each`in Visual Basic\) normali; un'eccezione non gestita fa sì che il ciclo termini immediatamente.  
  
 Quando si aggiunge una logica personalizzata di gestione delle eccezioni nei cicli paralleli, gestire il caso della generazione simultanea di eccezioni simili in più thread e il caso in cui un'eccezione generata in un determinato thread comporta la generazione di un'altra eccezione in un altro thread.  Per gestire entrambi questi casi è possibile eseguire il wrapping di tutte le eccezioni del ciclo in un oggetto <xref:System.AggregateException?displayProperty=fullName>.  L'esempio seguente mostra uno degli approcci possibili.  
  
> [!NOTE]
>  Quando "Just My Code" è abilitato, Visual Studio in alcuni casi si interromperà in corrispondenza della riga che genera l'eccezione e visualizzerà un messaggio di errore simile a "Eccezione non gestita dal codice utente". Questo errore non è grave.  È possibile premere F5 per continuare e osservare il comportamento di gestione delle eccezioni illustrato negli esempi seguenti.  Per impedire l'interruzione di Visual Studio al primo errore, deselezionare semplicemente la casella di controllo "Just My Code" in **Strumenti, Opzioni, Debug, Generale**.  
  
## Esempio  
 In questo esempio vengono rilevate tutte le eccezioni e quindi ne viene eseguito il wrapping in un oggetto <xref:System.AggregateException?displayProperty=fullName> che viene generato.  Il chiamante può decidere quali eccezioni gestire.  
  
 [!code-csharp[TPL_Exceptions#08](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/exceptions.cs#08)]
 [!code-vb[TPL_Exceptions#08](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/exceptionsinloops.vb#08)]  
  
## Vedere anche  
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)   
 [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)