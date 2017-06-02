---
title: "How to: Perform Action When a Dataflow Block Receives Data | Microsoft Docs"
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
  - "Task Parallel Library, dataflows"
  - "TPL dataflow library, receiving data"
ms.assetid: fc2585dc-965e-4632-ace7-73dd02684ed3
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Perform Action When a Dataflow Block Receives Data
I tipi di *blocco del flusso di esecuzione* chiamano il delegato fornito dall'utente quando ricevono i dati.  Le classi <xref:System.Threading.Tasks.Dataflow.ActionBlock%601?displayProperty=fullName>, <xref:System.Threading.Tasks.Dataflow.TransformBlock%602?displayProperty=fullName> e <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602?displayProperty=fullName> sono tipi di blocco del flusso di esecuzione.  È possibile utilizzare la parola chiave `delegate` \(`Sub` in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\), <xref:System.Action%601>, <xref:System.Func%602>, o un'espressione lambda quando viene fornita una funzione lavoro a un blocco di dati di esecuzione.  In questo documento viene descritto come utilizzare <xref:System.Func%602> ed espressioni lambda per eseguire l'operazione nei blocchi di esecuzione.  
  
> [!TIP]
>  La libreria del flusso di dati TPL \(spazio dei nomi <xref:System.Threading.Tasks.Dataflow?displayProperty=fullName>\) non viene distribuita con [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].  Per installare lo spazio dei nomi <xref:System.Threading.Tasks.Dataflow>, aprire il progetto in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)], scegliere dal menu del progetto **Gestisci pacchetti NuGet** e scegliere cerca online il pacchetto `Microsoft.Tpl.Dataflow`.  
  
## Esempio  
 Nell'esempio seguente viene utilizzato il flusso di dati per leggere un file da disco e viene calcolato il numero di byte nel file uguali a zero.  Utilizza <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> per leggere il file e calcolare il numero di byte zero e <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> per stampare il numero di byte zero nella console.  L'oggetto <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> specifica un oggetto <xref:System.Func%602> per eseguire il lavoro quando i blocchi ricevono i dati.  L'oggetto <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> utilizza un'espressione lambda per la stampa nella console del numero di byte zero che vengono letti.  
  
 [!code-csharp[TPLDataflow_ExecutionBlocks#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_executionblocks/cs/dataflowexecutionblocks.cs#1)]
 [!code-vb[TPLDataflow_ExecutionBlocks#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_executionblocks/vb/dataflowexecutionblocks.vb#1)]  
  
 Sebbene sia possibile immettere un'espressione lambda in un oggetto <xref:System.Threading.Tasks.Dataflow.TransformBlock%602>, questo esempio utilizza <xref:System.Func%602> per consentire all'altro codice di utilizzare il metodo `CountBytes`.  L'oggetto <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> utilizza un'espressione lambda in quanto il lavoro da eseguire è specifico di questa attività e non potrà essere utile ad altri codici.  Per ulteriori informazioni sull'utilizzo di espressioni lambda nella Task Parallel Library, vedere [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md).  
  
 La sezione Sommario dei Tipi Delegato nel documento di [Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md) riepiloga i tipi delegati da poter fornire a <xref:System.Threading.Tasks.Dataflow.ActionBlock%601>, a <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> e agli oggetti <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>.  La tabella specifica anche se il tipo delegato viene eseguito in modo sincrono o asincrono.  
  
## Compilazione del codice  
 Copiare il codice di esempio e incollarlo in un progetto di Visual Studio, oppure incollarlo in un file denominato `DataflowExecutionBlocks.cs` \(`DataflowExecutionBlocks.vb` per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) e quindi eseguire il comando seguente in una finestra del prompt dei comandi di Visual Studio.  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowExecutionBlocks.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowExecutionBlocks.vb**  
  
## Programmazione efficiente  
 In questo esempio viene fornito un delegato di tipo <xref:System.Func%602> all'oggetto di <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> per eseguire l'attività del blocco di dati in modo sincrono.  Per consentire al blocco di dati di comportarsi in modo asincrono, fornire un delegato di tipo <xref:System.Func%601> al blocco di dati.  Quando un blocco di dati funziona in modo asincrono, l'attività del blocco del flusso di dati è completa solo quando l'oggetto <xref:System.Threading.Tasks.Task%601> restituito finisce.  Nell'esempio seguente viene modificato il metodo `CountBytes` e vengono utilizzati gli operatori [async](../Topic/async%20\(C%23%20Reference\).md) e [await](../Topic/await%20\(C%23%20Reference\).md) \([Async](../Topic/Async%20\(Visual%20Basic\).md) e [Await](../Topic/Await%20Operator%20\(Visual%20Basic\).md) in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) per calcolare in modo asincrono il numero totale di byte che sono zero nel file specificato.  Il metodo <xref:System.IO.FileStream.ReadAsync%2A> esegue operazioni di lettura da file in modo asincrono.  
  
 [!code-csharp[TPLDataflow_ExecutionBlocks#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_executionblocks/cs/dataflowexecutionblocks.cs#2)]
 [!code-vb[TPLDataflow_ExecutionBlocks#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_executionblocks/vb/dataflowexecutionblocks.vb#2)]  
  
 È inoltre possibile utilizzare le espressioni lambda asincrone per eseguire operazioni in un blocco di dati di esecuzione.  Nell'esempio seguente viene modificato l'oggetto <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> utilizzato nell'esempio precedente in modo da utilizzare un'espressione lambda per eseguire il lavoro in modo asincrono.  
  
 [!code-csharp[TPLDataflow_ExecutionBlocks#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_executionblocks/cs/dataflowexecutionblocks.cs#3)]
 [!code-vb[TPLDataflow_ExecutionBlocks#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_executionblocks/vb/dataflowexecutionblocks.vb#3)]  
  
## Vedere anche  
 [Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)