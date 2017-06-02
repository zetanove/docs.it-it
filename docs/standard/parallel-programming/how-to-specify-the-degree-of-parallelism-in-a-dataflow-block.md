---
title: "How to: Specify the Degree of Parallelism in a Dataflow Block | Microsoft Docs"
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
  - "dataflow block, specifying parallelism in TPL"
  - "Task Parallel Library, dataflows"
  - "TPL dataflow library, specifying parallelism"
ms.assetid: e4088541-ee05-40db-95f5-147cfe62fde7
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# How to: Specify the Degree of Parallelism in a Dataflow Block
In questo documento viene descritto come impostare la proprietà <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions.MaxDegreeOfParallelism%2A?displayProperty=fullName> per consentire a un blocco di flussi di dati di esecuzione di elaborare più messaggi alla volta.  Questa operazione è utile quando è presente un blocco di flussi di dati in cui viene eseguito un calcolo di lunga durata ed è possibile trarre vantaggio dall'elaborazione di messaggi in parallelo.  Nell'esempio viene usata la classe <xref:System.Threading.Tasks.Dataflow.ActionBlock%601?displayProperty=fullName> per eseguire più operazioni di flussi di dati contemporaneamente; tuttavia, è possibile specificare il massimo grado di parallelismo in uno dei tipi di blocchi di esecuzione predefiniti forniti dalla libreria del flusso di dati TPL, <xref:System.Threading.Tasks.Dataflow.ActionBlock%601>, <xref:System.Threading.Tasks.Dataflow.TransformBlock%602?displayProperty=fullName> e <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602?displayProperty=fullName>.  
  
> [!TIP]
>  La libreria del flusso di dati TPL \(spazio dei nomi <xref:System.Threading.Tasks.Dataflow?displayProperty=fullName>\) non viene distribuita con [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].  Per installare lo spazio dei nomi <xref:System.Threading.Tasks.Dataflow>, aprire il progetto in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)], scegliere **Gestisci pacchetti NuGet** dal menu Progetto e cercare online il pacchetto `Microsoft.Tpl.Dataflow`.  
  
## Esempio  
 Nell'esempio seguente vengono eseguiti due calcoli del flusso di dati e viene stampato il tempo trascorso richiesto per ogni calcolo.  Nel primo calcolo viene specificato un grado massimo di parallelismo pari a 1, vale a dire l'impostazione predefinita.  Un grado massimo di parallelismo pari a 1 determina un'elaborazione seriale dei messaggi da parte del blocco di flussi di dati.  Il secondo calcolo è simile al primo, con la differenza che specifica un massimo grado di parallelismo uguale al numero di processori disponibili.  Ciò consente al blocco di flusso di dati di eseguire più operazioni in parallelo.  
  
 [!code-csharp[TPLDataflow_DegreeOfParallelism#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_degreeofparallelism/cs/dataflowdegreeofparallelism.cs#1)]
 [!code-vb[TPLDataflow_DegreeOfParallelism#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_degreeofparallelism/vb/dataflowdegreeofparallelism.vb#1)]  
  
## Compilazione del codice  
 Copiare il codice di esempio e incollarlo in un progetto di Visual Studio oppure incollarlo in un file denominato `DataflowDegreeOfParallelism.cs` \(`DataflowDegreeOfParallelism.vb` per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\), quindi eseguire il comando riportato di seguito in una finestra del prompt dei comandi di Visual Studio.  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowDegreeOfParallelism.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowDegreeOfParallelism.vb**  
  
## Programmazione efficiente  
 Per impostazione predefinita, tramite ogni blocco di flussi di dati predefinito i messaggi vengono propagati all'esterno nell'ordine in cui vengono ricevuti.  Anche se vengono elaborati più messaggi contemporaneamente quando si specifica un grado massimo di parallelismo maggiore di 1, questi vengono comunque propagati all'esterno nell'ordine in cui vengono ricevuti.  
  
 Poiché la proprietà <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions.MaxDegreeOfParallelism%2A> rappresenta il grado massimo di parallelismo, il blocco di flussi di dati può essere eseguito con un grado di parallelismo minore rispetto a quello specificato.  Con il blocco di flussi di dati è possibile usare un minore grado di parallelismo per soddisfare i relativi requisiti funzionali o per tener conto della mancanza di risorse di sistema disponibili.  Da parte di un blocco di flussi di dati non viene mai scelto un parallelismo maggiore di quello specificato.  
  
## Vedere anche  
 [Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)