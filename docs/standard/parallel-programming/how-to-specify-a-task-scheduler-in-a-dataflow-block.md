---
title: "How to: Specify a Task Scheduler in a Dataflow Block | Microsoft Docs"
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
  - "TPL dataflow library, linking to task scheduler in TPL"
  - "Task Parallel Library, dataflows"
  - "task scheduler, linking from TPL"
ms.assetid: 27ece374-ed5b-49ef-9cec-b20db34a65e8
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# How to: Specify a Task Scheduler in a Dataflow Block
In questo documento viene illustrato come associare una specifica utilità di pianificazione delle attività quando si utilizza il flusso di dati nell'applicazione.  Nell'esempio viene utilizzata la classe <xref:System.Threading.Tasks.ConcurrentExclusiveSchedulerPair?displayProperty=fullName> in un'applicazione Windows Form per visualizzare quando le attività del lettore sono attive e quando invece lo è una del writer.  Viene inoltre utilizzato il metodo <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=fullName> per consentire a un blocco di flussi di dati l'esecuzione nel thread dell'interfaccia utente.  
  
> [!TIP]
>  La libreria del flusso di dati TPL \(spazio dei nomi <xref:System.Threading.Tasks.Dataflow?displayProperty=fullName>\) non viene distribuita con [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].  Per installare lo spazio dei nomi <xref:System.Threading.Tasks.Dataflow>, aprire il progetto in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)], scegliere **Gestisci pacchetti NuGet** dal menu Progetto e cercare online il pacchetto `Microsoft.Tpl.Dataflow`.  
  
### Per creare l'applicazione Windows Form  
  
1.  Creare un progetto di [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] o di **Applicazione Windows Form** di Visual Basic.  Nei passaggi seguenti il progetto viene denominato `WriterReadersWinForms`.  
  
2.  Nella finestra di progettazione del form per il form principale, Form1.cs \(Form1.vb per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\), aggiungere quattro controlli <xref:System.Windows.Forms.CheckBox>.  Impostare la proprietà <xref:System.Windows.Forms.Control.Text%2A> su Reader 1 per `checkBox1`, Reader 2 per `checkBox2`, Reader 3 per `checkBox3` e Writer per `checkBox4`.  Impostare la proprietà <xref:System.Windows.Forms.Control.Enabled%2A> per ogni controllo su `False`.  
  
3.  Aggiungere un controllo <xref:System.Windows.Forms.Timer> al form.  Impostare la proprietà <xref:System.Windows.Forms.Timer.Interval%2A> su `2500`.  
  
## Aggiunta di funzionalità del flusso di dati  
 In questa sezione viene descritto come creare i blocchi di flussi di dati che fanno parte dell'applicazione e come associare ognuno di essi a un'utilità di pianificazione delle attività.  
  
#### Per aggiungere funzionalità del flusso di dati all'applicazione  
  
1.  Nel progetto aggiungere un riferimento a System.Threading.Tasks.Dataflow.dll.  
  
