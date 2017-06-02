---
title: "Walkthrough: Creating a Custom Dataflow Block Type | Microsoft Docs"
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
  - "TPL dataflow library, creating custom dataflow blocks"
  - "dataflow blocks, creating custom in TPL"
ms.assetid: a6147146-0a6a-4d9b-ab0f-237b3c1ac691
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Walkthrough: Creating a Custom Dataflow Block Type
Sebbene la libreria di dati TPL fornisca diversi tipi di blocco del flusso di dati che abilitano una varietà di funzionalità, è anche possibile creare tipi di blocco personalizzati.  In questo documento viene descritto come creare un tipo di blocco del flusso di dati che implementa un comportamento personalizzato.  
  
## Prerequisiti  
 Leggere [Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md) prima di leggere questo documento.  
  
> [!TIP]
>  La libreria del flusso di dati TPL \(spazio dei nomi <xref:System.Threading.Tasks.Dataflow?displayProperty=fullName>\) non viene distribuita con [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].  Per installare lo spazio dei nomi <xref:System.Threading.Tasks.Dataflow>, aprire il progetto in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)], scegliere dal menu del progetto **Gestisci pacchetti NuGet** e scegliere cerca online il pacchetto `Microsoft.Tpl.Dataflow`.  
  
## Definizione del blocco di dati della finestra scorrevole  
 Si consideri un'applicazione di dati che richiede che i valori immessi siano memorizzati nel buffer e quindi vengano mostrati in una finestra a scorrimento.  Ad esempio, per i valori di input {0, 1, 2, 3, 4, 5} e la dimensione della finestra pari a tre, un blocco di dati della finestra scorrevole produce le matrici di output {0, 1, 2}, {1, 2, 3}, {2, 3, 4} e {3, 4, 5}.  Nelle sezioni seguenti vengono illustrati due modi per creare un tipo di blocco del flusso di dati che implementa questo comportamento personalizzato.  La prima tecnica utilizza il metodo <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Encapsulate%2A> per combinare la funzionalità di un oggetto <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> e di un oggetto <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> in un blocco di propagazione.  La seconda tecnica definisce una classe che deriva da <xref:System.Threading.Tasks.Dataflow.IPropagatorBlock%602> e combina funzionalità esistenti per eseguire il comportamento.  
  
## Utilizzo del metodo Encapsulate per definire il blocco di dati della finestra scorrevole  
 Nell'esempio seguente viene utilizzato il metodo <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Encapsulate%2A> per creare un blocco di propagazione da origine a destinazione.  Un blocco di propagazione consente a un blocco di origine e a un blocco di destinazione di agire come da destinatario e mittente dei dati.  
  
 Questa tecnica è utile quando è necessaria una funzionalità personalizzata del flusso di dati, ma non è necessario un tipo che fornisce metodi aggiuntivi, proprietà, o campi.  
  
 [!code-csharp[TPLDataflow_SlidingWindowBlock#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_slidingwindowblock/cs/slidingwindowblock.cs#1)]
 [!code-vb[TPLDataflow_SlidingWindowBlock#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_slidingwindowblock/vb/slidingwindowblock.vb#1)]  
  
## Derivazione da IPropagatorBlock per definire il blocco di dati della finestra scorrevole  
 Nell'esempio seguente viene illustrata la classe `SlidingWindowBlock`.  Questa classe deriva da <xref:System.Threading.Tasks.Dataflow.IPropagatorBlock%602> in modo che possa fungere da origine e da destinazione dei dati.  Come nell'esempio precedente, la classe `SlidingWindowBlock` viene compilata su tipi di blocco di dati esistenti.  Tuttavia, la classe `SlidingWindowBlock` implementa anche i metodi richiesti da <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601>, da <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> e le interfacce <xref:System.Threading.Tasks.Dataflow.IDataflowBlock>.  Tutti questi metodi trasmettono il lavoro ai membri predefiniti dei tipi di blocco di dati.  Ad esempio, il metodo `Post` ripianifica il lavoro al membro dati `m_target`, che è anche un oggetto <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601>.  
  
 Questa tecnica è utile quando è necessaria una funzionalità personalizzata del flusso di dati, ed è anche necessario un tipo che fornisce metodi aggiuntivi, proprietà, o campi.  Ad esempio, la classe `SlidingWindowBlock` deriva anche da <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601> in modo che possa fornire i metodi <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceiveAll%2A> e <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A>.  La classe `SlidingWindowBlock` illustra inoltre l'estensibilità fornendo la proprietà `WindowSize`, che recupera il numero di elementi nella finestra scorrevole.  
  
 [!code-csharp[TPLDataflow_SlidingWindowBlock#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_slidingwindowblock/cs/slidingwindowblock.cs#2)]
 [!code-vb[TPLDataflow_SlidingWindowBlock#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_slidingwindowblock/vb/slidingwindowblock.vb#2)]  
  
## Esempio completo  
 Nell'esempio riportato di seguito viene illustrato il codice completo per questa procedura guidata.  Viene inoltre illustrato come utilizzare entrambi i blocchi della finestra scorrevole in un metodo che scrittura nel blocco, legge da esso e stampa il risultato nella console.  
  
 [!code-csharp[TPLDataflow_SlidingWindowBlock#100](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_slidingwindowblock/cs/slidingwindowblock.cs#100)]
 [!code-vb[TPLDataflow_SlidingWindowBlock#100](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_slidingwindowblock/vb/slidingwindowblock.vb#100)]  
  
## Compilazione del codice  
 Copiare il codice di esempio e incollarlo in un progetto di Visual Studio, oppure incollarlo in un file denominato `SlidingWindowBlock.cs` \(`SlidingWindowBlock.vb` per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) e quindi eseguire il comando seguente in una finestra del prompt dei comandi di Visual Studio.  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe \/r:System.Threading.Tasks.Dataflow.dll SlidingWindowBlock.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe \/r:System.Threading.Tasks.Dataflow.dll SlidingWindowBlock.vb**  
  
## Passaggi successivi  
  
## Vedere anche  
 [Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)