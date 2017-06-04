---
title: "How to: Implement a Producer-Consumer Dataflow Pattern | Microsoft Docs"
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
  - "TPL dataflow library, implementing producer-consumer pattern"
  - "Task Parallel Library, dataflows"
  - "producer-consumer patterns, implementing [TPL]"
ms.assetid: 47a1d38c-fe9c-44aa-bd15-937bd5659b0b
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# How to: Implement a Producer-Consumer Dataflow Pattern
In questo documento viene descritto come utilizzare la libreria di dati TPL per applicare un modello producer\-consumer.  In questo modello il *producer* invia i messaggi a un blocco dei messaggi e il *consumer* legge i messaggi da tale blocco.  
  
> [!TIP]
>  La libreria del flusso di dati TPL \(spazio dei nomi <xref:System.Threading.Tasks.Dataflow?displayProperty=fullName>\) non viene distribuita con [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].  Per installare lo spazio dei nomi <xref:System.Threading.Tasks.Dataflow>, aprire il progetto in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)], scegliere dal menu del progetto **Gestisci pacchetti NuGet** e scegliere cerca online il pacchetto `Microsoft.Tpl.Dataflow`.  
  
## Esempio  
 Nell'esempio seguente viene illustrato un modello di base producer\-consumer che utilizza il flusso di dati.  Il metodo `Produce` scrive matrici contenenti byte casuali dei dati in un oggetto <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601?displayProperty=fullName> e il metodo `Consume` legge byte da un oggetto <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601?displayProperty=fullName>.  Agendo sulle interfacce <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> e <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601>, anziché sui relativi tipi derivati, è possibile scrivere codice riutilizzabile che possa agire su diversi tipi di blocco di dati.  Nell'esempio viene utilizzata la classe <xref:System.Threading.Tasks.Dataflow.BufferBlock%601>.  Poiché la classe <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> funge sia da blocco di origine che da blocco di destinazione, il producer e il consumer possono utilizzare un oggetto condiviso per il trasferimento dei dati.  
  
 Il metodo `Produce` chiama il metodo <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A> in un ciclo per scrivere i dati in modo sincrono nel blocco di destinazione.  Dopo che il metodo `Produce` scrive tutti i dati nel blocco di destinazione, chiama il metodo <xref:System.Threading.Tasks.Dataflow.IDataflowBlock.Complete%2A> per indicare che il blocco non avrà mai dati aggiuntivi disponibili.  Il metodo `Consume` utilizza gli operatori [await](../Topic/await%20\(C%23%20Reference\).md) e [async](../Topic/async%20\(C%23%20Reference\).md) \([Async](../Topic/Async%20\(Visual%20Basic\).md) e [Await](../Topic/Await%20Operator%20\(Visual%20Basic\).md) in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) per calcolare in modo asincrono il numero totale di byte che vengono ricevuti dall'oggetto <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601>.  Per agire in modo asincrono, il metodo `Consume` chiama il metodo <xref:System.Threading.Tasks.Dataflow.DataflowBlock.OutputAvailableAsync%2A> per ricevere una notifica quando il blocco di origine ha dati disponibili e quando il blocco di origine non avrà mai dati aggiuntivi disponibili.  
  
 [!code-csharp[TPLDataflow_ProducerConsumer#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_producerconsumer/cs/dataflowproducerconsumer.cs#1)]
 [!code-vb[TPLDataflow_ProducerConsumer#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_producerconsumer/vb/dataflowproducerconsumer.vb#1)]  
  
## Compilazione del codice  
 Copiare il codice di esempio e incollarlo in un progetto di Visual Studio, oppure incollarlo in un file denominato `DataflowProducerConsumer.cs` \(`DataflowProducerConsumer.vb` per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) e quindi eseguire il comando seguente in una finestra del prompt dei comandi di Visual Studio.  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowProducerConsumer.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowProducerConsumer.vb**  
  
## Programmazione efficiente  
 In questo esempio viene utilizzato solo un consumer per elaborare i dati di origine.  Se si dispone di più consumer nell'applicazione, utilizzare il metodo <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> per leggere i dati dal blocco di origine, come illustrato nell'esempio seguente.  
  
 [!code-csharp[TPLDataflow_ProducerConsumer#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_producerconsumer/cs/dataflowproducerconsumer.cs#2)]
 [!code-vb[TPLDataflow_ProducerConsumer#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_producerconsumer/vb/dataflowproducerconsumer.vb#2)]  
  
 Il metodo <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> restituisce `False` quando non sono disponibili dati.  Quando più consumer devono accedere al blocco di origine contemporaneamente, questo meccanismo garantisce che i dati siano sempre disponibili dopo la chiamata a <xref:System.Threading.Tasks.Dataflow.DataflowBlock.OutputAvailableAsync%2A>.  
  
## Vedere anche  
 [Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)