2.  Assicurarsi che in Form1.cs \(Form1.vb per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) siano contenute le seguenti istruzioni `using` \(`Imports` in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\).  
  
     [!code-csharp[TPLDataflow_WriterReadersWinForms#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/cs/writerreaderswinforms/form1.cs#1)]
     [!code-vb[TPLDataflow_WriterReadersWinForms#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/vb/writerreaderswinforms/form1.vb#1)]  
  
3.  Aggiungere un membro dati <xref:System.Threading.Tasks.Dataflow.BroadcastBlock%601> alla classe `Form1`.  
  
     [!code-csharp[TPLDataflow_WriterReadersWinForms#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/cs/writerreaderswinforms/form1.cs#2)]
     [!code-vb[TPLDataflow_WriterReadersWinForms#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/vb/writerreaderswinforms/form1.vb#2)]  
  
4.  Nel costruttore `Form1`, dopo la chiamata a `InitializeComponent`, creare un oggetto <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> tramite cui viene alternato lo stato degli oggetti <xref:System.Windows.Forms.CheckBox>.  
  
     [!code-csharp[TPLDataflow_WriterReadersWinForms#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/cs/writerreaderswinforms/form1.cs#3)]
     [!code-vb[TPLDataflow_WriterReadersWinForms#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/vb/writerreaderswinforms/form1.vb#3)]  
  
5.  Nel costruttore `Form1` creare un oggetto <xref:System.Threading.Tasks.ConcurrentExclusiveSchedulerPair> e quattro oggetti <xref:System.Threading.Tasks.Dataflow.ActionBlock%601>, un oggetto <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> per ogni oggetto <xref:System.Windows.Forms.CheckBox>.  Per ogni oggetto <xref:System.Threading.Tasks.Dataflow.ActionBlock%601>, specificare un oggetto <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions> con la proprietà <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.TaskScheduler%2A> impostata sulla proprietà <xref:System.Threading.Tasks.ConcurrentExclusiveSchedulerPair.ConcurrentScheduler%2A> per i lettori e la proprietà <xref:System.Threading.Tasks.ConcurrentExclusiveSchedulerPair.ExclusiveScheduler%2A> per il writer.  
  
     [!code-csharp[TPLDataflow_WriterReadersWinForms#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/cs/writerreaderswinforms/form1.cs#4)]
     [!code-vb[TPLDataflow_WriterReadersWinForms#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/vb/writerreaderswinforms/form1.vb#4)]  
  
6.  Nel costruttore `Form1` avviare l'oggetto <xref:System.Windows.Forms.Timer>.  
  
     [!code-csharp[TPLDataflow_WriterReadersWinForms#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/cs/writerreaderswinforms/form1.cs#5)]
     [!code-vb[TPLDataflow_WriterReadersWinForms#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/vb/writerreaderswinforms/form1.vb#5)]  
  
7.  Nella finestra di progettazione del form per il form principale creare un gestore eventi per l'evento <xref:System.Windows.Forms.Timer.Tick> per il timer.  
  
8.  Implementare l'evento <xref:System.Windows.Forms.Timer.Tick> per il timer.  
  
     [!code-csharp[TPLDataflow_WriterReadersWinForms#6](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/cs/writerreaderswinforms/form1.cs#6)]
     [!code-vb[TPLDataflow_WriterReadersWinForms#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/vb/writerreaderswinforms/form1.vb#6)]  
  
 Poiché il blocco di flussi di dati `toggleCheckBox` viene utilizzato nell'interfaccia utente, è importante che questa azione si verifichi nel thread dell'interfaccia utente.  A tale scopo, durante la costruzione questo oggetto fornisce un oggetto <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions> con la proprietà <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.TaskScheduler%2A> impostata su <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=fullName>.  Tramite il metodo <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A> viene creato un oggetto <xref:System.Threading.Tasks.TaskScheduler> mediante il quale viene eseguito il lavoro nel contesto di sincronizzazione corrente.  Poiché il costruttore `Form1` viene chiamato dal thread dell'interfaccia utente, l'azione per il blocco di flussi di dati `toggleCheckBox` viene eseguita anche nel thread dell'interfaccia utente.  
  
 In questo esempio viene inoltre utilizzata la classe <xref:System.Threading.Tasks.ConcurrentExclusiveSchedulerPair> per consentire ad alcuni blocchi di flussi di dati di agire simultaneamente e a un altro blocco di flussi di dati di agire in modo esclusivo rispetto a tutti gli altri blocchi di flussi di dati in esecuzione nello stesso oggetto <xref:System.Threading.Tasks.ConcurrentExclusiveSchedulerPair>.  Questa tecnica è utile quando da parte di più blocchi di flussi di dati viene condivisa una risorsa mentre altri richiedono l'accesso esclusivo a quest'ultima, poiché viene eliminata la necessità di sincronizzare manualmente l'accesso alla risorsa in questione.  L'eliminazione della sincronizzazione manuale può rendere il codice più efficiente.  
  
## Esempio  
 Nell'esempio seguente viene illustrato il codice completo per Form1.cs \(Form1.vb per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\).  
  
 [!code-csharp[TPLDataflow_WriterReadersWinForms#100](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/cs/writerreaderswinforms/form1.cs#100)]
 [!code-vb[TPLDataflow_WriterReadersWinForms#100](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/vb/writerreaderswinforms/form1.vb#100)]  
  
## Vedere anche  
 [Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)