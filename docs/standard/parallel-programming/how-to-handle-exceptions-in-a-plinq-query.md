---
title: "How to: Handle Exceptions in a PLINQ Query | Microsoft Docs"
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
  - "PLINQ queries, how to handle exceptions"
ms.assetid: 8d56ff9b-a571-4d31-b41f-80c0b51b70a5
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# How to: Handle Exceptions in a PLINQ Query
Il primo esempio di questo argomento mostra come gestire l'oggetto <xref:System.AggregateException?displayProperty=fullName> che può essere generato da una query PLINQ quando viene eseguita.  Nel secondo esempio viene mostrato come inserire blocchi try\-catch all'interno dei delegati, nel punto più vicino possibile a quello in cui verranno generate le eccezioni.  In questo modo sarà possibile rilevarle nel momento in cui si verificano e, in alcuni casi, continuare l'esecuzione della query.  Quando alle eccezioni è consentita la propagazione fino al thread di unione, è possibile che una query continui a elaborare alcuni elementi dopo la generazione dell'eccezione.  
  
 In alcuni casi, quando PLINQ esegue il fallback all'esecuzione sequenziale e si verifica un'eccezione, l'eccezione può essere propagata direttamente e non viene eseguito il wrapping in <xref:System.AggregateException>.  Inoltre, le eccezioni <xref:System.Threading.ThreadAbortException> vengono sempre propagate direttamente.  
  
> [!NOTE]
>  Quando viene abilitato "Just My Code", Visual Studio si interromperà in corrispondenza della riga che genera l'eccezione e in cui viene visualizzato un messaggio di errore che indica che l'eccezione non è gestita dal codice utente. Questo errore è benigno.  È possibile premere F5 per continuare e visualizzare il comportamento di gestione delle eccezioni illustrato negli esempi riportati di seguito.  Per impedire l'interruzione di Visual Studio al primo errore, deselezionare semplicemente la casella di controllo "Just My Code" in **Strumenti, Opzioni, Debug, Generale**.  
>   
>  Lo scopo di questo esempio è dimostrare l'utilizzo e potrebbe non essere eseguito più velocemente dell'equivalente query LINQ to Objects sequenziale.  Per ulteriori informazioni sull'aumento di velocità, vedere [Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md).  
  
## Esempio  
 In questo esempio viene mostrato come aggiungere i blocchi try\-catch nel codice che esegue la query per rilevare qualsiasi oggetto <xref:System.AggregateException?displayProperty=fullName> eventualmente generato.  
  
 [!code-csharp[PLINQ#41](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#41)]
 [!code-vb[PLINQ#41](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#41)]  
  
 In questo esempio, la query non può continuare dopo la generazione dell'eccezione.  Quando il codice dell'applicazione rileverà l'eccezione, PLINQ avrà già interrotto la query in tutti i thread.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come aggiungere un blocco try\-catch in un delegato per consentire il rilevamento di un'eccezione senza tuttavia interrompere l'esecuzione della query.  
  
 [!code-csharp[PLINQ#42](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#42)]
 [!code-vb[PLINQ#42](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#42)]  
  
## Compilazione del codice  
  
-   Per compilare ed eseguire questi esempi, copiarli nell'esempio PLINQ Data Sample e chiamare il metodo da Main.  
  
## Programmazione efficiente  
 Rilevare soltanto le eccezioni che si è in grado di gestire in modo tale da non danneggiare lo stato del programma.  
  
## Vedere anche  
 <xref:System.Linq.ParallelEnumerable>   
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)