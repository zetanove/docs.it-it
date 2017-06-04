---
title: "How to: Use JoinBlock to Read Data From Multiple Sources | Microsoft Docs"
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
  - "TPL dataflow library, joining blocks in"
  - "dataflow blocks, joining in TPL"
ms.assetid: e9c1ada4-ac57-4704-87cb-2f5117f8151d
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# How to: Use JoinBlock to Read Data From Multiple Sources
In questo documento viene illustrato come utilizzare la classe <xref:System.Threading.Tasks.Dataflow.JoinBlock%602> per eseguire un'operazione quando i dati sono disponibili da più origini.  Inoltre illustra come utilizzare la modalità non greedy per consentire a più blocchi di unione di condividere in modo più efficiente un'origine dati.  
  
> [!TIP]
>  La libreria del flusso di dati TPL \(spazio dei nomi <xref:System.Threading.Tasks.Dataflow?displayProperty=fullName>\) non viene distribuita con [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].  Per installare lo spazio dei nomi <xref:System.Threading.Tasks.Dataflow>, aprire il progetto in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)], scegliere dal menu del progetto **Gestisci pacchetti NuGet** e scegliere cerca online il pacchetto `Microsoft.Tpl.Dataflow`.  
  
## Esempio  
 Nell'esempio vengono definiti tre tipi di risorsa, `NetworkResource`, `FileResource` e `MemoryResource` ed vengono eseguite operazioni quando le risorse diventano disponibili.  Questo esempio richiede una coppia di `MemoryResource` e di `NetworkResource` per eseguire la prima operazione e una coppia di `MemoryResource` e di `FileResource` per eseguire la seconda operazione.  Per consentire a queste operazioni di verificare se tutte le risorse necessarie sono disponibili, questo esempio utilizza la classe <xref:System.Threading.Tasks.Dataflow.JoinBlock%602>.  Quando un oggetto <xref:System.Threading.Tasks.Dataflow.JoinBlock%602> riceve dati da tutte le origini, propaga i dati alla destinazione, che in questo esempio è un oggetto <xref:System.Threading.Tasks.Dataflow.ActionBlock%601>.  Entrambi gli oggetti <xref:System.Threading.Tasks.Dataflow.JoinBlock%602> leggono da un pool condiviso di oggetti `MemoryResource`.  
  
 [!code-csharp[TPLDataflow_NonGreedyJoin#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_nongreedyjoin/cs/nongreedyjoin.cs#1)]
 [!code-vb[TPLDataflow_NonGreedyJoin#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_nongreedyjoin/vb/nongreedyjoin.vb#1)]  
  
 Per consentire un utilizzo efficiente del pool condiviso degli oggetti `MemoryResource`, questo esempio specifica un oggetto <xref:System.Threading.Tasks.Dataflow.GroupingDataflowBlockOptions> che dispone della proprietà <xref:System.Threading.Tasks.Dataflow.GroupingDataflowBlockOptions.Greedy%2A> settata a `False` per creare oggetti <xref:System.Threading.Tasks.Dataflow.JoinBlock%602> che agiscono in modalità non\-greedy.  Un blocco join non\-greedy posticipa tutti i messaggi in arrivo finché non ne è disponibile uno da ogni origine.  Se qualche messaggio posposto viene accettato da un altro blocco, il blocco join riavvia il processo.  La modalità non\-greedy consente ai blocchi di join che condividono uno o più blocchi di origine di proseguire il lavoro mentre gli altri blocchi attendono i dati.  In questo esempio, se un oggetto `MemoryResource` viene aggiunto al pool di `memoryResources`, il primo blocco join per ricevere la seconda origine dati può proseguire.  Se questo esempio stesse utilizzando la modalità greedy, ovvero l'impostazione predefinita, un blocco join può utilizzare l'oggetto `MemoryResource` e attendere che la seconda risorsa diventi disponibile.  Tuttavia, se l'altro blocco di join ha la seconda origine dati disponibile, non può proseguire perché l'oggetto `MemoryResource` è stato ricavato dall'altro blocco di join.  
  
## Compilazione del codice  
 Copiare il codice di esempio e incollarlo in un progetto di Visual Studio, oppure incollarlo in un file denominato `DataflowNonGreedyJoin.cs` \(`DataflowNonGreedyJoin.vb` per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) e quindi eseguire il comando seguente in una finestra del prompt dei comandi di Visual Studio.  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowNonGreedyJoin.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowNonGreedyJoin.vb**  
  
## Programmazione efficiente  
 L'utilizzo di join non\-greedy può inoltre aiutare ad impedire una deadlock nell'applicazione.  In un'applicazione software il *deadlock* si verifica quando due o più processi contengono ognuno una risorsa e attendono reciprocamente che l'altro processo rilasci l'altra risorsa.  Si consideri un'applicazione che definisce due oggetti <xref:System.Threading.Tasks.Dataflow.JoinBlock%602>.  Entrambi gli oggetti leggono i dati da due blocchi di origine condivisi.  In modalità greedy, se un blocco join legge la prima origine e il secondo blocco join legge la seconda origine, potrebbe verificarsi una deadlock poiché entrambi i blocchi join attendono il completamento dell'altro per liberare la risorsa.  In modalità non\-greedy, ogni blocco join legge dalle origini solo quando tutti i dati sono disponibili e di conseguenza, il rischio di deadlock viene eliminato.  
  
## Vedere anche  
 [Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)