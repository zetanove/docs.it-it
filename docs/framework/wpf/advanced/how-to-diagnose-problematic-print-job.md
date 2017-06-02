---
title: "Procedura: diagnosticare processi di stampa problematici | Microsoft Docs"
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
  - "processi di stampa, diagnosi di problemi"
  - "processi di stampa, risoluzione dei problemi"
  - "risoluzione dei problemi del processo di stampa"
ms.assetid: b081a170-84c6-48f9-a487-5766a8d58a82
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: diagnosticare processi di stampa problematici
Gli amministratori di rete spesso devono far fronte ai reclami degli utenti relativamente a processi di stampa non eseguiti oppure lenti.  La vasta gamma di proprietà dei processi di stampa esposta nelle [!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)] di [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)] consente la rapida diagnosi remota di questi processi.  
  
## Esempio  
 Di seguito vengono descritti i passaggi principali per la creazione di questo tipo di utilità.  
  
1.  Identificare il processo di stampa oggetto del reclamo dell'utente.  Spesso, infatti, gli utenti non sono in grado di individuarlo con precisione,  in quanto è probabile che non conoscano i nomi dei server di stampa o delle stampanti  e indichino il percorso della stampante con una terminologia diversa da quella utilizzata nell'impostazione della proprietà <xref:System.Printing.PrintQueue.Location%2A>.  Di conseguenza, è opportuno generare un elenco dei processi inviati dall'utente in quel momento.  Nel caso in cui si tratti di più processi, è possibile utilizzare la comunicazione tra l'utente e l'amministratore del sistema di stampa per individuare il processo problematico.  La procedura è indicata di seguito.  
  
    1.  Ottenere un elenco di tutti i server di stampa.  
  
    2.  Scorrere i server per eseguire una query sulle relative code di stampa.  
  
    3.  In ogni passaggio del ciclo di server, scorrere tutte le code del server per eseguire una query sui relativi processi.  
  
    4.  In ogni passaggio del ciclo di code, scorrere i processi e raccogliere le informazioni di identificazione relative ai processi inviati dall'utente che ha eseguito il reclamo.  
  
