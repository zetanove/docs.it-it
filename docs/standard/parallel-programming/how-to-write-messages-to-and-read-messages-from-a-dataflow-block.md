---
title: "How to: Write Messages to and Read Messages from a Dataflow Block | Microsoft Docs"
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
  - "TPL dataflow library, reading and writing messages"
ms.assetid: 1a9bf078-aa82-46eb-b95a-f87237f028c5
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Write Messages to and Read Messages from a Dataflow Block
In questo documento viene descritto come utilizzare la libreria di dati TPL per scrivere e leggere i messaggi da un blocco di dati.  La libreria di dati TPL fornisce i metodi sincroni e asincroni per la lettura e scrittura di messaggi da e su un blocco di dati.  In questo documento viene utilizzata la classe <xref:System.Threading.Tasks.Dataflow.BufferBlock%601?displayProperty=fullName>.  La classe <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> mette i messaggi nel buffer e si comporta sia da origine del messaggio che da destinazione.  
  
> [!TIP]
>  La libreria del flusso di dati TPL \(spazio dei nomi <xref:System.Threading.Tasks.Dataflow?displayProperty=fullName>\) non viene distribuita con [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].  Per installare lo spazio dei nomi <xref:System.Threading.Tasks.Dataflow>, aprire il progetto in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)], scegliere dal menu del progetto **Gestisci pacchetti NuGet** e scegliere cerca online il pacchetto `Microsoft.Tpl.Dataflow`.  
  
## Scrittura e lettura da un blocco di dati in modo sincrono  
 Nell'esempio seguente viene utilizzato il metodo <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A> per scrivere sul blocco di dati <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> e il metodo <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Receive%2A> per leggere dallo stesso oggetto.  
  
 [!code-csharp[TPLDataflow_ReadWrite#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs#2)]
 [!code-vb[TPLDataflow_ReadWrite#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb#2)]  
  
 È inoltre possibile utilizzare il metodo <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> per leggere da un blocco di dati, come mostrato nell'esempio seguente.  Il metodo <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> non blocca il thread corrente e risulta utile quando si sondano i dati occasionalmente.  
  
 [!code-csharp[TPLDataflow_ReadWrite#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs#3)]
 [!code-vb[TPLDataflow_ReadWrite#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb#3)]  
  
 Poiché il metodo di <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A> agisce in modo sincrono, l'oggetto di <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> negli esempi precedenti riceve tutti i dati prima che il secondo ciclo legga i dati.  L'esempio seguente estende il primo utilizzando <xref:System.Threading.Tasks.Parallel.Invoke%2A> per la lettura e la scrittura contemporanea del blocco di messaggi.  Poiché <xref:System.Threading.Tasks.Parallel.Invoke%2A> esegue operazioni contemporaneamente, i valori non vengono scritti nell'oggetto <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> in un ordine specifico.  
  
 [!code-csharp[TPLDataflow_ReadWrite#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs#4)]
 [!code-vb[TPLDataflow_ReadWrite#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb#4)]  
  
## Scrittura e lettura da un blocco di dati in modo asincrono  
 Nell'esempio seguente viene utilizzato il metodo <xref:System.Threading.Tasks.Dataflow.DataflowBlock.SendAsync%2A> per scrivere in modo asincrono un oggetto <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> e il metodo <xref:System.Threading.Tasks.Dataflow.DataflowBlock.ReceiveAsync%2A> per leggere in modo asincrono dallo stesso oggetto.  Questo esempio utilizza gli operatori [await](../Topic/await%20\(C%23%20Reference\).md) e [async](../Topic/async%20\(C%23%20Reference\).md) \([Async](../Topic/Async%20\(Visual%20Basic\).md) e [Await](../Topic/Await%20Operator%20\(Visual%20Basic\).md) in Visual Basic\) per inviare e per leggere i dati dal blocco di destinazione in modo asincrono.  Il metodo <xref:System.Threading.Tasks.Dataflow.DataflowBlock.SendAsync%2A> è utile quando è necessario consentire a un blocco di dati di posticipare i messaggi.  Il metodo <xref:System.Threading.Tasks.Dataflow.DataflowBlock.ReceiveAsync%2A> è utile quando si desidera agire sui dati quando tali dati diventano disponibili.  Per ulteriori informazioni su come i messaggi si propagano tra i blocchi, vedere il la sezione Passaggio Parametri in [Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md).  
  
 [!code-csharp[TPLDataflow_ReadWrite#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs#5)]
 [!code-vb[TPLDataflow_ReadWrite#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb#5)]  
  
## Un esempio completo  
 Nell'esempio riportato di seguito viene illustrato il codice completo di questo documento.  
  
 [!code-csharp[TPLDataflow_ReadWrite#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs#1)]
 [!code-vb[TPLDataflow_ReadWrite#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb#1)]  
  
## Compilazione del codice  
 Copiare il codice di esempio e incollarlo in un progetto di Visual Studio, oppure incollarlo in un file denominato `DataflowReadWrite.cs` \(`DataflowReadWrite.vb` per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) e quindi eseguire il comando seguente in una finestra del prompt dei comandi di Visual Studio.  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowReadWrite.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowReadWrite.vb**  
  
## Passaggi successivi  
 In questo esempio viene mostrato come leggere e scrivere da e su un blocco di messaggi direttamente.  È anche possibile connettere i blocchi del flusso di dati per creare *pipeline*, che sono sequenze lineari di blocchi del flusso di dati, o *reti*, ovvero grafici dei blocchi di dati.  In una pipeline o una rete, le origini propagano i dati verso le destinazioni in modo asincrono man mano che tali dati diventano disponibili.  Per un esempio in cui viene creata una pipeline di base del flusso di dati, vedere [Walkthrough: Creating a Dataflow Pipeline](../../../docs/standard/parallel-programming/walkthrough-creating-a-dataflow-pipeline.md).  Per un esempio in cui viene creata una rete più complessa del flusso di dati, vedere [Walkthrough: Using Dataflow in a Windows Forms Application](../../../docs/standard/parallel-programming/walkthrough-using-dataflow-in-a-windows-forms-application.md).  
  
## Vedere anche  
 [Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)