---
title: "Procedura: individuare se &#232; possibile eseguire o meno un processo di stampa all&#39;orario indicato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "processi di stampa, temporizzazione"
  - "code di stampa, temporizzazione"
  - "stampanti, disponibilità"
ms.assetid: 7e9c8ec1-abf6-4b3d-b1c6-33b35d3c4063
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: individuare se &#232; possibile eseguire o meno un processo di stampa all&#39;orario indicato
Le code di stampa non sempre sono disponibili 24 ore al giorno.  È possibile impostare le proprietà relative all'ora di inizio e di fine per renderle non disponibili in determinati orari del giorno.  Questa funzione può essere utilizzata, ad esempio, per riservare l'uso esclusivo di una stampante per un determinato reparto dopo le 17.00.  In tal modo, il reparto avrebbe una coda di stampa diversa rispetto a quella degli altri reparti.  La coda per gli altri reparti sarebbe impostata come non disponibile dopo le 17.00 mentre quella per il reparto selezionato sarebbe impostata come disponibile per tutto il tempo.  
  
 Inoltre, gli stessi processi di stampa possono essere impostati come stampabili solo entro un intervallo di tempo specificato.  
  
 Le classi <xref:System.Printing.PrintQueue> e <xref:System.Printing.PrintSystemJobInfo> esposte nelle [!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)] di [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)] consentono di controllare in remoto se un determinato processo di stampa può essere eseguito su una determinata coda all'ora corrente.  
  
## Esempio  
 L'esempio riportato di seguito consente di diagnosticare i problemi di un processo di stampa.  
  
 Di seguito vengono riportati i due passaggi principali di questo tipo di funzione.  
  
1.  Leggere le proprietà <xref:System.Printing.PrintQueue.StartTimeOfDay%2A> e <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A> di <xref:System.Printing.PrintQueue> per determinare se comprendono l'ora corrente.  
  
2.  Leggere le proprietà <xref:System.Printing.PrintSystemJobInfo.StartTimeOfDay%2A> e <xref:System.Printing.PrintSystemJobInfo.UntilTimeOfDay%2A> di <xref:System.Printing.PrintSystemJobInfo> per determinare se comprendono l'ora corrente.  
  
 Tuttavia, i problemi scaturiscono dal fatto che queste proprietà non sono oggetti <xref:System.DateTime> ma oggetti <xref:System.Int32> che esprimono l'orario come numero di minuti a partire dalla mezzanotte.  Inoltre, non si tratta della mezzanotte del fuso orario corrente ma della mezzanotte ora UTC \(Coordinated Universal Time\).  
  
 Il primo esempio di codice presenta il metodo statico **ReportQueueAndJobAvailability** a cui viene passato <xref:System.Printing.PrintSystemJobInfo> e che chiama i metodi di supporto per stabilire se il processo può essere stampato all'ora corrente o, in caso contrario, quando può essere stampato.  Si noti che <xref:System.Printing.PrintQueue> non viene passato al metodo  perché <xref:System.Printing.PrintSystemJobInfo> include un riferimento alla coda nella relativa proprietà <xref:System.Printing.PrintSystemJobInfo.HostingPrintQueue%2A>.  
  
 I metodi subordinati includono il metodo di overload **ReportAvailabilityAtThisTime** che può utilizzare <xref:System.Printing.PrintQueue> o <xref:System.Printing.PrintSystemJobInfo> come parametro.  È disponibile anche **TimeConverter.ConvertToLocalHumanReadableTime**.  Tutti questi metodi vengono esaminati di seguito.  
  
 Il metodo **ReportQueueAndJobAvailability** verifica innanzitutto se la coda o il processo di stampa sono disponibili in quel preciso momento.  Se uno dei due non è disponibile, viene verificata la disponibilità della coda.  Se la coda non è disponibile, il metodo segnala questa situazione insieme all'ora in cui sarà nuovamente disponibile la coda.  Quindi, il metodo verifica il processo di stampa e, nel caso in cui non fosse disponibile, segnala il successivo intervallo di tempo in cui può essere stampato.  Infine, segnala il primo orario disponibile in cui il processo può essere stampato.  Si tratta della seconda condizione riportata di seguito.  
  
-   Il primo orario in cui è disponibile la coda di stampa.  
  