2.  Una volta identificato il processo di stampa problematico, esaminare le proprietà rilevanti per individuare l'eventuale problema.  Verificare, ad esempio, se il processo si trova in uno stato di errore oppure se la stampante che gestisce la coda è passata alla modalità offline prima della stampa.  
  
 Il codice riportato di seguito è costituito da una serie di esempi di codice.  Il primo esempio di codice contiene il ciclo per scorrere le code di stampa  \(vedere il passaggio 1c precedente\). La variabile `myPrintQueues` è l'oggetto <xref:System.Printing.PrintQueueCollection> per il server di stampa corrente.  
  
 L'esempio di codice ha inizio con l'aggiornamento dell'oggetto coda di stampa corrente con <xref:System.Printing.PrintQueue.Refresh%2A?displayProperty=fullName>.  In tal modo si garantisce che le proprietà dell'oggetto rappresentino con precisione lo stato della stampante fisica.  L'applicazione ottiene quindi la raccolta dei processi di stampa attualmente presenti nella coda di stampa utilizzando <xref:System.Printing.PrintQueue.GetPrintJobInfoCollection%2A>.  
  
 Successivamente l'applicazione scorre la raccolta <xref:System.Printing.PrintSystemJobInfo> e confronta ciascuna proprietà <xref:System.Printing.PrintSystemJobInfo.Submitter%2A> con l'alias dell'utente che ha eseguito il reclamo.  Se questi corrispondono, alla stringa visualizzata verranno aggiunte delle informazioni di identificazione relative al processo.  Le variabili `userName` e `jobList` vengono inizializzate precedentemente all'interno applicazione.  
  
 [!code-cpp[DiagnoseProblematicPrintJob#EnumerateJobsInQueues](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#enumeratejobsinqueues)]
 [!code-csharp[DiagnoseProblematicPrintJob#EnumerateJobsInQueues](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#enumeratejobsinqueues)]
 [!code-vb[DiagnoseProblematicPrintJob#EnumerateJobsInQueues](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#enumeratejobsinqueues)]  
  
 Nel successivo esempio di codice l'applicazione viene illustrata a partire dal passaggio 2  \(vedere sopra\). Il processo problematico è stato individuato e l'applicazione richiede le informazioni che consentono di identificarlo.  Tali informazioni vengono utilizzate per creare gli oggetti <xref:System.Printing.PrintServer>, <xref:System.Printing.PrintQueue> e <xref:System.Printing.PrintSystemJobInfo>.  
  
 A questo punto l'applicazione conterrà una struttura con diramazioni, corrispondente alle due modalità di verifica dello stato di un processo di stampa:  
  
-   È possibile leggere i flag della proprietà <xref:System.Printing.PrintSystemJobInfo.JobStatus%2A> di tipo <xref:System.Printing.PrintJobStatus>.  
  
-   È possibile leggere ciascuna proprietà rilevante, ad esempio <xref:System.Printing.PrintSystemJobInfo.IsBlocked%2A> e <xref:System.Printing.PrintSystemJobInfo.IsInError%2A>.  
  
 Nell'esempio vengono illustrati entrambi i metodi. All'utente è stato pertanto richiesto di scegliere il metodo da utilizzare e di rispondere con "Y" per utilizzare i flag della proprietà <xref:System.Printing.PrintSystemJobInfo.JobStatus%2A>.  Per informazioni dettagliate relative ai due metodi vedere di seguito.  Infine, l'applicazione utilizza un metodo denominato **ReportQueueAndJobAvailability** per segnalare se è possibile eseguire il processo di stampa in quel preciso momento.  Il metodo viene illustrato in [Verificare l'eventuale possibilità di eseguire un processo di stampa in questo preciso momento](../../../../docs/framework/wpf/advanced/how-to-discover-whether-a-print-job-can-be-printed-at-this-time-of-day.md).  
  
 [!code-cpp[DiagnoseProblematicPrintJob#IdentifyAndDiagnoseProblematicJob](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#identifyanddiagnoseproblematicjob)]
 [!code-csharp[DiagnoseProblematicPrintJob#IdentifyAndDiagnoseProblematicJob](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#identifyanddiagnoseproblematicjob)]
 [!code-vb[DiagnoseProblematicPrintJob#IdentifyAndDiagnoseProblematicJob](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#identifyanddiagnoseproblematicjob)]  
  
 Per controllare lo stato del processo di stampa utilizzando i flag della proprietà <xref:System.Printing.PrintSystemJobInfo.JobStatus%2A>, esaminare ogni flag pertinente per verificare se è impostato.  La modalità standard per verificare se in un set di flag di bit è stato impostato un determinato bit consiste nell'eseguire un'operazione di AND logico in cui un operando sia costituito dal set di flag e l'altro dal flag stesso.  Dal momento che il flag stesso dispone di un solo bit impostato, il risultato dell'operazione di AND logico consisterà, al più, nell'impostazione dello stesso bit.  Per verificare se il bit è impostato, confrontare il risultato dell'operazione di AND logico con il flag stesso.  Per ulteriori informazioni, vedere <xref:System.Printing.PrintJobStatus>, [Operatore & \(Riferimenti per C\#\)](../Topic/&%20Operator%20\(C%23%20Reference\).md) e <xref:System.FlagsAttribute>.  
  
 Per ciascun attributo in cui il bit è impostato, il codice invia una segnalazione allo schermo della console, talvolta insieme a un suggerimento relativo alla modalità di risposta.  Il metodo **HandlePausedJob**, chiamato se il processo o la coda è in pausa, è illustrato di seguito.  
  
 [!code-cpp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobAttributes](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#spottroubleusingjobattributes)]
 [!code-csharp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobAttributes](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#spottroubleusingjobattributes)]
 [!code-vb[DiagnoseProblematicPrintJob#SpotTroubleUsingJobAttributes](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#spottroubleusingjobattributes)]  
  
 Per controllare lo stato del processo di stampa utilizzando proprietà separate, leggere ciascuna proprietà e, se il relativo valore è `true`, inviare una segnalazione allo schermo della console insieme a un eventuale suggerimento relativo alla modalità di risposta.  Il metodo **HandlePausedJob**, chiamato se il processo o la coda è in pausa, è illustrato di seguito.  
  
 [!code-cpp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobProperties](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#spottroubleusingjobproperties)]
 [!code-csharp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobProperties](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#spottroubleusingjobproperties)]
 [!code-vb[DiagnoseProblematicPrintJob#SpotTroubleUsingJobProperties](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#spottroubleusingjobproperties)]  
  
 Il metodo **HandlePausedJob** consente all'utente dell'applicazione di riprendere i processi in pausa da postazione remota.  Dal momento che la sospensione della coda di stampa potrebbe essere causata da un motivo valido, all'utente viene chiesto innanzitutto di decidere se riprenderla.  Se la risposta è "Y", viene chiamato il metodo <xref:System.Printing.PrintQueue.Resume%2A?displayProperty=fullName>.  
  
 Successivamente all'utente viene richiesto di decidere se riprendere il processo stesso, nel caso quest'ultimo fosse in pausa indipendentemente dalla coda di stampa.  Confrontare <xref:System.Printing.PrintQueue.IsPaused%2A?displayProperty=fullName> e <xref:System.Printing.PrintSystemJobInfo.IsPaused%2A?displayProperty=fullName>. Se la risposta è "Y", viene chiamato <xref:System.Printing.PrintSystemJobInfo.Resume%2A?displayProperty=fullName>; in caso contrario, viene chiamato <xref:System.Printing.PrintSystemJobInfo.Cancel%2A>.  
  
 [!code-cpp[DiagnoseProblematicPrintJob#HandlePausedJob](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#handlepausedjob)]
 [!code-csharp[DiagnoseProblematicPrintJob#HandlePausedJob](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#handlepausedjob)]
 [!code-vb[DiagnoseProblematicPrintJob#HandlePausedJob](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#handlepausedjob)]  
  
## Vedere anche  
 <xref:System.Printing.PrintJobStatus>   
 <xref:System.Printing.PrintSystemJobInfo>   
 <xref:System.FlagsAttribute>   
 <xref:System.Printing.PrintQueue>   
 [Operatore & \(Riferimenti per C\#\)](../Topic/&%20Operator%20\(C%23%20Reference\).md)   
 [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [Cenni preliminari sulla stampa](../../../../docs/framework/wpf/advanced/printing-overview.md)