---
title: "How to: Unlink Dataflow Blocks | Microsoft Docs"
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
  - "dataflow blocks, unlinking in TPL"
  - "Task Parallel Library, dataflows"
  - "TPL dataflow library, unlinking dataflow blocks"
ms.assetid: 40f0208d-4618-47f7-85cf-4913d07d2d7d
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Unlink Dataflow Blocks
In questo documento viene descritto come scollegare un blocco di destinazione del flusso di dati dall'origine.  
  
> [!TIP]
>  La libreria del flusso di dati TPL \(spazio dei nomi <xref:System.Threading.Tasks.Dataflow?displayProperty=fullName>\) non viene distribuita con [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].  Per installare lo spazio dei nomi <xref:System.Threading.Tasks.Dataflow>, aprire il progetto in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)], scegliere dal menu del progetto **Gestisci pacchetti NuGet** e scegliere cerca online il pacchetto `Microsoft.Tpl.Dataflow`.  
  
## Esempio  
 Nell'esempio seguente vengono creati tre oggetti <xref:System.Threading.Tasks.Dataflow.TransformBlock%602>, ognuno dei quali chiama il metodo di `TrySolution` per calcolare un valore.  Questo esempio richiede solo il risultato della prima chiamata a `TrySolution` per finire.  
  
 [!code-csharp[TPLDataflow_ReceiveAny#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_receiveany/cs/dataflowreceiveany.cs#1)]
 [!code-vb[TPLDataflow_ReceiveAny#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_receiveany/vb/dataflowreceiveany.vb#1)]  
  
 Per ottenere il valore dal primo oggetto <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> che termina, viene definito il metodo `ReceiveFromAny(T)`.  Il metodo `ReceiveFromAny(T)` accetta una matrice di oggetti <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> e collega ciascuno di questi oggetti a un oggetto <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601>.  Quando si utilizza il metodo <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A> per collegare un blocco di origine del flusso di dati a un blocco di destinazione, l'origine propaga i messaggi alla destinazione appena i dati diventano disponibili.  Poiché la classe <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> accetta solo il primo messaggio offerto, il metodo `ReceiveFromAny(T)` produce il risultato chiamando il metodo <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Receive%2A>.  Questo produce il primo messaggio offerto all'oggetto <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601>.  Il metodo <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A> dispone di una versione di overload che accetta un parametro <xref:System.Boolean>, `unlinkAfterOne` che, quando viene impostato a `True`, indica al blocco di origine di scollegarsi dalla destinazione dopo che la destinazione riceve un messaggio dall'origine.  Per l'oggetto <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> è importante scollegarsi dall'origine perché la relazione tra la matrice delle origini e l'oggetto <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> non è più richiesta dopo che l'oggetto <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> riceve un messaggio.  
  
 Per abilitare le chiamate rimanenti a `TrySolution` per terminare dopo che una di esse calcola un valore, il metodo `TrySolution` prende un oggetto <xref:System.Threading.CancellationToken> che viene annullato dopo la chiamata a `ReceiveFromAny(T)` ritorna.  Il metodo <xref:System.Threading.SpinWait.SpinUntil%2A> ritorna quando questo oggetto <xref:System.Threading.CancellationToken> viene annullato.  
  
## Compilazione del codice  
 Copiare il codice di esempio e incollarlo in un progetto di Visual Studio, oppure incollarlo in un file denominato `DataflowReceiveAny.cs` \(`DataflowReceiveAny.vb` per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) e quindi eseguire il comando seguente in una finestra del prompt dei comandi di Visual Studio.  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowReceiveAny.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe \/r:System.Threading.Tasks.Dataflow.dll DataflowReceiveAny.vb**  
  
## Programmazione efficiente  
  
## Vedere anche  
 [Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)