-   Il primo orario in cui è disponibile il processo di stampa.  
  
 Per il report degli orari, viene chiamato anche il metodo <xref:System.DateTime.ToShortTimeString%2A> che elimina gli anni, i mesi e i giorni dall'output.  Non è possibile limitare la disponibilità di una coda o di un processo di stampa ad anni, mesi o giorni specifici.  
  
 [!code-cpp[DiagnoseProblematicPrintJob#ReportQueueAndJobAvailability](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#reportqueueandjobavailability)]
 [!code-csharp[DiagnoseProblematicPrintJob#ReportQueueAndJobAvailability](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#reportqueueandjobavailability)]
 [!code-vb[DiagnoseProblematicPrintJob#ReportQueueAndJobAvailability](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#reportqueueandjobavailability)]  
  
 I due overload del metodo **ReportAvailabilityAtThisTime** sono identici ad eccezione del tipo ricevuto. Di seguito, viene quindi presentata solo la versione <xref:System.Printing.PrintQueue>.  
  
> [!NOTE]
>  Il fatto che i metodi siano identici ad eccezione del tipo, pone la questione del perché l'esempio non crea un metodo **ReportAvailabilityAtThisTime\<T\>** generico.  Il motivo è che questo metodo dovrebbe essere limitato a una classe con le proprietà **StartTimeOfDay** e **UntilTimeOfDay** chiamate dal metodo, ma un metodo generico può essere limitato a una sola classe e l'unica classe comune a <xref:System.Printing.PrintQueue> e a <xref:System.Printing.PrintSystemJobInfo> nella struttura ad albero di ereditarietà è <xref:System.Printing.PrintSystemObject> che non dispone di tali proprietà.  
  
 Il metodo **ReportAvailabilityAtThisTime**, illustrato nell'esempio di codice di seguito, avvia l'inizializzazione di una variabile sentinel <xref:System.Boolean> su `true`.  Se la coda non è disponibile, verrà reimpostata su `false`.  
  
 Quindi, il metodo verifica se l'ora di inizio e l'ora di fine coincidono.  In tal caso, la coda è sempre disponibile e il metodo restituisce `true`.  
  
 Se la coda non è disponibile per tutto il tempo, il metodo utilizza la proprietà statica <xref:System.DateTime.UtcNow%2A> per ottenere l'ora corrente come oggetto <xref:System.DateTime>.  L'ora locale non è necessaria perché le proprietà <xref:System.Printing.PrintQueue.StartTimeOfDay%2A> e <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A> sono in formato UTC.  
  
 Tuttavia, queste due proprietà non sono oggetti <xref:System.DateTime> ma oggetti <xref:System.Int32> che esprimono l'orario come numero di minuti dopo la mezzanotte ora UTC.  È quindi necessario convertire l'oggetto <xref:System.DateTime> in minuti dopo la mezzanotte.  Quindi, il metodo verifica se "now" si trova tra l'ora di inizio e l'ora di fine della coda, imposta sentinel su false se "now" non è compreso tra i due orari e quindi restituisce sentinel.  
  
 [!code-cpp[DiagnoseProblematicPrintJob#PrintQueueStartUntil](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#printqueuestartuntil)]
 [!code-csharp[DiagnoseProblematicPrintJob#PrintQueueStartUntil](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#printqueuestartuntil)]
 [!code-vb[DiagnoseProblematicPrintJob#PrintQueueStartUntil](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#printqueuestartuntil)]  
  
 Il metodo **TimeConverter.ConvertToLocalHumanReadableTime**, illustrato nell'esempio di codice di seguito, non utilizza alcun metodo introdotto con [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)].  Il metodo deve eseguire una doppia attività di conversione: deve convertire un numero intero che esprime i minuti dopo la mezzanotte in un orario leggibile e quindi convertire quest'ultimo nell'ora locale.  A tale scopo, viene creato prima un oggetto <xref:System.DateTime>, impostato sulla mezzanotte ora UTC, quindi viene utilizzato il metodo <xref:System.DateTime.AddMinutes%2A> per aggiungere i minuti passati al metodo.  Viene restituito un nuovo oggetto <xref:System.DateTime> che esprime l'ora originale passata al metodo.  Quindi, il metodo <xref:System.DateTime.ToLocalTime%2A> la converte nell'ora locale.  
  
 [!code-cpp[DiagnoseProblematicPrintJob#TimeConverter](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#timeconverter)]
 [!code-csharp[DiagnoseProblematicPrintJob#TimeConverter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#timeconverter)]
 [!code-vb[DiagnoseProblematicPrintJob#TimeConverter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#timeconverter)]  
  
## Vedere anche  
 <xref:System.DateTime>   
 <xref:System.Printing.PrintSystemJobInfo>   
 <xref:System.Printing.PrintQueue>   
 [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [Cenni preliminari sulla stampa](../../../../docs/framework/wpf/advanced/printing-overview.md)